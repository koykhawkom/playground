# การตรวจบนเครื่อง Dev — ประกอบหน้า 12 (v4)

หลักฐานที่อ่านแล้ว: ภาพต้นฉบับ, YAML ของแอปในบทสนทนา และ /workflow/.gitflow-Docker.gitlab-ci.yml ที่แนบ; ยังไม่ได้รับ Template ย่อย Job Log รายงานจริง หรือข้อมูลยืนยันว่าไฟล์ตรงกับ Commit ในภาพ; ตัวอย่างเครื่องมือ Dev อ้างเอกสารภายนอกและแยกจากข้อเท็จจริงของระบบ; ข้อมูลเพิ่มเติมจากผู้ใช้: Image Scan ใช้ Amazon ECR; ยังไม่ระบุ Basic / Enhanced

## ข้อมูลที่ยืนยัน

ผู้ใช้ยืนยันว่า Image Scan ใช้ Amazon ECR. Job image-scan เรียก .ecr_docker_scan ตาม Workflow ที่ส่งมา. ยังไม่ยืนยันโหมด Basic / Enhanced และเกณฑ์ผ่าน. Script ของ unit-test ยังเป็น echo แจ้งข้ามการทดสอบ ส่วน Test ใน Build ยังไม่ยืนยัน

ข้อมูลจากภาพและ YAML แสดงแยกจากตัวอย่างเครื่องมือสำหรับ Dev ด้านล่าง คำสั่งเป็นตัวอย่างสำหรับ macOS / Linux / WSL ต้องติดตั้งเครื่องมือที่องค์กรอนุมัติ รันในโปรเจกต์ที่มีสิทธิ์ตรวจ และปรับตาม Configuration จริง ยังไม่ได้รันคำสั่งเหล่านี้กับ Source Code ของลูกค้า

#### 1. gemnasium-maven-dependency_scanning

จากชื่อ Job ในภาพ (ยังต้องยืนยัน Analyzer Image และ Script ใน Template ย่อย): ชื่อนี้ตรงกับ Gemnasium Maven Analyzer ของ GitLab Dependency Scanning แบบเดิม ใช้ตรวจช่องโหว่ที่รู้จักใน Dependency รวมถึง Dependency ทางอ้อมของโปรเจกต์ JVM ไม่ใช่การตรวจ Logic ใน Source Code

ตรวจเอง: OWASP Dependency-Check Maven Plugin เป็นเครื่องมือประเภทใกล้เคียงสำหรับตรวจ Library แต่ไม่ใช่ Engine เดียวกัน ฐานข้อมูลช่องโหว่ วิธีจับคู่ Package และเกณฑ์จัดระดับอาจทำให้ผลต่างกัน ไม่ควรใช้รายงานนี้ยืนยันว่า Gemnasium จะผ่าน

วิธีให้ใกล้ CI มากขึ้น: ขอ Gemnasium Maven Analyzer Image พร้อม Tag หรือ Digest, JDK/Maven, Profiles, Scopes, Dependency Repository และค่าที่ใช้จริงจากทีม Platform แล้วตกลงวิธีรันบนเครื่อง Dev ห้ามใส่รหัสผ่านของ Repository ลงใน Image หรือ Script ที่ Commit

คำสั่งด้านล่างต้องกำหนด DEPENDENCY_CHECK_VERSION เป็นรุ่นที่อนุมัติและรองรับ JDK/Maven ที่ใช้ หากไม่มี Maven Wrapper ให้ใช้ mvn แทน ./mvnw ต้องเตรียมการเข้าถึงข้อมูล NVD เช่น API Key หรือ Mirror ตามนโยบาย โดยเก็บ Key นอก Source Code การดึงฐานข้อมูลครั้งแรกอาจใช้เวลานาน

Gemnasium เป็นแนวทางที่ GitLab ประกาศ Deprecated แล้ว เอกสารใหม่แนะนำ Dependency Scanning แบบ SBOM สำหรับการวางระบบใหม่ แต่ภาพนี้ยังต้องอธิบายตาม Job ที่ใช้อยู่ ไม่ถือว่ามีการย้ายแล้ว

```bash
: "${DEPENDENCY_CHECK_VERSION:?Set the approved plugin version first}"
./mvnw -B "org.owasp:dependency-check-maven:${DEPENDENCY_CHECK_VERSION}:check"
```

- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- [GitLab — Legacy dependency scanning (Gemnasium)](https://docs.gitlab.com/user/application_security/dependency_scanning/legacy_dependency_scanning/)
- [OWASP Dependency-Check — Maven plugin](https://dependency-check.github.io/DependencyCheck/dependency-check-maven/)
- [GitLab — Migration from Gemnasium to SBOM scanning](https://docs.gitlab.com/user/application_security/dependency_scanning/migration_guide_to_sbom_based_scans/)

#### 2. gitlab-advanced-sast

จากชื่อ Job ในภาพ (ยังต้องยืนยัน Analyzer Image และ Script ใน Template ย่อย): GitLab Advanced SAST เป็น Analyzer ของ GitLab ในระดับ Ultimate ใช้วิเคราะห์เส้นทางข้อมูลข้ามฟังก์ชันและข้ามไฟล์ เช่น ข้อมูลจาก Request ถูกส่งผ่านหลาย Method ก่อนถึงคำสั่ง SQL

ตรวจเอง: Semgrep CE หรือ SonarQube ที่ทีมมีอยู่ช่วยตรวจ Source Code เบื้องต้นได้ แต่เป็นการตรวจประเภทใกล้เคียง ไม่ใช่ตัวแทน Advanced SAST แบบหนึ่งต่อหนึ่ง และไม่ได้รับประกัน Coverage หรือผลตรวจเท่ากัน

การรัน Advanced SAST นอก Pipeline ต้องให้ทีม Platform ยืนยันวิธีที่รองรับและสิทธิ์ใช้งานก่อน ไม่ควรสมมติว่าเปิดใช้ Semgrep ฟรีแล้วเท่ากับได้ Advanced SAST บนเครื่อง Dev ส่วนผลรับงานยังต้องอ้างการตรวจตามนโยบายบน GitLab

- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- [GitLab — Advanced SAST](https://docs.gitlab.com/user/application_security/sast/gitlab_advanced_sast/)
- [GitLab — SAST analyzers and GitLab-managed Semgrep rules](https://docs.gitlab.com/user/application_security/sast/analyzers/)
- [SonarQube Server — GitLab integration](https://docs.sonarsource.com/sonarqube-server/devops-platform-integration/gitlab-integration)

#### 3. kics-iac-sast

จากชื่อ Job ในภาพ (ยังต้องยืนยัน Analyzer Image และ Script ใน Template ย่อย): ใช้ KICS สำหรับ Infrastructure as Code หรือ IaC เพื่อตรวจไฟล์ เช่น Dockerfile, Kubernetes YAML และ Terraform ตรวจการตั้งค่าที่มีความเสี่ยง ไม่ใช่การหา CVE ใน Package ที่ติดตั้งอยู่ภายใน Image

ตรวจเอง: ใช้ KICS CLI หรือ KICS Container ได้ ถือว่าใช้ Engine กลุ่มเดียวกัน แต่ต้องเทียบรุ่น KICS, Queries, ไฟล์ที่ตรวจ และ Ruleset ของ GitLab ให้ตรงกัน ตัวอย่างด้านล่างใช้ Queries เริ่มต้นของ KICS ที่ติดตั้ง จึงยังไม่ใช่การจำลอง CI ทั้งหมด

ตัวอย่างสิ่งที่ตรวจคือการตั้งสิทธิ์หรือค่าของ Container ที่ไม่เหมาะสม การผ่าน KICS ไม่ได้แทนผลจาก image-scan ทั้งสองขั้นตอนตรวจคนละส่วน

```bash
mkdir -p .local-reports/kics
kics scan -p . -o .local-reports/kics
```

- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- [GitLab — Infrastructure as Code scanning (KICS)](https://docs.gitlab.com/user/application_security/iac_scanning/)
- [KICS — Command line interface](https://docs.kics.io/latest/commands/)

#### 4. secret_detection

จากชื่อ Job ในภาพ (ยังต้องยืนยัน Analyzer Image และ Script ใน Template ย่อย): เป็น Job ตรวจข้อมูลลับ เช่น Token และ Private Key สำหรับ Analyzer แบบมาตรฐานที่ใช้ Gitleaks นั้น GitLab มี Wrapper และ Rules ของตนเอง ปัจจุบัน GitLab มี Analyzer แบบอื่นด้วย จึงต้องดู Image และ Job Log เพื่อยืนยันรุ่นจริง ไม่สรุป Engine จากชื่อ Job เพียงอย่างเดียว

ตรวจเอง: ใช้ Gitleaks CLI ตรวจประวัติ Git และไฟล์บนเครื่องได้ คำสั่ง git ตรวจประวัติที่มีอยู่ใน Repository ส่วน dir ตรวจไฟล์ปัจจุบัน จึงใช้ตรวจโค้ดที่ยังไม่ Commit ได้ด้วย โดย --redact ลดการแสดงค่าลับในผลลัพธ์

ตัวอย่างนี้ใช้ Rules เริ่มต้น ถ้าทีมมี Config ที่ตรงกับ GitLab ให้ใช้ -c ตามไฟล์ที่อนุมัติและกำหนด Commit Range ให้ตรงกัน การมีชื่อ Engine เหมือนกันแต่ Rules ต่างกันยังทำให้ผลต่างกันได้ หากพบ Secret ที่เคย Push แล้ว ต้องแจ้งเจ้าของเพื่อเพิกถอนหรือเปลี่ยน Secret ไม่ใช่ลบข้อความออกอย่างเดียว

```bash
gitleaks git --redact .
gitleaks dir --redact .
```

- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- [GitLab — Pipeline secret detection](https://docs.gitlab.com/user/application_security/secret_detection/pipeline/)
- [GitLab — Detected secrets and analyzer types](https://docs.gitlab.com/user/application_security/secret_detection/detected_secrets/)
- [Gitleaks — CLI, configuration and pre-commit](https://github.com/gitleaks/gitleaks)

#### 5. semgrep-sast

จากชื่อ Job ในภาพ (ยังต้องยืนยัน Analyzer Image และ Script ใน Template ย่อย): GitLab Semgrep Analyzer ใช้ Semgrep OSS Engine พร้อมชุดกฎที่ GitLab ดูแล ตรวจรูปแบบโค้ดที่มีความเสี่ยงตามภาษาและกฎที่เปิดใช้

ตรวจเอง: ใช้ Semgrep CLI ได้ แต่ควรขอชุดกฎและ Exclusions ที่สอดคล้องกับ GitLab คำสั่งด้านล่างสมมติว่าทีมเตรียม Rules ไว้ที่ ./security-rules/semgrep แล้ว ไม่ได้มีไฟล์เหล่านี้แนบอยู่ใน Presentation นี้

คำสั่งใช้ Rules ในเครื่อง ปิด Metrics และ Version Check และใช้ --error เพื่อคืนสถานะไม่สำเร็จเมื่อพบประเด็นตามกฎ ขณะเดียวกันต้องอ่านข้อผิดพลาดเรื่อง Parse, Timeout หรือไฟล์ที่ถูกข้ามด้วย ไม่ใช้เพียง Exit Code เป็นเกณฑ์ทั้งหมด

การใช้ --config auto หรือกฎจาก Registry โดยตรงไม่ใช่ชุดกฎเดียวกับ GitLab โดยอัตโนมัติ วิธีที่ใกล้กว่าคือรัน GitLab Semgrep Analyzer Image ตัวเดียวกับ CI ตามตัวอย่างในหัวข้อรัน Analyzer ด้านล่าง ทั้งนี้ Semgrep CE ไม่เท่ากับ GitLab Advanced SAST

```bash
semgrep scan --oss-only \
  --config ./security-rules/semgrep \
  --metrics off --disable-version-check --error .
```

- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- [GitLab — SAST analyzers and GitLab-managed Semgrep rules](https://docs.gitlab.com/user/application_security/sast/analyzers/)
- [Semgrep — CLI reference](https://docs.semgrep.dev/cli-reference)
- [Semgrep — Run local rules](https://docs.semgrep.dev/running-rules)
- [GitLab — Running analyzers locally with Docker](https://docs.gitlab.com/development/sec/analyzer_development_guide/)

#### 6. unit-test — Script ปัจจุบันยังเป็น Placeholder

ข้อมูลจาก YAML ของแอป: Script ของ Job นี้มีเพียง echo "No Maven unit tests configured as separate job - skipping (handled in build)" และใช้ alpine:latest โดยตั้ง allow_failure: true จึงยังไม่มีคำสั่งรัน Unit Test จริงใน Script ที่เห็น ไม่ใช้ชื่อ Job หรือเครื่องหมายผ่านในภาพเป็นหลักฐานว่ามีการทดสอบแล้ว

ข้อความ handled in build เป็นข้อความจากผู้เขียน Pipeline ไม่ใช่หลักฐานว่ารัน Test จริง ต้องดู .buildkit_build_image, Dockerfile และ Job Log เพิ่ม ตัวอย่าง Maven + JUnit + JaCoCo ใน Workflow กลางถูก Comment ไว้ จึงไม่ใช่ Job ที่เปิดทำงาน

ตัวอย่างสำหรับ Dev: หากโครงการใช้ Maven และมีชุดทดสอบ ให้รัน ./mvnw -B test หรือ mvn -B test ด้วย JDK, Profiles และการตั้งค่าที่ตกลงกัน ตรวจจำนวน Test และรายงานด้วย คำสั่งนี้เป็นข้อเสนอ ไม่ใช่คำสั่งที่อ่านพบใน Job ปัจจุบัน

Maven Surefire ใช้รัน Unit Test ส่วน Framework เช่น JUnit หรือ TestNG ขึ้นอยู่กับ Dependency ของโปรเจกต์ หากใช้ verify, Gradle หรือคำสั่งเฉพาะต้องปรับตามโครงการ การรัน test ไม่ครอบคลุม Integration Test ทุกแบบ

Tests 0 ในภาพเพียงอย่างเดียวไม่บอกว่าทดสอบส่วนอื่นหรือไม่ เพราะแท็บรายงานต้องรับผลทดสอบเข้ามา แต่ในกรณีนี้ YAML เพิ่มหลักฐานแล้วว่า Script ของ unit-test เป็น echo ส่วน Test ใน Build ยังไม่ยืนยัน

```bash
# Local example only; NOT the current CI job script.
# Requires Maven Wrapper and configured project tests.
./mvnw -B test
# Without Maven Wrapper: mvn -B test
```

- ข้อมูลผู้ใช้ — .gitlab-ci.yml ของ wf4pos-revamp/backend — YAML ที่วางในบทสนทนา: .pipeline_rule, unit-test, build, image-scan, deploy-service และ deploy-service-uat-1/2
- ข้อมูลผู้ใช้ — /workflow/.gitflow-Docker.gitlab-ci.yml — ไฟล์แนบ Pasted text(2).txt: stages บรรทัด 9–13; ตัวอย่าง Maven ที่เป็น Comment บรรทัด 247–277; extends บรรทัด 375–392
- [Apache Maven — Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/)
- [GitLab — Unit test reports](https://docs.gitlab.com/ci/testing/unit_test_reports/)

#### 7. image-scan — Amazon ECR

ผู้ใช้ยืนยันว่า Image Scan ใช้ Amazon ECR. Job image-scan เรียก .ecr_docker_scan ตาม Workflow ที่ส่งมา โดยไฟล์แอปปรับ Rules ของ Job นี้

ยังไม่ยืนยันโหมด Basic / Enhanced และเกณฑ์ผ่าน. ยังไม่เห็น Script ภายใน Template จึงยังไม่ระบุวิธีเรียกสแกน การรอผล หรือเงื่อนไขหยุด Deploy

ข้อมูลประกอบจาก AWS: Basic Scanning ตรวจ Package ของระบบปฏิบัติการ ส่วน Enhanced Scanning ใช้ Amazon Inspector ตรวจ Package ของระบบปฏิบัติการและภาษาโปรแกรม นี่เป็นข้อมูลของบริการ ไม่ใช่การยืนยันโหมดของระบบนี้

ตัวอย่างสำหรับ Dev: ใช้ Trivy ตรวจช่องโหว่ใน Container Image ที่สร้างไว้ในเครื่องได้ แต่เป็นการตรวจเบื้องต้น ไม่ใช่การจำลอง Job image-scan ของระบบนี้ และไม่ใช่การอนุมัติให้ Deploy

Trivy และ Amazon ECR เป็นคนละเครื่องมือ ผลตรวจอาจต่างกัน ควรเทียบ Image Digest, Platform, Package/CVE และเวลาสแกน ไม่ใช้ผล Local แทนผลจาก ECR หรือเกณฑ์อนุมัติของ Pipeline

ตัวอย่างด้านล่างเน้นช่องโหว่ด้วย --scanners vuln และคืน Exit Code 1 เมื่อพบระดับ HIGH หรือ CRITICAL ซึ่งเป็นเกณฑ์ตัวอย่างเท่านั้น ไม่ใช่นโยบายที่ยืนยันของลูกค้า ต้องอ่านรายงานและข้อผิดพลาดในการสแกนด้วย

```bash
# Local pre-check only. The pipeline uses Amazon ECR, not this CLI.
# myapp:local must already exist. Severity is an example.
trivy image --scanners vuln \
  --severity HIGH,CRITICAL --exit-code 1 myapp:local
```

- ข้อมูลผู้ใช้ — Image Scan ใช้ Amazon ECR — ยืนยันในบทสนทนาวันที่ 14 ตุลาคม 2026; ไม่ได้ระบุโหมดหรือเกณฑ์ผ่าน
- ข้อมูลผู้ใช้ — /workflow/.gitflow-Docker.gitlab-ci.yml — ไฟล์แนบ Pasted text(2).txt: stages บรรทัด 9–13; ตัวอย่าง Maven ที่เป็น Comment บรรทัด 247–277; extends บรรทัด 375–392
- ข้อมูลผู้ใช้ — .gitlab-ci.yml ของ wf4pos-revamp/backend — YAML ที่วางในบทสนทนา: .pipeline_rule, unit-test, build, image-scan, deploy-service และ deploy-service-uat-1/2
- [AWS - Amazon ECR image scanning (Basic / Enhanced)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)
- [Trivy — Container image scanning](https://trivy.dev/docs/latest/guide/target/container_image/)

#### ข้อมูลที่ต้องตรวจเพิ่มของ Amazon ECR

ยืนยัน Basic / Enhanced, Repository และ Scan filters จากการตั้งค่า ECR ที่ใช้จริง ไม่สรุปโหมดจากชื่อ Job เพียงอย่างเดียว

ดู Full configuration ใน Pipeline editor หรือไฟล์ที่ขยาย include/extends แล้ว โดยตรวจ image, script, before_script, variables และการรับรายงานของ image-scan จากนั้นเทียบกับ Job Log และ Commit ของ Pipeline ในภาพ

ตรวจว่า Script รอผลสแกนอย่างไร เมื่อสแกนไม่สำเร็จหรือไม่มีรายงานทำอย่างไร และใช้ Severity ข้อยกเว้น หรือเกณฑ์ใดตัดสินให้ Job ผ่าน หรือหยุด Deploy

เทียบ Account, Region, Repository และ Image Digest ให้ตรงกับรุ่นที่ Deploy พร้อมตรวจสถานะและเวลาของผลสแกน

- ข้อมูลผู้ใช้ — Image Scan ใช้ Amazon ECR — ยืนยันในบทสนทนาวันที่ 14 ตุลาคม 2026; ไม่ได้ระบุโหมดหรือเกณฑ์ผ่าน
- ข้อมูลผู้ใช้ — /workflow/.gitflow-Docker.gitlab-ci.yml — ไฟล์แนบ Pasted text(2).txt: stages บรรทัด 9–13; ตัวอย่าง Maven ที่เป็น Comment บรรทัด 247–277; extends บรรทัด 375–392
- [GitLab — Pipeline editor and full configuration](https://docs.gitlab.com/ci/pipeline_editor/)
- [AWS - Amazon ECR image scanning (Basic / Enhanced)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)
- [AWS CLI - describe-image-scan-findings](https://docs.aws.amazon.com/cli/latest/reference/ecr/describe-image-scan-findings.html)

#### ดูผล Amazon ECR ด้วย AWS CLI (อ่านอย่างเดียว)

ตัวอย่างจากเอกสาร AWS ไม่ใช่ Script ที่อ่านพบใน Pipeline: ใช้ describe-image-scan-findings เพื่อดูผลของ Image ที่มีใน ECR แล้ว คำสั่งนี้ไม่ Push Image ไม่เริ่ม Scan และไม่แก้การตั้งค่า

ต้องติดตั้ง AWS CLI และใช้ Profile/Role ที่มีสิทธิ์อ่านผลใน Account, Region และ Repository ที่อนุญาต กำหนดตัวแปรด้านล่างก่อนรัน ไม่ใส่ Access Key หรือ Secret ลงในโค้ด

เป็นการเรียกดูผลจากบริการ AWS ไม่ใช่การรัน Scanner ในเครื่อง Dev คำสั่ง API สำเร็จไม่ได้แปลว่าผ่านเกณฑ์ความปลอดภัย ต้องดูสถานะการสแกน Findings และเกณฑ์จริง การไม่พบรายงานไม่ได้แปลว่าไม่มีช่องโหว่

```bash
# Read existing findings only; not the pipeline script.
# Use an approved AWS profile and an existing scanned image digest.
: "${AWS_PROFILE:?Set an approved AWS profile}"
: "${AWS_REGION:?Set the ECR region}"
: "${ECR_REGISTRY_ID:?Set the registry AWS account ID}"
: "${ECR_REPOSITORY:?Set the repository name}"
: "${IMAGE_DIGEST:?Set the existing image digest, including sha256:}"
aws ecr describe-image-scan-findings \
  --profile "$AWS_PROFILE" \
  --region "$AWS_REGION" \
  --registry-id "$ECR_REGISTRY_ID" \
  --repository-name "$ECR_REPOSITORY" \
  --image-id "imageDigest=$IMAGE_DIGEST" \
  --output json --no-cli-pager
```

- [AWS CLI - describe-image-scan-findings](https://docs.aws.amazon.com/cli/latest/reference/ecr/describe-image-scan-findings.html)
- [AWS - Amazon ECR image scanning (Basic / Enhanced)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)

#### ตัวอย่างรัน GitLab Semgrep Analyzer บนเครื่อง Dev

สำหรับการเทียบกับ semgrep-sast ให้ขอ Image พร้อม Digest ที่ใช้จริงจากทีม Platform แล้วกำหนดตัวแปร GITLAB_SEMGREP_IMAGE ก่อนรัน ตัวอย่างนี้อ้างรูปแบบ /analyzer run ของ GitLab แต่ต้องเติมค่าที่ Pipeline ของโปรเจกต์ต้องใช้

ใช้สำเนาโปรเจกต์ที่มีสิทธิ์ตรวจ เพราะ Analyzer สามารถเขียนไฟล์รายงานลงโฟลเดอร์ที่ Mount ได้ บาง Image รองรับเฉพาะ linux/amd64 บนเครื่อง ARM ต้องใช้ Environment หรือการ Emulate ที่ทีมรองรับ การรัน Image เดียวกันยังต้องใช้ Rules, Environment Variables, Paths และ Git Context ให้ตรงด้วย

ตัวอย่างนี้เฉพาะ Semgrep Analyzer ไม่ใช่คำสั่งสากลสำหรับทุก Scanner และไม่ใช่คำยืนยันสิทธิ์รัน GitLab Advanced SAST ในเครื่อง การเชื่อม Registry หรือ Dependency ภายในต้องผ่านช่องทางที่อนุมัติ

```bash
: "${GITLAB_SEMGREP_IMAGE:?Set the approved CI analyzer image and digest}"
docker run --rm \
  --volume "$PWD:/tmp/app" \
  --env CI_PROJECT_DIR=/tmp/app \
  --workdir /tmp/app \
  "$GITLAB_SEMGREP_IMAGE" /analyzer run
```

- [GitLab — Running analyzers locally with Docker](https://docs.gitlab.com/development/sec/analyzer_development_guide/)
- [GitLab — SAST analyzers and GitLab-managed Semgrep rules](https://docs.gitlab.com/user/application_security/sast/analyzers/)

#### สรุปสิ่งที่ต้องตรงกันก่อนเปรียบเทียบผล

เปรียบเทียบโค้ด Commit เดียวกัน รวมถึง Submodules และไฟล์ที่ Generate, Engine และ Version เดียวกัน, Ruleset และ Exclusions เดียวกัน, JDK/Maven/Profile และ Dependency Scope เดียวกัน รวมถึง Image/Platform และฐานข้อมูลช่องโหว่ที่ใกล้เคียงกัน

ขอเกณฑ์ Severity, การอนุมัติข้อยกเว้น และเงื่อนไข Block ให้ตรงกับลูกค้า แยกให้ออกว่าเครื่องมือทำงานเสร็จหรือผลผ่านเกณฑ์แล้ว การสแกนในเครื่องใช้พบและแก้ปัญหาก่อน Push แต่ไม่ควรใช้แทนการตรวจและอนุมัติใน CI

คำสั่งตัวอย่างต้องติดตั้งเครื่องมือและเตรียม Rules ก่อน ใช้เฉพาะ Source Code ที่มีสิทธิ์ตรวจ ไม่ส่ง Source Code หรือรายงานที่มีข้อมูลลับไปบริการภายนอกที่ยังไม่อนุมัติ และอย่า Commit ไฟล์ผลสแกนที่อาจมีข้อมูลละเอียดอ่อนลง Repository

- [GitLab — SAST analyzers and GitLab-managed Semgrep rules](https://docs.gitlab.com/user/application_security/sast/analyzers/)
- [GitLab — Pipeline secret detection](https://docs.gitlab.com/user/application_security/secret_detection/pipeline/)
- [GitLab — Container scanning](https://docs.gitlab.com/user/application_security/container_scanning/)


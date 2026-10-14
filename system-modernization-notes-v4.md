# การปรับระบบตามมาตรฐานใหม่ — v4

17 สไลด์ | แนวพูด 19:40 นาที ไม่รวมถามตอบ

ผู้ใช้ยืนยันว่า Image Scan ใช้ Amazon ECR; ยังไม่ยืนยันโหมด Basic / Enhanced และเกณฑ์ผ่าน. หน้า 10–12 อ่านจากภาพ Pipeline, YAML ของแอป และ Workflow กลางที่ผู้ใช้ส่งมา การระบุหน้าที่ของ Analyzer เทียบกับเอกสารทางการ แต่ยังไม่มี Template ย่อย Job Log หรือผลสแกนให้ตรวจ เครื่องมือสำหรับ Dev เป็นตัวอย่างแยกต่างหาก ไม่ใช่หลักฐานว่า Pipeline ใช้เครื่องมือเดียวกัน ส่วนแนวทางด้านกระบวนการและหน้าที่ในหน้าอื่นยังเป็นข้อเสนอที่ต้องตกลงกับลูกค้า

## 01. การปรับระบบ ตามมาตรฐานใหม่

เริ่มที่ 00:00 | เวลาแนะนำ 00:30 นาที

**ประเด็นหลัก:** อธิบายเรื่องที่จะคุยและสิ่งที่ต้องเตรียม

วันนี้จะคุยเรื่องการปรับระบบให้รองรับมาตรฐานใหม่ของลูกค้า ทั้งเทคโนโลยีที่ใช้ การตรวจสอบความปลอดภัย และขั้นตอนส่งมอบระบบ

จะเริ่มจากระบบที่เราดูแลอยู่ แล้วดูว่าส่วนไหนต้องปรับ ทีมต้องเตรียมอะไร และควรเริ่มจากงานส่วนใด โดยยังไม่จำเป็นต้องเปลี่ยนทุกระบบพร้อมกัน

**การอธิบาย:** บอกขอบเขตของเรื่องที่จะนำเสนอ

**ประโยคเชื่อม:** เริ่มจากระบบที่ใช้งานอยู่ในปัจจุบัน

**ที่มาของเนื้อหา:** กรอบการนำเสนอที่เสนอสำหรับงานนี้

## 02. ระบบที่ใช้งาน ในปัจจุบัน

เริ่มที่ 00:30 | เวลาแนะนำ 01:05 นาที

**ประเด็นหลัก:** สรุปเทคโนโลยีและสภาพแวดล้อมของระบบเดิม

ระบบเดิมตามข้อมูลที่มี ประกอบด้วย JSP กับ Java และ Oracle รวมถึง .NET กับ SQL Server ส่วนสภาพแวดล้อมที่ใช้รันมี WebLogic, IIS และ Windows Service ซึ่งไม่ใช่ Application Server ประเภทเดียวกันทั้งหมด

ก่อนปรับระบบ ควรตรวจว่าแอปใช้ Library อะไร มี Configuration อยู่ที่ใด ใช้ Font สำหรับรายงานอย่างไร และเชื่อมต่อกับฐานข้อมูลหรือระบบอื่นแบบไหน

รายการเหล่านี้ช่วยแยกว่าส่วนใดใช้ต่อได้ ส่วนใดต้องปรับ และส่วนใดต้องทดสอบเพิ่ม ไม่ได้หมายความว่าระบบเดิมทุกตัวมีปัญหาเหมือนกัน

**การอธิบาย:** ยกตัวอย่างจากงานเดิมหนึ่งกรณี เช่น Library หรือ Font หลังอัปเกรด

**ประโยคเชื่อม:** นอกจากตัวระบบแล้ว ต้องดูข้อกำหนดในการส่งมอบด้วย

**ที่มาของเนื้อหา:** รายการระบบและสภาพแวดล้อมจากข้อมูลของผู้ใช้

## 03. การส่งมอบระบบ ต้องเตรียมอะไรบ้าง

เริ่มที่ 01:35 | เวลาแนะนำ 00:45 นาที

**ประเด็นหลัก:** อธิบายสิ่งที่ควรตกลงก่อนส่งมอบระบบ

ในส่วนการส่งมอบ ผมเสนอให้ตกลงกันสามเรื่อง คือขั้นตอน Build ที่ทำซ้ำได้ ข้อมูลเวอร์ชันและผลการตรวจสอบ และเอกสารที่ทีมรับดูแลต้องใช้

เช่น เมื่อส่งระบบหนึ่งรุ่น ควรทราบว่ามาจากโค้ดชุดไหน ทดสอบอะไรแล้ว และใช้ขั้นตอนใดในการ Deploy รายละเอียดต้องตกลงกับลูกค้าก่อนเริ่มงาน

สามเรื่องนี้เป็นข้อเสนอสำหรับหารือ ไม่ใช่ข้อสรุปว่าระบบเดิมยังไม่มี หรือเป็นเกณฑ์ที่ลูกค้ายืนยันแล้ว

**การอธิบาย:** อธิบายโดยอ้างถึงการส่งระบบหนึ่งรุ่น

**ประโยคเชื่อม:** งานที่ต้องปรับแบ่งพิจารณาได้เป็นสามส่วน

**ที่มาของเนื้อหา:** ข้อเสนอด้านกระบวนการสำหรับหารือกับลูกค้า

## 04. สิ่งที่ต้องปรับ มี 3 ส่วน

เริ่มที่ 02:20 | เวลาแนะนำ 00:50 นาที

**ประเด็นหลัก:** แยกขอบเขตงานที่ต้องประเมิน

ส่วนแรกคือแอปและฐานข้อมูล ส่วนที่สองคือวิธีจัดเตรียมและรันแอป เช่น การใช้ Container ส่วนที่สามคือการตรวจสอบและส่งมอบผ่าน CI/CD

แต่ละส่วนเริ่มคนละช่วงเวลาได้ เช่น ทำ Build และ Test ของระบบเดิมให้เป็นขั้นตอนก่อน แล้วค่อยพิจารณาเปลี่ยนเทคโนโลยีหรือย้ายฐานข้อมูล

GitLab Runner รองรับการรันงานหลายแบบ การใช้ CI/CD จึงไม่จำเป็นต้องรอให้แอปเป็น Container ส่วนการย้ายฐานข้อมูลต้องประเมิน SQL, Stored Procedure และข้อมูลจริงแยกต่างหาก

**การอธิบาย:** แยกขอบเขตทั้งสามส่วนให้ชัด

**ประโยคเชื่อม:** เทคโนโลยีที่เสนอสำหรับระบบใหม่มีดังนี้

**ที่มาของเนื้อหา:** สามด้านเป็นกรอบเสนอ; ความสามารถ Runner อ้างอิงเอกสาร GitLab

[Sources]

- [GitLab — Runners](https://docs.gitlab.com/ci/runners/)

## 05. เทคโนโลยี สำหรับระบบใหม่

เริ่มที่ 03:10 | เวลาแนะนำ 01:20 นาที

**ประเด็นหลัก:** อธิบายหน้าที่ของเทคโนโลยีเป้าหมาย

ตามข้อมูลที่เสนอ Frontend ใช้ React โดยมี Next.js เป็น Framework ส่วน Java ทำหน้าที่ประมวลผลและให้บริการ API และ PostgreSQL เป็นฐานข้อมูลเป้าหมาย

Next.js ทำงานฝั่ง Server ได้ด้วย จึงต้องตกลงว่าจะวางการยืนยันตัวตน Session และการประมวลผลแต่ละส่วนไว้ที่ใด ภาพนี้เป็นการแบ่งหน้าที่ที่เสนอ ไม่ใช่ข้อจำกัดของ Next.js

การย้ายจาก Oracle หรือ SQL Server ไป PostgreSQL ต้องตรวจ SQL, Procedure, ชนิดข้อมูล และรายงานด้วย ไม่ใช่เปลี่ยนเพียง Connection String ส่วน Java เดิมอาจใช้ต่อได้บางส่วนหลังประเมิน

**การอธิบาย:** อธิบายหน้าที่ของ Frontend, Backend และ Database

**ประโยคเชื่อม:** เมื่อเลือกเทคโนโลยีแล้ว ต้องกำหนดวิธีจัดเตรียมแอปสำหรับรัน

**ที่มาของเนื้อหา:** Stack เป้าหมายจากผู้ใช้; บทบาท React/Next.js จากเอกสารทางการ; รายการประเมินเป็นข้อเสนอ

[Sources]

- [Next.js — Documentation](https://nextjs.org/docs)

## 06. จัดเตรียมแอป ด้วย Container

เริ่มที่ 04:30 | เวลาแนะนำ 01:15 นาที

**ประเด็นหลัก:** อธิบายสิ่งที่ต้องเตรียมเมื่อใช้ Container

Container Image รวมแอปกับ Runtime และ Library ที่เลือกใช้ เพื่อให้มีชุดไฟล์สำหรับนำไปรัน เราต้องกำหนดวิธีสร้าง Image และระบุเวอร์ชันให้ตรวจสอบได้

สิ่งที่ควรตกลงคือ Base Image ที่อนุญาต Package ที่จำเป็น และการรันแบบ Non-root เมื่อเหมาะสม ส่วน Configuration ของแต่ละ Environment และข้อมูลลับต้องจัดการแยกจาก Image

นอกจากนี้ต้องเตรียม Log, Health Check, ที่เก็บข้อมูลถาวร และสิทธิ์การเข้าถึงด้วย การใช้ Container ไม่ได้แทน Application Server ทุกกรณี และไม่ได้หมายความว่าต้องย้ายฐานข้อมูลเข้า Container ตามไปด้วย

**การอธิบาย:** ใช้ตัวอย่างแอปหนึ่งตัว พร้อม Runtime และ Library ที่ต้องใช้

**ประโยคเชื่อม:** จากนั้นมาดูรายการที่ทีมต้องส่งมอบในแต่ละรุ่น

**ที่มาของเนื้อหา:** หลักการสร้าง Image อ้างอิง Docker; รายการมาตรฐานเป็นข้อเสนอที่ต้องตกลง

[Sources]

- [Docker — Building best practices](https://docs.docker.com/build/building/best-practices/)

## 07. รายการส่งมอบ ของแต่ละรุ่น

เริ่มที่ 05:45 | เวลาแนะนำ 01:05 นาที

**ประเด็นหลัก:** สรุปรายการส่งมอบที่ควรเตรียม

สำหรับระบบที่ใช้ Container รายการส่งมอบที่เสนอมีสี่ส่วน คือ Source Code ชุดทดสอบและผล Image ที่จะนำไปรัน และเอกสารประกอบ

เอกสารอาจมีผลสแกน Release Notes วิธีตั้งค่า ขั้นตอน Deploy และวิธี Rollback โดยเลือกตามขอบเขตงานที่ตกลง ไม่ได้หมายความว่าทีมพัฒนาต้องสร้าง Platform หรือ Monitoring ใหม่ทั้งหมด

ควรระบุผู้รับผิดชอบและเกณฑ์รับงานของแต่ละส่วนด้วย งานปรับโครงสร้างหรือย้ายฐานข้อมูลต้องตรวจว่าอยู่ใน SOW หรือขอบเขต MA เดิมหรือไม่

**การอธิบาย:** อธิบายรายการส่งมอบและผู้ที่จะนำไปใช้

**ประโยคเชื่อม:** รายการหนึ่งที่ต้องเตรียมคือผลการตรวจสอบความปลอดภัย

**ที่มาของเนื้อหา:** ข้อเสนอชุดส่งมอบและเกณฑ์รับงาน ไม่ใช่ข้อกำหนดลูกค้าที่ยืนยันแล้ว

## 08. ส่วนที่ต้องตรวจ ก่อนขึ้นระบบ

เริ่มที่ 06:50 | เวลาแนะนำ 01:00 นาที

**ประเด็นหลัก:** อธิบายขอบเขตของการตรวจความปลอดภัย

การตรวจมีหลายส่วน SAST ใช้วิเคราะห์ Source Code ส่วน Dependency Scanning ใช้ตรวจ Library ที่แอปนำมาใช้ Secret Detection ตรวจข้อมูลลับที่อาจอยู่ใน Repository และ Container Scanning ตรวจ Package ใน Image

อีกส่วนคือ DAST ซึ่งตรวจแอปที่รันอยู่แล้วในสภาพแวดล้อมทดสอบที่ได้รับอนุญาต จึงเป็นคนละขั้นตอนกับการสแกน Source Code

รายการนี้เป็นภาพรวมของประเภทการตรวจ ไม่ได้ยืนยันว่าครบทุกความเสี่ยง ต้องกำหนดขอบเขต Branch ที่สแกน และวิธีจัดการผลให้เหมาะกับแต่ละระบบ

**การอธิบาย:** ยกตัวอย่างปัญหาสั้น ๆ เช่น SQL Injection หรือ Token ในโค้ด

**ประโยคเชื่อม:** เมื่อสแกนเสร็จ ยังต้องพิจารณาผลตามเกณฑ์ที่ตกลง

**ที่มาของเนื้อหา:** ประเภทการตรวจอ้างอิงเอกสาร GitLab

[Sources]

- [GitLab — Security detection and scanner configuration](https://docs.gitlab.com/user/application_security/detect/)
- [GitLab — Static application security testing](https://docs.gitlab.com/user/application_security/sast/)
- [GitLab — Dependency scanning](https://docs.gitlab.com/user/application_security/dependency_scanning/)
- [GitLab — Pipeline secret detection](https://docs.gitlab.com/user/application_security/secret_detection/pipeline/)
- [GitLab — Container scanning](https://docs.gitlab.com/user/application_security/container_scanning/)

## 09. การพิจารณาผลสแกน

เริ่มที่ 07:50 | เวลาแนะนำ 01:00 นาที

**ประเด็นหลัก:** แยกสถานะการสแกนออกจากผลการพิจารณาความปลอดภัย

Job สแกนอาจทำงานสำเร็จและสร้างรายงานได้ แม้ในรายงานจะยังมีประเด็นที่ต้องแก้ จึงต้องดูทั้งผลสแกนและเงื่อนไขที่ตั้งไว้ ไม่ดูเพียงสถานะ Pipeline

ต้องตกลงว่าประเด็นระดับใดต้องแก้ก่อน Release ใครวิเคราะห์ผล ใครแก้ และใครอนุมัติข้อยกเว้น โดยใช้เกณฑ์ที่ลูกค้ายืนยัน

ผลตรวจและข้อยกเว้นควรผูกกับรุ่นที่จะใช้งานจริง พร้อมเหตุผลและวันหมดอายุตามกระบวนการที่ตกลง

**การอธิบาย:** อธิบายด้วยตัวอย่าง Job สำเร็จแต่รายงานยังพบประเด็น

**ประโยคเชื่อม:** เครื่องมือที่ใช้ตรวจสามารถทำงานร่วมกับ GitLab ได้หลายตัว

**ที่มาของเนื้อหา:** พฤติกรรมรายงานและการบังคับนโยบายจาก GitLab; ขั้นตอนพิจารณาผลเป็นกรอบเสนอ

[Sources]

- [GitLab — Security detection and scanner configuration](https://docs.gitlab.com/user/application_security/detect/)

## 10. การตรวจใน Pipeline

เริ่มที่ 08:50 | เวลาแนะนำ 01:25 นาที

**ประเด็นหลัก:** อธิบายงานตรวจใน Pipeline และ Amazon ECR สำหรับ Image Scan

ในภาพมี Job gitlab-advanced-sast และ semgrep-sast สำหรับกลุ่มตรวจโค้ด มี gemnasium-maven-dependency_scanning สำหรับ Library และ secret_detection สำหรับข้อมูลลับ ชื่อเหล่านี้เทียบกับหน้าที่ตามเอกสาร GitLab ส่วนรุ่นและกฎที่รันจริงยังต้องดู Template ย่อยและ Job Log

Job kics-iac-sast อยู่ในกลุ่มตรวจไฟล์ตั้งค่าโครงสร้างพื้นฐาน หรือ IaC เช่น Dockerfile และไฟล์ตั้งค่า Deployment ตามชนิดไฟล์ที่รองรับ ต้องแยกจากการตรวจ Package ที่อยู่ภายใน Container Image

ผู้ใช้ยืนยันว่า Image Scan ใช้ Amazon ECR และ Job image-scan เรียก .ecr_docker_scan ตาม Workflow ที่ส่งมา. ยังไม่ยืนยันโหมด Basic / Enhanced และเกณฑ์ผ่าน ต้องดูการตั้งค่า ECR และ Script เพิ่ม

ข้อมูลที่ส่งมายังไม่ยืนยันว่ามี SonarQube ใน Pipeline นี้ ส่วน Trivy และเครื่องมือที่ใช้ตรวจบนเครื่อง Dev เก็บเป็นตัวอย่างใน Notes หน้า 12 ไม่ใช่รายการเครื่องมือที่ยืนยันแล้วของลูกค้า

**การอธิบาย:** อธิบายว่าตรวจอะไรทีละกลุ่ม ชื่อ Job แบบเต็มอยู่ในภาพหน้า 12 ไม่ต้องอ่านชื่อทั้งหมดบนสไลด์นี้

**ประโยคเชื่อม:** ต่อไปเป็นลำดับ Stage สำหรับกรณี UAT เพื่อเทียบกับภาพ Pipeline ในหน้าถัดไป

**ที่มาของเนื้อหา:** หลักฐานของระบบ: ภาพ Pipeline และ YAML ที่ผู้ใช้ส่งมา; หน้าที่ของ Analyzer: เอกสารทางการ; ยังไม่เห็น security-ultimate.gitlab-ci.yml, build.gitlab-ci.yml และ deploy-docker.gitlab-ci.yml; ข้อมูลเพิ่มเติมจากผู้ใช้: Image Scan ใช้ Amazon ECR; ยังไม่ระบุ Basic / Enhanced

[Sources]

- ข้อมูลผู้ใช้ — Image Scan ใช้ Amazon ECR — ยืนยันในบทสนทนาวันที่ 14 ตุลาคม 2026; ไม่ได้ระบุโหมดหรือเกณฑ์ผ่าน
- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- ข้อมูลผู้ใช้ — .gitlab-ci.yml ของ wf4pos-revamp/backend — YAML ที่วางในบทสนทนา: .pipeline_rule, unit-test, build, image-scan, deploy-service และ deploy-service-uat-1/2
- ข้อมูลผู้ใช้ — /workflow/.gitflow-Docker.gitlab-ci.yml — ไฟล์แนบ Pasted text(2).txt: stages บรรทัด 9–13; ตัวอย่าง Maven ที่เป็น Comment บรรทัด 247–277; extends บรรทัด 375–392
- [GitLab — Advanced SAST](https://docs.gitlab.com/user/application_security/sast/gitlab_advanced_sast/)
- [GitLab — SAST analyzers and GitLab-managed Semgrep rules](https://docs.gitlab.com/user/application_security/sast/analyzers/)
- [GitLab — Legacy dependency scanning (Gemnasium)](https://docs.gitlab.com/user/application_security/dependency_scanning/legacy_dependency_scanning/)
- [GitLab — Infrastructure as Code scanning (KICS)](https://docs.gitlab.com/user/application_security/iac_scanning/)
- [GitLab — Pipeline secret detection](https://docs.gitlab.com/user/application_security/secret_detection/pipeline/)
- [AWS - Amazon ECR image scanning (Basic / Enhanced)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)

## 11. ขั้นตอน Pipeline สำหรับ UAT

เริ่มที่ 10:15 | เวลาแนะนำ 01:35 นาที

**ประเด็นหลัก:** อธิบายลำดับ Stage ที่ประกาศไว้สำหรับ UAT ไม่ขยายเป็นกระบวนการ Production ที่ยังไม่ยืนยัน

หน้านี้แสดงลำดับ Stage ที่ประกาศไว้คือ test, build, image-scan และ deploy โดยเลือกกรณี Branch uat ที่ไม่ได้สั่งข้าม Build และ Image Scan รายละเอียดการเลือก Job ต้องอ่าน Rules ของไฟล์แอปร่วมกับ Template

ใน Stage test มี Job สแกนตามภาพ ส่วน unit-test ในไฟล์แอปมี Script เป็น echo แจ้งว่าข้ามการทดสอบ ยังไม่เห็นคำสั่งรัน Unit Test จริงใน Job นี้ ข้อความว่าทดสอบใน Build ต้องตรวจ Script และ Dockerfile ต่อ

Workflow ให้ build เรียก .buildkit_build_image และ Job image-scan เรียก .ecr_docker_scan ตาม Workflow ที่ส่งมา. ผู้ใช้ยืนยันว่า Image Scan ใช้ Amazon ECR. ยังไม่เห็น Script ภายใน Template จึงยังไม่ระบุวิธีเรียกสแกน การรอผล หรือเงื่อนไขหยุด Deploy

ไฟล์แอปกำหนด deploy-service-uat-1 และ deploy-service-uat-2 เป็น Manual ทั้งคู่ โดย Job ที่สองมี needs อ้าง Job แรกและทั้งคู่ตั้ง allow_failure: true จึงไม่ใช้สถานะ Pipeline สำเร็จเป็นหลักฐานว่า Deploy สำเร็จครบสองเครื่อง และยังไม่ยืนยันการจัดการ F5 หรือ Health Check

Rules ที่แอปกำหนดใหม่ไม่เลือก build และ image-scan ใน MR Pipeline และสามารถข้ามสอง Job นี้เมื่อกด Run Pipeline พร้อม ALLOW_BUILD=false ได้ จึงไม่เล่าว่าทุก Commit หรือ MR รันครบเส้นทางนี้ ส่วน SIT, DAST, Production Deploy และกระบวนการอนุมัติยังไม่มีข้อมูลยืนยันในส่วนที่ได้รับ

**การอธิบาย:** ไล่สี่ Stage ตามภาพ ระบุปลายทางว่า UAT และบอกว่าเป็นการกด Deploy ไม่ใช่การยืนยัน Approval Workflow

**ประโยคเชื่อม:** หน้าถัดไปเป็นภาพ Job เพื่ออธิบายงานสแกน และแยกสิ่งที่ Dev ตรวจเองได้ออกจากผลตรวจของ Pipeline

**ที่มาของเนื้อหา:** ลำดับ Stage และ extends จาก Workflow ที่แนบ; เงื่อนไข UAT/MR, Placeholder และ Manual Deploy จาก YAML ของแอป; พฤติกรรม rules, include และ allow_failure อ้างเอกสาร GitLab ไม่ใช่ผลการทดลองรันระบบ; ข้อมูลเพิ่มเติมจากผู้ใช้: Image Scan ใช้ Amazon ECR; ยังไม่ระบุ Basic / Enhanced

[Sources]

- ข้อมูลผู้ใช้ — Image Scan ใช้ Amazon ECR — ยืนยันในบทสนทนาวันที่ 14 ตุลาคม 2026; ไม่ได้ระบุโหมดหรือเกณฑ์ผ่าน
- ข้อมูลผู้ใช้ — .gitlab-ci.yml ของ wf4pos-revamp/backend — YAML ที่วางในบทสนทนา: .pipeline_rule, unit-test, build, image-scan, deploy-service และ deploy-service-uat-1/2
- ข้อมูลผู้ใช้ — /workflow/.gitflow-Docker.gitlab-ci.yml — ไฟล์แนบ Pasted text(2).txt: stages บรรทัด 9–13; ตัวอย่าง Maven ที่เป็น Comment บรรทัด 247–277; extends บรรทัด 375–392
- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- [GitLab — Include และการแทนค่า Configuration](https://docs.gitlab.com/ci/yaml/includes/)
- [GitLab — เงื่อนไขเลือก Job ด้วย rules](https://docs.gitlab.com/ci/jobs/job_rules/)
- [GitLab — Predefined variables และ CI_COMMIT_BRANCH](https://docs.gitlab.com/ci/variables/predefined_variables/)
- [GitLab — Manual jobs และ allow_failure](https://docs.gitlab.com/ci/jobs/job_control/)
- [AWS - Amazon ECR image scanning (Basic / Enhanced)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)

## 12. ตัวอย่าง Pipeline ที่ใช้งาน

เริ่มที่ 11:50 | เวลาแนะนำ 02:00 นาที

**ประเด็นหลัก:** อธิบาย Job ตามหลักฐานล่าสุด พร้อมตัวอย่างตรวจเบื้องต้นบนเครื่อง Dev

ภาพนี้มี Stage test, build, image-scan และ deploy โดยปลายทางที่แสดงเป็น UAT สองเครื่อง ภาพบอกชื่อและสถานะ Job แต่ไม่ได้บอก Engine, Rules หรือสิ่งที่ Script ทำครบทั้งหมด จึงต้องอ่าน YAML ประกอบ

กลุ่มสแกนใน test ประกอบด้วย Gemnasium Maven, Advanced SAST, KICS, Secret Detection และ Semgrep ชื่อเหล่านี้เทียบหน้าที่กับเอกสาร GitLab แต่ยังต้องดู Template ย่อยเพื่อยืนยัน Image ของ Analyzer เวอร์ชันและขอบเขตที่ตรวจจริง

มี Job ชื่อ unit-test แต่ Script ในไฟล์แอปเพียง echo แจ้งว่าข้ามการทดสอบ ยังไม่มีคำสั่งรัน Test ใน Script นี้ ส่วนข้อความ handled in build ต้องตรวจคำสั่ง Build และ Dockerfile ต่อ ตัวอย่าง Maven Test ใน Workflow กลางก็ยังเป็น Comment

ผู้ใช้ยืนยันว่า Image Scan ใช้ Amazon ECR. Job image-scan เรียก .ecr_docker_scan ตาม Workflow ที่ส่งมา. ยังไม่ยืนยันโหมด Basic / Enhanced และเกณฑ์ผ่าน. Trivy ในรายละเอียดด้านล่างเป็นตัวอย่างตรวจบนเครื่อง Dev ไม่ใช่เครื่องมือเดียวกับ Amazon ECR

Dev ตรวจเบื้องต้นได้ด้วยชุดทดสอบของโปรเจกต์และเครื่องมือที่เหมาะกับงาน เช่น Dependency-Check, Semgrep, KICS, Gitleaks และ Trivy ผลในเครื่องไม่แทนผลจาก GitLab ต้องเทียบเครื่องมือ เวอร์ชัน กฎ ขอบเขตไฟล์ และ Image ที่ตรวจ ส่วน Advanced SAST ไม่ถือว่า Semgrep CE ตรวจแทนได้ครบ

**การอธิบาย:** ใช้ประมาณ 2 นาที อธิบาย Amazon ECR และสถานะ unit-test ส่วนคำสั่งสำหรับ Dev เก็บไว้ตอบคำถาม

**ประโยคเชื่อม:** จากตัวอย่าง UAT ต่อไปเป็นเรื่องผู้รับผิดชอบ การอนุมัติ และการย้อนกลับที่ต้องตกลงเพิ่ม ไม่ได้ถือว่าปุ่ม Manual ยืนยันว่ามีกระบวนการเหล่านี้ครบแล้ว

**ที่มาของเนื้อหา:** หลักฐานที่อ่านแล้ว: ภาพต้นฉบับ, YAML ของแอปในบทสนทนา และ /workflow/.gitflow-Docker.gitlab-ci.yml ที่แนบ; ยังไม่ได้รับ Template ย่อย Job Log รายงานจริง หรือข้อมูลยืนยันว่าไฟล์ตรงกับ Commit ในภาพ; ตัวอย่างเครื่องมือ Dev อ้างเอกสารภายนอกและแยกจากข้อเท็จจริงของระบบ; ข้อมูลเพิ่มเติมจากผู้ใช้: Image Scan ใช้ Amazon ECR; ยังไม่ระบุ Basic / Enhanced

### รายละเอียดสำหรับ Dev

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

[Sources]

- ข้อมูลผู้ใช้ — Image Scan ใช้ Amazon ECR — ยืนยันในบทสนทนาวันที่ 14 ตุลาคม 2026; ไม่ได้ระบุโหมดหรือเกณฑ์ผ่าน
- ข้อมูลผู้ใช้ — ภาพ GitLab Pipeline หน้า 12 — Screenshot 2026-10-14 at 03.27.52.png; ภาพต้นฉบับฝังอยู่ใน HTML โดยไม่แก้ไข
- ข้อมูลผู้ใช้ — .gitlab-ci.yml ของ wf4pos-revamp/backend — YAML ที่วางในบทสนทนา: .pipeline_rule, unit-test, build, image-scan, deploy-service และ deploy-service-uat-1/2
- ข้อมูลผู้ใช้ — /workflow/.gitflow-Docker.gitlab-ci.yml — ไฟล์แนบ Pasted text(2).txt: stages บรรทัด 9–13; ตัวอย่าง Maven ที่เป็น Comment บรรทัด 247–277; extends บรรทัด 375–392
- [GitLab — SAST analyzers and GitLab-managed Semgrep rules](https://docs.gitlab.com/user/application_security/sast/analyzers/)
- [GitLab — Legacy dependency scanning (Gemnasium)](https://docs.gitlab.com/user/application_security/dependency_scanning/legacy_dependency_scanning/)
- [GitLab — Advanced SAST](https://docs.gitlab.com/user/application_security/sast/gitlab_advanced_sast/)
- [GitLab — Infrastructure as Code scanning (KICS)](https://docs.gitlab.com/user/application_security/iac_scanning/)
- [GitLab — Pipeline secret detection](https://docs.gitlab.com/user/application_security/secret_detection/pipeline/)
- [Trivy — Container image scanning](https://trivy.dev/docs/latest/guide/target/container_image/)
- [AWS - Amazon ECR image scanning (Basic / Enhanced)](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)
- [AWS CLI - describe-image-scan-findings](https://docs.aws.amazon.com/cli/latest/reference/ecr/describe-image-scan-findings.html)

## 13. การอนุมัติ และการย้อนกลับ

เริ่มที่ 13:50 | เวลาแนะนำ 01:00 นาที

**ประเด็นหลัก:** ระบุจุดตรวจ ผู้อนุมัติ และขั้นตอนย้อนกลับ

ส่วนนี้เป็นข้อเสนอเรื่องผู้รับผิดชอบและการเตรียมขึ้นระบบ ไม่ใช่การยืนยันว่าตัวอย่าง UAT มี Approval Workflow ครบแล้ว CI/CD ช่วยทำงานซ้ำตามขั้นตอนที่กำหนด แต่ยังต้องระบุว่าใครตรวจโค้ด ใคร Merge ได้ ใครอนุมัติ Release และใครมีสิทธิ์ Deploy

GitLab มี Protected Environments และ Deployment Approvals ในระดับที่รองรับ วิธีที่ใช้จริงต้องดู Subscription และการตั้งค่าของลูกค้า

ก่อนใช้งานจริงควรมีวิธีตรวจหลัง Deploy และแผน Rollback ที่ทดสอบแล้ว หากมีการเปลี่ยนข้อมูล ต้องมีแผนข้อมูลแยกด้วย เพราะการย้อนเวอร์ชันแอปไม่ได้ย้อนข้อมูลในฐานข้อมูลให้อัตโนมัติ

**การอธิบาย:** อธิบายว่าแต่ละจุดมีใครรับผิดชอบและต้องเตรียมอะไร

**ประโยคเชื่อม:** หน้าที่เหล่านี้ต้องตกลงร่วมกับทีมของเมืองไทย

**ที่มาของเนื้อหา:** ความสามารถอนุมัติจาก GitLab; การกำหนดสิทธิ์และแผนย้อนกลับเป็นข้อเสนอ

[Sources]

- [GitLab — Deployment approvals](https://docs.gitlab.com/ci/environments/deployment_approvals/)

## 14. การทำงานร่วมกับ เมืองไทย

เริ่มที่ 14:50 | เวลาแนะนำ 01:30 นาที

**ประเด็นหลัก:** สรุปเรื่องที่ต้องตกลงกับเมืองไทย

การแบ่งหน้าที่ในหน้านี้เป็นตัวอย่างสำหรับคุยกับลูกค้า ยังไม่ใช่หน้าที่ที่ตกลงแล้ว ต้องยืนยันว่าใครดูแล Pipeline Template, Runner, Registry, Runtime, Secret และสิทธิ์ Deploy

ทีมพัฒนาเตรียมโค้ดที่ Build ได้ ชุดทดสอบ และข้อมูลสำหรับวิเคราะห์ผลสแกน ส่วนงาน Platform และผู้อนุมัติความเสี่ยงต้องระบุผู้รับผิดชอบตามที่ตกลงกัน

ก่อนเริ่ม ควรขอ Pipeline Template เกณฑ์ที่ใช้ตรวจรับ และรายชื่อผู้รับผิดชอบหรือผู้อนุมัติ แล้วจึงกำหนดรายการส่งมอบให้ตรงกัน

งานสร้าง Platform, Major Upgrade หรือย้ายฐานข้อมูลต้องตรวจตาม SOW และแยกจากงาน MA เดิมเมื่ออยู่นอกขอบเขต

**การอธิบาย:** ระบุข้อมูลที่ยังขาดและต้องขอจากลูกค้า

**ประโยคเชื่อม:** เมื่อทราบข้อกำหนดและผู้รับผิดชอบแล้ว จึงเลือกงานที่จะเริ่มปรับ

**ที่มาของเนื้อหา:** ข้อเสนอเพื่อหารือกับเมืองไทย; ไม่มีการยืนยันขั้นตอนภายในหรือการมอบหมายหน้าที่จริง

## 15. แผนเริ่มต้น ปรับระบบ

เริ่มที่ 16:20 | เวลาแนะนำ 01:30 นาที

**ประเด็นหลัก:** เสนอขั้นตอนเริ่มต้นปรับระบบ

เริ่มจากสำรวจระบบเดิม ทั้ง Library ระบบเชื่อมต่อ ข้อมูล ชุดทดสอบ และข้อจำกัดของ Platform จากนั้นเลือกหนึ่งระบบหรือหนึ่งโมดูลที่กำหนดขอบเขตและผู้รับผิดชอบได้

งานนำร่องอาจเริ่มจาก Build, Test และ Scan ของระบบเดิมก่อน ไม่จำเป็นต้องเขียนระบบใหม่ทั้งหมด แล้วค่อยเลือกส่วนที่เหมาะจะใช้เทคโนโลยีหรือ Container ตามเป้าหมาย

ระหว่างทดลองต้องตรวจฟังก์ชัน ประสิทธิภาพ ความปลอดภัย และการดูแล หากย้ายฐานข้อมูลต้องมีแผนตรวจข้อมูล การสลับใช้งาน และการกู้คืนแยกด้วย

เมื่อแก้ปัญหาและผ่านเกณฑ์แล้ว จึงนำขั้นตอนที่ได้ไปใช้กับระบบถัดไป และตรวจให้ครบก่อนเลิกใช้ส่วนเดิม

**การอธิบาย:** อธิบายลำดับงาน โดยยังไม่กำหนดระยะเวลาโครงการที่ไม่ได้ประเมิน

**ประโยคเชื่อม:** ก่อนนำไปใช้จริง ต้องตรวจความพร้อมตามเกณฑ์ที่ตกลง

**ที่มาของเนื้อหา:** แผนเปลี่ยนผ่านที่เสนอสำหรับงานนี้ ไม่ใช่กำหนดการที่ตกลงแล้ว

## 16. ตรวจความพร้อม ก่อนใช้งานจริง

เริ่มที่ 17:50 | เวลาแนะนำ 01:05 นาที

**ประเด็นหลัก:** สรุปสิ่งที่ต้องตรวจให้ครบก่อนใช้งานจริง

ควรตรวจทั้งฟังก์ชันและข้อมูล ทดสอบการกู้คืนหรือย้อนกลับ และเตรียมคู่มือกับทีมรับดูแล ไม่ใช้เพียงสถานะ Deploy สำเร็จเป็นเกณฑ์รับงาน

ข้อมูลที่ใช้ติดตามได้ เช่น เวลาที่ใช้ส่งมอบแต่ละรุ่น จำนวนครั้งที่ Deploy ไม่สำเร็จ ประเด็นความปลอดภัยคงค้าง และผลการทดสอบกู้คืน

ควรเก็บข้อมูลก่อนเริ่มปรับเพื่อใช้เปรียบเทียบ แล้วตกลงเป้าหมายจากข้อมูลจริง ยังไม่ควรสรุปว่าจะเร็วขึ้นหรือประหยัดเท่าไรจนกว่าจะมีผลทดสอบ

**การอธิบาย:** ระบุเกณฑ์ที่ต้องตกลงและหลักฐานที่ต้องเก็บ

**ประโยคเชื่อม:** ส่วนที่ต้องทำต่อจากการคุยครั้งนี้มีสามเรื่อง

**ที่มาของเนื้อหา:** ข้อเสนอเกณฑ์รับงานและตัวชี้วัด ไม่มีตัวเลขผลลัพธ์ที่อ้างว่าเกิดขึ้นแล้ว

## 17. สิ่งที่ต้องทำ ต่อจากนี้

เริ่มที่ 18:55 | เวลาแนะนำ 00:45 นาที

**ประเด็นหลัก:** สรุปงานที่ต้องทำต่อและเปิดถามตอบ

เรื่องที่จะต้องทำต่อคือยืนยันมาตรฐานกับเมืองไทย เลือกระบบหรือโมดูลที่จะเริ่มปรับ และกำหนดผู้รับผิดชอบกับเกณฑ์รับงาน

เมื่อได้ข้อมูลครบแล้ว จึงประเมินขอบเขต แผนงาน และสิ่งที่ต้องเตรียมของแต่ละทีม

ช่วงถามตอบสามารถคุยต่อได้ว่า ระบบใดเหมาะจะเริ่ม และยังต้องขอข้อมูลส่วนใดจากลูกค้า

**การอธิบาย:** สรุปสามเรื่องแล้วเปิดรับคำถาม

**ประโยคเชื่อม:** ถามตอบประมาณ 2 นาที

**ที่มาของเนื้อหา:** ข้อเสนอการดำเนินการต่อ


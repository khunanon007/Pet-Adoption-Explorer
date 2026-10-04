# Pet Adoption Explorer — Sprint 1 Report

**Final Term Project:** CP352301 Script Programming  
**Sprint:** Sprint 1 — Application Foundation  
**Period:** Week 12  
**Presentation:** 15–16 September 2026  
**Due Date:** 18 September 2026  
**Status:** ✅ Completed  
**Repository:** https://github.com/khunanon007/Pet-Adoption-Explorer  
**Pull Request:** #2  

---

## 1. Sprint Overview

Sprint 1 มุ่งเน้นการวางโครงสร้างพื้นฐาน (Application Foundation) สำหรับโครงการ Pet Adoption Explorer ในรูปแบบ Command Line Interface (CLI) แอปพลิเคชันพัฒนาขึ้นเพื่อทดสอบและรองรับฟังก์ชันการทำงานหลักของระบบค้นหาและสำรวจข้อมูลสัตว์เลี้ยงเพื่อการรับเลี้ยง ได้แก่ ระบบเมนูนำทาง (Menu Navigation), การรับและตรวจสอบข้อมูลเข้า (User Input Validation), การค้นหาข้อมูลสัตว์เลี้ยง (Search), การแสดงสถิติการรับเลี้ยง (Adoption Statistics), การจำแนกประเภทสัตว์เลี้ยง (Species/Breeds) และการแสดงรายการสัตว์เลี้ยงที่ต้องการบ้านด่วน (Urgent Adoption)[cite: 5]

ในระยะนี้ ระบบทำงานร่วมกับ Local Sample Dataset จำนวน 8 รายการในรูปแบบโครงสร้างข้อมูลภายในภาษา Python (In-Memory Data Structure) โดยยังไม่มีการเชื่อมต่อกับภายนอก เช่น API, Database (SQLite) หรือ Web UI (Streamlit) เพื่อให้แน่ใจว่าลอจิกการทำงานของระบบเสถียร ปลอดภัย และไม่เกิดข้อผิดพลาดในการทำงาน (Crash)

---

## 2. Sprint Goal

พัฒนาระบบ CLI Foundation สำหรับ Pet Adoption Explorer ที่มีฟังก์ชันการทำงานพื้นฐานครบถ้วนและสมบูรณ์:

* แสดงข้อความต้อนรับ (Welcome Message) และเมนูหลัก (Main Menu) ได้อย่างถูกต้อง
* รับ Input และตรวจสอบความถูกต้อง (Input Validation) เพื่อป้องกันกรณีระบุข้อมูลผิดพลาด เช่น ข้อความว่างเปล่า, ตัวอักษรแทนตัวเลข, ค่าติดลบ หรือตัวเลือกนอกเหนือจากรายการ
* แสดงรายการสัตว์เลี้ยงทั้งหมดพร้อมรายละเอียด (Name, Species, Breed, Age, Status)
* ค้นหาข้อมูลสัตว์เลี้ยงจากชื่อหรือสายพันธุ์แบบ Partial Match และ Case-insensitive
* คำนวณและแสดงสถิติการรับเลี้ยงสัตว์พื้นฐาน (จำนวนรวม, อายุเฉลี่ย, จำนวนสัตว์ต้องการบ้านด่วน)
* แยกแยะและแสดงประเภทสัตว์เลี้ยง (Species) พร้อมสายพันธุ์ (Breeds)
* กรองและแสดงผลเฉพาะรายการสัตว์เลี้ยงที่ต้องการบ้านด่วน (Urgent Adoption)
* จัดการข้อผิดพลาดขณะรันโปรแกรม (Exception Handling) เพื่อให้ออกจากโปรแกรมได้อย่างถูกต้องและปลอดภัย

---

## 3. Team Members & Roles

| สมาชิก | บทบาท | ขอบเขตความรับผิดชอบหลัก |
| :--- | :--- | :--- |
| **วาเรน** | Planner | วางแผนงาน วางโครงสร้าง Scope ของ Sprint 1 กำหนด Requirements และประสานงาน |
| **ฟีฟ่า** | Coder | เขียนฟังก์ชันหลักทั้งหมดของ CLI Application |
| **โดนัท** | Debugger | ทดสอบระบบ (QA Testing) ตรวจสอบ Bugs ปรับแต่ง Exception Handling และยืนยันความถูกต้องของผลลัพธ์ |
| **ภีม** | Coder | ออกแบบ Architecture พัฒนาโค้ดและ Main Logic |

---

## 4. Scope (In Scope & Out of Scope)

### In Scope
* Command Line Interface (CLI) Application
* Welcome Message และ Main Menu Navigation
* Menu Input Validation & Exception Handling (ป้องกัน Program Crash)
* View All Pets (แสดงรายการสัตว์เลี้ยงทั้งหมด 8 รายการ)
* Search Pet (ค้นหาตามชื่อ/สายพันธุ์)
* View Adoption Statistics (คำนวณและแสดงสถิติภาพรวม)
* View Species & Breeds (จำแนกชนิดและสายพันธุ์)
* View Urgent Adoption Pets (กรองสัตว์เลี้ยงสถานะ Urgent)
* Local Sample Dataset (โครงสร้างข้อมูลสัตว์เลี้ยง 8 รายการ)

### Out of Scope
* External API Integration (e.g., Petfinder API)
* Database Storage (SQLite / PostgreSQL)
* Web User Interface (Streamlit Framework)
* Automated Unit Testing Frameworks (pytest / unittest)
* CI/CD Pipelines
* AI Matching / Recommendation Algorithm

---

## 5. Functional Requirements

* **FR-01 — Welcome Message:** ระบบต้องแสดงข้อความต้อนรับเข้าสู่ระบบ Pet Adoption Explorer พร้อมคำอธิบายสั้นๆ เมื่อเริ่มต้นใช้งาน
* **FR-02 — Main Menu:** ระบบต้องแสดงเมนูหลัก 6 ตัวเลือก ให้ผู้ใช้เลือก ได้แก่:
  1. View Pets (ดูรายการสัตว์เลี้ยงทั้งหมด)
  2. Search Pet (ค้นหาสัตว์เลี้ยง)
  3. View Adoption Statistics (ดูสถิติการรับเลี้ยง)
  4. View Species & Breeds (ดูประเภทและสายพันธุ์สัตว์เลี้ยง)
  5. View Urgent Adoption Pets (ดูสัตว์เลี้ยงที่ต้องการบ้านด่วน)
  6. Exit (ออกจากระบบ - พิมพ์ 0)
* **FR-03 — Menu Input:** ระบบต้องสามารถรับ Input จากผู้ใช้เพื่อเลือกเมนูการทำงานได้
* **FR-04 — Input Validation:** ระบบต้องตรวจสอบ Input ทุกครั้ง หากผู้ใช้ป้อนค่าว่าง (Blank), ข้อความที่ไม่ใช่ตัวเลข (Non-numeric), ค่าติดลบ หรือตัวเลขอันดับที่ไม่มีในเมนู ระบบต้องแจ้งเตือนและรับค่าใหม่โดยไม่ Crash
* **FR-05 — Search Pet:** ระบบต้องรองรับการค้นหาสัตว์เลี้ยงจากชื่อ (Name) หรือสายพันธุ์ (Breed) โดยไม่จำกัดตัวพิมพ์เล็ก-ใหญ่ (Case-insensitive) และรองรับการพิมพ์เพียงบางส่วน (Partial Match)
* **FR-06 — Return to Main Menu:** ระบบต้องวนลูปกลับมาแสดงเมนูหลักหลังจากทำงานแต่ละฟังก์ชันเสร็จสิ้น จนกว่าผู้ใช้จะเลือกเมนูออก
* **FR-07 — Safe Exit:** ระบบต้องสามารถออกจากโปรแกรมได้อย่างปลอดภัยเมื่อผู้ใช้พิมพ์ 0 พร้อมแสดงข้อความกล่าวขอบคุณ

---

## 6. Local Sample Dataset

ข้อมูลสัตว์เลี้ยงสำหรับการทดสอบใน Sprint 1 มีจำนวนทั้งหมด 8 รายการ ดังตารางต่อไปนี้:

| ID | Name | Species | Breed | Age (Years) | Health Status |
| :-: | :--- | :--- | :--- | :-: | :--- |
| 1 | Luna | Cat | Domestic Shorthair | 2 | Healthy |
| 2 | Max | Dog | Golden Retriever | 3 | Vaccinated |
| 3 | Milo | Dog | Beagle | 1 | Vaccinated |
| 4 | Oliver | Cat | Siamese | 4 | Healthy |
| 5 | Bella | Rabbit | Holland Lop | 1 | Healthy |
| 6 | Charlie | Dog | Labrador | 2 | Vaccinated |
| 7 | Coco | Bird | Cockatiel | 1 | Healthy |
| 8 | Rocky | Dog | German Shepherd | 5 | Urgent |

---

## 7. Application Flow & Main Functions

### Application Flow

- Start: display_welcome_message()
- Main Menu Loop: display_main_menu() -> get_menu_choice()
- Option 1: view_pets()
- Option 2: search_pet()
- Option 3: view_statistics()
- Option 4: view_species()
- Option 5: view_urgent_pets()
- Option 0: main() Exit

### Main Functions Summary

| ชื่อฟังก์ชัน Python | หน้าที่และความรับผิดชอบ |
| :--- | :--- |
| display_welcome_message() | แสดงข้อความต้อนรับเข้าสู่ระบบ Pet Adoption Explorer |
| display_main_menu() | แสดงรายการเมนูหลัก (Option 1-5, 0) |
| get_menu_choice() | รับ Input จากผู้ใช้ พร้อมตรวจสอบ Input Validation และ Exception Handling |
| view_pets(dataset) | วนลูปแสดงข้อมูลสัตว์เลี้ยงทั้งหมด 8 รายการ จัดรูปแบบในลักษณะตาราง/รายการ |
| search_pet(dataset) | รับคำค้นหา ค้นหาสัตว์เลี้ยงจากชื่อ/สายพันธุ์แบบ Case-insensitive และ Partial Match |
| view_statistics(dataset) | คำนวณจำนวนสัตว์เลี้ยงรวม, อายุเฉลี่ย และจำนวนสัตว์เลี้ยงที่ต้องการบ้านด่วน |
| view_species(dataset) | จัดกลุ่มประเภทสัตว์เลี้ยง (Species) พร้อมแสดงสายพันธุ์ (Breeds) ทั้งหมดที่มี |
| view_urgent_pets(dataset) | กรองและแสดงเฉพาะสัตว์เลี้ยงที่มี Health Status เป็น Urgent |
| main() | ฟังก์ชันหลักสำหรับควบคุม Control Flow และ State ของโปรแกรมทั้งหมด |

---

## 8. Implemented Features

* **View All Pets (ฟังก์ชันดูรายการสัตว์เลี้ยง):**  
  แสดงรายการสัตว์เลี้ยงครบทั้ง 8 ตัว จัดรูปแบบชัดเจน ระบุ Name, Species, Breed, Age และ Status

* **Search Pet (ฟังก์ชันค้นหาสัตว์เลี้ยง):**  
  ค้นหาได้แม่นยำ ตัวอย่างเช่น พิมพ์คำว่า "Golden" หรือ "golden" ระบบสามารถแสดงผลลัพธ์ของ Max (Golden Retriever) ได้ถูกต้อง หากไม่พบข้อมูล ระบบจะแสดงข้อความเตือนอย่างสุภาพโดยไม่หยุดการทำงาน

* **View Adoption Statistics (ฟังก์ชันแสดงสถิติ):**  
  * แสดงสถิติรวม: Total Pets: 8 ตัว
  * คำนวณอายุเฉลี่ย (Average Age): (2 + 3 + 1 + 4 + 1 + 2 + 1 + 5) / 8 = 2.38 ปี
  * แสดงจำนวนสัตว์ที่ต้องการบ้านด่วน (Urgent Pets Count): 1 ตัว (Rocky)

* **View Species & Breeds (ฟังก์ชันแสดงประเภทและสายพันธุ์):**  
  จัดกลุ่มประเภทสัตว์เลี้ยง เช่น Dog (4 ตัว: Golden Retriever, Beagle, Labrador, German Shepherd), Cat (2 ตัว: Domestic Shorthair, Siamese), Rabbit (1 ตัว: Holland Lop), Bird (1 ตัว: Cockatiel)

* **View Urgent Adoption Pets (ฟังก์ชันแสดงสัตว์เลี้ยงต้องการบ้านด่วน):**  
  คัดกรองและแสดงเฉพาะ Rocky (Dog / German Shepherd / Age 5 / Status: Urgent) เพื่อความสะดวกในการช่วยเหลือสัตว์เลี้ยงด่วน

---

## 9. QA Test Cases & Summary

### QA Test Cases Table

| Case ID | Test Scenario | Input | Expected Result | Status |
| :-: | :--- | :-: | :--- | :-: |
| **TC-01** | Display Welcome Message | - | แสดงข้อความต้อนรับระบบเมื่อเริ่มโปรแกรม | PASS |
| **TC-02** | Display Main Menu | - | แสดงรายการเมนู 1-5 และ 0 ได้ครบถ้วน | PASS |
| **TC-03** | Valid Menu Selection | 1 | เข้าสู่ฟังก์ชัน view_pets() แสดงข้อมูล 8 รายการ | PASS |
| **TC-04** | Invalid Menu - Non-numeric | abc | แสดงข้อความแจ้งเตือนป้อนข้อมูลไม่ถูกต้อง และขอให้กรอกใหม่ | PASS |
| **TC-05** | Invalid Menu - Out of Range | 9 | แสดงข้อความแจ้งเตือนตัวเลือกไม่อยู่ในเมนู | PASS |
| **TC-06** | Invalid Menu - Blank | [Enter] | แสดงข้อความแจ้งเตือนห้ามเว้นว่าง | PASS |
| **TC-07** | Invalid Menu - Negative | -1 | แสดงข้อความแจ้งเตือนค่าไม่อยู่ในช่วงที่กำหนด | PASS |
| **TC-08** | Search Pet - Exact Match | Luna | แสดงผลลัพธ์ของ Luna ได้ถูกต้อง | PASS |
| **TC-09** | Search Pet - Partial & Case-insensitive | golden | แสดงผลลัพธ์ของ Max (Golden Retriever) | PASS |
| **TC-10** | Search Pet - Not Found | Elephant | แสดงข้อความ "No pets found matching your query" | PASS |
| **TC-11** | View Statistics Calculation | 3 | แสดง Total: 8, Avg Age: 2.38, Urgent: 1 | PASS |
| **TC-12** | View Species & Breeds Grouping | 4 | แสดงแยกหมวดหมู่ Dog, Cat, Rabbit, Bird ได้ถูกต้อง | PASS |
| **TC-13** | View Urgent Adoption Filter | 5 | แสดงเฉพาะ Rocky (Status: Urgent) | PASS |
| **TC-14** | Safe Exit Program | 0 | แสดงข้อความขอบคุณและออกจากโปรแกรมอย่างปลอดภัย | PASS |

### QA Testing Summary
* **Total Test Cases:** 14
* **Passed:** 14
* **Failed:** 0
* **Pass Rate:** 100%

---

## 10. Contribution Matrix

| สมาชิก | หน้าที่หลัก | การประเมินตนเอง (%) | การประเมินโดยทีม (%) | สรุปผลการมีส่วนร่วม (%) |
| :--- | :--- | :-: | :-: | :-: |
| **วาเรน** | Planner | 50 / 50 | 50 / 50 | **100%** |
| **ฟีฟ่า** | Coder | 50 / 50 | 50 / 50 | **100%** |
| **ภีม** | Coder | 50 / 50 | 50 / 50 | **100%** |
| **โดนัท** | Debugger | 50 / 50 | 50 / 50 | **100%** |

> **หมายเหตุ:** สมาชิกทุกคนในทีมปฏิบัติงานครบถ้วนตามภาระหน้าที่ที่ได้รับมอบหมายใน Sprint 1 และได้รับการประเมินความพึงพอใจในระดับสมบูรณ์ (100%)

---

## 11. Wow! & Whoops!

### 🌟 Wow! (สิ่งที่ทำได้ดี)
* **Modular Structure:** การแบ่งฟังก์ชันแยกจากกันอย่างเป็นระบบ ทำให้โค้ดอ่านง่าย สามารถนำไปต่อยอดรับ API/Database ใน Sprint ถัดไปได้ทันที
* **Robust Input Validation:** ออกแบบการดักจับข้อผิดพลาดอย่างครอบคลุม ทั้งค่าว่าง, ตัวอักษร และตัวเลขนอกช่วง ทำให้โปรแกรมมีความเสถียรสูง
* **Flexible Search Engine:** ระบบค้นหารองรับ Partial Match และ Case-insensitive ช่วยให้ค้นหาสัตว์เลี้ยงได้สะดวกยิ่งขึ้น
* **Comprehensive QA Coverage:** มีการทดสอบคลอบคลุมถึง 14 Test Cases และได้ Pass Rate 100%

### ⚠️ Whoops! (ปัญหาที่พบและแนวทางแก้ไข)
* **ปัญหาที่พบ:** ในช่วงแรกของการพัฒนา เมื่อผู้ใช้ป้อนตัวอักษรลงในช่องเลือกเมนู โปรแกรมเกิดข้อผิดพลาด ValueError เนื่องจากเกิดความพยายามในการแปลง String เป็น Integer (int()) ส่งผลให้โปรแกรม Crash ทันที
* **แนวทางแก้ไข:** ทีมงาน (ออม และ ฟลุ๊ค) ร่วมกันปรับปรุงฟังก์ชัน get_menu_choice() โดยครอบด้วยโครงสร้าง try-except ValueError และสร้าง Validation Loop เพื่อแจ้งเตือนผู้ใช้และรับค่าใหม่จนกว่าจะถูกต้อง ช่วยแก้ปัญหานี้ได้อย่างสมบูรณ์

---

## 12. Sprint 1 Final Status

- **Foundation CLI System:** COMPLETE
- **Main Menu & Navigation:** COMPLETE
- **Input Validation & Exception Handling:** COMPLETE
- **View / Search / Stats / Species / Urgent Functions:** COMPLETE
- **QA Test Pass Rate:** 100% (14/14 Passed)
- **Status:** ✅ COMPLETED

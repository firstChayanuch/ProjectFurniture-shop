# ProjectFurniture-shop

## บทนำ (Assignment 3) 

เฟอร์นิเจอร์ เป็นธุรกิจที่มีการนำ smart contract Smart Contract มาใช้ เพื่อพัฒนาธุรกิจให้ง่าย สะดวก รวดเร็ว โปร่งใส และมีความปลอดภัย สำหรับผู้ใช้ที่ต้องการดูข้อมูลและรายละเอียดเกี่ยวกับของตกแต่งบ้าน สามารถดูข้อมูลได้จากทางเว็บไซต์ ``` Furniture-shop ```  โดยไม่ต้องเสียเวลาเดินทางเข้ามาสอบถามรายละเอียดด้วยตนเองโดยงตรง สามารถเลือกซื้อสินค้าได้สะดวกรวดเร็ว

#### โดยทางโครงการได้นำโปรเจค pet-shop จากที่อาจารย์ได้สอนมาพัฒนา ปรับเปลี่ยนให้เป็นเว็บไซต์ Furniture-shop โดยมีขั้นตอนดังต่อไปนี้

## 1. กำหนดค่าสิ่งแวดล้อม
#### 1.1 สร้างไดเร็กทอรีสำหรับบันทึกโปรเจ็คนี้ เช่น ใช้คำสั่งต่อไปนี้เพื่อสร้างและย้ายเข้าไปยังไดเร็กทอรี่ชื่อ  Furniture-shop ไว้ใน DApp ซึ่งอยู่ใน Document

```
mkdir Furniture-shop
cd Furniture-shop
```
#### 1.2 ดาวน์โหลดโครงสร้างของโปรเจ็ค pet-shop ซึ่งมีอยู่ใน Truffle Framework โดยใช้คำสั่งต่อไปนี้

```
truffle unbox pet-shop
```
#### 1.3 ใช้คำสั่ง ```ls -l``` เพื่อดูโครงสร้างของโปรเจ็ค สังเกตว่า มีไดเร็กทอรี่และไฟล์ที่สำคัญต่อไปนี้

- contracts: เป็นไดเร็กทอรีที่ใช้เก็บ Smart Contracts ที่เขียนด้วยภาษา Solidity
- migrations: เป็นไดเร็กทอรีที่ใช้เก็บไฟล์ JavaScript ซึ่งเป็นโค้ดที่ใช้ในการจัดการ Smart Contracts ให้ลงไปยังบล็อกเชน
- src: เป็นไดเร็กทอรีที่ใช้เก็บไฟล์ที่เกี่ยวข้องกับ Web Application เช่น JavaScript, CSS, HTML, images เป็นต้น
- test: เป็นไดเร็กทอรีใช้ที่เก็บไฟล์ Solidity หรือ JavaScript ก็ได้ ที่ใช้เพื่อทดสอบ Smart Contracts
- truffle-config.js: คือไฟล์ที่ใช้ในการกำหนดค่าของโปรเจ็ค

#### 1.4 เปิด Visual Studio Code ที่ VirtualBox โดยไปที่ ``` File/Open Folder/Document/DApp/home-sale``` แล้วกด OK

## 2. สร้าง Smart Contract
#### 2.1. Adoption Smart Contract

ใช้ Visual Studio Code เพื่อสร้างไฟล์ชื่อ Adoption.sol ในไดเร็กทอรี contracts โดยมีโค้ดดังนี้

```
pragma solidity ^0.5.0;
contract Adoption {
    address[12] public adopters;
    function adopt(uint petId) public returns (uint) {
        require(petId >= 0 && petId <=11);
        adopters[petId] = msg.sender;
        return petId;
    }
    function getAdopters() public view returns (address[12] memory) {
        return adopters;
    }
}
```

#### 2.2. Compile และ Migrate
#### ทำการคอมไพล์ Smart Contracts โดยใช้คำสั่ง

```
truffle compile
```
ตรวจสอบว่า สามารถคอมไพล์ได้สำเร็จก่อนทำขั้นตอนต่อไป

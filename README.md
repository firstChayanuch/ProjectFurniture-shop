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

### 2.2. compile และ migrate
ทำการคอมไฟล์ Smart Contracts โดยใช้คำสั่ง


โปรดตรวจสอบว่า สามารถคอมไพล์ได้สำเร็จก่อนทำในขั้นตอนต่อไป

ใช้ Visual Studio Code ในการสร้างไฟล์ 2_deploy_contracts.js ในไดเร็กทอรี migrations ดังนี้

```
var Adoption = artifacts.require("Adoption");

module.exports = function(deployer) {
  deployer.deploy(Adoption);
};
```

เปิดโปรแกรม Ganache โดยการใช้เมาส์ดับเบิลคลิกที่ชื่อไฟล์ จากนั้นคลิกที่ New Workspace ในกรณีที่ใช้งานครั้งแรก ครั้งต่อไปไม่จำเป็นต้องสร้าง Workspace ใหม่ทุกครั้ง

![ganache](https://user-images.githubusercontent.com/77536689/104815368-a5599a80-5846-11eb-9e40-cdcff82b1a51.jpg)

ที่ Workspace Name ให้ตั้งชื่อเช่น CNF274 แล้วคลิก Save Workspace

![Addproject](https://user-images.githubusercontent.com/77536689/104815399-dfc33780-5846-11eb-832e-cf16bd9207f2.jpg)

ผลลัพธ์ที่ได้เป็นดังรูป โดย Ganache สร้างบัญชีให้ 10 บัญชี แต่ละบัญชีมี 100 ETH โดยดีฟอล์ต

![Account](https://user-images.githubusercontent.com/77536689/104815405-f49fcb00-5846-11eb-9a38-60ea0f4d5d75.jpg)

เมื่อ Ganache ทำงานได้ดังรูปข้างต้น ขั้นตอนต่อไปคือการ migrate ทำได้โดยใช้คำสั่งต่อไปนี้

```
truffle migrate
```

### 2.3. ทดสอบ Smart Contract
ใช้ Visual Studio Code ในการสร้างไฟล์ TestAdoption.sol เพื่อทดสอบ Adoption.sol และบันทึกลงในไดเร็กทอรี test 

```
pragma solidity ^0.5.0;

import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../contracts/Adoption.sol";

contract TestAdoption {
  // The address of the adoption contract to be tested
  Adoption adoption = Adoption(DeployedAddresses.Adoption());

  // The id of the pet that will be used for testing
  uint expectedPetId = 8;

  //The expected owner of adopted pet is this contract
  address expectedAdopter = address(this);

  function testUserCanAdoptPet() public {
    uint returnedId = adoption.adopt(expectedPetId);
    Assert.equal(returnedId, expectedPetId, "Adoption of the expected pet should match what is returned.");
  }

  // Testing retrieval of a single pet's owner
  function testGetAdopterAddressByPetId() public {
    address adopter = adoption.adopters(expectedPetId);
    Assert.equal(adopter, expectedAdopter, "Owner of the expected pet should be this contract");
  }

  // Testing retrieval of all pet owners
  function testGetAdopterAddressByPetIdInArray() public {
    // Store adopters in memory rather than contract's storage
    address[16] memory adopters = adoption.getAdopters();
    Assert.equal(adopters[expectedPetId], expectedAdopter, "Owner of the expected pet should be this contract");
  }
}
```
ต่อไปคือ การรันการทดสอบที่เขียนไว้ในไดเร็กทอรี test โดยใช้คำสั่งต่อไปนี้

```
truffle test
```
หากผลการทดสอบผ่านทั้ง 3 กรณีจะได้ผลลัพธ์ดังรูปต่อไปนี้
```
   Using network 'development'.

   Compiling your contracts...
   ===========================
   > Compiling ./test/TestAdoption.sol
   > Artifacts written to /var/folders/z3/v0sd04ys11q2sh8tq38mz30c0000gn/T/test-11934-19747-g49sra.0ncrr
   > Compiled successfully using:
      - solc: 0.5.0+commit.1d4f565a.Emscripten.clang

     TestAdoption
       ✓ testUserCanAdoptPet (91ms)
       ✓ testGetAdopterAddressByPetId (70ms)
       ✓ testGetAdopterAddressByPetIdInArray (89ms)


     3 passing (670ms)
```

## 3. ออกแบบ UI เพื่อใช้เชื่อมต่อกับผู้ใช้
ส่วนติดต่อกับผู้ใช้ เป็นดังรูปต่อไปนี้

![web](https://user-images.githubusercontent.com/77536689/104815480-6aa43200-5847-11eb-847a-cd792b7612d6.jpg)

สร้างผลลัพธ์เช่นรูปข้างต้นได้โดยใช้ไฟล์ ```src/index.html``` โปรดเปิดไฟล์นี้โดยใช้ Visual Studio Code และสำรวจโครงสร้างของไฟล์ สังเกตได้ว่า มีส่วนที่เป็น Template ในขณะที่ข้อมูลที่ใช้ในการแสดงผลจะถูกกำหนดโดยส่วน Backend

## 4. สร้าง Backend ที่สามารถเชื่อมต่อกับ Smart Contract
แก้ไขไฟล์ ```src/js/app.js``` ให้มีโค้ดดังนี้

```
App = {
 web3Provider: null,
 contracts: {},
 
 init: async function() {
   // Load furnitures.
   $.getJSON('../Furniture.json', function(data) {
     var furnituresRow = $('#FurnituresRow');
     var furnitureTemplate = $('#FurnitureTemplate');
 
     for (i = 0; i < data.length; i ++) {
       furnitureTemplate.find('.panel-title').text(data[i].name);
       furnitureTemplate.find('img').attr('src', data[i].picture);
       furnitureTemplate.find('.Furniture-color').text(data[i].color);
       furnitureTemplate.find('.Furniture-price').text(data[i].price);
       furnitureTemplate.find('.Furniture-leng').text(data[i].leng);
       furnitureTemplate.find('.btn-adopt').attr('data-id', data[i].id);
 
       furnituresRow.append(furnitureTemplate.html());
     }
   });
 
   return await App.initWeb3();
 },
 
 initWeb3: async function() {
   if (window.ethereum) {
     App.web3Provider = window.ethereum;
     try {
       // Request account access
       await window.ethereum.enable();
     } catch (error) {
       // User denied account access...
       console.error("User denied account access")
     }
   }
   // Legacy dapp browsers...
   else if (window.web3) {
     App.web3Provider = window.web3.currentProvider;
   }
   // If no injected web3 instance is detected, fall back to Ganache
   else {
     App.web3Provider = new Web3.providers.HttpProvider('http://localhost:7545');
   }
   web3 = new Web3(App.web3Provider);
   return App.initContract();
 },
 
 initContract: function() {
 
   $.getJSON('Adoption.json', function(data) {
     // Get the necessary contract artifact file and instantiate it with @truffle/contract
     var AdoptionArtifact = data;
     App.contracts.Adoption = TruffleContract(AdoptionArtifact);
  
     // Set the provider for our contract
     App.contracts.Adoption.setProvider(App.web3Provider);
  
     // Use our contract to retrieve and mark the adopted furnitures
     return App.markAdopted();
   });
 
   return App.bindEvents();
 },
 
 bindEvents: function() {
   $(document).on('click', '.btn-adopt', App.handleAdopt);
 },
 
 markAdopted: function() {
   var adoptionInstance;
 
App.contracts.Adoption.deployed().then(function(instance) {
 adoptionInstance = instance;
 
 return adoptionInstance.getAdopters.call();
}).then(function(adopters) {
 for (i = 0; i < adopters.length; i++) {
   if (adopters[i] !== '0x0000000000000000000000000000000000000000') {
     $('.panel-furniture').eq(i).find('button').text('Success').attr('disabled', true);
   }
 }
}).catch(function(err) {
 console.log(err.message);
});
 },
 
 handleAdopt: function(event) {
   event.preventDefault();
 
   var furnitureId = parseInt($(event.target).data('id'));
 
   var adoptionInstance;
 
web3.eth.getAccounts(function(error, accounts) {
 if (error) {
   console.log(error);
 }
 
 var account = accounts[0];
 
 App.contracts.Adoption.deployed().then(function(instance) {
   adoptionInstance = instance;
 
   // Execute adopt as a transaction by sending account
   return adoptionInstance.adopt(furnitureId, {from: account});
 }).then(function(result) {
   return App.markAdopted();
 }).catch(function(err) {
   console.log(err.message);
 });
});
 }
 
};
 
$(function() {
 $(window).load(function() {
   App.init();
 });
});
```
## 5. ติดตั้ง MetaMask
- ติดตั้ง MetaMask ที่บราวเซอร์ Firefox
- เมื่อเริ่มใช้งาน MetaMask จะได้ดังรูป 

![H_Metamask](https://user-images.githubusercontent.com/77536689/104815634-5a408700-5848-11eb-8c3f-368d5576b672.jpg)

- คลิกที่ Get Started จะได้ผลลัพธ์ดังรูปด้านล่าง

![create_Metamask](https://user-images.githubusercontent.com/77536689/104815659-73e1ce80-5848-11eb-89cb-86946e412d59.jpg)

- คลิกที่ Import Wallet เพื่อเชื่อมต่อ MetaMask เข้ากับ Wallet ของ Ganache

![Detail_Metemask](https://user-images.githubusercontent.com/77536689/104815750-05e9d700-5849-11eb-9929-7dbbe6842eb2.jpg)

- ทำการก็อปปี้ Seed จาก Ganache นำมาวางลงในช่อง Wallet Seed ตั้งพาสเวิร์ด ติ๊กที่ I have read and agree to the Terms of Use แล้วคลิก Import

![custom_Metamaask](https://user-images.githubusercontent.com/77536689/104815704-aee40200-5848-11eb-823f-bde53e122bb7.jpg)

- ทำการย้ายจาก Ethereum Mainnet มาที่ Ganache โดยคลิกที่ Ethereum Mainnet แล้วเลือก Custom RPC

![custom_Metamask2](https://user-images.githubusercontent.com/77536689/104815709-bc998780-5848-11eb-9596-0cd16e89cd14.jpg)

- ป้อนข้อมูล Network Name (เป็นค่าใดๆ ก็ได้ ในรูปนี้ตั้งชื่อเป็น Ganache) ส่วน New RPC URL ต้องเป็น URL ของ Ganache ซึ่งในที่นี้คือ ```http://127.0.0.1:7545```

## 6. รันโปรแกรม 

รัน Backend โดยใช้คำสั่ง 

```
npm run dev
```

จากนั้นเปิด Firefox ที่ URL ดังนี้ ```http://localhost:3000```










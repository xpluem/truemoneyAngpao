# คู่มือการใช้งาน API : TrueMoney Angpao

API สำหรับการส่งและรับเงินผ่านลิงค์ซองของขวัญ TrueMoney โดยสามารถใช้งานได้ผ่าน HTTP Method `GET` โดยมีรายละเอียดดังนี้:

---

## **Endpoint**

**[GET]** `https://api.xpluem.com/:link/:phone`

### **พารามิเตอร์**

| พารามิเตอร์  | ประเภท    | คำอธิบาย                                               |
|--------------|-----------|--------------------------------------------------------|
| `link`       | `string`  | ลิงค์ซองของขวัญ (เฉพาะส่วนหลังเครื่องหมาย `?v=`)      |
| `phone`      | `string`  | เบอร์โทรศัพท์ของผู้รับเงิน (รูปแบบ 10 หลัก)            |

**ตัวอย่างลิงค์ซองของขวัญ** `https://gift.truemoney.com/campaign/?v=ลิงค์ซองของขวัญ`  

**ตัวอย่างการใช้งาน** `https://api.xpluem.com/ลิงค์ซองของขวัญ/เบอร์ผู้รับเงิน`

---

## **Response**

### **โครงสร้างการตอบกลับ**
```javascript
{
    "success": true,                                // สถานะ (true = สำเร็จ, false = ไม่สำเร็จ)
    "status": 200,                                  // HTTP Status Code
    "message": "รับเงินสำเร็จ",                        // ข้อความผลลัพธ์
    "data": {                                       // ข้อมูลเพิ่มเติม (ถ้าล้มเหลว, data จะเป็น null)
        "name": "นาย ทดสอบ ***",                    // ชื่อผู้ส่งเงิน (ซ่อนบางส่วน)
        "amount": "10.00"                           // จำนวนเงินที่ได้รับ
    }
}
```

---

### **ผลลัพธ์ที่เป็นไปได้**

| `success` | `status` | `message`                                     |
|-----------|----------|-----------------------------------------------|
| `true`    | `200`    | รับเงินสำเร็จ                                 |
| `false`   | `400`    | ลิงค์ซองของขวัญถูกใช้งานแล้ว                  |
| `false`   | `400`    | ลิงค์ซองของขวัญไม่ถูกต้อง                     |
| `false`   | `400`    | ไม่สามารถใช้อั่งเปาของตัวเองได้                |
| `false`   | `400`    | ลิงค์ซองของขวัญหมดอายุ                        |
| `false`   | `400`    | เบอร์รับเงินนี้ รับเงินไปแล้ว                  |
| `false`   | `400`    | เบอร์รับเงิน ไม่ถูกต้อง                        |
| `false`   | `400`    | กรุณาเลือกให้รับซองได้เพียวคนเดียว            |
| `false`   | `404`    | 404 Not Found                                  |
| `false`   | `405`    | 405 Method Not Allowed                         |
| `false`   | `500`    | เกิดข้อผิดพลาดเซิฟเวอร์                       |

---

## **ตัวอย่างการใช้งาน**

### **Request**
```
GET https://api.xpluem.com/abc1234567890/0801234567
```

### **Response (สำเร็จ)**
```json
{
    "success": true,
    "status": 200,
    "message": "รับเงินสำเร็จ",
    "data": {
        "name": "นาย ทดสอบ ***",
        "amount": "10.00"
    }
}
```

### **Response (ล้มเหลว)**
```json
{
    "success": false,
    "status": 400,
    "message": "ลิงค์ซองของขวัญหมดอายุ",
    "data": null
}
```

---

# CURL

```cmd
curl --location 'https://api.xpluem.com/ลิงค์ซองของขวัญ/เบอร์รับเงิน'
```
# PHP

```php
$link = 'ลิงค์ซองของขวัญ';
$phone = 'เบอร์ผู้รับเงิน';
$curl = curl_init();
curl_setopt_array($curl, array(
    CURLOPT_URL => 'https://api.xpluem.com/'.$link.'/'.$phone,
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'GET',
));
$response = curl_exec($curl);
curl_close($curl);
echo $response;
```

# NODEJS

```javascript
const axios = require('axios');

const link = 'ลิงค์ซองของขวัญ';
const phone = 'เบอร์ผู้รับเงิน';

const trueMoneyAngpao = async () => {
    try {
        const response = await axios.get(`https://api.xpluem.com/${link}/${phone}`);
        console.log(response.data);
    } catch (error) {
        console.error('Error:', error.response ? error.response.data : error.message);
    }
};

trueMoneyAngpao();
```

## **หมายเหตุ**

1. ควรตรวจสอบข้อมูล `link` และ `phone` ให้ถูกต้องก่อนส่งคำขอ
2. หากเกิดข้อผิดพลาด 500 ให้ลองทำคำขอใหม่ หรือแจ้งผู้พัฒนา API

---

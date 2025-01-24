# truemoneyAngpao

[GET] https://api.xpluem.com/:link/:phone

link = https://gift.truemoney.com/campaign/?v=ลิงค์ซองของขวัญ  <---- ลิงค์ซองของขวัญคือลิ้งหลัง ?v=

phone = เบอร์ผู้รับเงิน

# Response

| success     | status  | message              |
| -------- | ------- | ----------------------- |
| true      | 200   | รับเงินสำเร็จ   |
| false      | 400   | ลิงค์ซองของขวัญถูกใช้งานแล้ว   |
| false      | 400   | ลิงค์ซองของขวัญไม่ถูกต้อง   |
| false      | 400   | ไม่สามารถใช้อั่งเปาของตัวเองได้   |
| false      | 400   | ลิงค์ซองของขวัญหมดอายุ   |
| false      | 400   | เบอร์รับเงินนี้ รับเงินไปแล้ว   |
| false      | 400   | เบอร์รับเงิน ไม่ถูกต้อง   |
| false      | 400   | กรุณาเลือกให้รับซองได้เพียวคนเดียว   |
| false      | 404   | 404 Not Found'   |
| false      | 405   | 405 Method Not Allowed   |
| false      | 500   | เกิดข้อผิดพลาดเซิฟเวอร์   |

```json
{
    "success": true,                                // สถานะ (true = สำเร็จ, false = ไม่สำเร็จ)
    "status": 200,                                  // http status code
    "message": "รับเงินสำเร็จ",                        // ข้อความตอบกลับ 
    "data": {                                       //โชว์ Data ถ้าหาก status เป็น error Data จะเป็น Null
        "name": "นาย ทดสอบ ***",                    //ชื่อผู้เติม
        "amount": "10.00"                           //จำนวนที่ได้รับ
    }
}
```

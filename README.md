# ALGOR LEDGER

**small computer · real books**

ระบบบัญชี + สินค้าคงคลัง แบบ CLI / GUI สำหรับร้านค้าและบริษัทเล็ก  
Offline 100% · เข้ารหัส · ไม่พึ่ง cloud · ไฟล์ HTML เดียว

> UI สไตล์เทอร์มินัลยุค midrange / AS/400 — จอ **CRT amber phosphor**

[![License](https://img.shields.io/badge/license-use%20freely-8a5a12?style=flat-square)](#สิทธิ์การใช้งาน)
[![Offline](https://img.shields.io/badge/offline-100%25-ffb000?style=flat-square)](#)
[![UI](https://img.shields.io/badge/UI-CRT%20amber-ffb000?style=flat-square&labelColor=100a04)](#)

---

## เปิดใช้ทันที

| วิธี | รายละเอียด |
|------|------------|
| **GitHub Pages** | เปิดหน้าเว็บ → กด **Launch** |
| **ไฟล์เดียว** | ดาวน์โหลด `algor-ledger.html` → เปิดด้วย Chrome / Edge |
| **พกพา** | copy `algor-ledger.html` + ไฟล์ `.vault` ไปด้วยกัน |

ไม่ต้องติดตั้ง ไม่ต้องเซิร์ฟเวอร์ ไม่ต้องสมัครบัญชี

---

## คุณสมบัติ

- **สินค้าคงคลัง** — เพิ่ม / แก้ / ปรับสต็อก / แจ้งเตือนใกล้หมด
- **ขาย & ซื้อ** — บิล interactive หรือพิมพ์เร็ว `SALE A001 2`
- **ใบเสร็จ** — ชื่อร้าน · ที่อยู่ · โทร · เลขผู้เสียภาษี · ท้ายใบกำหนดเอง
- **พิมพ์** — รองรับกระดาษม้วน ~80mm, พิมพ์อัตโนมัติหลังขายได้
- **รายงาน** — รายวัน / เดือน / รายสินค้า / กำไรขั้นต้น
- **CLI + GUI** — เทอร์มินัลเต็มรูปแบบ หรือกด `F7` เข้าหน้าต่างกราฟิก
- **ความปลอดภัย** — AES-256-GCM + PBKDF2, ไฟล์ `.vault` เข้ารหัส
- **สองภาษา** — ไทย / English

---

## เริ่มต้นเร็ว

1. เปิด `algor-ledger.html`
2. เลือกภาษา `1` = ไทย
3. พิมพ์ตามลำดับ:

```text
MODE OWNER
SETPASS your-password
SETNAME ร้านของฉัน
SETADDR ที่อยู่ร้าน
SETPHONE 02-xxx-xxxx
SETTAXID 0xxxxxxxxxxxxx
ITEM ADD A001 น้ำดื่ม600ml ขวด 5 10 100
SALE
A001 2
END
cash
PRINT
SAVE
```

หรือกด **F7** เพื่อใช้โหมด GUI (ขาย / สินค้า / รายงาน / ระบบ)

---

## คำสั่งหลัก

### ระบบ
| คำสั่ง | ความหมาย |
|--------|----------|
| `MODE OWNER` / `MODE STAFF` | เจ้าของ / พนักงาน |
| `MODE GUI` / `F7` | หน้าต่างกราฟิก |
| `LOAD` / `SAVE` / `SAVERO` | โหลด / บันทึก / บันทึกแบบอ่านอย่างเดียว |
| `SETNAME` `SETADDR` `SETPHONE` `SETTAXID` | ข้อมูลร้านบนใบเสร็จ |
| `SETPRINT ON\|OFF` | พิมพ์ใบเสร็จอัตโนมัติหลังขาย |
| `SETFOOTER ...` | ข้อความท้ายใบเสร็จ |
| `LOCK` | ล็อกเซสชัน |

### สินค้า
```text
ITEM ADD <code> <name> <unit> <cost> <price> [qty]
ITEM LIST · ITEM VIEW · ITEM SEARCH · LOWSTOCK
STOCK IN|OUT|SET <code> <qty>
```

### ขาย / ใบเสร็จ
```text
SALE                  # interactive
SALE A001 2 B001 1    # ขายเร็ว
RECEIPT [ref|LAST]
RECEIPT LIST
PRINT [ref|LAST]
REPRINT
```

### รายงาน
```text
REPORT DAY
REPORT MONTH
REPORT ITEM <code>
TXN LIST
```

---

## โครงสร้างไฟล์ (สำหรับ GitHub Pages)

```text
.
├── index.html           ← หน้าแรก (landing CRT amber)
├── algor-ledger.html    ← ตัวระบบ (เปิดใช้จริง)
└── README.md            ← ไฟล์นี้
```

### เปิด GitHub Pages

1. สร้าง repo แล้วอัปโหลดไฟล์ด้านบน
2. **Settings → Pages → Deploy from branch → `main` / root**
3. รอสักครู่ แล้วเปิด `https://<user>.github.io/<repo>/`

---

## ความปลอดภัย

- รหัสผ่าน **ไม่ถูกเก็บ** ลงดิสก์ — ต้องใส่ทุกครั้งที่ `LOAD`
- เข้ารหัสด้วย Web Crypto API (AES-256-GCM, PBKDF2 120,000 rounds)
- ลืมรหัส = กู้ข้อมูลจาก `.vault` ไม่ได้
- `SAVERO` สร้างไฟล์ที่เปิดได้แค่โหมดดู

---

## แนวคิด

คอมพิวเตอร์เล็ก ๆ ที่ทำงานได้มากบนข้อมูลจำกัด —  
แบบเครื่องบัญชีและเทอร์มินัลยุค AS/400 ที่ร้านและบริษัทสมัยก่อนใช้  
เบา อยู่กับเครื่องคุณ และดีกว่าต้องพึ่ง cloud สำหรับร้านเล็ก

---

## สิทธิ์การใช้งาน

ใช้ได้อย่างอิสระสำหรับงานส่วนตัวและร้านเล็ก  
หากอ้างอิงแหล่งที่มาจะขอบคุณมาก แต่ไม่บังคับ

---

**ALGOR LEDGER** — *small computer · real books*

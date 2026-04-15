# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-SONCHEMJO999
**Name:** Son Chem Jo 999
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Agent tim dung san pham gia cao nhat trong nhom Electronics. Ket qua chinh xac, tra loi ro rang, co ban. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Agent bi Anh huong boi Duplicate ID (id=1 bi lap), Wrong data type (price = "ten dollars"), Extreme Outlier (999999), Null values (None). Ket qua sai nghiem trong. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent bi fail nghiem trong khi su dung garbage data vi cac ly do chinh sau day:

**Duplicate IDs (Ban ghi trung lap):** Trong garbage_data.csv, ban ghi co id=1 xuat hien 2 lan voi san pham "Laptop" va "Banana". Day la loi nhan dang duplicate identity, lam Agent khong biet nen tin ban ghi nao la chinh xac. Agent bi danh gia sai so luong san pham thuc te co trong he thong, dan den viec loc va tim kiem bi sai lech.

**Wrong Data Types (Kieu du lieu sai):** Ban ghi "Broken Chair" co price = "ten dollars" (string) thay vi so. Khi Agent doc du lieu va so sanh so sanh, no khong the ep kieu thanh cong vao so. Python se khong so sanh duoc string voi so, dan den loi hoac gia tri bi bo qua, lam mat chinh xac cua phep tinh.

**Extreme Outliers (Gia tri ngoai lai cuc doan):** Ban ghi "Nuclear Reactor" co gia 999999, muc gia nay vo cung lon so voi cac san pham binh thuong nhu Laptop (1200), Chair (45). Agent tim san pham co gia cao nhat, va no chon dung Nuclear Reactor vi so soanh logic idxmax() chon gia tri lon nhat. Day la loi khong loc outlier, lam ket qua bi sai hoan toan.

**Null Values (Gia tri rong):** Ban ghi "Ghost Item" co id = None, category = None, price = 0. Khi Agent doc vao DataFrame, gia tri None/0 se lam crash hoac tra ve gia tri NaN, gay ra loi runtime va Agent khong the tra loi dung.

### Tai sao Clean Data lai tot hon?

Clean data da duoc ETL pipeline xu ly, loai bo cac ban ghi loi (price <= 0, category rong), dam bao tat ca gia tri deu hop le. Agent khi do chi nhan dien 3 san pham Electronics: Laptop (1200), Monitor (300), va tu dong loc, tra ve Laptop voi gia 1200 la san pham gia cao nhat. Day la logic dung.

Ke luan, chat luong du lieu rat quan trong doi voi AI Agent. Neu dau vao rac, Agent se dua ra ket qua rac. Chi viec train model tot khong duoc, ma du lieu dau vao phai sach, chinh xac, nhat quan. Mot prompt hay khong the bu dc du lieu cham.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y, va rat dong y.

Mot prompt chat nhung du lieu dau vao cham se cho ket qua sai. Ngay ca khi prompt duoc viet rat chi tiet va ro rang, neu du lieu nguon (data source) chua duplicate, null, outlier, sai kieu du lieu, thi Agent chi nhan vao du lieu do va tra ve ket qua sai. Cu the trong thi nghiem nay, prompt cua Agent la "What is the best electronic product?" - prompt nay rat don gian va ro rang. Voi clean data, Agent tra loi dung. Voi garbage data, Agent tra loi sai hoan toan (Nuclear Reactor gia 999999). Dieu nay chung minh rang "Garbage in, Garbage out" - du lieu rac dau vao se cho ket qua rac dau ra, bat chap prompt nhu the nao. Vi vay, ETL pipeline va data observability rat quan trong de dam bao du lieu dau vao cho AI Agent luon chat luong cao.

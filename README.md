[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574319&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** email@example.com
**Name:** Son Chem Jo 999

---

## Mo ta

Day la bai lab xay dung mot Automated ETL Pipeline (Extract, Transform, Load) voi Data Observability. Chuong trinh doc du lieu tu file JSON (raw_data.json), kiem tra va loc bo du lieu khong hop le (price <= 0 hoac category rong), tinh gia giam 10%, chuan hoa category thanh Title Case, them timestamp xu ly, va luu ket qua ra file CSV (processed_data.csv).

Bai lab cung bao gom thi nghiem stress test voi AI Agent, so sanh ket qua khi Agent su dung clean data vs garbage data de minh hoa tam quan trong cua Data Quality doi voi AI.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Chay generate_garbage.py de tao garbage_data.csv
python generate_garbage.py

# Buoc 2: Chay agent_simulation.py de so sanh ket qua
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
├── agent_simulation.py      # AI Agent simulation
├── generate_garbage.py     # Tao garbage data
├── garbage_data.csv         # Poisoned data for testing
├── raw_data.json            # Raw input data
└── README.md                # File nay
```

---

## Ket qua

ETL Pipeline xu ly thanh cong 5 records tu raw_data.json:
- Loai bo 2 records khong hop le: id=3 (price=-10), id=4 (category rong)
- Con lai 3 records hop le: Laptop (Electronics), Chair (Furniture), Monitor (Electronics)
- Tinh discounted_price = price * 0.9
- Chuan hoa category thanh Title Case
- Them cot processed_at voi timestamp

Stress Test:
- Clean data: Agent tra loi chinh xac (Laptop at $1200)
- Garbage data: Agent tra loi sai nghiem trong (Nuclear Reactor at $999999)
- Ket luan: Quality Data > Quality Prompt

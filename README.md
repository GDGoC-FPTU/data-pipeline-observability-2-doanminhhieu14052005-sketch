[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112845&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** doanminhhieu14052005@gmail.com
**Name:** Đoàn Minh Hiếu
**Student ID:** 2A202600841

---

## Mô tả

Bài lab này xây dựng một ETL Pipeline tự động để xử lý dữ liệu từ file JSON sang CSV. Pipeline gồm 4 bước: Extract (đọc dữ liệu), Validate (loại bỏ dữ liệu không hợp lệ), Transform (chuẩn hóa và tính toán), và Load (lưu kết quả). Ngoài ra, bài lab cũng thực hiện thí nghiệm stress test để so sánh ảnh hưởng của dữ liệu sạch và dữ liệu rác lên một AI Agent đơn giản.

---

## Cách chạy (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chạy ETL Pipeline
```bash
python solution.py
```
Sau khi chạy, file `processed_data.csv` sẽ được tạo ra với dữ liệu đã được làm sạch và transform.

### Chạy Agent Simulation (Stress Test)
```bash
# Tạo dữ liệu rác
python generate_garbage.py

# Chạy agent với cả 2 bộ dữ liệu (clean và garbage)
python agent_simulation.py
```

---

## Cấu trúc thư mục

```
├── solution.py              # ETL Pipeline script chính
├── raw_data.json            # Dữ liệu đầu vào (5 records)
├── processed_data.csv       # Output của pipeline (3 records hợp lệ)
├── generate_garbage.py      # Script tạo dữ liệu rác
├── garbage_data.csv         # Dữ liệu rác cho stress test
├── agent_simulation.py      # Script mô phỏng AI Agent
├── experiment_report.md     # Báo cáo thí nghiệm stress test
├── tests/
│   └── test_autograder.py   # Autograding tests (DO NOT MODIFY)
└── README.md                # File này
```

---

## Kết quả

- **Tổng số records đầu vào:** 5 records từ `raw_data.json`
- **Records bị loại:** 2 records (Mystery Box có giá âm -10, Phone có category rỗng)
- **Records hợp lệ:** 3 records (Laptop, Chair, Monitor)
- **Các cột mới:** `discounted_price` (giá giảm 10%), `category` (Title Case), `processed_at` (timestamp)
- **Stress Test:** Agent trả lời chính xác với Clean Data (Laptop $1200), nhưng trả lời sai với Garbage Data (Nuclear Reactor $999999 - outlier)

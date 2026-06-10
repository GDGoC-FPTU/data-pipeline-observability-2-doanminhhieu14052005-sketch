# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600841
**Name:** Đoàn Minh Hiếu
**Date:** 2026-06-10

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Kết quả chính xác, Laptop là sản phẩm electronics có giá cao nhất |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Kết quả sai hoàn toàn, Agent bị ảnh hưởng bởi dữ liệu rác có outlier |

---

## 2. Phân tích & nhận xét (Phan tich & nhan xet)

### Tại sao Agent trả lời sai khi dùng Garbage Data? (Tai sao Agent tra loi sai)

Khi sử dụng dữ liệu rác (garbage_data.csv), Agent đã trả lời hoàn toàn sai vì nhiều lý do liên quan đến chất lượng dữ liệu. Thứ nhất, dữ liệu chứa Duplicate IDs - cả Laptop và Banana đều có id = 1, gây nhầm lẫn cho hệ thống khi truy vấn. Thứ hai, có wrong data types như giá của Broken Chair là "ten dollars" (kiểu string) thay vì số, khiến việc tính toán và so sánh giá bị lỗi. Thứ ba, dữ liệu chứa extreme outlier như Nuclear Reactor có giá 999999, đây là giá trị bất thường khiến Agent chọn sản phẩm này là "best choice" mặc dù nó không phải sản phẩm electronics thực tế. Thứ tư, dữ liệu có null values như Ghost Item có id là None, giá bằng 0 và category là None, đây là những bản ghi không hợp lệ hoàn toàn. Tất cả những vấn đề này cho thấy rằng nếu không có bước validation và data cleaning trước khi đưa dữ liệu vào Agent, kết quả trả về sẽ không đáng tin cậy và có thể dẫn đến những quyết định sai lầm nghiêm trọng.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** Đồng ý hoàn toàn. Dù cho prompt có tốt đến đâu, nếu dữ liệu đầu vào bị lỗi (duplicate, null, outlier, wrong type), Agent sẽ không thể trả lời chính xác. Data quality là nền tảng quan trọng nhất của bất kỳ hệ thống AI nào - "Garbage In, Garbage Out". Pipeline ETL với bước validation giúp đảm bảo chất lượng dữ liệu trước khi đưa vào mô hình AI.

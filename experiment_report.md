# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600678
**Name:** Nguyễn Đăng Dương
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. |10 | Sản phảm đúng giá trị ở các thuộc tính |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Sản phẩm có trong dataset nhưng chứa giá trị lỗi cần được loại bỏ|

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

<!-- (Viet nhan xet cua ban o day — it nhat 50 tu)

(Hay phan tich cac van de nhu Duplicate IDs, wrong data types, outliers, null values
va giai thich tai sao chung anh huong den ket qua cua Agent.) -->

Trong garbage.csv có các vấn đề như: Lặp ids (1,Laptop,1200,electronics và 1,Banana,2,fruit), thiếu ids và category (,Ghost Item,0,), và sai phạm vi giá trị của thuộc tính 'price' (3,Nuclear Reactor,999999,electronics). Vì thế, khi gọi agent_simulation.py với data_path là garbage_data.csv, logic trong file python đang lựa chọn sản phẩm theo giá trị price lớn nhất ('idxmax()'), chính vì vậy Nuclear Reactor,999999,electronics sẽ được chọn. Từ đó trả về trả lời sai.

## 3. Ket luan

**Quality Data > Quality Prompt?** 

Tôi đồng ý Quality data quan trọng hơn quality prompt vì Prompt có thể hướng dẫn mô hình cách sử dụng thông tin, nhưng Data quality quyết định mô hình có thông tin gì để sử dụng. Nếu thông tin sai mà prompt tốt thì mô hình chỉ đang thực hiện tốt trên data sai (đang làm đúng cái sai).

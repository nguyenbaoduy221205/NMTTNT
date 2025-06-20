# README

## Công nghệ sử dụng

| Thành phần | Mục đích |
|------------|---------|
| **Python 3.10+** | Ngôn ngữ lập trình chính cho toàn bộ thuật toán. |
| **Jupyter Notebook (IPYNB)** | Môi trường tương tác để chạy, hiển thị kết quả và trực quan hoá quá trình giải. |
| **NumPy** | Hỗ trợ thao tác mảng nhanh chóng và biểu diễn bàn cờ dưới dạng ma trận. |
| **random** (thư viện chuẩn) | Sinh số ngẫu nhiên (nếu muốn khởi tạo trạng thái thử nghiệm). |

## Cách hoạt động của code

1. **Khởi tạo**: Tập lệnh thiết lập các tham số chính (kích thước, số lần lặp, hạt giống ngẫu nhiên).  
2. **Xử lý dữ liệu**: Dữ liệu đầu vào được chuyển thành mảng NumPy để tăng tốc xử lý.  
3. **Thuật toán cốt lõi**: Hàm chính thực thi thuật toán tối ưu – vòng lặp qua N epoch, cập nhật trạng thái dựa trên hàm chi phí.  
4. **Trực quan hoá**: Sử dụng Jupyter để hiển thị biểu đồ quá trình hội tụ và kết quả cuối cùng.  
5. **Lưu & tải**: Kết quả được lưu về định dạng `.npy` hoặc `.csv`, sẵn sàng cho các bước hậu xử lý khác.

### Chạy thử nhanh

```bash
pip install -r requirements.txt
jupyter notebook TH_2.ipynb
```
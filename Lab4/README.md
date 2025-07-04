# Lab 3 – Thuật Toán Di Truyền (Genetic Algorithm)

[⬇️ Tải notebook **Lab3.ipynb**](sandbox:/mnt/data/lab3.ipynb)

## Công nghệ sử dụng
- Python 3.x
- Jupyter Notebook (.ipynb)
- Thư viện: **numpy**, **matplotlib** (kèm *mpl_toolkits*), *math*, *random*

## Cấu trúc chính notebook
1. **Giới thiệu & lý thuyết** về Thuật Toán Di Truyền  
2. **Ví dụ 1: Tối ưu hàm một biến**  
3. **Ví dụ 2: Tối ưu hàm hai biến**  
4. **Phân tích kết quả** (đồ thị hội tụ & thảo luận)  
5. **Bài tập 1–4** – yêu cầu sinh viên hoàn thiện GA cho từng đề bài  

## Cách hoạt động của code (phần bài tập)
Mỗi bài tập đều lặp qua 5 bước chính:
1. Định nghĩa **hàm mục tiêu** *(fitness function)*  
2. Khởi tạo **quần thể** ngẫu nhiên ban đầu  
3. Vòng lặp **GA**: *selection → crossover → mutation → evaluation*  
4. Cập nhật & lưu **best fitness** từng thế hệ  
5. Vẽ **đồ thị hội tụ** bằng `matplotlib`  

Toàn bộ hàm & biến được trình bày trong các ô code liên tiếp, có chú thích rõ ràng.

## Hướng dẫn chạy thử
```bash
# 1 – (Tuỳ chọn) tạo môi trường ảo
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# 2 – Cài đặt phụ thuộc
pip install numpy matplotlib

# 3 – Mở notebook
jupyter notebook lab3.ipynb
# Hoặc dùng VS Code / JupyterLab tuỳ ý

# 4 – Chạy toàn bộ
# Trong Jupyter: Run ▶ hoặc Run All
```
Sau khi chạy, đồ thị và kết quả sẽ hiển thị ngay dưới các ô code.

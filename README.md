# Algorithmic-trading-with-FPT-Stock

## 📌 Giới thiệu Dự án
Dự án này xây dựng một hệ thống Machine Learning ứng dụng trong giao dịch định lượng (Quantitative Trading) cho mã cổ phiếu FPT. Thay vì phân tích chuỗi thời gian cố định (Time-bar) thông thường, hệ thống sử dụng cách tiếp cận **Điều hướng theo sự kiện (Event-driven)** kết hợp Phân tích Cơ bản và Vi cấu trúc thị trường.

## 🧠 Kiến trúc Thuật toán Cốt lõi
Hệ thống được xây dựng dựa trên các triết lý học máy tài chính tiên tiến:
1. **Symmetric CUSUM Filter:** Lọc bỏ nhiễu thị trường, chỉ kích hoạt tín hiệu giao dịch khi Doanh thu thuần của FPT có sự thay đổi cấu trúc vượt ngưỡng 10%.
2. **Triple-Barrier Labeling:** Gắn nhãn phân lớp (Chốt lời `1`, Cắt lỗ `-1`, Hết hạn `0`) dựa trên biên độ biến động (Volatility) trượt, mô phỏng chính xác rủi ro của một vị thế giao dịch thực tế.
3. **Sample Uniqueness (Trung bình điều hòa):** Xử lý triệt để lỗi Overfitting do chồng lấn lệnh (Concurrency) thường gặp trong dữ liệu chuỗi thời gian tài chính.
4. **Multi-timeframe Features:** Xây dựng ma trận đặc trưng đo lường động lượng (Momentum) và biến động (Volatility) từ 7 ngày đến 360 ngày.

## 🚀 Hướng dẫn Cài đặt và Sử dụng

### 1. Yêu cầu hệ thống (Prerequisites)
Cài đặt các thư viện cần thiết:
`pip install pandas numpy scikit-learn vnstock`

### 2. Khởi chạy Pipeline
* Hệ thống sử dụng thư viện `vnstock` để cào dữ liệu EOD (Giá) và Báo cáo tài chính (Doanh thu) trực tiếp từ VCI.
* Chạy file chính để tải dữ liệu, dán nhãn, tính trọng số và huấn luyện mô hình:
`python main_fpt_model.py`

### 3. Kết quả Thực nghiệm (Giai đoạn 2007 - 2025)
* **Out-of-Sample (OOS) Accuracy:** Đạt **58.2%** (vượt trội so với Baseline 42.9%).
* **Feature Importances:** Mô hình phát hiện ra đà tăng trưởng giá 1 năm (`360_day_return`) và độ nén biến động ngắn hạn (`7_day_vol`) là 2 yếu tố quyết định cao nhất đến khả năng chạm rào chốt lời của FPT.

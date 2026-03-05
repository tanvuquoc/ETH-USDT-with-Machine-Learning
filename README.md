# Quantitative Trading Strategy: ETH/USDT with Machine Learning

## 📝 Giới thiệu Dự án
Dự án này tập trung nghiên cứu, thiết kế và kiểm định (backtest) một chiến lược giao dịch định lượng trên cặp tiền điện tử ETH/USDT. Thay vì giao dịch dựa trên cảm tính hoặc các chỉ báo kỹ thuật rule-based đơn lẻ, dự án ứng dụng Machine Learning (Logistic Regression & XGBoost) để dự báo xu hướng thị trường và tối ưu hóa quyết định đầu tư. 

Mục tiêu cốt lõi: Xây dựng một đường ống (pipeline) định lượng hoàn chỉnh từ khâu cào dữ liệu thô, tiền xử lý, trích xuất đặc trưng (Feature Engineering), huấn luyện mô hình, cho đến việc xây dựng hệ thống Backtest thủ công để đánh giá độ hiệu quả của chiến lược "Smart HODL" so với chiến lược "Buy & Hold" truyền thống.

## 🚀 Các Tính Năng Nổi Bật (Key Features)
- **Data Preprocessing & EDA:** Khám phá chuỗi thời gian tài chính, kiểm định phân phối chuẩn (Jarque-Bera Test) và biến đổi chuỗi lợi suất (Log-Returns).
- **Feature Engineering:** Trích xuất các đặc trưng định lượng từ dữ liệu nến (OHLCV) bao gồm Động lượng và Biến động: `RSI`, `PPO`, `Bollinger Bands (PctB)`, `ATR`, `Volume Ratio`.
- **Stationarity Testing:** Sử dụng kiểm định Augmented Dickey-Fuller (ADF) để đảm bảo tính dừng (Stationarity) của chuỗi dữ liệu đầu vào, tránh hiện tượng hồi quy giả mạo (Spurious Regression) trước khi đưa vào mô hình học máy.
- **Machine Learning Models:** Đánh giá và so sánh hiệu suất giữa mô hình học máy tuyến tính (Logistic Regression) và thuật toán Ensemble (XGBoost).
- **Custom Backtesting Engine:** Tự code hàm backtest thủ công thay vì phụ thuộc hoàn toàn vào các thư viện đóng gói sẵn (như `vectorbt`). Việc này giúp kiểm soát chặt chẽ logic giao dịch (mô phỏng "Smart HODL") và triệt tiêu hiện tượng rò rỉ dữ liệu (Data Leakage / Look-ahead bias).

## 🛠 Tech Stack
- **Ngôn ngữ lập trình:** Python
- **Xử lý & Thao tác dữ liệu:** `pandas`, `numpy`
- **Machine Learning:** `scikit-learn`, `xgboost`
- **Phân tích định lượng & Thống kê:** `statsmodels`, `scipy`
- **Trực quan hóa:** `matplotlib`, `seaborn`
- **Thử nghiệm Baseline:** `vectorbt`

## 📊 Kiến trúc Dự án (Project Pipeline)

1. **Khởi tạo & Tiền xử lý (Data Preparation):**
   - Chuyển đổi định dạng thời gian (`timestamp`), xử lý các quan sát có Volume bất thường để tránh lỗi chia cho 0.
   - Tính toán Log-Return để chuẩn hóa biên độ dữ liệu tài chính.
2. **Xây dựng Baseline (Rule-based Strategy):**
   - Chạy thử nghiệm chiến lược cơ sở dựa trên RSI bằng thư viện `vectorbt`. Đánh giá các hạn chế của logic giao dịch bằng luật (Rule-based).
3. **Feature Engineering & Lọc biến:**
   - Tạo tập hợp các chỉ báo kỹ thuật đại diện cho Market Microstructure (Động lượng, Biến động, Khối lượng).
   - Kiểm định tính dừng của các Features.
4. **Huấn luyện & Backtest Thủ công (Modeling & Custom Backtest):**
   - Phân chia tập Train/Test theo thứ tự thời gian (Time-Series Split).
   - Thiết lập chiến lược **Smart HODL**: Bot chỉ mở vị thế MUA (Hold) khi mô hình ML dự báo có xác suất tăng giá cao, và tiến hành cắt lệnh (đứng ngoài thị trường/chuyển sang USDT) khi phát hiện rủi ro giảm giá.
   - Huấn luyện và dự phóng với Logistic Regression và XGBoost.

## 📈 Kết quả (Results)
Kết quả kiểm định (Backtest) chứng minh mô hình **XGBoost kết hợp với chiến lược Smart HODL** mang lại hiệu suất vượt trội so với chiến lược Buy & Hold:
- **Đường cong vốn (Equity Curve):** Tài khoản của Bot tăng trưởng ổn định và có mức lợi nhuận tích lũy cao hơn đáng kể.
- **Quản trị Rủi ro:** Chiến lược ML giúp hạn chế được các đợt sụt giảm tài khoản nghiêm trọng (Drawdown) trong những chu kỳ thị trường đi xuống (Downtrend) nhờ khả năng nhận diện sớm rủi ro và đứng ngoài thị trường.


**💡 LƯU Ý QUAN TRỌNG:** Dự án này sử dụng nhiều thư viện chuyên biệt. Nếu quá trình chạy file `.ipynb` trên máy tính cá nhân (VS Code/Jupyter) gặp lỗi môi trường, khuyến nghị tải file lên **Google Colab** để thực thi mượt mà nhất.


# Banking Customer Analysis and Personalized Product Recommendation

## 1. Tổng quan dự án

Dự án này phân tích dữ liệu khách hàng ngân hàng nhằm hiểu rõ đặc điểm khách hàng, hành vi sử dụng sản phẩm tài chính và xây dựng hệ thống đề xuất sản phẩm cá nhân hóa.

Mục tiêu chính của dự án là dự đoán các sản phẩm ngân hàng mà khách hàng có khả năng mua thêm trong kỳ tiếp theo, từ đó hỗ trợ ngân hàng tối ưu chiến lược bán chéo, bán thêm và cải thiện trải nghiệm khách hàng.

Dự án kết hợp phân tích khám phá dữ liệu, tiền xử lý dữ liệu lớn, feature engineering và mô hình học máy XGBoost để tạo danh sách sản phẩm đề xuất phù hợp cho từng khách hàng.

## 2. Bối cảnh kinh doanh

Ngân hàng bán lẻ cung cấp nhiều sản phẩm tài chính như tài khoản thanh toán, tài khoản tiết kiệm, thẻ tín dụng, khoản vay, bảo hiểm, đầu tư và các sản phẩm tài chính cá nhân khác.

Tuy nhiên, nếu hệ thống đề xuất sản phẩm chưa tối ưu, ngân hàng có thể gặp các vấn đề như:

- Một số khách hàng nhận quá nhiều gợi ý không phù hợp.
- Một số khách hàng tiềm năng lại không nhận được đề xuất nào.
- Cơ hội bán chéo và bán thêm bị bỏ lỡ.
- Trải nghiệm khách hàng không đồng đều.
- Chi phí marketing bị lãng phí do nhắm sai nhóm khách hàng.

Vì vậy, việc xây dựng hệ thống đề xuất sản phẩm cá nhân hóa giúp ngân hàng hiểu rõ hơn nhu cầu của từng khách hàng, tăng tỷ lệ chuyển đổi và nâng cao lòng trung thành khách hàng.

## 3. Mục tiêu phân tích

Dự án tập trung trả lời các câu hỏi chính:

- Khách hàng của ngân hàng có đặc điểm nhân khẩu học như thế nào?
- Các nhóm khách hàng khác nhau đang sử dụng sản phẩm ngân hàng ra sao?
- Những yếu tố nào liên quan đến tổng số sản phẩm mà khách hàng sở hữu?
- Khách hàng có xu hướng mua thêm sản phẩm nào trong kỳ tiếp theo?
- Có thể xây dựng mô hình dự đoán sản phẩm phù hợp cho từng khách hàng không?
- Mô hình đề xuất có hoạt động hiệu quả trên nhóm khách hàng thực sự phát sinh giao dịch không?

## 4. Phương pháp thực hiện

Dự án sử dụng các phương pháp chính sau:

### 4.1. Exploratory Data Analysis

Phân tích khám phá dữ liệu được sử dụng để đánh giá đặc điểm khách hàng, phân phối độ tuổi, giới tính, thu nhập, thâm niên, quốc gia cư trú, kênh gia nhập và hành vi sử dụng sản phẩm ngân hàng.

### 4.2. Product Usage Analysis

Dự án phân tích mức độ sử dụng sản phẩm theo các nhóm khách hàng khác nhau như giới tính, trạng thái hoạt động, nhóm thu nhập, độ tuổi và thâm niên gắn bó với ngân hàng.

### 4.3. Correlation Analysis

Phân tích tương quan được sử dụng để xem xét mối quan hệ giữa các biến như tuổi, thu nhập, thâm niên, trạng thái hoạt động và tổng số sản phẩm khách hàng sở hữu.

### 4.4. Data Preprocessing

Dữ liệu được xử lý thông qua các bước:

- Loại bỏ các cột có tỷ lệ thiếu quá cao hoặc ít ý nghĩa phân tích.
- Xử lý missing values cho các biến như thu nhập, phân khúc, kênh gia nhập và giới tính.
- Mã hóa các biến phân loại thành dạng số.
- Chuẩn hóa các biến số như tuổi, thâm niên và thu nhập.
- Tạo biến sản phẩm sở hữu trong các tháng trước.
- Tạo nhãn dự đoán là sản phẩm mới mà khách hàng mua thêm.

### 4.5. Feature Engineering

Dự án tạo các nhóm đặc trưng chính:

- Đặc trưng khách hàng: tuổi, giới tính, quốc gia cư trú, phân khúc, trạng thái hoạt động.
- Đặc trưng tài chính: thu nhập hộ gia đình, thâm niên khách hàng.
- Đặc trưng hành vi: sản phẩm đã sở hữu trong các tháng trước.
- Đặc trưng sản phẩm mới: sản phẩm khách hàng mua thêm trong kỳ dự đoán.

### 4.6. Model Training

Mô hình XGBoost được sử dụng để dự đoán xác suất khách hàng mua từng sản phẩm ngân hàng. Mô hình được huấn luyện theo hướng multi-class classification với `objective = multi:softprob`, từ đó trả về xác suất cho từng sản phẩm.

### 4.7. Model Evaluation

Mô hình được đánh giá bằng các chỉ số:

- MAP
- MAP@5
- Precision@5
- Recall@5

Các chỉ số này phù hợp với bài toán recommendation vì không chỉ đánh giá sản phẩm dự đoán đúng hay sai mà còn xét đến thứ tự xếp hạng của sản phẩm được đề xuất.

## 5. Cấu trúc file dự án

```text
Banking-Product-Recommendation/
│
├── Notebook.ipynb
│   └── Notebook chính dùng để xử lý dữ liệu, phân tích khám phá dữ liệu, tiền xử lý, tạo đặc trưng, huấn luyện mô hình XGBoost và đánh giá hệ thống đề xuất sản phẩm.
│
└── Report.pdf
    └── Báo cáo tổng hợp kết quả phân tích, bao gồm bối cảnh kinh doanh, EDA, data preprocessing, model training, model evaluation, tối ưu code, kết luận và khuyến nghị.
```

## 6. Hướng dẫn đọc dự án

Dự án gồm các file chính sau:

- `Report.pdf`: Dùng để đọc nhanh toàn bộ logic dự án, bao gồm bối cảnh kinh doanh, phân tích khách hàng, phương pháp tiền xử lý, mô hình đề xuất sản phẩm và kết quả đánh giá.
- `Notebook.ipynb`: Dùng để xem chi tiết quá trình xử lý dữ liệu, phân tích EDA, tạo biến đầu vào, huấn luyện XGBoost và tạo danh sách sản phẩm đề xuất cho từng khách hàng.

## 7. Kết quả chính

Một số kết quả nổi bật của dự án:

- Bộ dữ liệu gồm 48 biến, bao gồm biến số, biến phân loại và biến nhị phân thể hiện thông tin khách hàng và sản phẩm ngân hàng.
- Khách hàng chủ yếu là người ngoài ngân hàng, không phải nhân viên nội bộ.
- Phần lớn khách hàng cư trú tại Tây Ban Nha, trong đó tập trung mạnh ở các thành phố lớn như Madrid, Barcelona và Valencia.
- Khách hàng tập trung chủ yếu trong độ tuổi lao động, đặc biệt ở nhóm trẻ từ khoảng 23–25 tuổi và nhóm 40–45 tuổi.
- Tỷ lệ khách hàng nam và nữ tương đối cân bằng, trong đó nữ nhỉnh hơn một chút.
- Khách hàng có thâm niên cao thường sở hữu nhiều sản phẩm ngân hàng hơn.
- Nhóm khách hàng thu nhập thấp chủ yếu sử dụng tài khoản hiện tại và ghi nợ tự động.
- Nhóm khách hàng thu nhập cao có xu hướng sử dụng nhiều sản phẩm tài chính phức tạp hơn như đầu tư, tín dụng, khoản vay và bảo hiểm.
- Chỉ số hoạt động của khách hàng có tương quan dương đáng kể với tổng số sản phẩm mà khách hàng sở hữu.
- Mô hình XGBoost được sử dụng để dự đoán xác suất khách hàng mua từng sản phẩm và xếp hạng top sản phẩm phù hợp.
- Trên toàn bộ tập kiểm tra, mô hình đạt MAP@5 = 0.0275, Precision@5 = 0.0077 và Recall@5 = 0.0302.
- Khi chỉ xét nhóm khách hàng thực sự mua thêm sản phẩm, mô hình đạt MAP@5 = 0.9010, Precision@5 = 0.2418 và Recall@5 = 0.9513.
- Kết quả cho thấy mô hình hoạt động tốt hơn rõ rệt trên nhóm khách hàng có nhu cầu thực sự, nhưng bài toán vẫn khó do dữ liệu mất cân bằng khi phần lớn khách hàng không mua thêm sản phẩm mới.

## 8. Công cụ sử dụng

Dự án sử dụng các công cụ và thư viện chính sau:

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- XGBoost
- GridSearchCV
- StratifiedKFold
- csv.DictReader
- Jupyter Notebook

## 9. Hạn chế của dự án

Dự án vẫn có một số hạn chế:

- Dữ liệu có kích thước lớn, gây áp lực về RAM và thời gian xử lý, đặc biệt khi chạy trên Google Colab.
- Dữ liệu mất cân bằng mạnh vì chỉ một tỷ lệ nhỏ khách hàng thực sự mua thêm sản phẩm mới.
- Một số cột có tỷ lệ thiếu cao hoặc ít ý nghĩa phân tích nên phải loại bỏ.
- Một số biến có outlier như tuổi và thu nhập hộ gia đình, cần xử lý cẩn thận để tránh ảnh hưởng đến mô hình.
- Mô hình dự đoán sản phẩm dựa trên hành vi lịch sử, chưa kết hợp thêm các yếu tố ngoài dữ liệu như chiến dịch marketing, ưu đãi cá nhân hóa hoặc hành vi tương tác trên ứng dụng.

## 10. Định hướng phát triển tiếp theo

Trong các phiên bản tiếp theo, dự án có thể được mở rộng theo các hướng:

- Xây dựng mô hình hai bước: dự đoán khách hàng có khả năng mua thêm sản phẩm trước, sau đó mới đề xuất sản phẩm cụ thể.
- Thử nghiệm thêm các mô hình recommendation như collaborative filtering, matrix factorization hoặc learning-to-rank.
- Kết hợp thêm dữ liệu chiến dịch marketing, hành vi giao dịch và lịch sử tương tác để cải thiện độ chính xác.
- Xây dựng dashboard theo dõi tỷ lệ chuyển đổi của từng sản phẩm và từng nhóm khách hàng.
- Cá nhân hóa số lượng sản phẩm đề xuất thay vì cố định top-5 cho mọi khách hàng.
- Tối ưu pipeline xử lý dữ liệu lớn để giảm thời gian chạy và tiết kiệm bộ nhớ.

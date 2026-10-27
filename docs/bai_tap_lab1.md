# TỔNG HỢP CÁC BÀI TẬP LAB 1 - KHAI PHÁ DỮ LIỆU
*(Trích xuất từ tài liệu `docs/lab1.pdf`)*

---

## MỤC LỤC
1. [Bảng ánh xạ bài tập & Tập dữ liệu (Datasets)](#-bảng-ánh-xạ-bài-tập--tập-dữ-liệu-datasets)
2. [Phần 1 - Bài 2 (Trang 15-17): Lập trình tiền xử lý dữ liệu Titanic](#1-phần-1---bài-2-trang-15-17)
3. [Phần 1 - Bài 2 (Trang 28-29): Tiền xử lý dữ liệu Bank Marketing](#2-phần-1---bài-2-trang-28-29)
4. [Phần 1 - Trang 30 (Bài tập thêm - Bài 2): Tiền xử lý dữ liệu cảm biến môi trường tb_tracking](#3-phần-1---trang-30-bài-2)
5. [Phần 2 - Bài 2 (Trang 37-38): Khai phá tập phổ biến & luật kết hợp dữ liệu Online Retail](#4-phần-2---bài-2-trang-37-38)
6. [Phần 2 - Bài 5a (Trang 45): Phân tích luật kết hợp cho thị trường Đức (Germany)](#5-phần-2---bài-5a-trang-45)
7. [Phần 2 - Bài 6 (Trang 45): So sánh hiệu năng Apriori và FP-Growth trên Groceries Dataset](#6-phần-2---bài-6-trang-45)

---

## 📁 BẢNG ÁNH XẠ BÀI TẬP & TẬP DỮ LIỆU (DATASETS)

| STT | Bài tập | Tập dữ liệu yêu cầu | Đường dẫn file trong thư mục `datasets/` | Ghi chú |
| :---: | :--- | :--- | :--- | :--- |
| **1** | Phần 1 - Bài 2 (Tr. 15-17) | Titanic Dataset | [../datasets/titanic.csv](../datasets/titanic.csv) | Đã có sẵn trong `datasets/` |
| **2** | Phần 1 - Bài 2 (Tr. 28-29) | Bank Marketing Dataset | [../datasets/Bank/](../datasets/Bank/)<br>• [../datasets/Bank/bank.csv](../datasets/Bank/bank.csv)<br>• [../datasets/Bank/bank-full.csv](../datasets/Bank/bank-full.csv) | Đã có sẵn trong `datasets/Bank/` |
| **3** | Phần 1 - Trang 30 (Bài 2) | Dữ liệu môi trường nhà xưởng | [../datasets/tb_tracking.xlsx](../datasets/tb_tracking.xlsx) | Đã có sẵn trong `datasets/` |
| **4** | Phần 2 - Bài 2 (Tr. 37-38) | Online Retail Dataset | [../datasets/Online Retail.xlsx](../datasets/Online%20Retail.xlsx) | Đã có sẵn trong `datasets/` |
| **5** | Phần 2 - Bài 5a (Tr. 45) | Online Retail (Thị trường Đức) | [../datasets/Online Retail.xlsx](../datasets/Online%20Retail.xlsx) | Dùng chung tập Online Retail |
| **6** | Phần 2 - Bài 6 (Tr. 45) | Groceries Dataset | [../datasets/groceries.csv](../datasets/groceries.csv) | Đã có sẵn trong `datasets/` (9835 giao dịch) |

---

## 1. PHẦN 1 - BÀI 2 (TRANG 15-17)
- **Tập dữ liệu sử dụng**: `titanic.csv`
- **Liên kết dataset**: [../datasets/titanic.csv](../datasets/titanic.csv) (hoặc `datasets/titanic.csv` từ thư mục gốc)
- **Công cụ**: Python, Jupyter Notebook (thư viện: `numpy`, `pandas`, `seaborn`, `matplotlib`)
- **Vị trí tài liệu**: Phần 1 - Mục III. Hướng dẫn chung -> Mục 2: Yêu cầu lập trình (Trang 15–17)

### Đề bài & Các yêu cầu:
Sinh viên tải về dữ liệu Titanic đầy đủ ở phần Tài liệu tham khảo và thực hiện các yêu cầu về lập trình trên ngôn ngữ Python, sử dụng công cụ Jupyter Notebook:

1. **Câu 1**: Nhập dữ liệu và thống kê những thông tin cơ bản của các thuộc tính:
   - Đọc dữ liệu từ file `titanic.csv`.
   - Xem một số dòng đầu tiên (`head()`), cấu trúc và kiểu dữ liệu (`info()`).
   - Thống kê chỉ số của các thuộc tính định lượng: số lượng giá trị, giá trị lớn nhất, nhỏ nhất, trung bình, độ lệch chuẩn, tứ phân vị... (`describe()`).
2. **Câu 2**: Liệt kê danh sách 5 thuộc tính có số lượng giá trị rỗng nhiều nhất.
3. **Câu 3**: Vẽ biểu đồ khảo sát sự liên quan giữa thuộc tính Độ tuổi (`age`), Giới tính (`sex`) và thuộc tính quyết định – khả năng sống sót (`survived`) và đưa ra nhận xét.
4. **Câu 4**: Vẽ biểu đồ khảo sát sự liên quan giữa thuộc tính Cổng lên tàu (`embarked`) và loại vé (`pclass`) với khả năng sống sót (`survived`), phân biệt theo Giới tính (`sex`) và đưa ra nhận xét.
5. **Câu 5**: Thống kê số người đi cùng (anh chị em/vợ chồng hoặc cha mẹ/con cái) và khảo sát sự liên quan với thuộc tính quyết định và đưa ra nhận xét.
6. **Câu 6**: Tiền xử lý các thuộc tính thiếu dữ liệu và xóa bỏ các thuộc tính không cần thiết.
7. **Câu 7**: Biến đổi các thuộc tính sau:
   - Chuyển đổi thuộc tính giá vé (`fare`) về kiểu nguyên.
   - Trích xuất thuộc tính danh hiệu (`title`) từ cột tên (`name`).
   - Chuyển đổi thuộc tính giới tính (`sex`) và cổng lên tàu (`embarked`) thành dạng số.
   - Chia giá trị thuộc tính tuổi (`age`) thành 8 nhóm cân bằng số phần tử, gợi ý:
     + Nhóm 1: dưới 11 tuổi
     + Nhóm 2: trên 11 tuổi đến 18 tuổi
     + Nhóm 3: trên 18 tuổi đến 22 tuổi
     + Nhóm 4: trên 22 tuổi đến 27 tuổi
     + Nhóm 5: trên 27 tuổi đến 33 tuổi
     + Nhóm 6: trên 33 tuổi đến 40 tuổi
     + Nhóm 7: trên 40 tuổi đến 66 tuổi
     + Nhóm 8: trên 66 tuổi
   - Chia giá trị thuộc tính giá vé (`fare`) thành 6 nhóm, gợi ý:
     + Nhóm 1: nhỏ hơn hoặc bằng 7.91
     + Nhóm 2: lớn hơn 7.91 đến 14.454
     + Nhóm 3: lớn hơn 14.454 đến 31
     + Nhóm 4: lớn hơn 31 đến 99
     + Nhóm 5: lớn hơn 99 đến 250
     + Nhóm 6: lớn hơn 250
8. **Câu 8**: Tạo ra các thuộc tính mới:
   - Thuộc tính tuổi * loại vé (`age_class`): tích của tuổi và loại vé (`age * pclass`).
   - Thuộc tính giá vé trên mỗi người (`fare_per_person`): giá vé chia cho số người đi cùng người đó (có làm trơn + 1): `fare / (relatives + 1)`.

---

## 2. PHẦN 1 - BÀI 2 (TRANG 28-29)
- **Tập dữ liệu sử dụng**: `bank marketing` (mẫu bảng dữ liệu trang 28-29 hoặc tập dữ liệu `bank-additional-full.csv`)
- **Liên kết dataset**: Thư mục [../datasets/Bank/](../datasets/Bank/) (gồm file nhỏ [bank.csv](../datasets/Bank/bank.csv) và file đầy đủ [bank-full.csv](../datasets/Bank/bank-full.csv))
- **Vị trí tài liệu**: Phần 1 - Mục V. Thực hành -> Bài 2 (Trang 28–29)

### Đề bài:
Để thực hiện chiến dịch marketing cho chương trình gửi tiền có kì hạn, một ngân hàng dựa trên bộ dữ liệu người dùng được cho trong mẫu sau để tìm hiểu khả năng người dùng sẽ đăng kí chương trình gửi tiền có kì hạn ở ngân hàng hay không (mẫu được trích từ tập dữ liệu bank marketing):

| Job | Marial | Education | Default | Loan | Duration | Cons.price.idx | Subscribe |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| housemaid | Married | basic.4y | no | no | 261 | 93.994 | no |
| services | Married | high.school | unknown | no | 149 | 93.994 | no |
| blue-collar | Divorced | basic.4y | unknown | no | 1575 | 93.994 | yes |
| admin. | Single | high.school | no | no | 338 | 93.994 | no |
| blue-collar | Single | basic.9y | no | no | 179 | 93.994 | no |
| services | Married | high.school | no | no | 1030 | 93.994 | yes |
| management | Married | high.school | unknown | no | 149 | 93.994 | no |
| unemployed | | university.degree | unknown | no | 424 | 93.994 | no |
| technician | Married | professional.course | no | no | 1623 | 93.994 | yes |
| services | Divorced | high.school | unknown | no | 568 | 93.994 | no |
| blue-collar | Married | high.school | no | no | 1297 | 93.994 | yes |
| self-employed | Married | basic.9y | no | no | 376 | 93.918 | no |
| entrepreneur | Married | professional.course | no | yes | 576 | 93.994 | no |
| services | Single | high.school | no | no | 1059 | 93.2 | yes |
| technician | Married | basic.9y | no | no | 705 | 93.2 | yes |
| retired | Married | high.school | no | no | 532 | 93.2 | no |

### Mô tả thuộc tính:
- `Job`: Nghề nghiệp.
- `Marial`: Tình trạng hôn nhân.
- `Education`: Trình độ học vấn.
- `Default`: Đã có tín dụng mặc định hay chưa.
- `Loan`: Đã có khoản vay nào chưa.
- `Duration`: Thời lượng lần contact cuối cùng, tính trên đơn vị giây.
- `Cons.price.idx`: Chỉ số giá tiêu dùng.
- `Subscribe`: Khách hàng có đồng ý đăng ký gửi tiền có kỳ hạn hay không (thuộc tính quyết định).

### Yêu cầu:
Sinh viên thực hiện khảo sát và tiền xử lý dữ liệu cho dữ liệu Bank marketing giống như phần hướng dẫn (thống kê thuộc tính, kiểm tra giá trị thiếu/unknown, tiền xử lý, biến đổi/mã hóa đặc trưng, phân tích tương quan với thuộc tính quyết định).

---

## 3. PHẦN 1 - TRANG 30 (BÀI 2)
- **Tập dữ liệu sử dụng**: `tb_tracking.xlsx`
- **Liên kết dataset**: [../datasets/tb_tracking.xlsx](../datasets/tb_tracking.xlsx)
- **Vị trí tài liệu**: Phần 1 - Mục VI. Bài tập thêm -> Bài 2 (Trang 30)

### Đề bài:
Dữ liệu môi trường của một nhà xưởng sản xuất được đo và trình bày trong tập tin đính kèm `tb_tracking.xlsx`. Thực hiện các thao tác tiền xử lý sau:

### Các yêu cầu cụ thể:
- **a)** Thêm vào tiêu đề các cột theo thứ tự:
  + `id`: định danh của dòng dữ liệu
  + `device_id`: định danh của thiết bị đo
  + `co_level`: nồng độ khí CO
  + `humidity`: độ ẩm
  + `temperature`: nhiệt độ
  + `time`: thời điểm đo đạc
- **b)** Do điều chỉnh cảm biến nên dữ liệu đo được bắt đầu từ ngày `03/01/2018` mới chính xác. Những dữ liệu còn lại không có giá trị, yêu cầu sinh viên loại bỏ.
- **c)** Từ cột `time`, sinh viên bóc tách dữ liệu thành thời điểm đo đạc trong ngày tính theo phút, đặt tên cột mới là `minutes`.
- **d)** Vẽ đồ thị phân tán (scatter-plots) lần lượt biểu diễn dữ liệu nồng độ khí CO, độ ẩm và nhiệt độ theo cột `minutes` vừa tạo ở yêu cầu trên.

---

## 4. PHẦN 2 - BÀI 2 (TRANG 37-38)
- **Tập dữ liệu sử dụng**: `Online Retail.xlsx`
- **Liên kết dataset**: [../datasets/Online Retail.xlsx](../datasets/Online%20Retail.xlsx)
- **Công cụ & Thư viện**: Python, Jupyter Notebook, `mlxtend`, `xlrd`, `pandas`, `seaborn`, `matplotlib`
- **Vị trí tài liệu**: Phần 2 - Mục III. Hướng dẫn chung -> Mục 2: Yêu cầu lập trình (Trang 37–38)

### Đề bài:
Cho dữ liệu Online Retail là lịch sử bán hàng của một cửa hàng bán lẻ trực tuyến tại Châu Âu. Cửa hàng này chuyên bán quà tặng độc đáo vào nhiều dịp lễ trong năm và cũng có nhiều khách hàng mua sỉ. Hãy thực hiện những yêu cầu sau:

### Các yêu cầu cụ thể:
1. Đọc dữ liệu vào chương trình.
2. Tiền xử lý dữ liệu: cắt bỏ các ký tự thừa ở tên mặt hàng mua (cột `Description`), xóa các dòng dữ liệu không có số hóa đơn (cột `InvoiceNo`) và chuyển nó về kiểu dữ liệu chuỗi.
3. Trong dữ liệu đã cho, có một số hóa đơn là hóa đơn tín dụng thay vì là hóa đơn ghi nợ vì vậy hãy xóa những hóa đơn đó. Chúng được xác định với ký tự `'C'` chứa trong số hóa đơn `InvoiceNo`.
4. Thống kê số dòng dữ liệu theo từng quốc gia.
5. Lấy ra dữ liệu hóa đơn từ nước Anh (`'United Kingdom'`) và gom nhóm cột Số lượng mua (`Quantity`) theo Số hóa đơn (`InvoiceNo`) và Tên mặt hàng (`Description`).
6. Chuyển đổi dữ liệu về dạng hot encoding, với mỗi dòng dữ liệu là một hóa đơn.
7. Chuyển đổi dữ liệu từ dạng hot encoding thành one-hot encoding (giá trị $\le 0$ thành $0$, $\ge 1$ thành $1$).
8. Do cột `'POSTAGE'` là tiền cước phí trên mỗi hóa đơn nên cần xóa nó đi.
9. Tìm tập phổ biến bằng thuật toán Apriori với `min_sup = 3%` (`min_support = 0.03`).
10. Tạo luật kết hợp với `min_conf = 50%` (`min_threshold = 0.5`) và in ra các luật này.
11. Biểu diễn độ tin cậy (`confidence`), độ hỗ trợ (`support`) của tập luật lên đồ thị phân tán (scatter plot).
12. Tìm tập phổ biến và luật kết hợp bằng thuật toán FP-Growth với `min_sup = 3%`, `min_conf = 50%`. So sánh kết quả với thuật toán Apriori ở trên.

---

## 5. PHẦN 2 - BÀI 5a (TRANG 45)
- **Tập dữ liệu sử dụng**: `Online Retail.xlsx`
- **Liên kết dataset**: [../datasets/Online Retail.xlsx](../datasets/Online%20Retail.xlsx)
- **Vị trí tài liệu**: Phần 2 - Mục IV. Thực hành -> Bài 5a (Trang 45)

### Đề bài & Yêu cầu:
(Lập trình) Hãy thực hiện lại bài tập lập trình ở phần hướng dẫn chung nhưng thay đổi các yêu cầu thành:
- **a) Nước Đức (‘Germany’), `min_sup = 5%` và `min_conf = 50%`.**
*(Ghi chú: Câu 5b là Nước Pháp ‘France’, `min_sup = 7%` và `min_conf = 70%`).*

### Các bước thực hiện chi tiết cho câu 5a:
1. Lọc các hóa đơn thuộc quốc gia Đức (`Country == 'Germany'`).
2. Gom nhóm theo `InvoiceNo` và `Description` với tổng số lượng mua `Quantity`.
3. Chuyển đổi ma trận giỏ hàng sang dạng one-hot encoding và loại bỏ cột `'POSTAGE'` nếu có.
4. Áp dụng thuật toán Apriori với `min_sup = 0.05` (5%) để tìm các tập mục phổ biến.
5. Sinh các luật kết hợp từ tập phổ biến với ngưỡng độ tin cậy `min_conf = 0.5` (50%).
6. Áp dụng thuật toán FP-Growth với cùng ngưỡng để so sánh.
7. Xuất và nhận xét các luật kết hợp tìm được (support, confidence, lift).

---

## 6. PHẦN 2 - BÀI 6 (TRANG 45)
- **Tập dữ liệu sử dụng**: `Groceries Dataset` (`groceries.csv` gồm 9835 giao dịch và 169 items)
- **Liên kết dataset**: [../datasets/groceries.csv](../datasets/groceries.csv)
- **Vị trí tài liệu**: Phần 2 - Mục IV. Thực hành -> Bài 6 (Trang 45)

### Đề bài:
(Lập trình) Cho mẫu dữ liệu Groceries Dataset về các giao dịch trong một tháng của một cửa hàng outlet, gồm 9835 giao dịch và 169 items.
Với `min_sup` từ `0.01%` đến `0.1%`, hãy:

### Các yêu cầu cụ thể:
- **a)** Tìm tất cả các tập phổ biến trong từng trường hợp bằng giải thuật Apriori và ghi nhận thời gian xử lý của thuật toán.
  *Gợi ý*: Sinh viên có thể sử dụng module `OneHotTransactions` hoặc `TransactionEncoder` của thư viện `mlxtend` để chuyển dữ liệu về dạng one-hot encoding trước khi đưa vào thuật toán.
- **b)** Tìm tất cả các tập phổ biến trong từng trường hợp bằng giải thuật FP-Growth và ghi nhận thời gian xử lý của thuật toán.
- **c)** Vẽ biểu đồ so sánh thời gian xử lý của hai thuật toán trên với nhau theo các mức `min_sup`. Sinh viên đưa ra nhận xét và giải thích vì sao có sự chênh lệch thời gian giữa hai giải thuật.

---
*(Tài liệu được trích xuất tự động và chuẩn hóa phục vụ làm bài tập thực hành môn Khai phá dữ liệu - IT1.231.3)*

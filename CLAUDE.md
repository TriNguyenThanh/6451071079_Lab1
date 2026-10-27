# HƯỚNG DẪN & QUY TẮC DỰ ÁN LAB 1 - KHAI PHÁ DỮ LIỆU (DATA MINING)
> Bản đặc tả quy chuẩn chung cho tất cả các AI Agent (Cursor, Windsurf, Copilot, Roo, Aider...): xem [AGENTS.md](AGENTS.md).

## 1. THÔNG TIN CHUNG

- **Môn học**: Khai phá dữ liệu (Data Mining - IT1.231.3) - Lab 1
- **Sinh viên**: Nguyễn Thành Trí
- **Mã số sinh viên (MSSV)**: `6451071079`
- **Tài liệu tham chiếu**: [docs/lab1.pdf](docs/lab1.pdf), [docs/bai_tap_lab1.md](docs/bai_tap_lab1.md), [docs/Template nộp bài LAB1.docx](docs/Template nộp bài LAB1.docx)

---

## 2. QUY TẮC MÔI TRƯỜNG & PYTHON (ENVIRONMENT & DEPENDENCIES)

1. **Bắt buộc dùng môi trường ảo `.venv`**:
   - Mọi lệnh Python hoặc Jupyter phải thực thi thông qua `.venv/bin/python`, `.venv/bin/pip`, hoặc kích hoạt `source .venv/bin/activate`.
   - **Tuyệt đối không** sử dụng Python hệ thống (`/usr/bin/python3`) vì thiếu các thư viện chuyên môn.
2. **Quản lý thư viện (`requirements.txt`)**:
   - File [requirements.txt](requirements.txt) quản lý danh mục thư viện tối thiểu:
     ```
     numpy
     pandas
     seaborn
     matplotlib
     ipykernel
     openpyxl
     mlxtend
     ```
   - Khi cần cài thêm thư viện: dùng `.venv/bin/pip install -r requirements.txt`.
3. **Cấu hình Jupyter Kernel**:
   - Sử dụng kernel gắn liền với `.venv`: `Python 3 (.venv)`.

---

## 3. QUY TẮC TRUY CẬP VÀ ĐỌC DỮ LIỆU (DATASETS)

1. **Vị trí tập dữ liệu**:
   - Tất cả dữ liệu nguồn được lưu tại thư mục [datasets/](datasets/):
     - `titanic.csv`: Tiền xử lý dữ liệu Titanic (Phần 1 - Bài 1).
     - `Bank/bank.csv`, `Bank/bank-full.csv`: Dữ liệu Bank Marketing (Phần 1 - Bài 2).
     - `tb_tracking.xlsx`: Dữ liệu cảm biến môi trường xưởng (Phần 1 - Bài 3).
     - `Online Retail.xlsx`: Khai phá tập phổ biến & luật kết hợp (Phần 2 - Bài 2, Bài 5a).
     - `groceries.csv`: So sánh hiệu năng Apriori và FP-Growth (Phần 2 - Bài 6).
2. **Đường dẫn tương đối an toàn trong code**:
   - Code có thể chạy từ thư mục gốc hoặc từ các thư mục con (`Phan1/Bai1`, `Phan2/Bai2`, v.v.). Do đó, luôn dùng hàm kiểm tra đường dẫn linh hoạt:

     ```python
     import os

     def get_data_path(rel_path):
         candidates = [
             rel_path,
             os.path.join("..", rel_path),
             os.path.join("..", "..", rel_path),
             os.path.join("datasets", os.path.basename(rel_path))
         ]
         for p in candidates:
             if os.path.exists(p):
                 return p
         raise FileNotFoundError(f"Không tìm thấy file dữ liệu: {rel_path}")

     def get_img_dir(subpath=""):
         for base in [".", "..", "../.."]:
             img_root = os.path.join(base, "images")
             if os.path.exists(img_root) and (os.path.exists(os.path.join(base, "datasets")) or os.path.exists(os.path.join(base, "CLAUDE.md"))):
                 target = os.path.join(img_root, subpath) if subpath else img_root
                 os.makedirs(target, exist_ok=True)
                 return target
         target = os.path.join("images", subpath) if subpath else "images"
         os.makedirs(target, exist_ok=True)
         return target
     ```

---

## 4. QUY CHUẨN TRÌNH BÀY CODE VÀ NOTEBOOK

1. **Quy tắc đặt tên file notebook**:
   - Mỗi bài tập là **MỘT notebook duy nhất**, gộp toàn bộ các câu hỏi của bài đó.
   - **Tuyệt đối không** tách từng câu hỏi ra thành file riêng (không tạo `Bai1_cau1.ipynb`, `Bai1_cau2.ipynb`, v.v.).
   - Tên file theo quy ước: `<MSSV>_LAB1_Bai<X>.ipynb`
     - `Phan1/Bai1/6451071079_LAB1_Bai1.ipynb` — Titanic
     - `Phan1/Bai2/6451071079_LAB1_Bai2.ipynb` — Bank Marketing
     - `Phan1/Bai3/6451071079_LAB1_Bai3.ipynb` — tb_tracking
     - `Phan2/Bai2/6451071079_LAB1_Bai2.ipynb` — Online Retail UK
     - `Phan2/Bai5a/6451071079_LAB1_Bai5a.ipynb` — Online Retail Germany
     - `Phan2/Bai6/6451071079_LAB1_Bai6.ipynb` — Groceries

2. **Cấu trúc bên trong notebook**:
   - **Cell Markdown đầu tiên**: Tiêu đề + định danh sinh viên:
     ```markdown
     # Nguyễn Thành Trí - MSSV: 6451071079
     ## [Tên phần / bài tập cụ thể]
     ```
   - **Cell Code đầu tiên**: Import thư viện, hàm tiện ích, in định danh:
     ```python
     # Nguyễn Thành Trí - 6451071079
     print("Họ tên: Nguyễn Thành Trí - MSSV: 6451071079")
     ```
   - **Các câu hỏi tiếp theo**: Lặp lại cặp `Markdown (câu hỏi) → Code (giải)`:
     - **Cell Markdown**: Ghi lại nội dung câu hỏi/yêu cầu đề bài (ví dụ: "**Câu 3**: Vẽ biểu đồ khảo sát...").
     - **Cell Code**: Code giải bài, có chú thích ngắn gọn, hiển thị kết quả (`display()`, `head()`, biểu đồ).
   - **KHÔNG tạo cell Markdown nhận xét** sau mỗi câu code. Nếu cần nhận xét ngắn, viết bằng `print()` trực tiếp trong cell code.

3. **Trực quan hóa dữ liệu (Visualization)**:
   - Sử dụng `matplotlib` và `seaborn`.
   - Luôn thiết lập tiêu đề (`plt.title`), nhãn trục (`plt.xlabel`, `plt.ylabel`), chú thích (`plt.legend`) và lưới (`plt.grid(True, alpha=0.3)`).
   - Lưu ảnh minh họa cho báo cáo Word: lưu vào `images/<PhanX>/<BaiY>/` bằng hàm `get_img_dir("PhanX/BaiY")` với `plt.savefig(os.path.join(img_dir, 'tên_anh.png'), bbox_inches='tight', dpi=300)`. Tuyệt đối không tạo thư mục `images` lồng trong thư mục con bài làm.

4. **Quy tắc quản lý file & Giữ sạch thư mục gốc (Root Hygiene)**:
   - **Tuyệt đối không** tạo các file script tạm, file nháp hoặc file vá lỗi (như `fix_*.py`, `test_*.py`, `temp_*.py`, `generate_*.py`) tại thư mục gốc.
   - Khi chỉnh sửa file hoặc notebook, luôn thao tác trực tiếp (in-place) qua công cụ `Edit`/`Write` hoặc lệnh Python một dòng (`python -c "..."`), không viết script trung gian ra đĩa.
   - Nếu cần viết script tự động hóa để sinh notebook hàng loạt, script đó **bắt buộc phải đặt trong thư mục `scripts/`** (ví dụ: `scripts/make_phan2_bai5a.py`), không bao giờ để ở thư mục gốc. Sau khi hoàn thành phải dọn sạch các file nháp không cần thiết.

---

## 5. QUY CHUẨN THUẬT TOÁN & TIÊU CHÍ ĐÁNH GIÁ (LAB 1 CRITERIA)

1. **Phần 1 - Tiền xử lý dữ liệu**:
   - Nhận diện đúng ký tự rỗng (vd: `na_values=['?']` trong Titanic).
   - Điền khuyết thiếu có lý do: dùng mode cho biến phân loại, median cho biến phân phối lệch (skewed), mean cho biến chuẩn.
   - Chia nhóm (binning): phân biệt rõ `pd.qcut` (chia cân bằng số lượng - equal frequency) và `pd.cut` (chia theo khoảng giá trị cố định).
   - One-hot encoding / Label encoding: áp dụng đúng bản chất biến định danh hay thứ bậc.
2. **Phần 2 - Khai phá tập phổ biến & Luật kết hợp**:
   - Làm sạch hóa đơn: loại bỏ `InvoiceNo` chứa `'C'` (hóa đơn hủy/hoàn trả), loại bỏ chi phí dịch vụ phi hàng hóa (`'POSTAGE'`).
   - One-hot matrix: giá trị $\le 0 \to 0$, $\ge 1 \to 1$ với kiểu dữ liệu `bool` hoặc `int`.
   - Lựa chọn thuật toán:
     - `mlxtend.frequent_patterns.apriori(df, min_support=..., use_colnames=True)`
     - `mlxtend.frequent_patterns.fpgrowth(df, min_support=..., use_colnames=True)`
     - `mlxtend.frequent_patterns.association_rules(frequent_itemsets, metric="confidence", min_threshold=...)`
   - Đo lường và so sánh hiệu năng:
     - Dùng `time.perf_counter()` đo thời gian thực thi độc lập cho Apriori và FP-Growth trên cùng danh sách `min_sup` từ `0.01%` (`0.0001`) đến `0.1%` (`0.001`).
     - Giải thích bản chất thuật toán: Apriori tốn chi phí sinh tập ứng viên và quét CSDL nhiều lần ($O(2^d)$); FP-Growth sử dụng cấu trúc cây FP-Tree nén trong bộ nhớ và khai phá theo phương pháp chia để trị, không sinh ứng viên.

---

## 6. KỸ NĂNG VÀ LỆNH HỖ TRỢ (SKILLS)

Dự án được trang bị các skill chuyên biệt trong `.claude/skills/`:

- `/solve-lab`: Hướng dẫn hoặc triển khai giải chi tiết từng bài tập trong Lab 1.
- `/check-env`: Kiểm tra trạng thái môi trường `.venv`, thư viện đã cài đặt và các tập dữ liệu.
- `/review-solution`: Rà soát code và notebook theo chuẩn báo cáo của mẫu nộp bài.

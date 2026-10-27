# AGENTS.MD - HƯỚNG DẪN & QUY CHUẨN DÀNH CHO TẤT CẢ CÁC AI AGENT
> Tài liệu này là quy chuẩn chung (Universal Agent Instructions) áp dụng cho mọi AI Coding Agent (Claude Code, Cursor, Windsurf, Copilot, Roo Code, Aider, v.v.) khi làm việc trong dự án này.

---

## 1. THÔNG TIN DỰ ÁN & ĐỊNH DANH SINH VIÊN

- **Môn học**: Khai phá dữ liệu (Data Mining - Mã học phần: IT1.231.3) - Lab 1
- **Sinh viên thực hiện**: Nguyễn Thành Trí
- **Mã số sinh viên (MSSV)**: `6451071079`
- **Lớp**: CQ.64.CNTT
- **Tài liệu tham chiếu**:
  - `docs/bai_tap_lab1.md`: Nội dung chi tiết đề bài từng phần.
  - `docs/Template nộp bài LAB1.docx`: Mẫu báo cáo Word chính thức.
  - `docs/lab1.pdf`: Giáo trình thực hành gốc.

### Quy chuẩn định danh bắt buộc trên mã nguồn:
1. **Ô Markdown đầu tiên của mỗi Notebook**:
   ```markdown
   # Nguyễn Thành Trí - MSSV: 6451071079
   ## [Tên phần / bài tập cụ thể]
   ```
2. **Trong từng ô code chính**:
   ```python
   # Nguyễn Thành Trí - 6451071079
   print("Họ tên: Nguyễn Thành Trí - MSSV: 6451071079")
   ```

---

## 2. QUY TẮC MÔI TRƯỜNG & PYTHON RUNTIME

1. **Bắt buộc sử dụng môi trường ảo `.venv`**:
   - Tất cả các lệnh Python, Jupyter hoặc package manager phải thực thi qua `.venv/bin/python`, `.venv/bin/pip`, hoặc kích hoạt `source .venv/bin/activate`.
   - **Tuyệt đối không** sử dụng Python hệ thống (`/usr/bin/python3`).
2. **Quản lý thư viện phụ thuộc (`requirements.txt`)**:
   - Các gói thư viện tối thiểu gồm:
     ```text
     numpy
     pandas
     seaborn
     matplotlib
     ipykernel
     openpyxl
     mlxtend
     ```
   - Cài đặt/cập nhật qua: `.venv/bin/pip install -r requirements.txt`.
3. **Jupyter Kernel**:
   - Kernel gắn với môi trường ảo: `Python 3 (.venv)`.

---

## 3. QUY TẮC BẤT DI BẤT DỊCH (CORE AGENT RULES)

Mọi AI Agent khi can thiệp vào codebase này **phải tuyệt đối tuân thủ 4 quy tắc sau**:

### Rule 1: Giữ sạch thư mục gốc (Root Hygiene) & Quản lý file tạm
- **Nghiêm cấm** tạo bất kỳ file script tạm, file nháp hoặc file vá lỗi (ví dụ: `fix_*.py`, `temp_*.py`, `test_*.py`, `generate_*.py`) ở thư mục gốc của dự án.
- **Thực hiện trực tiếp (In-place editing)**: Khi sửa lỗi code hoặc notebook, sử dụng trực tiếp công cụ chỉnh sửa file của môi trường hoặc lệnh inline `python -c "..."`.
- **Nếu bắt buộc viết script tự động hóa**: Mọi script sinh dữ liệu / notebook phải đặt trong thư mục `scripts/` (ví dụ: `scripts/make_phan2_bai5a.py`). Thư mục `scripts/` đã được Git bỏ qua trong `.gitignore`. Sau khi hoàn thành phải dọn dẹp các file nháp tạm.

### Rule 2: Định tuyến đường dẫn an toàn (Safe Relative Paths)
Code có thể được người dùng hoặc giảng viên chạy từ thư mục gốc hoặc từ thư mục con bài tập (`Phan1/Bai1/`, `Phan2/Bai2/`, v.v.). Mọi code phải sử dụng hai hàm an toàn sau:

```python
import os

def get_data_path(rel_path):
    """Tìm đường dẫn đến file trong thư mục datasets từ bất kỳ cấp thư mục nào."""
    candidates = [
        rel_path,
        os.path.join("..", rel_path),
        os.path.join("..", "..", rel_path),
        os.path.join("datasets", os.path.basename(rel_path)),
        os.path.join("..", "datasets", os.path.basename(rel_path)),
        os.path.join("..", "..", "datasets", os.path.basename(rel_path))
    ]
    for p in candidates:
        if os.path.exists(p):
            return p
    raise FileNotFoundError(f"Không tìm thấy file dữ liệu: {rel_path}")

def get_img_dir(subpath=""):
    """Đảm bảo thư mục lưu ảnh luôn trỏ về thư mục gốc images/<subpath>."""
    for base in [".", "..", "../.."]:
        img_root = os.path.join(base, "images")
        if os.path.exists(img_root) and (os.path.exists(os.path.join(base, "datasets")) or os.path.exists(os.path.join(base, "CLAUDE.md")) or os.path.exists(os.path.join(base, "AGENTS.md"))):
            target = os.path.join(img_root, subpath) if subpath else img_root
            os.makedirs(target, exist_ok=True)
            return target
    target = os.path.join("images", subpath) if subpath else "images"
    os.makedirs(target, exist_ok=True)
    return target
```

### Rule 3: Quy hoạch thư mục ảnh tập trung (`images/`)
- Mọi biểu đồ và hình chụp minh họa **chỉ được lưu vào thư mục gốc [images/](images/)** theo cấu trúc phân cấp:
  - `images/Phan1/Bai1/`: Biểu đồ Titanic.
  - `images/Phan1/Bai2/`: Biểu đồ Bank Marketing.
  - `images/Phan1/Bai3/`: Đồ thị cảm biến CO, Độ ẩm, Nhiệt độ.
  - `images/Phan2/Bai2/`: Đồ thị luật kết hợp Online Retail UK.
  - `images/Phan2/Bai5a/`: Đồ thị luật kết hợp Online Retail Germany.
  - `images/Phan2/Bai6/`: Biểu đồ so sánh thời gian Apriori vs FP-Growth.
- **Tuyệt đối không** tạo thư mục `images/` con nằm bên trong các thư mục bài làm `Phan1/` hay `Phan2/`.
- Khi lưu ảnh dùng: `plt.savefig(os.path.join(img_dir, 'ten_anh.png'), dpi=300, bbox_inches='tight')`.

### Rule 4: Chuẩn mực trình bày đồ thị (Data Visualization)
- Luôn có đầy đủ tiêu đề (`plt.title`), nhãn trục (`plt.xlabel`, `plt.ylabel`), chú thích (`plt.legend`) và lưới mờ (`plt.grid(True, alpha=0.3)` hoặc `linestyle='--'`).
- Sử dụng màu sắc tương phản rõ ràng, hỗ trợ hiển thị đẹp trong báo cáo Word.

---

## 4. CẤU TRÚC CODEBASE

```text
├── datasets/                   # Dữ liệu nguồn bài tập
│   ├── titanic.csv             # Phần 1 - Bài 2 (tr. 15-17)
│   ├── Bank/bank.csv           # Phần 1 - Bài 2 (tr. 28-29)
│   ├── tb_tracking.xlsx        # Phần 1 - Bài 2 (tr. 30)
│   ├── Online Retail.xlsx      # Phần 2 - Bài 2 & Bài 5a (tr. 34-38)
│   └── groceries.csv           # Phần 2 - Bài 6 (tr. 39-41)
├── docs/                       # Tài liệu hướng dẫn & mẫu nộp bài
│   ├── bai_tap_lab1.md         # Yêu cầu chi tiết của từng bài
│   ├── lab1.pdf                # Giáo trình gốc
│   └── Template nộp bài LAB1.docx # Mẫu Word nộp bài
├── images/                     # Toàn bộ ảnh xuất ra phục vụ báo cáo
│   ├── Phan1/ (Bai1, Bai2, Bai3)
│   └── Phan2/ (Bai2, Bai5a, Bai6)
├── Phan1/                      # Bài làm Phần 1 - Tiền xử lý dữ liệu
│   ├── Bai1/                   # Titanic (.ipynb)
│   ├── Bai2/                   # Bank Marketing (.ipynb)
│   └── Bai3/                   # Cảm biến xưởng (.ipynb)
├── Phan2/                      # Bài làm Phần 2 - Khai phá tập phổ biến & Luật kết hợp
│   ├── Bai2/                   # Online Retail UK (.ipynb)
│   ├── Bai5a/                  # Online Retail Germany (.ipynb)
│   └── Bai6/                   # So sánh Apriori vs FP-Growth (.ipynb)
├── scripts/                    # Scripts công cụ sinh code / tự động hóa (gitignored)
├── requirements.txt            # Danh sách thư viện Python
├── AGENTS.md                   # Hướng dẫn chung cho tất cả AI Agent
└── CLAUDE.md                   # Hướng dẫn riêng cho Claude Code CLI
```

---

## 5. QUY TRÌNH THỰC HIỆN CÔNG VIỆC (AGENT WORKFLOWS)

Mọi Agent có thể gọi hoặc làm theo 3 quy trình công việc chuẩn sau:

### Workflow 1: Kiểm tra môi trường (Environment Verification)
1. Kiểm tra Python runtime trong môi trường ảo: `.venv/bin/python --version`.
2. Kiểm tra nạp các thư viện:
   ```bash
   .venv/bin/python -c "import numpy, pandas, matplotlib, seaborn, openpyxl, mlxtend; print('OK')"
   ```
3. Kiểm tra tính toàn vẹn của các file dữ liệu trong `datasets/`.

### Workflow 2: Triển khai giải bài tập (Lab Implementation)
1. Đọc yêu cầu bài tập từ `docs/bai_tap_lab1.md`.
2. Tạo/cập nhật file Notebook `.ipynb` tại đúng thư mục phân mục (`Phan1/BaiX` hoặc `Phan2/BaiX`).
3. Đảm bảo cấu trúc mỗi bài:
   - Cell Markdown: Đề bài, câu hỏi, ý nghĩa thuộc tính.
   - Cell Code: Khai báo định danh sinh viên, hàm `get_data_path()`, hàm `get_img_dir()`, code xử lý dữ liệu, biểu đồ trực quan.
   - Cell Markdown: Nhận xét kết quả cụ thể, phân tích nghiệp vụ rõ ràng.
4. Chạy kiểm thử notebook bằng `.venv/bin/jupyter execute <notebook.ipynb>`.

### Workflow 3: Kiểm định chất lượng & Tiêu chuẩn nộp bài (Quality Review)
1. **Kiểm tra thông tin sinh viên**: `Nguyễn Thành Trí` - `6451071079` xuất hiện đúng quy chuẩn.
2. **Kiểm tra tính chạy được**: Notebook chạy tuần tự từ đầu đến cuối không phát sinh lỗi.
3. **Kiểm tra tính đúng đắn nghiệp vụ**:
   - Nhận diện đúng missing ẩn (`?`, `'unknown'`).
   - Lọc sạch hóa đơn hủy (`InvoiceNo` chứa `'C'`) và loại bỏ chi phí dịch vụ phi hàng hóa (`'POSTAGE'`).
   - Ma trận giỏ hàng dạng 0/1 boolean.
   - Ngưỡng `min_sup` và `min_conf` chuẩn theo đề bài.
   - So sánh định lượng thời gian chạy bằng `time.perf_counter()` giữa Apriori và FP-Growth trên `groceries.csv`.
4. **Kiểm tra thư mục**:
   - Thư mục gốc sạch sẽ, không có script tạm.
   - Toàn bộ ảnh đã được lưu vào thư mục chuẩn `images/<PhanX>/<BaiY>/`.

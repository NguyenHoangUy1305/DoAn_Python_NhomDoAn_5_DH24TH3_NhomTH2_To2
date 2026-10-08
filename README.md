# 🐍 HỆ THỐNG QUẢN LÝ BỆNH NHÂN & ĐƠN THUỐC (PYTHON TKINTER & MYSQL)

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3" />
  <img src="https://img.shields.io/badge/GUI-Tkinter-FFD43B?style=for-the-badge&logo=python&logoColor=306998" alt="Tkinter" />
  <img src="https://img.shields.io/badge/Modeling-MySQL_Workbench-00758F?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL Workbench" />
  <img src="https://img.shields.io/badge/Database-MySQL_%2F_SQL_Server-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="Database" />
  <img src="https://img.shields.io/badge/Driver-pypyodbc-00599C?style=for-the-badge" alt="ODBC Driver" />
</p>

---

## 📌 1. TỔNG QUAN ĐỀ TÀI
* **Môn học:** Chuyên đề Python (COS525)
* **Đơn vị đào tạo:** Khoa Công nghệ Thông tin – Trường Đại học An Giang (ĐHQG TP.HCM)
* **Giảng viên hướng dẫn:** ThS. Nguyễn Ngọc Minh
* **Sinh viên thực hiện:**
  - **Nguyễn Hoàng Uy** (MSSV: `DTH235812`) – Lớp: DH24TH3
  - **Tạ Nguyễn Thành Tín** (MSSV: `DTH235787`) – Lớp: DH24TH3

Đề tài nghiên cứu và xây dựng phần mềm máy tính **Quản lý bệnh nhân** bằng ngôn ngữ **Python**, áp dụng thư viện đồ họa **Tkinter** kết hợp cơ sở dữ liệu quan hệ **MySQL / SQL Server**. Ứng dụng cung cấp giải pháp chuyển đổi số cho cơ sở y tế với giao diện hiện đại, trực quan, hỗ trợ quản lý bệnh nhân, kê đơn thuốc tự động và kiểm soát tồn kho thuốc.

---

## 💡 2. ĐIỂM NHẤN KỸ THUẬT NỔI BẬT

1. **Custom UI Component (ShapeButton with Smooth Color Animation):**
   - Tự xây dựng lớp `ShapeButton` kế thừa `tk.Frame` sử dụng Canvas API để vẽ nút bấm bo tròn góc cạnh (Rounded Rectangle).
   - Tự cài đặt thuật toán nội suy mã màu RGB (`_animate_color_transition`), tạo hiệu ứng chuyển đổi màu mượt mà khi hover chuột (Hover Transition Effect).
2. **Kiến trúc Đa tầng & Module hóa (Tab-Based Architecture):**
   - Phân tách độc lập từng module chức năng thành các file tab riêng biệt (`benhnhan_tab.py`, `donthuoc_tab.py`, `thuoc_tab.py`,...), giúp dễ dàng bảo trì và mở rộng code.
3. **Cơ chế Dò tìm Cấu hình Kết nối Tự động (Fallback Connection Strategy):**
   - File `db_connect.py` cài đặt danh sách các chuỗi kết nối dự phòng (ODBC Driver 17, Driver 18, SQL Server Express, Localhost), giúp ứng dụng tự động thích ứng với cấu hình máy chủ của người dùng mà không cần cấu hình lại thủ công.
4. **Mô hình hóa dữ liệu chuyên nghiệp (EER / ERD):**
   - Thiết kế sơ đồ quan hệ thực thể trực tiếp trên **MySQL Workbench** (`DG_QuanlyBenhNhan.mwb`), đảm bảo chuẩn hóa dữ liệu 3NF và khóa ngoại chặt chẽ.

---

## 🏗️ 3. KIẾN TRÚC & CÔNG NGHỆ ÁP DỤNG

| Thành phần | Công nghệ / Thư viện | Vai trò |
| :--- | :--- | :--- |
| **Ngôn ngữ** | Python 3.9+ | Xử lý logic nghiệp vụ, tính toán tiền thuốc và điều hướng |
| **Giao diện (GUI)** | Tkinter & `ttk` | Xây dựng giao diện Desktop, Data Table (`ttk.Treeview`) |
| **DatePicker** | `tkcalendar` (`DateEntry`) | Chọn ngày sinh, ngày khám bệnh, ngày tái khám trực quan |
| **Cơ sở dữ liệu** | MySQL / SQL Server | Lưu trữ quan hệ thực thể, ràng buộc toàn vẹn |
| **DB Driver** | `pypyodbc` / `pyodbc` | Kết nối ODBC Driver tốc độ cao, quản lý Cursor và Transaction |
| **Thiết kế CSDL** | MySQL Workbench | Thiết kế file sơ đồ dữ liệu mô hình vật lý `.mwb` |

---

## 🗄️ 4. CẤU TRÚC CƠ SỞ DỮ LIỆU

Hệ thống được thiết kế với **10 bảng thực thể** (tham chiếu file `QuanLyBenhNhan.sql` và `DG_QuanlyBenhNhan.mwb`):

* **`benhnhan`**: `MaBN` (PK), `HoTenBN`, `GioiTinhBN`, `TuoiBN`, `SDTBN`, `NgaySinh`, `DiaChiBN`, `MaBenh` (FK).
* **`chitietbenhnhan`**: `MaCTBN` (PK Auto-Increment), `MaBN` (FK), `MaNV` (FK), `MaBenh` (FK), `NgayKham`, `ChanDoan`, `KetQua`.
* **`donthuoc`**: `MaDT` (PK), `MaBN` (FK), `MaNV` (FK), `NgayLap`, `TongTien`.
* **`chitietdonthuoc`**: `MaDT` (PK/FK), `MaThuoc` (PK/FK), `SoLuong`, `HuongDanUong`, `NgayKhamBenh`, `NgayTaiKham`.
* **`thuoc`**: `MaThuoc` (PK), `TenThuoc`, `DonViTinh`, `DonGia`, `CongDung`.
* **`macbenh`**: `MaBenh` (PK), `LoaiBenh`.
* **`khoa`**: `MaKhoa` (PK), `TenKhoa`.
* **`chucvu`**: `MaCV` (PK), `TenCV`.
* **`nhanvien`**: `MaNV` (PK), `HoTenNV`, `TuoiNV`, `GioiTinhNV`, `SDTNV`, `MaKhoa` (FK), `MaCV` (FK).

---

## 📂 5. CẤU TRÚC THƯ MỤC MÃ NGUỒN

```text
DoAn_Python/
├── Chương trình quản lý bệnh nhân (Python).docx  # Báo cáo đồ án chi tiết (Word)
├── DG_QuanlyBenhNhan.mwb                         # Sơ đồ CSDL vật lý (MySQL Workbench)
├── QuanLyBenhNhan.sql                            # Kịch bản DDL/DML khởi tạo Database
├── db_connect.py                                 # Module cấu hình kết nối DB & Helper căn giữa cửa sổ
├── main.py                                       # File chính khởi chạy Dashboard điều hướng
├── benhnhan_tab.py                               # Phân hệ quản lý hồ sơ bệnh nhân
├── chitietbenhnhan_tab.py                        # Phân hệ hồ sơ bệnh án & chẩn đoán
├── donthuoc_tab.py                               # Phân hệ lập và quản lý đơn thuốc
├── chitietdonthuoc_tab.py                        # Phân hệ chi tiết thuốc, liều dùng, tái khám
├── thuoc_tab.py                                  # Phân hệ danh mục kho thuốc & đơn giá
├── nhanvien_tab.py                               # Phân hệ quản lý nhân viên y tế
├── khoa_tab.py                                   # Phân hệ chuyên khoa phòng ban
├── chucvu_tab.py                                 # Phân hệ danh mục chức vụ
├── macbenh_tab.py                                # Phân hệ danh mục phân loại bệnh
├── assets/                                       # Tài nguyên đồ họa, icon chương trình
└── README.md
```

---

## 🚀 6. HƯỚNG DẪN CÀI ĐẶT & CHẠY LOCAL

### Yêu cầu hệ thống:
* Đã cài đặt **Python 3.9+** trên máy tính.
* Đã cài đặt **ODBC Driver for SQL Server** (Driver 17 hoặc 18) hoặc máy chủ **MySQL / SQL Server**.

### Các bước khởi chạy:
1. **Clone repository về máy:**
   ```bash
   git clone https://github.com/NguyenHoangUy1305/DoAn_Python_NhomDoAn_5_DH24TH3_NhomTH2_To2.git
   cd DoAn_Python_NhomDoAn_5_DH24TH3_NhomTH2_To2
   ```
2. **Cài đặt các thư viện cần thiết:**
   ```bash
   pip install pypyodbc tkcalendar
   ```
3. **Chuẩn bị Cơ sở dữ liệu:**
   - Sử dụng file `QuanLyBenhNhan.sql` để import dữ liệu vào Database của bạn.
4. **Khởi chạy ứng dụng:**
   ```bash
   python main.py
   ```

---

## 👨‍💻 7. NHÓM TÁC GIẢ
* **Nguyễn Hoàng Uy** – *Full-stack Python GUI, Connection Fallback & Database Modeling* – [`NguyenHoangUy1305`](https://github.com/NguyenHoangUy1305)
* **Tạ Nguyễn Thành Tín** – *Giao diện Tkinter & Nghiệp vụ Quản lý Khám Bệnh* – [`Thanh-Tin`](https://github.com/Thanh-Tin)

*Khoa Công nghệ Thông tin – Trường Đại học An Giang (ĐHQG TP.HCM)*

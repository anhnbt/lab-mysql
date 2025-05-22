# Lab 1 – Xây dựng Cơ sở dữ liệu quản lý bán hàng (MySQL)

## Yêu cầu:

1. Sử dụng **MySQL** để tạo **Cơ sở dữ liệu** có tên: `quan_ly_ban_hang`.
2. Tạo các bảng theo cấu trúc bên dưới, sử dụng cú pháp **`snake_case`** cho tên bảng và tên cột.
3. Đảm bảo mỗi bảng có **khóa chính**, và các khóa ngoại phải **tham chiếu đúng bảng liên quan**.
4. Nhập dữ liệu mẫu cho **mỗi bảng ít nhất 5 bản ghi**.
5. Viết các **truy vấn SQL** theo yêu cầu ở phần dưới.
6. Nộp file SQL (`lab1_quan_ly_ban_hang.sql`) **file chứa các câu lệnh SQL** (tạo CSDL, tạo bảng, thêm dữ liệu, truy vấn).

---

## Cấu trúc các bảng

### 1. Bảng `khach_hang`

| Tên cột         | Kiểu dữ liệu   | Mô tả                        |
| --------------- | -------------- | ---------------------------- |
| `ma_khach_hang` | `VARCHAR(5)`   | Mã khách hàng (khóa chính)   |
| `ho_va_ten_lot` | `VARCHAR(50)`  | Họ và tên lót khách hàng     |
| `ten`           | `VARCHAR(50)`  | Tên khách hàng               |
| `dia_chi`       | `VARCHAR(255)` | Địa chỉ khách hàng           |
| `email`         | `VARCHAR(50)`  | Email khách hàng             |
| `dien_thoai`    | `VARCHAR(13)`  | Số điện thoại của khách hàng |

---

### 2. Bảng `san_pham`

| Tên cột       | Kiểu dữ liệu    | Mô tả                                  |
| ------------- | --------------- | -------------------------------------- |
| `ma_san_pham` | `INT`           | Mã sản phẩm (khóa chính, tự động tăng) |
| `ten_sp`      | `VARCHAR(50)`   | Tên sản phẩm                           |
| `mo_ta`       | `VARCHAR(255)`  | Mô tả về sản phẩm                      |
| `so_luong`    | `INT`           | Số lượng tồn kho (>= 0)                |
| `don_gia`     | `DECIMAL(15,2)` | Đơn giá sản phẩm (>= 0)                |

---

### 3. Bảng `hoa_don`

| Tên cột         | Kiểu dữ liệu  | Mô tả                                                   |
| --------------- | ------------- | ------------------------------------------------------- |
| `ma_hoa_don`    | `INT`         | Mã hóa đơn (khóa chính, tự động tăng)                   |
| `ngay_mua_hang` | `DATE`        | Ngày mua hàng                                           |
| `ma_khach_hang` | `VARCHAR(5)`  | Mã khách hàng (khóa ngoại tham chiếu `khach_hang`)      |
| `trang_thai`    | `VARCHAR(30)` | Trạng thái đơn hàng (đã thanh toán, chưa thanh toán...) |

---

### 4. Bảng `hoa_don_chi_tiet`

| Tên cột               | Kiểu dữ liệu | Mô tả                                                         |
| --------------------- | ------------ | ------------------------------------------------------------- |
| `ma_hoa_don_chi_tiet` | `INT`        | Mã chi tiết hóa đơn (khóa chính, tự động tăng)                |
| `ma_hoa_don`          | `INT`        | Mã hóa đơn (khóa ngoại tham chiếu `hoa_don`)                  |
| `ma_san_pham`         | `INT`        | Mã sản phẩm trong đơn hàng (khóa ngoại tham chiếu `san_pham`) |
| `so_luong`            | `INT`        | Số lượng mua                                                  |

---

## Các truy vấn SQL yêu cầu

- Hiển thị số lượng khách hàng có trong bảng `khach_hang`
- Hiển thị đơn giá lớn nhất trong bảng `san_pham`
- Hiển thị số lượng sản phẩm thấp nhất trong bảng `san_pham`
- Hiển thị tổng số lượng sản phẩm có trong bảng `san_pham`
- Hiển thị số hóa đơn đã xuất trong tháng 12/2016 mà có trạng thái **chưa thanh toán**
- Hiển thị mã hóa đơn và số loại sản phẩm được mua trong từng hóa đơn
- Hiển thị mã hóa đơn và số loại sản phẩm được mua trong từng hóa đơn, **chỉ hiển thị các hóa đơn có từ 5 loại sản phẩm trở lên**
- Hiển thị thông tin bảng `hoa_don` gồm các cột `ma_hoa_don`, `ngay_mua_hang`, `ma_khach_hang`, **sắp xếp theo thứ tự giảm dần của `ngay_mua_hang`**

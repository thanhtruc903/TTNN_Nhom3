# DNP Logistics WMS

Hệ thống quản lý kho thống nhất xây dựng bằng **Flask, SQLAlchemy và Alembic**. Ứng dụng có thể chạy offline ngay với SQLite hoặc sử dụng SQL Server 2022.

## Tính năng nổi bật

- **Phân quyền & Bảo mật:** Quản lý quyền chặt chẽ (`ADMIN`, `CS`, `WAREHOUSE`) với mật khẩu băm và CSRF.
- **Vận hành kho:** Quản lý một kho duy nhất tại Đà Nẵng. Theo dõi tồn kho theo sản phẩm, lot/pallet, hỗ trợ số thập phân và kiểm kê snapshot.
- **Nhập/Xuất hàng:** Hỗ trợ phiếu nhiều dòng, lấy hàng theo FEFO/FIFO, chặn xuất hàng hết hạn và ngăn tồn kho âm. Cập nhật tồn nguyên tử (rollback toàn bộ nếu có một dòng lỗi).
- **Giao diện & Báo cáo:** Dashboard hiển thị KPI trực quan. Giao diện tiếng Việt responsive, hỗ trợ thao tác bàn phím và máy quét mã vạch USB.

## SQLite

**Yêu cầu:** Python 3.10 trở lên.

Mở Terminal (hoặc PowerShell) và chạy các lệnh sau:

```powershell
# Tạo và kích hoạt môi trường ảo
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# Cài đặt thư viện
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
Copy-Item .env.example .env

# Khởi tạo DB và chạy ứng dụng
flask --app run.py db upgrade
flask --app run.py seed-db
python run.py
```

*Truy cập ứng dụng tại:* <http://127.0.0.1:5000>

## Tài khoản Demo

| Vai trò | Tên đăng nhập | Mật khẩu |
| :--- | :--- | :--- |
| **Quản trị viên** | `admin` | `Admin@123` |
| **CSKH** | `cs` | `Cs@123456` |
| **Nhân viên kho** | `warehouse` | `Kho@12345` |

## API Core

Hệ thống cung cấp các API chuẩn (luôn trả về `data` và `meta`) cho các nghiệp vụ:

- **Auth:** `POST /api/auth/login`, `POST /api/auth/logout`, `GET /api/auth/me`
- **Cấu hình & Master Data:** Quản lý danh mục, người dùng, hàng hóa, khách hàng.
- **Nghiệp vụ Kho:** Quản lý Phiếu nhập (`/api/inbound-receipts`), Phiếu xuất (`/api/outbound-receipts`), Tồn kho và Kiểm kê.
- **Báo cáo:** Trích xuất báo cáo tổng hợp và xuất file CSV.

## Cấu trúc Database & Lịch sử nhóm

- **SQL Server 2022:** Hỗ trợ kết nối qua Microsoft ODBC Driver 18 bằng chuỗi `DATABASE_URL` trong file `.env`.
- **Backup/Restore (SQLite):** Hỗ trợ lệnh CLI qua Flask (`backup-db`, `restore-db`).
- **Phân công đóng góp:**
  - `Anh_Thu`: Frontend, UI/UX, responsive và trải nghiệm người dùng.
  - `Le_Thao`: Backend, Database, transaction và toàn vẹn tồn kho.
  - `Thanh_Truc`: Phân tích yêu cầu, acceptance, báo cáo và tài liệu. 

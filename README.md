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

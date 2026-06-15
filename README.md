# USING AI CLAUDE

# VNStock Dashboard v4

Dashboard chứng khoán Việt Nam dùng **vnstock v4** — chạy local trên VS Code.

## Cấu trúc thư mục

```
vnstock-dashboard/
├── server.py          ← Backend FastAPI (Python)
├── requirements.txt   ← Các thư viện cần cài
├── templates/
│   └── index.html     ← Frontend dashboard
└── static/            ← (tùy chọn) file CSS/JS tĩnh
```

---

## Cài đặt & Chạy

### Bước 1 — Cài Python packages

```bash
pip install -r requirements.txt
```

Hoặc cài từng cái:
```bash
pip install fastapi uvicorn vnstock pandas
```

### Bước 2 — Chạy server

```bash
python server.py
```

Hoặc dùng uvicorn (có hot-reload):
```bash
uvicorn server:app --reload --port 8000
```

### Bước 3 — Mở trình duyệt

```
http://localhost:8000
```

API docs (Swagger):
```
http://localhost:8000/docs
```

---

## Các API endpoint

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| GET | `/api/health` | Kiểm tra server |
| GET | `/api/listing` | Danh sách cổ phiếu niêm yết |
| GET | `/api/stock/history` | Lịch sử giá OHLCV |
| GET | `/api/stock/intraday` | Dữ liệu intraday (tick) |
| GET | `/api/stock/profile` | Thông tin công ty |
| GET | `/api/stock/financials` | Báo cáo tài chính |
| GET | `/api/stock/news` | Tin tức cổ phiếu |
| GET | `/api/stock/events` | Sự kiện (cổ tức, ĐHCĐ) |
| GET | `/api/market/indices` | Lịch sử chỉ số (VNIndex...) |
| GET | `/api/market/board` | Bảng giá real-time |
| GET | `/api/market/top` | Top tăng/giảm/khối lượng |
| GET | `/api/market/group` | Nhóm VN30, VN100... |
| GET | `/api/market/forex` | Tỷ giá ngoại tệ |
| GET | `/api/market/crypto` | Giá crypto |
| GET | `/api/screener` | Bộ lọc cổ phiếu |

### Ví dụ gọi API

```bash
# Lịch sử giá VNM 3 tháng
curl "http://localhost:8000/api/stock/history?ticker=VNM&start=2025-02-01&end=2025-05-18"

# Báo cáo tài chính FPT theo quý
curl "http://localhost:8000/api/stock/financials?ticker=FPT&report=income&period=quarter"

# Top tăng mạnh HOSE
curl "http://localhost:8000/api/market/top?mode=gainers&exchange=HOSE&limit=10"

# Bảng giá VN30
curl "http://localhost:8000/api/market/board?symbols=VNM,FPT,VCB,ACB,HPG"

# VNIndex 90 ngày gần nhất
curl "http://localhost:8000/api/market/indices?symbols=VNINDEX&start=2025-02-01"
```

---

## Tính năng Dashboard

- **📊 4 chỉ số chính** — VN-Index, HNX, UPCOM, VN30 với sparkline
- **🔍 Tìm kiếm mã** — Tìm theo tên hoặc mã cổ phiếu
- **📈 Biểu đồ giá** — Chart nến/đường, các khung thời gian 1T/1M/3M/6M/1Y
- **🔥 Heatmap VN30** — Màu xanh/đỏ theo biến động
- **🏆 Top cổ phiếu** — Tăng mạnh / Giảm mạnh / Khối lượng lớn
- **📑 Báo cáo tài chính** — KQKD / CĐKT / LCTT / Chỉ số tài chính
- **📰 Tin tức** — Tin tức cổ phiếu real-time
- **🔄 Auto refresh** — Tự động cập nhật mỗi 60 giây

---

## Yêu cầu hệ thống

- Python 3.10+
- vnstock >= 4.0.0
- Kết nối internet (để lấy dữ liệu từ TCBS/SSI)

## Lưu ý

vnstock v4 yêu cầu API key cho một số tính năng nâng cao.  
Đăng ký miễn phí tại: https://vnstocks.com

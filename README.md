# HV INVEST – Hệ thống Hỗ trợ Đầu tư Chứng khoán

## Cài đặt và Chạy

```bash

python -m venv venv
source venv/bin/activate   
# venv\Scripts\activate   

# 2. Cài thư viện
pip install -r requirements.txt

# 3. Chạy server
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# 4. Mở trình duyệt
# http://localhost:8000
# http://127.0.0.1:8001
```

## Cấu trúc hệ thống

```
stock_app/
├── main.py              # FastAPI backend (5 nhóm API)
├── requirements.txt
└── static/
    └── index.html       # Frontend 5 trang (SPA)
```

## API Endpoints

| Endpoint | Mô tả |
|---|---|
| `GET /api/dashboard` | Dashboard: tất cả cổ phiếu, heatmap, regime |
| `GET /api/stock/{symbol}` | Phân tích chi tiết 1 mã (+ `?timeframe=7`) |
| `POST /api/backtest` | Backtest RF vs Buy&Hold |
| `GET /api/compare?symbols=VCB,BID,VNM` | So sánh nhiều mã |
| `GET /api/glossary` | Từ điển thuật ngữ |

<img width="1391" height="771" alt="Ảnh màn hình 2026-05-14 lúc 14 55 05" src="https://github.com/user-attachments/assets/ad9f4dfc-8cfa-459f-a0ea-b1492ec9b47c" />
<img width="1391" height="771" alt="Ảnh màn hình 2026-05-14 lúc 14 54 55" src="https://github.com/user-attachments/assets/28ec30ef-5776-4c09-b7b3-3ee93ce8ef92" />

<img width="1366" height="766" alt="Ảnh màn hình 2026-05-03 lúc 08 56 51" src="https://github.com/user-attachments/assets/b299935e-2a95-4033-97e4-11734db445b0" />
## Logic phân tích

- **Nhóm ngân hàng** (BID, VCB, CTG, MBB...): Random Forest Classifier (100 trees)
  - Features: RSI, MACD, MA, EMA, Bollinger Bands, Momentum, Volume
  - Label: "Model (Bank-trained)"
  
- **Các mã khác**: Technical Analysis thuần
  - RSI + MACD + MA Cross + Bollinger Bands
  - Label: "Phân tích kỹ thuật"

## Tính năng

1. **Dashboard** – Tổng quan, heatmap, top signals
2. **Phân tích Cổ Phiếu** – Biểu đồ giá, dự báo 7 ngày, multi-timeframe
3. **Máy Thời Gian** – Backtest chiến lược RF vs Buy&Hold
4. **So sánh Cổ Phiếu** – Sharpe, drawdown, return comparison
5. **Học thuật ngữ** – RSI, MACD, LSTM, Random Forest, indicators

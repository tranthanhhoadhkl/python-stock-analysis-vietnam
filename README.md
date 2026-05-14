# StockAI Vietnam – Hệ thống Hỗ trợ Đầu tư Chứng khoán

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
<img width="1364" height="756" alt="Ảnh màn hình 2026-04-30 lúc 16 56 04" src="https://github.com/user-attachments/assets/d9f585d0-9890-4280-8e47-88250d2db5f1" />
<img width="1457" height="770" alt="Ảnh màn hình 2026-04-29 lúc 15 39 20" src="https://github.com/user-attachments/assets/c25a34cc-57f8-4aea-a165-cbc34154b495" />
<img width="1457" height="770" alt="Ảnh màn hình 2026-04-28 lúc 08 28 04" src="https://github.com/user-attachments/assets/c3a002e4-a130-4bda-9c56-d3b390230b78" />
<img width="1457" height="729" alt="Ảnh màn hình 2026-04-28 lúc 08 27 55" src="https://github.com/user-attachments/assets/7aebeca2-2c00-4ad0-a177-e5063d7227f8" />
<img width="1457" height="729" alt="Ảnh màn hình 2026-04-28 lúc 08 27 46" src="https://github.com/user-attachments/assets/035ce7b8-b6c9-4113-b314-8e13a9d1c5a3" />

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

# Tego MQTT Broker

發酵設備用的 **EMQX** Broker（Docker）。測試用 Pub / Sub Edge 不在此倉庫。

- **映像**：`emqx/emqx:5.8.3`
- **MQTT**：`1883`
- **主題**：`/device/ferment`（設備與 `tego_backend` subscriber 使用）
- **Dashboard**：僅綁本機 `127.0.0.1:18083`

## 啟動

```bash
docker compose up -d
```

MQTT：`mqtt://<host>:1883`  
Dashboard（需 SSH 連到主機後再開）：http://127.0.0.1:18083  
預設帳號 `admin`；密碼請用環境變數 `EMQX_DASHBOARD_PASSWORD` 覆寫，不要用預設 `public`。

```bash
# 停止
docker compose down
```

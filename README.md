# Tego MQTT Broker

發酵設備用的 **EMQX** Broker（Docker）。與 `tego_backend` 的
`run_ferment_mqtt_subscriber` **同機跑在 VM**（不上 Cloud Run）。

- **映像**：`emqx/emqx:5.8.3`
- **MQTT**：`1883`
- **主題**：`/device/ferment`（設備與 backend subscriber 使用）
- **Dashboard**：僅綁本機 `127.0.0.1:18083`

## 部署切分

| 元件 | 位置 |
|------|------|
| EMQX（本倉庫） | VM：`docker compose up -d` |
| `run_ferment_mqtt_subscriber` | 同 VM：systemd（見 [tego_backend/deploy/vm](https://github.com/tegoyuhong-sys/tego_backend/tree/main/deploy/vm)） |
| Django HTTP / Next.js | Cloud Run |

```
設備 ──MQTT──► EMQX (本機 :1883)
                  │
                  ▼
         ferment subscriber (tego_backend on VM)
                  │
                  ▼
              Cloud SQL
```

## 啟動

```bash
docker compose up -d
```

MQTT：`mqtt://<host>:1883`  
同機 subscriber 請設 `MQTT_BROKER_HOST=127.0.0.1`。  
Dashboard（需 SSH 連到主機後再開）：http://127.0.0.1:18083  
預設帳號 `admin`；密碼請用環境變數 `EMQX_DASHBOARD_PASSWORD` 覆寫，不要用預設 `public`。

```bash
# 停止
docker compose down
```

開機自動：可 `docker update --restart unless-stopped tego_emqx`，或另加 systemd 包一層 `docker compose up -d`（見 `deploy/vm/`）。

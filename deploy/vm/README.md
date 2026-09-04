# VM：EMQX + ferment subscriber

本目錄只負責 **Broker**。寫入 DB 的 Django subscriber 在
`tego_backend/deploy/vm/`。

## 建議順序

1. 安裝本單元（EMQX）
2. 確認 `docker compose ps` / port `1883`
3. 再啟 `tego-mqtt-subscriber`（backend 倉庫）

```bash
sudo cp /home/tegoyuhong/mywork/tego_mqtt/deploy/vm/tego-emqx.service \
  /etc/systemd/system/tego-emqx.service
sudo systemctl daemon-reload
sudo systemctl enable --now tego-emqx
docker compose -f /home/tegoyuhong/mywork/tego_mqtt/docker-compose.yml ps
```

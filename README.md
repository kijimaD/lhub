複数のLAN用アプリケーションをKubernetesクラスターで一元管理する。

## クラスター作成

```bash
k3d cluster create lhub \
  --registry-create lhub-registry \
  -p "80:80@loadbalancer" \
  --volume ~/Project/or:/mnt/Project/or@server:0 \
  --volume ~/Project/srd:/mnt/Project/srd@server:0 \
  --volume ~/Public/q/public:/mnt/Public/q/public@server:0 \
  --volume ~/roam/public:/mnt/roam/public@server:0 \
  --volume /run/user/1000/emacs:/run/user/1000/emacs@server:0
```

## 起動

```bash
tilt up
```

Tilt UI: http://localhost:10350

## 停止

```bash
tilt down
```

## クラスター削除

```bash
k3d cluster delete lhub
```

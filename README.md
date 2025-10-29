# lhub - ローカル開発環境管理

複数のアプリケーションをKubernetesクラスターで一元管理する開発環境。

## 構成

- **k3d**: ローカルKubernetesクラスター
- **Tilt**: 自動ビルド・デプロイツール
- **Ingress**: ドメインベースルーティング

## クラスター作成

```bash
k3d cluster create dev \
  --port "80:80@loadbalancer" \
  --volume /home/violet/Project:/mnt/Project@server:0 \
  --volume /home/violet/Public:/mnt/Public@server:0 \
  --volume /home/violet/roam:/mnt/roam@server:0
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
k3d cluster delete dev
```

## 新しいアプリの追加

1. `k8s/新アプリ.yaml` を作成（Deployment + Service）
2. `Tiltfile` にビルド設定を追加
3. `k8s/ingress.yaml` にドメインルールを追加
4. Tiltが自動的に変更を検知してデプロイ

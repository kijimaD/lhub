# k3dクラスターを許可
allow_k8s_contexts('k3d-dev')

# k3dレジストリのアドレス
default_registry('localhost:5555')

# or-server
docker_build(
  'k3d-dev-registry:5000/or-server',
  '../or',
  target='app',
)

# srd-server
docker_build(
  'k3d-dev-registry:5000/srd-server',
  '../srd',
)

# opv-server
docker_build(
  'k3d-dev-registry:5000/opv-server',
  '../opv',
  target='app',
)

# Kubernetesマニフェストを適用
k8s_yaml([
        'k8s/or.yaml',
        'k8s/srd.yaml',
        'k8s/opv.yaml',
        'k8s/q.yaml',
        'k8s/mypdfs.yaml',
        'k8s/ingress.yaml',
        ])

# リソース定義（ブラウザUIでの表示用）
k8s_resource('or-server', port_forwards='0.0.0.0:8008:3000', labels=['apps'])
k8s_resource('srd-server', port_forwards='0.0.0.0:8013:8000', labels=['apps'])
k8s_resource('opv-server', port_forwards='0.0.0.0:8007:8007', labels=['apps'])
k8s_resource('q-server', port_forwards='0.0.0.0:8014:8000', labels=['apps'])
k8s_resource('mypdfs-server', port_forwards='0.0.0.0:8015:8000', labels=['apps'])
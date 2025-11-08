# k3dクラスターを許可
allow_k8s_contexts('k3d-lhub')

# k3dレジストリのアドレス
default_registry('localhost:5555')

# or-server
docker_build(
  'k3d-lhub-registry:5000/or-server',
  '../or',
  target='app',
)

# srd-server
docker_build(
  'k3d-lhub-registry:5000/srd-server',
  '../srd',
)

# opv-server
docker_build(
  'k3d-lhub-registry:5000/opv-server',
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
        'k8s/roam.yaml',
        'k8s/ingress.yaml',
        ])

# リソース定義（ブラウザUIでの表示用）
k8s_resource('or-server', links=['http://or.lan'], labels=['apps'])
k8s_resource('srd-server', links=['http://srd.lan'], labels=['apps'])
k8s_resource('opv-server', links=['http://opv.lan'], labels=['apps'])
k8s_resource('q-server', links=['http://q.lan'], labels=['apps'])
k8s_resource('mypdfs-server', links=['http://mypdfs.lan'], labels=['apps'])
k8s_resource('roam-server', links=['http://roam.lan'], labels=['apps'])
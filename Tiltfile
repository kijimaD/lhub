# k3dクラスターを許可
allow_k8s_contexts('k3d-dev')

# or-server
custom_build(
  'or-server',
  'cd /home/violet/Project/or && docker build -t $EXPECTED_REF --target app . && k3d image import -c dev $EXPECTED_REF',
  ['/home/violet/Project/or'],
  skips_local_docker=True,
)

# srd-server
custom_build(
  'srd-server',
  'cd /home/violet/Project/srd && docker build -t $EXPECTED_REF . && k3d image import -c dev $EXPECTED_REF',
  ['/home/violet/Project/srd'],
  skips_local_docker=True,
)

# Kubernetesマニフェストを適用
k8s_yaml(['k8s/or.yaml', 'k8s/srd.yaml', 'k8s/ingress.yaml'])

# リソース定義（ブラウザUIでの表示用）
# srd-serverはor-serverの後にビルド（k3d-tools競合回避）
k8s_resource('or-server', port_forwards='8008:3000', labels=['apps'])
k8s_resource('srd-server', port_forwards='8013:8000', labels=['apps'], resource_deps=['or-server'])

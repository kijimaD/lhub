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
k8s_yaml([
        'k8s/or.yaml',
        'k8s/srd.yaml',
        'k8s/q.yaml',
        'k8s/mypdfs.yaml',
        'k8s/ingress.yaml',
        ])

# リソース定義（ブラウザUIでの表示用）
# FIXME: k3d-tools競合回避するのでdepsをつけている...
k8s_resource('or-server', labels=['apps'], links=['http://or.localhost'])
k8s_resource('srd-server', labels=['apps'], resource_deps=['or-server'], links=['http://srd.localhost'])
k8s_resource('q-server', labels=['apps'], resource_deps=['srd-server'], links=['http://q.localhost'])
k8s_resource('mypdfs-server', labels=['apps'], resource_deps=['q-server'], links=['http://mypdfs.localhost'])
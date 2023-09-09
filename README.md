# rook-ceph-playground

Kustomize を使用して Rook/Ceph をデプロイする。[参考](https://rook.io/docs/rook/latest/Getting-Started/quickstart/#deploy-the-rook-operator)

**※ 3 ノード以上の ベアメタル Kubernetes クラスタが構築済みであるとします。**

## Requirement

```shell
### kubectl / kustomize コマンドが使用できることを確認
$ kubectl version -o yaml
clientVersion:
  buildDate: "2022-10-12T10:57:26Z"
  compiler: gc
  gitCommit: 434bfd82814af038ad94d62ebe59b133fcb50506
  gitTreeState: clean
  gitVersion: v1.25.3
  goVersion: go1.19.2
  major: "1"
  minor: "25"
  platform: darwin/amd64
kustomizeVersion: v4.5.7
serverVersion:
  buildDate: "2022-10-12T10:49:09Z"
  compiler: gc
  gitCommit: 434bfd82814af038ad94d62ebe59b133fcb50506
  gitTreeState: clean
  gitVersion: v1.25.3
  goVersion: go1.19.2
  major: "1"
  minor: "25"
  platform: linux/amd64
```

## Usage

### 1. Rook/Ceph

```shell
$ cd ./rook-ceph

### rook-ceph という Namespace を準備する
$ kubectl create namespace rook-ceph

### Rook/Ceph のデプロイ
$ kustomize build ./base | kubectl apply -f -

### Tool Boxのデプロイ（必要に応じて）
$ kubectl apply -f ./base/toolbox.yaml -n rook-ceph
```

### 2. MinIO Operator

```shell
$ cd ./minio/operator

### minio-operator という Namespace を準備する
$ kubectl create namespace minio-operator

### MinIO Operator のデプロイ
$ kustomize build ./base  | kubectl apply -f -
```

### 3. MinIO Tenant

```shell
$ cd ./minio/tetant

### minio-tenant-sample-bucket-provider という Namespace を準備する
$ kubectl create namespace minio-tenant-sample-bucket-provider

### MinIO Tenant のデプロイ
$ kustomize build ./base  | kubectl apply -f -
```

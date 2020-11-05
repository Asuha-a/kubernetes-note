# INSTALL.md

## ssh EC2 Instance

sshでEC2につなぐ

```terminal
ssh -i pemファイルのパス ec2-user@パブリックIPアドレス
```

## Install AWS CLI

```terminal
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

## Install kops

kopsの最新バージョンをダウンロードする

```terminal
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
```

こんなのが出る

```terminal
$ curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   640  100   640    0     0   2154      0 --:--:-- --:--:-- --:--:--  2154
100 93.9M  100 93.9M    0     0  7222k      0  0:00:13  0:00:13 --:--:-- 9431k
```

lsを実行するとダウンロードに成功していることがわかる

```terminal
$ ls
kops-linux-amd64
```

権限変更

```terminal
chmod +x kops-linux-amd64
```

PATHに　インストールしたファイルを移動

```terminal
sudo mv kops-linux-amd64 /usr/local/bin/kops
```

## S3バケットの作成

S3バケットにkopsで必要な各情報を保存していくのでバケットを作成

その後環境変数に作成したS3バケットのARNを設定

```terminal
export KOPS_STATE_STORE=arn:aws:s3:::kops-test-asuha
```

## クラスタの構築

```terminal
kops create cluster --zones=ap-northeast-1a ec2-3-112-173-190.ap-northeast-1.compute.amazonaws.com
```

## References

[SSH を使用した Linux インスタンスへの接続](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
[Installing, updating, and uninstalling the AWS CLI version 2 on Linux](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html)
[kopsを使ったAWS上でのKubernetesのインストール](https://kubernetes.io/ja/docs/setup/production-environment/tools/kops/)

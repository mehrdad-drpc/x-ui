# x-ui

xray panel that supports multi-protocol and multi-user

# Features

- System status monitoring
- Support multi-user and multi-protocol, web page visualization operation
- Supported protocols: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Support to configure more transport configurations
- Traffic statistics, limit traffic, limit expiration time
- Customizable xray configuration templates
- Support https access panel (self-provided domain name + ssl certificate)
- Support one-click SSL certificate application and automatic renewal
- For more advanced configuration items, see the panel for details

# Install & Upgrade

```shell
bash <(curl -Ls https://raw.githubusercontent.com/mehrdad-drpc/x-ui/main/install.sh)
```
You can read [this doc](https://seakfind.github.io/2021/10/10/X-UI/) for more info

## Manual installation & upgrade

1. First download the latest compressed package from https://github.com/vaxilu/x-ui/releases, generally choose `amd64` architecture
2. Then upload the compressed package to the `/root/` directory of the server, and use the `root` user to log in to the server

> If your server cpu architecture is not `amd64`, replace `amd64` in the command with other architectures

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Install using docker

> This docker tutorial and docker images are provided by [Chasing66](https://github.com/Chasing66)

1. Install docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Install x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
     -v $PWD/db/:/etc/x-ui/ \
     -v $PWD/cert/:/root/cert/ \
     --name x-ui --restart=unless-stopped\
     enwaiax/x-ui:latest
```

> Build your own image

```shell
docker build -t x-ui .
```

## SSL certificate application

> This function and tutorial are provided by [FranzKafkaYu](https://github.com/FranzKafkaYu)

The script has a built-in SSL certificate application function. To use this script to apply for a certificate, the following conditions must be met:

- Know the Cloudflare registered email address
- Know Cloudflare Global API Key
- The domain name has been resolved to the current server through cloudflare

How to get Cloudflare Global API Key:
     ![](media/bda84fbc2ede834deaba1c173a932223.png)
     ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

When using it, you only need to enter `domain name`, `email`, `API KEY`, the schematic diagram is as follows:
         ![](media/2022-04-04_141259.png)

Precautions:

- The script uses the DNS API for certificate requests
- Use Let'sEncrypt as the CA party by default
- The certificate installation directory is the /root/cert directory
- The certificates applied for by this script are all wild domain name certificates



## Migrating from v2-ui

```
x-ui v2-ui
```

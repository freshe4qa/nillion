<p align="center">
  <img height="100" height="auto" src="https://github.com/user-attachments/assets/780f9997-429f-4feb-9626-7e0b5162e59a">
</p>

# Nillion Testnet — Verifier

Official documentation:
>- [Validator setup instructions](https://verifier.nillion.com/verifier)

Explorer:
>- [Explorer](https://testnet.nillion.explorers.guru)

### Minimum Hardware Requirements
 - 4x CPUs; the faster clock speed the better
 - 8GB RAM
 - 100GB of storage (SSD or NVME)

### Recommended Hardware Requirements 
 - 8x CPUs; the faster clock speed the better
 - 16GB RAM
 - 1TB of storage (SSD or NVME)

Устанавливаем Verifier:

```
sudo apt update && sudo apt upgrade -y
```

```
apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev lz4 -y
```

```
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```
docker pull nillion/retailtoken-accuser:v1.0.0
```

```
mkdir -p nillion/accuser
```

```
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```

Далее вы увидите в консоли AccountID и PublicKey. Переходим на [сайт](https://verifier.nillion.com/verifier) и во вкладке Initialising the accuser вставляем наши значения. Далее подтверждаем транзакцию в кошельке.

Пополняем AccountID адрес токенами через [кран](https://faucet.testnet.nillion.com/).

Как только пройдет 1ч выполняем данную команду:

```
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "http://51.89.195.146:26657" --block-start 5024984
```





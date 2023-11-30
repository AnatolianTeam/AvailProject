# Avail Project Testnet Light Client Node Guide

![Avail-GitHub](https://github.com/AnatolianTeam/AvailProject/assets/102043225/b563145a-153b-4a1b-9e4c-54ebb58f305c)
Light Client Interest Form: https://docs.google.com/forms/d/e/1FAIpQLSeL6aXqz6vBbYEgD1cZKaQ4vwbN2o3Rxys-wKTuKySVR-oS8g/viewform 

## Links
 ✔️ [Website](https://www.availproject.org/)<br>
 ✔️ [Explorer](https://goldberg.avail.tools/#/explorer)<br>
 ✔️ [Telemetry](https://telemetry.avail.tools/#list/0x6f09966420b2608d1947ccfb0f2a362450d1fc7fd902c29b67c906eaa965a7ae)<br>
 ✔️ [Doküman](https://docs.availproject.org/)<br>
 ✔️ [GitHub](https://github.com/availproject)<br>
 ✔️ [Discord](https://discord.gg/TUVbtZMMpz)<br>

## Requirements 
| Component | Minimum | **Recommended** | 
| ------------ | ------------ | ------------ |
| CPU (amd64/x86 architecture) |	2 | 4 |
| RAM	| 4 GB | 8 GB |
| Storage (SSD)	| 20-40 GB | 200-300 GB  |

## Updating the system
```shell
apt update && apt upgrade -y
```

## Installing Necessary Packages
```shell
sudo apt install make clang pkg-config libssl-dev build-essential git screen protobuf-compiler -y
```

## Installing and Update Rust
```shell
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

## Installing Avail Light Client

```shell
git clone https://github.com/availproject/avail-light.git
cd avail-light
git checkout v1.7.4
cargo build --release
```

# Creating Service File
```shell
tee sudo nano /etc/systemd/system/availightd.service > /dev/null << EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart= /root/avail-light/target/release/avail-light --network goldberg
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
EOF
```

## Start Service
```shell
systemctl daemon-reload
systemctl enable availightd.service
systemctl start availightd.service
systemctl status availightd.service
```

* Servis dosyamız çalışıyorsa buradan CTRL C yapıp çıkıyoruz.

## Check Logs
```
journalctl -f -u availightd
```
OR
```
journalctl -u availightd -fo cat
```


# Follow Us:

[Website](https://anatolianteam.com)

[Twitter](https://twitter.com/anatolianteam)

[Medium](https://medium.com/@anatolianteam)

[YouTube](https://www.youtube.com/@anatolianteam)

[Telegram Duyuru](https://t.me/AnatolianTeamduyuru)

[Telegram Sohbet](https://t.me/AnatolianTeam)

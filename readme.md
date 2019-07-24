# DDoS-Amplification

[base repo](https://github.com/THSamurai/DDoS-Amplification)

## Attention

- 元のツールにパケット送信数を指定できるようにしたものです。
  - `-Count` オプション
- 仕様(コード)の変更により **D**DoS ではなくなりました
  - `deny()` を使う攻撃に影響があります

### previous

- `^C` で終了する他なかった (最後に `while: True`)
- 1スレッドにつき1ホストを攻撃対象として、 `-Thread` にて渡した数だけループ
  - `while: True` がないと攻撃対象リストとして渡したテキストを全て読み込まずにプログラムが終わる
- `deny()` 内部の `send(packet, loop=1)` によりパケットは無限に送られる

### changing

- `-Count` オプションを導入した
- 1スレッドにて攻撃対象全てに `-Count` オプションで指定した回数だけパケットを送る
- スレッドのデーモン化を削除 (`deny()` のみ)

## Usage

```sh
sudo python DDoS.py -A 3 -T xxx.xxx.xxx.xxx -F target.txt -Thread 1 -Count 10
```

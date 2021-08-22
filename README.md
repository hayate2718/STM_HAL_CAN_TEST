# STM_HAL_CAN_TEST
<b>HALを用いたCAN通信のテスト用プログラム(STM32F303K8)</b><br>
can通信のループバックモードを用いることでトランシーバを用いずに単体で通信のテストを行う<br>
ヌクレオボードを用いることで1sごとにメッセージを送信し、ループバックで受信したIDとデータを割り込みで読みこみLEDを点滅させることで視覚的に動作の確認ができる。<br>
※ヌクレオのLEDはPB3(D13)ピンがつながっている。<br>

|peripheral|pin|
|---|---|
|canrx|PA11(D10)|
|cantx|PA12(D2)|
|gpio|PB3(D13)|

## MX設定
|config|parameter|
|---|---|
|prescaler|4|
|TQB1|5|
|TQB2|2|
|RSJ|1|
|BaudRate|1Mbps|
|TTC|0|
|ABusOffM|1|
|AWakeUpM|1|
|ARetransission|1|
|RFL|0|
|TFP|0|
|OperatingM|loopback|

## コード注意
割り込みの優先順位を特に設定していないことにより、HAL_Delay()関数とメッセージ読みこみの割り込みコールバック関数と干渉するため、time_f変数によって無理やり干渉しないようにしている。

# DC/DC Convertor
## TPSM13604HNDWR

### Typical Application
#### $R_{ENT}, R_{ENB}$
EN ピンの電圧が 1.18 V より大きいか小さいかで DC/DC コンバータの有効無効が決まる。

V_IN を分圧して、V_IN の電圧が規定値を下回った時に、EN ピンが 1.18 V を下回るように分圧抵抗を決める。

DC/DC コンバータが有効になる条件式

$$\frac{R_{ENB}}{R_{ENT} + R_{ENB}} \times V_{IN} \ge 1.18 [V]$$

#### $R_{FBT}, R_{FBB}$
FB ピンの電圧が 0.8 V より大きいか小さいかで DC/DC コンバータのパルス出力を有効にするか無効にするかが決まる。

V_OUT を分圧して、V_OUT の電圧が規定値を下回った時に、FB ピンが 0.8 V を下回るように分圧抵抗を決める。

出力電圧の式

$$\frac{R_{FBB}}{R_{FBT} + R_{FBB}} \times V_{OUT} = 0.8 [V]$$

出力電圧を 5 V にしたいときは $V_{OUT}$ を 5 V にする。

尚、これらの抵抗 $R_{FBT}, R_{FBB}$ の値は 1k ~ 50k $\Omega$ の範囲で選択する必要がある。

#### $C_{SS}$
推奨値 : 4700 pF

出力電圧が安定するまでの時間 $t_{SS}$ に関わる。

この時間は、早すぎると出力電圧がオーバーシュートし、遅すぎると目的の出力電圧を得るのに時間がかかってしまう。

$$t_{SS} = 0.8 [V] \times \frac{C_{SS}}{0.8 [\mu A]}$$

という式で求めることが可能だが、$t_{SS}= 0 .5 [ms]$ が推奨値とされているため、$C_{{SS}} = 4700 [pF]$ が推奨とされる。

#### $C_{OUT}$
推奨コンデンサ : セラミックコンデンサ or ポリマー電解コンデンサ

$$C_{OUT} \ge I_{STEP} \times V_{FB} \times L \times \frac{V_{IN}}{4 \times V_{OUT} \times (V_{IN} - V_{OUT}) \times V_{OUT-TRAN}}$$

ここで、

- $V_{FB}$ は FB ピンの閾値 0.8 V
- $L$ はインダクタのリアクタンス 10 $\mu H$
- $V_{OUT-TRAN}$ はなんだよこれ 例として $V_{OUT-TRAN} = 50 [mV]$ になってる
- $I_{STEP}$ はおそらく最大出力電流 DC/DC  の最大出力電流が 4 A であるためこれ以下にする
- $V_{IN}, V_{OUT}$ はそれぞれ入力電圧と出力電圧

これらによって $C_{OUT}$ の最小値が決定される。

この条件を満たしたうえで、低 ESR のコンデンサを設定する。

この ESR の最大値も計算式が用意されているがよくわからん。

#### $R_{ON}$
スイッチング周波数を決定する抵抗。

以下の式でスイッチング周波数 $f_{SW(CCM)}$ が決定される。

$$f_{SW(CCM)} \approxeq \frac{V_{OUT}}{(1.3\times10^{-10}\times R_{ON}}$$

#### $C_{IN}$
$$C_{IN} \geq \frac{I_{OUT} \times D \times ( 1 - D)}{f_{SW-CCM} \times \Delta{V_{IN}}}$$
$$D \approxeq \frac{V_{OUT}}{V_{IN}}$$


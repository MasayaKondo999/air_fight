
2024年2月27日
observableから各MWSコンタクトのtruthが得られるため、各MWSコンタクトは誤りなく個体識別が可能です。よって、MWSコンタクトのtruthをリストに入れて管理し、最初にMWSコンタクトがあったタイミングからの経過時間等を管理しています。

また相手のミサイルは最大8発とわかっているため、今までにMWSコンタクトのあったtruthの数を数えると、相手の撃った数をカウントできます。相手が8発撃ちきったと判定したら、クランク等の回避起動を行わず相手を相手にまっすぐ突っ込んでいくモードに入ります。

尚、truthによるミサイルのカウント自体は第1回および第2回空戦AIチャレンジでも可能でしたが、中距離戦ではMWS圏内に入るまでに外れるミサイルが多かったため、あまり有効に働きませんでした。短距離戦となった結果殆のミサイルがMWS圏内に入るようになり、有効に働くようになりました。

MWSは僚機に撃たれたミサイルにも反応します。この仕様は普通に実装していると、1発のミサイルで2機とも回避起動を強要されたりして厄介なのですが、悪用すれば有効活用することも可能です。

2機で同じミサイルを検出した場合、2機からの方向がわかります。それらの交点を求めるとミサイルの位置がわかります。2フレーム連続して位置がわかればミサイルの速度もわかります。
尚、同じミサイルを検出しているかどうかは前述の通りtruthから判定可能です。

空戦AIのミサイルは比例航法で飛ぶため、自機宛のミサイルは、自機およびミサイルの進行方向に直線を引くと前方のどこかで交わります。逆に言うと、交点が自機の後ろの場合、ミサイルの後ろの場合、それらの直線が一定以上離れている場合は自分宛のミサイルではないと判定し無視できます

以上のようにOUT時間を最小限にし、積極的に攻撃するエージェントを作成することで600勝を達成することができました。

目標の選択は「自機から最も近い目標を選択する。ただし、味方機2機が同一目標を選択しており、かつその目標を場外まで押し出す前にもう1機の敵と接敵が予想される場合は、1機はそちらを対処する」というルールとしています。

ただしこれは恐らく最適な方法ではなく、実際の対戦を見ていると不合理な動きとなっているケースも多いです。

ちなみにターゲティングを簡易的な強化学習により学習させることも試みましたが、「学習開始時よりは動きがよく、たまに凄く綺麗な動きも見せるが全体としてはルールベース程は強くない」止まりでした。強化学習によるターゲティングは実装しましたが不採用となっています。

強化学習によるターゲティングは、「眼の前の敵を追いかけ続ければ勝っていたところを、突然放置して遠くの敵に向かっていく」といった現象が頻発していました。

恐らく、「眼の前の敵に必中圏内で撃って次のターゲットに行く」という正解行動に対し、ミサイルを撃っていることが重要、という要素が学習できなかったのだと思います。

今回のコンペのルールとして、短距離戦ではミサイル射撃司令から実際に発射されるまでの3秒の影響が大きかったです。すぐに撃ち返して逃げたいが3秒待たないといけない、3秒待っている間に敵とすれ違っている、等。

3秒間は人間による射撃許可の模擬とのことですが、例えば指定した目標には好きなタイミングで撃てる射撃許可を与える等、エージェントが撃ちたいタイミングでタイムラグなく撃てるようにした方が強い機体になると思います。

以上、空戦AIのこと好き好きクラブのみなさんによる第3回空戦AIチャレンジ解法解説でした
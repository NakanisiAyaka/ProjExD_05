# ゲーム のタイトル
Banging Splash
## 実行環境の必要条件
* python >= 3.10
* pygame >= 2.1

## ゲームの概要
プレイヤーは画面下部に配置されています。プレイヤーは左右に移動し、スペースキーを押すことで弾を発射できます。
敵は画面上部からランダムに出現し、左右に移動します。プレイヤーが弾を当てると、新しい敵がランダムな位置に再出現します。
ゲームの目標は、できるだけ多くの敵を倒してスコアを稼ぐことです。

## ゲームの実装
操作方法:
左矢印キー: プレイヤーを左に移動
右矢印キー: プレイヤーを右に移動
スペースキー: 弾を発射
左シフトキー: スコアを消費してバリアを生成
右シフトキー: スコアを消費して散弾銃モード

要素:4
プレイヤー（playerImg）: 左右に移動できる宇宙船。
敵（enemyImg）: 画面上部から左右に移動する敵宇宙船。
弾（bulletImg）: プレイヤーと敵が発射する弾。
バリア（shield）: プレイヤーが生成するバリア


得点:
敵宇宙船を倒すごとに、得点が加算されます。得点は画面左上に表示されます。

注意点:
敵宇宙船が放つ弾がプレイヤーに当たると、ゲームが終了します。

コードの構造:
Pygameライブラリを使用してウィンドウを作成し、ゲームのメインループを実装しています。
イベントハンドリングを使用して、キーボードの入力に応じてプレイヤーの動きや弾の発射を制御しています。
isCollision 関数は、弾と敵の衝突を検出しています。
スコアは画面左上に表示され、敵を倒すと増加します。

クリア条件:
敵が放つ弾に当たらずプレイヤーは敵を打ち落とし最高点を目指す

参考サイト:
https://www.youtube.com/watch?v=fAJ_BjLd3Ro

###共通基本機能
* 主人公キャラクターに関するクラス
方向キーで左右に移動
スペースキーで弾の放出
* 敵に関するクラス
ランダムのスピードで左右に移動一定の時間ごとに弾の放出

### 担当追加機能
* 伊藤
ゲージをある量使用して発生させるバリア生成機能
### ToDo
- [ ] バリア機能
- [ ] 弾の無効化機能

### メモ
シールドの状態や描画は、shield_state変数で管理されています。shield_stateが 'ready' のときはシールドが非アクティブで、'active' のときはシールドがアクティブです。

キー入力（'S'キー）によってシールドをアクティブにする処理があります。具体的には、キーが押されたとき（pygame.KEYDOWN イベント）、'S'キーが押された場合、shield_stateを 'active' に設定し、shieldXおよびshieldYをプレイヤーの位置に設定しています。

シールドがアクティブの場合、draw_shield関数が呼び出されて、シールドが描画されます。この関数は指定された位置 (x + 33, y) に半径 shield_radius の円を描画します。

敵がプレイヤーのシールドに当たったかどうかの判定は、isCollision関数で行われています。この関数は、円と円の衝突判定を行います。具体的には、isCollision(enemyX, enemyY, playerX, playerY, shield_radius, 32)のように呼び出されています。もしシールドがアクティブでかつ敵との衝突が検出されれば、shield_stateを 'ready' に設定し、新しい敵の位置をランダムに設定しています。

これにより、プレイヤーが 'S' キーを押すことでシールドをアクティブにし、敵の攻撃を防ぐことができるようになります。

今日は、ほかの人のゲージ生成と敵の弾が放出されて当たるコードをマージしていない
とりあえずシールドを生成して敵が自分に当たったら無効化されるコードの作成をした
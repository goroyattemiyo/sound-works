# PHASE 1 - Player Foundation

## 目的

SOUND WORKS の再生専用プレイヤーを完成させる。

## ゴール

songs/*.json を読み込み、曲を選択して、チップチューン風に再生できる状態にする。

## 実装対象

- LP/UI
- AudioContext 初期化
- square波テスト音
- songs/*.json 読み込み
- 曲一覧表示
- currentSong 保持
- 選択曲再生
- Play / Stop
- Loop
- gateTime
- Step Grid 可視化
- step選択状態

## 完了条件

- 曲一覧が表示される
- 曲を選択できる
- 曲のメタ情報が表示される
- Playで1回再生できる
- Stopで停止できる
- Loop Onで繰り返し再生できる
- Step Gridで現在位置が見える
- stepをクリックして選択できる
- 外部ライブラリなし
- index.htmlのみで動作する

## 注意点

- まだ本格的な編集機能は入れない
- まだ3音構成にはしない
- まずは1トラックの再生を安定させる

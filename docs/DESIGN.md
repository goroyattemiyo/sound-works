# SOUND WORKS DESIGN

## 概要

SOUND WORKS は、昔のガラケーの3音着メロ作成のように、手打ちで曲を作れるWebアプリです。

チップチューン風の音色で、メロディ、ベース、リズムを組み合わせ、ブラウザだけで作曲・再生・保存できることを目指します。

## コンセプト

- 昔のガラケー着メロ作成のような手打ち作曲体験
- 3音構成を基本にする
  - Melody
  - Bass
  - Rhythm
- チップチューン風
- 単一HTMLで完結
- 外部ライブラリなし
- Web Audio APIのみ使用
- songs/*.json で曲データを管理

## ターゲット体験

ユーザーは曲を選び、ステップを見ながら再生できます。
将来的には、stepを直接編集して、自分だけの短いチップチューン曲を作れるようにします。

目標は「難しいDAW」ではなく、「昔の携帯でポチポチ曲を打ち込む楽しさ」です。

## 現在の実装状況

- LP/UI
- AudioContext 初期化
- square波テスト音
- songs/*.json 読み込み
- 曲一覧表示
- currentSong 保持
- 選択曲の再生
- Play / Stop
- Loop
- gateTime
- Step Grid 可視化
- step選択状態

## データ構造

現在の曲データは、songs/*.json に保存します。

基本形:

{
  "title": "Song Title",
  "origin": "Traditional",
  "publicDomainNote": "Public domain melody.",
  "bpm": 120,
  "key": "C",
  "steps": ["C4", "D4", "E4", "REST"]
}

将来的には3音構成に拡張します。

{
  "title": "User Song",
  "bpm": 120,
  "key": "C",
  "tracks": {
    "melody": ["C5", "D5", "E5", "REST"],
    "bass": ["C3", "REST", "G2", "REST"],
    "rhythm": ["KICK", "REST", "SNARE", "REST"]
  }
}

## UI構成

- Hero / LP
- Start ボタン
- Song List
- Song Detail
- Play / Stop
- Loop
- Step Grid
- 将来: Compose Mode
- 将来: Track Editor
- 将来: Export / Import

## 音源設計

基本音源は Web Audio API の OscillatorNode を使います。

初期方針:

- square波中心
- GainNode で音量制御
- gateTime で音の切れ目を作る
- REST は無音
- 外部音源ファイルは使わない

将来的な拡張:

- waveform切替
- simple envelope
- melody / bass / rhythm の音色分離
- noise系リズム音

## 3音構成の将来設計

昔のガラケー着メロのように、同時に鳴らせる音を限定します。

基本構成:

1. Melody
2. Bass
3. Rhythm

制約があることで、シンプルで分かりやすい作曲体験にします。

## 作曲モード設計

作曲モードでは、Step Grid を編集可能にします。

予定機能:

- step選択
- note変更
- REST切替
- BPM変更
- key表示
- localStorage保存
- JSON export
- JSON import

最初は1トラックの編集から始め、後で3トラックに拡張します。

## 制約

- 単一HTML
- 外部ライブラリ禁止
- バニラJavaScriptのみ
- Web Audio APIのみ
- index.html を本体とする
- songs/*.json は曲データ置き場
- 小さな差分で実装する

## 今後の拡張方針

1. 再生プレイヤーを安定化
2. Step Gridを編集可能にする
3. 作曲モードを追加
4. localStorage保存
5. JSON export/import
6. 3音構成へ拡張
7. ユーザー曲管理

## 理想の作曲入力方式

SOUND WORKS の作曲モードは、最終的に「固定Stepを直接塗るDAW風」ではなく、昔のガラケー着メロ作成に近い入力体験を目指す。

理想形は、楽譜を見ながら1音ずつ以下を選び、順番に登録していく方式。

- 音価
  - 16分音符
  - 8分音符
  - 4分音符
  - 2分音符
  - 全音符
- 音程
  - C4
  - D4
  - E4
  - F4
  - G4
  - A4
  - B4
  - REST

例:

1. 「8分」+「A4」を選んで追加
2. 「4分」+「C4」を選んで追加
3. 「8分」+「REST」を選んで追加

このように、楽譜の内容を左から右へ入力していくと、1曲が完成する。

## Step Gridとの関係

現在の Step Grid は、再生位置の可視化と簡易編集には有効。

ただし将来的な本命は、固定16stepだけではなく、音符イベントを順番に積み上げる event sequence 方式とする。

現在:

{
  "steps": ["C4", "D4", "REST"]
}

将来:

{
  "events": [
    { "note": "A4", "length": "eighth" },
    { "note": "C4", "length": "quarter" },
    { "note": "REST", "length": "eighth" }
  ]
}

Step Grid は、events を表示用に展開したビューとして扱う。

## 入力体験の方向性

目指すのは複雑なDAWではなく、昔の携帯電話で着メロを手打ちしていたような体験。

- 音価を選ぶ
- 音程を選ぶ
- 追加する
- 1音ずつ並べる
- 再生して確認する
- 間違えた音を戻す/削除する

この「ポチポチ入力する楽しさ」を優先する。


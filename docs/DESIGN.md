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

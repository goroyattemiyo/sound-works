# PHASE 3 - 3 Voice Composer

## 目的

SOUND WORKS を、昔のガラケー3音着メロ作成のような作曲ツールに拡張する。

## ゴール

Melody / Bass / Rhythm の3パートを手打ちで作曲し、JSONとしてexport/importできるようにする。

## 実装対象

- 3トラック構成
- Melody Track
- Bass Track
- Rhythm Track
- Track切替
- Track別 Step Grid
- Track別音色
- JSON export
- JSON import
- ユーザー曲管理
- サンプル曲追加

## 3トラック構成

{
  "title": "My Chiptune",
  "bpm": 120,
  "key": "C",
  "tracks": {
    "melody": ["C5", "D5", "E5", "REST"],
    "bass": ["C3", "REST", "G2", "REST"],
    "rhythm": ["KICK", "REST", "SNARE", "REST"]
  }
}

## 音色方針

- Melody: square wave
- Bass: triangle または square low octave
- Rhythm: noise / short envelope

## Composer UI

- Track Tabs
  - Melody
  - Bass
  - Rhythm
- Step Grid
- Note Selector
- Rhythm Selector
- BPM Editor
- Save
- Export JSON
- Import JSON

## 完了条件

- 3パートを個別に編集できる
- 3パートを同時再生できる
- localStorageに保存できる
- JSONとしてexportできる
- JSONをimportできる
- ユーザー曲を管理できる

## 注意点

- 同時発音数は3音を基本とする
- 複雑なDAWにはしない
- 手打ち着メロ感を優先する
- UIはシンプルに保つ
- 単一HTML構成を維持する

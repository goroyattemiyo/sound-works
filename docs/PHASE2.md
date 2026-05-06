# PHASE 2 - Composer Entry

## 目的

作曲モードの入口を作る。

昔のガラケー着メロ作成のように、stepを選んで音を変更できる状態を目指す。

## ゴール

1トラックの step を編集でき、localStorage に保存できるようにする。

## 実装対象

- Compose Mode 切替
- Step Grid 編集
- selectedStepIndex
- note変更
- REST切替
- BPM変更
- editedSong 状態
- localStorage保存
- localStorage読込
- Reset機能
- Preview再生

## 予定UI

- Composer Mode ボタン
- Note Selector
- REST ボタン
- BPM Input
- Save ボタン
- Load ボタン
- Reset ボタン

## データ方針

既存の currentSong を直接壊さず、編集用に editedSong を作る。

編集対象:

{
  "steps": ["C4", "D4", "REST"]
}

## 完了条件

- stepを選択できる
- 選択stepのnoteを変更できる
- RESTに変更できる
- BPMを変更できる
- 編集した曲を再生できる
- localStorageに保存できる
- 再読込後も復元できる

## 注意点

- まだ3音構成にはしない
- 既存の再生機能を壊さない
- songs/*.json は直接変更しない
- export/import はPhase 3で扱う

## 将来構想: 音価 + 音程の順次入力

PHASE 2 の先に、作曲モードは固定Step編集だけでなく、音価と音程を選んで1音ずつ追加する方式へ拡張する。

### 目的

楽譜を見ながら、以下のように入力できるようにする。

- 8分のA4
- 4分のC4
- 8分休符
- 16分のG4

これにより、楽譜の内容を順番に打ち込むだけで曲を作れる。

### UI案

- Length Selector
  - 1/16
  - 1/8
  - 1/4
  - 1/2
  - 1/1
- Note Selector
  - C4
  - D4
  - E4
  - F4
  - G4
  - A4
  - B4
  - REST
- Add Note ボタン
- Delete Last ボタン
- Clear ボタン
- Preview ボタン

### データ案

{
  "title": "My Ringtone",
  "bpm": 120,
  "key": "C",
  "events": [
    { "note": "A4", "length": "eighth" },
    { "note": "C4", "length": "quarter" },
    { "note": "REST", "length": "eighth" }
  ]
}

### 実装方針

最初は既存の steps[] を維持しつつ、events[] を将来構造として追加する。

- steps[] は既存プレイヤー互換用
- events[] は作曲モード本命データ
- events[] から steps[] へ変換する関数を用意する
- 再生エンジンは将来的に events[] 直接再生へ移行する

### 注意点

- いきなり既存 steps[] を廃止しない
- 既存曲 JSON との互換性を壊さない
- まずは1トラックで実装する
- 3音構成はこの入力方式が安定してから行う


---

# Progress Log

## Completed

- AudioContext 初期化
- square wave test tone
- song list loading
- currentSong state
- step playback
- loop playback
- gate time / envelope
- Step Grid visualization
- selected step UI
- note editing
- BPM editing
- localStorage persistence
- JSON Export / Import
- built-in song protection
- New Song creation
- ringtone-style event composer
- events[] + steps[] compatibility layer

## Current State

SOUND WORKS is now functioning as a small retro ringtone composer.

Current workflow:

1. Select built-in song OR create New Song
2. Add notes with:
   - Length
   - Note
3. Playback / Loop
4. Edit BPM
5. Save locally
6. Export JSON
7. Import JSON

## Architecture Direction

Current internal structure:

events[]
↓
steps[] compatibility expansion
↓
playback engine

This allows future expansion without breaking old songs.

## Next Candidates

- Undo
- Measure visualization
- Playback cursor improvements
- Event editing
- Insert event
- Copy/Paste bar
- 3 voice support
- events[] native playback
- MIDI import tools

## Long-Term Goal

Target experience is NOT a modern DAW.

The goal is:

"Old mobile-phone ringtone composer experience"

Users input music one note at a time:

- choose length
- choose note
- add note
- repeat

This should feel playful, lightweight, and retro.


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

# 🎵 SOUND WORKS

Web Audio APIで作るチップチューン楽曲集 + エディター。
単一HTMLファイルで完結、外部ライブラリ・ビルド不要。

## 構成

- index.html — 本体（LP + エディター）
- docs/DESIGN.md — 設計書
- docs/PHASE1〜3.md — 実装フェーズ別指示書
- songs/ — ユーザー作成曲のJSONエクスポート保管用

## 実行方法

index.html をブラウザで開くだけ。
ローカルサーバー不要（localStorage が動く環境であればOK）。

簡易サーバーを使う場合:

python -m http.server 8000

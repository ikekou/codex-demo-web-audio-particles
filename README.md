# codex-demo-web-audio-particles

Codex を試して作った Web Audio + Canvas の音声連動パーティクル（デモ）。

- Demo URL: 後述の GitHub Pages 公開URL（有効化後に利用可能）
- 内容: マイク（拒否時はデモ音源）に反応して粒子が動く単一 `index.html`
- 依存: 外部ライブラリ不要（純粋な Web API のみ）

## 機能
- マイク入力（拒否/未対応時はデモ音源へ自動フォールバック）
- Web Audio の特徴量抽出（音量、低域/中域/高域、ピーク/重心、アタック検出）
- 粒子群のサイズ/速度/色/渦/軌跡が音に連動
- UI: 開始/停止、粒子数、トレイル（残像の長さ）、スクリーンショット保存
- モバイル/デスクトップ両対応、リサイズ時の再計算、DPR 対応

## 使い方
1. `index.html` をブラウザで開く
2. 「開始」を押してマイク権限を許可（拒否でもデモ音が動作）
3. スライダーで粒子数とトレイル（右ほど長く残る）を調整
4. 「スクリーンショット保存」で現在のフレームを PNG 保存

ヒント
- 低域でサイズと中心吸引、中域で速度、高域で渦ときらめきが増加
- アタック時（手拍子等）に発光と動きが強調

## 開発メモ
- 描画: `requestAnimationFrame`
- 構成: 初期化/解析/更新/描画/UI/オーディオ管理の関数を分離
- ハウリング防止のため入力をスピーカーへは流さない

---

English summary

Audio‑reactive particle visualizer built while trying Codex. Single `index.html` with no external libraries. Uses Web Audio API for analysis (RMS, bands, centroid/peak, attack) and Canvas for rendering. Includes start/stop, particle count, trail length, and screenshot. Works on mobile/desktop with resize and DPR handling.

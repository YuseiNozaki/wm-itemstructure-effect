# Working Memory and Item Structure Effect on Visual Search

## 概要
視野外にも及ぶ視覚検索におけるワーキングメモリ使用とオブジェクト配置構造の効果を分析するための心理学実験プログラムです。jsPsych v7を使用して構築されており、Web ブラウザ上で実行できます。

## 実験の目的
この実験は以下の要因が視覚検索タスクに与える影響を調査します：
- **ワーキングメモリ負荷**：有り（4x4グリッドの記憶課題併用）vs. 無し
- **オブジェクト配置構造**：構造化（グリッド配置）vs. 非構造化（ランダム配置）
- **視野条件**：フルスクリーン vs. ウィンドウ操作 vs. スクロール操作

## 実験デザイン
### 実験条件
- **視野条件（3種類）**
  - `fullscreen`: 画面全体表示
  - `window`: 小窓をドラッグして移動
  - `scroll`: 背景をドラッグしてスクロール
- **オブジェクト配置（2種類）**
  - `structured`: グリッド状の規則的配置
  - `unstructured`: ランダム配置
- **ワーキングメモリ負荷（2種類）**
  - `with-memory`: 記憶課題を併用
  - `without-memory`: 視覚検索のみ

### 実験の流れ
1. **練習ブロック**：各視野条件を体験（繰り返し可能）
2. **第1ブロック**：記憶課題なし（60試行）
3. **第2ブロック**：記憶課題あり（60試行）

### 測定指標
- 反応時間（reaction time）
- 正答率（accuracy）
- マウス移動軌跡（mouse trajectory）
- 総移動距離（total movement）
- ドラッグ距離（drag distance）

## 技術仕様
### 動作環境
- **対応OS**: Windows, Mac, Linux
- **必要なソフトウェア**: モダンなWebブラウザ（Chrome, Firefox, Safari, Edge）
- **解像度**: フルスクリーン表示に対応

### 使用技術
- **フレームワーク**: jsPsych v7.x
- **言語**: HTML5, CSS3, JavaScript (ES6+)
- **ライブラリ**: 
  - `@jspsych/plugin-html-keyboard-response`
  - `@jspsych/plugin-canvas-keyboard-response`
  - `@jspsych/plugin-survey-text`
  - `@jspsych/plugin-preload`
  - `@jspsych/plugin-instructions`
  - `@jspsych/plugin-survey-multi-choice`

### 実験パラメータ
```javascript
const params = {
  screenWidth: window.innerWidth,
  screenHeight: window.innerHeight,
  windowWidth: Math.floor(window.innerWidth / 3),
  windowHeight: Math.floor(window.innerHeight / 3),
  numObjects: 30,              // 試行あたりのオブジェクト数
  objectMinSize: 20,           // オブジェクトの最小サイズ
  objectMaxSize: 40,           // オブジェクトの最大サイズ
  targetTolerance: 0.8,        // ターゲット検出の許容範囲
  trialsPerCondition: 10,      // 条件あたりの試行数
  memoryGridSize: 4,           // 記憶課題のグリッドサイズ (4x4)
  memoryPositions: 2           // 記憶すべき位置の数
};
```

## 使用方法
### 基本的な実行方法
1. プロジェクトをローカルにダウンロード
2. Webブラウザで `index.html` を開く
3. 実験を開始

### Cognition.run での実行
プロジェクトはCognition.run プラットフォームでの実行にも対応しています。詳細は `COGNITION_RUN_DEPLOYMENT.md` を参照してください。

## ファイル構成
```
wm-itemstructure-effect/
├── index.html                          # メイン実験ファイル
├── styles.css                          # スタイルシート
├── README.md                           # このファイル
├── LICENSE                             # ライセンス
├── COGNITION_RUN_DEPLOYMENT.md         # Cognition.run用デプロイ手順
├── JSPSYCH_UPGRADE_NOTES.md           # jsPsychアップグレード記録
├── preview_pages/                      # プレビューページ群
│   ├── comprehensive_preview.html     # 包括プレビューページ（説明・結果ページ一括確認）
│   └── ... (その他のプレビューファイル)
├── screen_shots/                       # 実験画面のスクリーンショット
│   ├── 1_target_presentation.png            # ターゲット図形表示例
│   ├── 2_fullscreen.png                    # 全画面条件例
│   ├── 3_window_initial.png          # ウィンドウ条件（初期状態）
│   ├── 4_window_after_move.png          # ウィンドウ条件（移動後）
│   ├── 5_scroll_initial.png          # スクロール条件（初期状態）
│   ├── 6_scroll_after_move.png          # スクロール条件（移動後）
│   ├── 7_memory_task_presentation.png              # 記憶課題の表示例
│   └── 8_memory_task_response.png              # 記憶課題の回答画面
└── tests/                              # テストファイル群
    ├── test_integration.html           # 統合テスト
    ├── test_memory.html                # 記憶課題テスト
    ├── test_fixation.html              # 注視点表示テスト
    ├── test_window_drag.html           # ウィンドウドラッグテスト
    ├── test_scroll_drag.html           # スクロールドラッグテスト
    ├── test_collision_validation.html  # 衝突検出テスト
    ├── test_tolerance_parameter.html   # 許容範囲パラメータテスト
    └── ... (その他のテストファイル)
```

## 特徴的な機能
### 1. 適応的ターゲット検出
ターゲットオブジェクトに対してクリック許容範囲を拡大し、実験参加者の精密なクリック技術ではなく、視覚検索能力そのものを測定。

### 2. 記憶課題統合
4x4グリッド上の色付きセルの位置を記憶し、視覚検索後に再現する二重課題パラダイム。

### 3. 多様な視野条件
- フルスクリーン表示
- 限定された視野窓の操作
- 仮想空間内でのスクロール操作

### 4. 詳細なマウス軌跡記録
参加者の視覚検索戦略を分析するための詳細な行動データを収集。

## 実験参加者への注意事項
- 実験はフルスクリーンモードで実行してください
- 実験中はブラウザの戻るボタンやリロードを避けてください  
- 静かな環境で集中して取り組んでください
- 練習試行で操作方法を十分理解してから本実験に進んでください

## データ出力
実験終了時に以下のデータがJSON形式で出力されます：
- 試行ごとの反応時間と正答率
- 視野条件、配置構造、記憶負荷の組み合わせ
- マウス移動軌跡と総移動距離
- 記憶課題の成績（該当ブロックのみ）
- 参加者の人口統計学的情報

## 開発・テスト
### テストファイル
`tests/` ディレクトリには各機能の動作確認用テストファイルが含まれています：

- **統合テスト**: 実験全体の動作確認
- **機能別テスト**: 記憶課題、視野操作、衝突検出など個別機能のテスト
- **パラメータテスト**: 設定値の調整と動作確認

### プレビューページ
`preview_pages/` ディレクトリには各ページの確認用プレビューファイルが含まれています：

- **包括プレビューページ**: `preview_pages/comprehensive_preview.html`
  - 説明ページ（4パターン）とリザルトページを一括確認
  - 記憶課題先行・後行の初期説明・中間説明、結果表示
  - 実際の実験と同じ画像・レイアウトを使用

**⚠️ 重要：説明ページおよびリザルトページに変更を加える場合は、包括プレビューページ（`comprehensive_preview.html`）も同様に更新してください。**

### jsPsych バージョン管理
プロジェクトはjsPsych v6.3.1からv7.xにアップグレード済みです。詳細な変更内容は `JSPSYCH_UPGRADE_NOTES.md` を参照してください。

## ライセンス
このプロジェクトのライセンス情報については `LICENSE` ファイルを参照してください。

## 研究での利用
この実験プログラムを研究で使用される場合は、適切な引用をお願いします。また、実験パラメータや条件を変更される場合は、研究目的に応じて適切に調整してください。

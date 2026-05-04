# 🏮 local-walk-guide

**GPS連動型まち歩きガイドアプリ**  
スマートフォンのGPSを使い、スポットに近づくと自動で音声ガイドが流れる、まち歩き体験アプリです。  
Googleスプレッドシートでコンテンツを管理し、GitHub Pagesで無料公開できます。

---

> **English Summary**  
> A GPS-triggered walking guide app for local tourism, developed in Masuda Town, Yokote City, Akita, Japan.  
> Audio guides play automatically when visitors approach registered spots.  
> Content is managed via Google Spreadsheets and deployed on GitHub Pages at zero cost.  
> Free to fork and adapt with attribution required. Community support available for tourism organizations — visit Masuda first.  
> See [License](#license) and [Community](#コミュニティサポート) sections for details.

---

## アプリの全体構成

本プロジェクトは3つのアプリで構成されています。

| アプリ | 対象者 | 用途 |
|--------|--------|------|
| **🏮 まち歩きガイド**（本リポジトリ） | 来訪者 | GPS連動でスポットを巡る本体アプリ |
| **🗺️ スポット編集アプリ** | 運営担当者 | スポットの情報・位置を登録・編集（PC用） |
| **📋 フィールド調査アプリ** | 調査担当者 | 現地を歩きながらスポット候補を記録（モバイル用） |

> 各地域・団体は「まち歩きガイド」をURLパラメータで共用し、  
> 編集・調査ツールはPC・スマートフォンで使い分ける運用を想定しています。

---

## 目次

1. [特徴](#特徴)
2. [デモ](#デモ)
3. [クイックスタート](#クイックスタート)
4. [スプレッドシート構成](#スプレッドシート構成)
5. [config設定一覧](#config設定一覧)
6. [音声ガイドについて](#音声ガイドについて)
7. [Google Analytics 4 の設定](#google-analytics-4-の設定)
8. [コミュニティ・サポート](#コミュニティサポート)
9. [クレジット表記について（重要）](#クレジット表記について重要)
10. [ライセンス](#ライセンス)

---

## 特徴

- 📍 **GPS自動到着検知** ── スポットに近づくと自動で音声ガイドを再生
- 🔊 **音声ガイド** ── Google DriveのMP3ファイル、またはブラウザTTS（読み上げ）に対応
- 🗺️ **地図表示** ── Leaflet.js（OpenStreetMap）による現在地・目的地マップ
- 🏅 **プライズ・スタンプ機能** ── コース完走でデジタル修了証・御朱印帳を発行
- ☁️ **Googleアカウント連携** ── 進捗・プライズをGoogle Driveにバックアップ
- 📊 **Google Analytics 4対応** ── 来訪者の動線・スポット到着データを計測可能
- ⚙️ **スプレッドシートで完結** ── HTMLの知識不要でコンテンツ編集・追加が可能
- 🆓 **無料で公開可能** ── GitHub Pages + Googleスプレッドシートのみで運用できる

---

## デモ

**増田まち歩きガイド（秋田県横手市増田町）**  
https://kosa-e-mon.github.io/local-walk-guide/

> 重要伝統的建造物群保存地区「増田の内蔵」を巡るモデルコースです。  
> まずはこのデモを実際に現地で体験してみてください。

---

## クイックスタート

### 🚀 最速スタート（フォーク不要）

**各地域・各団体は、GitHubのフォークやデプロイ作業は不要です。**  
スプレッドシートを準備するだけで、すぐに自分たちのまち歩きアプリが使えます。

### ① スプレッドシートをコピーする

[テンプレートスプレッドシート（増田サンプル）](https://docs.google.com/spreadsheets/d/1fugAECsnEQIHXgQh1qyPOaLJL-6wMuW0B4dA6Ac6k24)を開き、  
「ファイル」→「コピーを作成」でご自身のGoogleアカウントにコピーします。

> **重要：** スプレッドシートにはAPI連携の設定が組み込まれています。  
> コピー後はスプレッドシート内の各設定を貴団体の情報に書き換えてください。  
> シート名・列の順序は変更しないでください。

### ② スプレッドシートを公開設定にする

スプレッドシートの「共有」→「リンクを知っている全員が閲覧可」に設定します。

### ③ スプレッドシートIDを確認する

```
https://docs.google.com/spreadsheets/d/【ここがシートID】/edit
```

### ④ アプリのURLにシートIDを付けて完成

```
https://kosa-e-mon.github.io/local-walk-guide/?sid=【あなたのシートID】
```

このURLをQRコード化して観光パンフレットに掲載するだけで運用開始できます。

---

### フォークして独自デプロイする場合

Google Analytics・Google OAuth を独自設定したい場合など、高度なカスタマイズが必要な場合はフォークしてください。

1. GitHubの「Fork」ボタンでリポジトリをコピー
2. `index.html` をテキストエディタで開き、各種APIキーを設定
3. GitHub Pages で公開（「Settings」→「Pages」→「Branch: main / root」）

> **フォーク時もクレジット表記の維持が必須です。**  
> 詳細は[クレジット表記について](#クレジット表記について重要)を参照してください。

---

## スプレッドシート構成

| シート名 | 内容 |
|----------|------|
| `config` | アプリ全体の設定（タイトル・カラー・距離設定など） |
| `courses` | コース一覧（コース名・距離・所要時間など） |
| `spots` | スポット情報（場所・説明・音声・写真） |
| `course_spots` | コースとスポットの対応関係 |
| `facilities` | 施設情報（トイレ・駐車場など周辺アナウンス） |

### spots シートの主要列

| 列名 | 内容 | 必須 |
|------|------|------|
| `spot_id` | スポットID（英数字） | ✅ |
| `spot_name` | スポット名 | ✅ |
| `lat` / `lng` | 緯度・経度 | ✅ |
| `description` | 説明文（TTSのテキストにも使用） | ✅ |
| `arrive_dist` | 到着判定距離（m）デフォルト15 | |
| `approach_dist` | 接近通知距離（m）デフォルト50 | |
| `audio_arrive_url` | 到着時MP3のGoogle Drive URL | |
| `audio_explain_url` | 解説MP3のGoogle Drive URL | |
| `audio_next_url` | 次スポット誘導MP3のGoogle Drive URL | |
| `photo_url` | 写真のGoogle Drive URL | |
| `keywords` | キーワード（カンマ区切り） | |

---

## config設定一覧

`config` シートは `key` / `value` の縦並び形式です。

### 基本設定

| key | デフォルト | 説明 |
|-----|-----------|------|
| `app_title` | まち歩き | アプリのタイトル |
| `app_subtitle` | コースを選んでください | サブタイトル |
| `area_display` | custom | エリア表示モード（`custom` / `pref+city` / `pref+city+town` など） |
| `area_name` | （空） | エリア名（area_display=custom時） |
| `area_pref` | （空） | 都道府県名 |
| `area_city` | （空） | 市区町村名 |
| `area_town` | （空） | 町・大字名 |
| `prefecture` | （空） | 都道府県（プライズ表示用） |
| `city` | （空） | 市区町村（プライズ表示用） |

### 外観設定

| key | デフォルト | 説明 |
|-----|-----------|------|
| `color_primary` | #B83232 | メインカラー（ボタン・アクセント） |
| `color_bg` | #F4EFE4 | 背景色 |
| `color_paper` | #FAF7F1 | カード背景色 |
| `color_ink` | #1C1A16 | 文字色 |
| `color_gold` | #9A7A3A | ゴールドカラー |
| `font_size_base` | 14px | 基本文字サイズ |
| `font_size_heading` | 20px | 見出し文字サイズ |
| `font_size_explain` | 14px | 解説文字サイズ |
| `header_type` | （空） | `image` にすると画像ヘッダーを使用 |
| `header_image_url` | （空） | ヘッダー画像URL |
| `header_style` | A | ヘッダースタイル（`A` / `B` / `C`） |

### 動作設定

| key | デフォルト | 説明 |
|-----|-----------|------|
| `next_lock_sec` | （空） | 到着後「次へ」ボタンをロックする最大秒数。音声完了で自動解除。保険として **45** を推奨 |

### 上級設定（Google連携）

| key | 説明 |
|-----|------|
| `ga_measurement_id` | Google Analytics 4のMeasurement ID（`G-XXXXXXXXXX`形式）※index.htmlに直接記載 |

---

## 音声ガイドについて

### MP3ファイルの準備

1. Google Driveに音声ファイルをアップロード
2. ファイルを「リンクを知っている全員が閲覧可」に共有設定
3. 共有リンクをスプレッドシートのURL列に貼り付け

### 音声の優先順位

```
到着時：audio_arrive_url（MP3）→ なければTTS読み上げ
解説　：audio_explain_url（MP3）→ なければTTS読み上げ（到着がTTSの場合のみ）
次誘導：audio_next_url（MP3）→ なければTTS読み上げ
```

> ⚠️ **到着音声にMP3を使用した場合、解説のTTS読み上げは自動的に抑制されます。**

### 音声ガイドのガイドライン

まち歩きの屋外環境を考慮し、以下を制作の目安としてください。

- **目標：20〜30秒**（原稿150〜200文字程度）
- 専門用語より「へぇ！」と感じるエピソードを優先
- 長くても1スポット45秒以内を推奨

---

## Google Analytics 4 の設定

1. [Google Analytics](https://analytics.google.com/) でプロパティを作成
2. Measurement ID（`G-XXXXXXXXXX`形式）を取得
3. `index.html` 内の該当箇所を書き換え

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### 計測されるイベント

| イベント名 | 計測タイミング |
|-----------|---------------|
| `spot_arrive` | スポット到着時（auto：GPS自動 / manual：手動） |
| `course_start` | コース開始時 |
| `course_complete` | コース完走時 |

---

## コミュニティ・サポート

### 基本的な考え方

本プロジェクトはオープンソースですが、コミュニティへの参加と導入サポートは  
**地域の観光・まちづくりに本気で取り組む団体・担当者を対象**としています。

ツールとして自由に使っていただくことは歓迎しますが、  
将人さんと一緒に取り組む関係を築くには、**まず増田に来てください。**

増田の内蔵を実際に歩き、アプリを体験し、このプロジェクトが何を目指しているかを  
感じてもらうことが、すべての出発点です。

---

### サポートの二層構造

**① フォーク・自由利用（サポートなし）**

- GitHubからフォークして自由に使えます
- クレジット表記の維持のみ必須
- 個別サポートはありません

**② コミュニティ参加（サポートあり）**

- 増田まち歩きの現地体験が前提
- 観光協会・自治体観光部署・まちづくり団体に所属していること
- 参加申請時に所属団体と活用目的を明記

---

### 参加対象

以下に該当する方を対象としています。

- 観光協会・観光ガイド団体に所属している
- 自治体の観光・まちづくり関連部署に所属している
- 地域の魅力発信を目的とした任意団体・NPOに属している
- 上記に準ずる活動をしており、増田への現地訪問が可能な方

> 一般企業・個人・観光と無関係の団体からの参加はご遠慮いただいています。  
> 熱量のある方が集まる場として運営しています。

---

### コミュニティの場（整備中）

| 用途 | ツール | 状況 |
|------|--------|------|
| 個別相談・不具合報告 | メール | 運用中 |
| バージョンアップ情報・事例共有 | Googleグループ | 準備中 |
| 定期オンライン情報交換会 | Google Meet | 導入団体が集まり次第開催予定 |
| バグ報告・機能要望 | GitHub Issues | 運用中 |

**メール：** masato.kosaka@gmail.com

---

## クレジット表記について（重要）

### アプリ内クレジット（削除・改変禁止）

アプリのホーム画面下部に表示されている以下の表記は、  
**削除・非表示化・改変をしないでください。**

```
企画・ディレクション：小坂将人
増田町観光協会理事 ／ 増田町観光ガイドの会理事
```

他地域向けにカスタマイズして公開する場合は、上記に加えてご自身の情報を**追記**する形で対応してください。

### READMEへの記載

フォークしたリポジトリのREADMEに、以下を記載してください。

```
このアプリは local-walk-guide（https://github.com/Kosa-E-Mon/local-walk-guide）を
ベースに構築されています。
Original: 小坂将人（増田町観光ガイドの会）
```

---

## ライセンス

本ソフトウェアはMITライセンスに準拠しますが、**クレジット表記の維持を追加条件とします。**

```
MIT License with Attribution Requirement

Copyright (c) 2024 小坂将人（Masato Kosaka）
増田町観光ガイドの会 / 増田町観光協会
Masuda Town Tourism Guide Association, Yokote City, Akita, Japan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, subject to the following conditions:

1. The above copyright notice and this permission notice shall be included in
   all copies or substantial portions of the Software.

2. The credit text displayed in the application's home screen footer
   ("企画・ディレクション：小坂将人 / 増田町観光協会理事 ／ 増田町観光ガイドの会理事")
   must not be removed or obscured. Additional attribution may be added,
   but the original credit must remain visible.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

*本アプリは増田町の地域活性化を目的に開発されました。*  
*同じ思いを持つ全国の地域・観光協会の皆さんにご活用いただけることを願っています。*  
*— 小坂将人（増田町観光ガイドの会）*

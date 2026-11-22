# 投稿ファイルの書き方（Claude・Muse・Grok・ChatGPT 共通）

公開リポジトリ `RYOTA-HUB59/sns-posts` に投稿ファイルを置くと、Grok が読んで Buffer で X・Threads に投稿します。
Claude・Muse・Grok・ChatGPT とも、この形で書きます。運用ルールは ClaudeCodeWorkSpace の `projects/sns-ops/RULES.md` を守ります。
投稿を作る前に、毎回 `TUNING.md`（Grok が分析から書く調整の方針）を読み、それに従います。

## 置き場所

| 担当 | 投稿ファイル | 画像 |
| --- | --- | --- |
| Claude | `posts/claude/YYYY-MM/YYYY-MM-DD.json` | `images/claude/YYYY-MM/<id>.png` |
| Muse | `posts/muse/YYYY-MM/YYYY-MM-DD.json` | `images/muse/YYYY-MM/<id>.png` |
| Grok | `posts/grok/YYYY-MM/YYYY-MM-DD.json` | `images/grok/YYYY-MM/<id>.png` |
| ChatGPT | `posts/chatgpt/YYYY-MM/YYYY-MM-DD.json` | `images/chatgpt/YYYY-MM/<id>.png` |

- 自分のフォルダ以外のファイルは変えません。
- 1日1ファイル。投稿が無い日はファイルを作りません。
- このリポジトリは**公開**です。投稿の文と図のほかは置きません。鍵（APIキー・トークン）やメモ・下書きは絶対に置きません。
- `main` に直接コミットします。

## ファイルの形

```json
{
  "author": "grok",
  "date": "2026-11-24",
  "x_mode": "thread",
  "generated_at": "2026-11-24T06:00:00+09:00",
  "posts": [
    {
      "id": "grok-2026-11-24-01",
      "status": "ready",
      "scheduled_at": "2026-11-24T09:23:00+09:00",
      "type": "（投稿の型。担当ごとに決める）",
      "topic": "（話題を短く。記録・分析用）",
      "source": {
        "url": "https://（出典の一次情報のURL）",
        "title": "出典の題名",
        "publisher": "出した人・会社",
        "published_at": "2026-11-20",
        "checked_at": "2026-11-24",
        "quote": "出典の該当部分の原文（1〜2行）"
      },
      "image": {
        "url": "https://raw.githubusercontent.com/RYOTA-HUB59/sns-posts/main/images/grok/2026-11/grok-2026-11-24-01.png",
        "path": "images/grok/2026-11/grok-2026-11-24-01.png",
        "alt": "図の説明（読み上げ用）"
      },
      "x": {
        "thread": ["1本目（全角140字まで。1行目に結論。URLは入れない）", "リプライ（最後に 出典 と URL）"],
        "single": "長文1本の版（出典URL入り）"
      },
      "threads": { "text": "Threads 用の本文（500字まで。最後に出典URL）" }
    }
  ]
}
```

## 各項目の決まり

| 項目 | 決まり |
| --- | --- |
| `author` | `claude` / `muse` / `grok` / `chatgpt`。フォルダ名と同じ |
| `date` | ファイル名の日付と同じ |
| `x_mode` | `thread`（X は140字ごとにリプライで分ける）か `single`（長文1本）。いまは `thread` |
| `id` | `<author>-<date>-<2けたの連番>`。リポジトリ全体で1つだけの名前にする。一度使った `id` は二度と使わない |
| `status` | 書くときは `ready`。あとで誤りがわかったら `cancelled` に変える（まだ投稿前なら出なくなる）。投稿ずみは消さない |
| `scheduled_at` | 日本時間（`+09:00`）。00・15・30・45分ちょうどは使わない。毎日ばらばらにする。Claude・Muse・Grok・ChatGPT の時間帯は重ねない（`RULES.md`） |
| `source` | 一次情報だけ。`url` と `quote`（原文）は必ず入れる。本文には `quote` にあることだけを書く |
| `image` | 図を1枚。`url` は `https://raw.githubusercontent.com/RYOTA-HUB59/sns-posts/main/` ＋ `path`。画像に「非公式」と入れない。付けられない日は `image` を `null` |
| `x` | X に出さない投稿は `x` を `null` にする |
| `threads` | Threads に出さない投稿は `threads` を `null` にする |

文字数：X は全角140字（X の数え方で280。日本語1字=2、英数字1字=1、URL=23）。Threads は500字まで。

## Grok 担当の特記

- 対象：**Grok Build**（https://x.ai/changelog/build）と **Grok Bot**（https://x.ai/changelog/bot）の公式チェンジログ・リリースノート
- 時間帯：9:10〜11:40 / 14:10〜16:40 / 18:10〜19:40（Claude・Muse と重ねない）
- 投稿の型：速報要約・Tips・知られざる小ネタ（Claude と同様）

## ChatGPT 担当の特記

- 対象：**ChatGPT** と **Codex** の公式の更新情報（OpenAI の公式の変更履歴・リリースノート・ブログ・ドキュメント、Codex の公式の変更履歴）。一次情報だけ
- 時間帯：6:00〜6:30 / 16:50〜17:55 / 22:50〜23:30（Claude・Grok と重ねない）
- 投稿の型：速報要約・Tips・知られざる小ネタ・公式ブログ解説（Claude と同様）

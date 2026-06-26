# 🍵 teatimes — コーヒーチャット・メンターマッチングプラットフォーム

멘토와 멘티를 연결하는 커피챗 예약 서비스입니다.  
メンターとメンティーをつなぐコーヒーチャット予約サービスです。

---

## 🔧 技術スタック

| カテゴリ | 技術 |
|--------|------|
| Frontend | React, JavaScript |
| Backend | FastAPI, Python |
| Database | PostgreSQL, pgvector |
| AI | Azure OpenAI (GPT-4o-mini) |
| その他 | WebSocket, REST API, STT |

---

## ✨ 主な機能

### 🤖 AIおすすめ質問機能
- コーヒーチャット中にSTTでリアルタイム会話を収集
- 45秒ごとにAIが自動でおすすめ質問を生成・更新
- WebSocket経由でAzure OpenAIを呼び出し、結果をDBに蓄積保存

### 📅 予約・セッション管理
- 予約ステータス（PAID / CONFIRMED）に基づくタブ分類
- 時間ベースで「進行中 / 終了」を自動判定するUI
- セッション開始5分前に入室ボタンを有効化

### ⭐ レビュー・メンター推薦
- 星評価＋テキストレビューの投稿機能
- 類似職種のメンター推薦機能（セッション終了後に表示）
- 実際のレビューとプロフィール写真をDBから連携表示

---

## 🗄️ データベース設計（主要テーブル）

```sql
-- AIおすすめ質問を保存
chat_sessions (
  id, booking_id, recommended_questions JSONB, ...
)

-- レビュー情報
reviews (
  id, booking_id, mentor_id, user_id, rating, review, ...
)
```

---

## 🔌 主要API

| メソッド | エンドポイント | 説明 |
|--------|-------------|------|
| POST | `/api/booking/review/create` | レビュー保存 |
| GET | `/api/booking/reviews/{mentor_id}` | メンターレビュー取得 |
| GET | `/api/booking/recommend/{booking_id}` | 類似職種メンター推薦 |
| WS | `/ws/llm` | AIおすすめ質問生成（Azure OpenAI） |

---

## 👤 担当範囲

- フロントエンド：予約一覧・詳細・チャットルーム・レビュー画面の実装
- バックエンド：レビュー・推薦APIの設計・実装
- DB：テーブル設計・pgvectorを用いた類似度検索
- AI連携：Azure OpenAIを用いたおすすめ質問生成機能の実装

---

## 📬 連絡先

- GitHub：[github.com/hooonseung](https://github.com/hooonseung)
- Email：hooonseung@gmail.com

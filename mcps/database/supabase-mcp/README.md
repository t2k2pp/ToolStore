# Supabase MCP

## 概要

Supabaseデータベースとの連携を提供するModel Context Protocol。

## ステータス

🚧 **プレースホルダー** - 実装予定

## 予定機能

- PostgreSQL クエリ実行
- 認証連携
- リアルタイムサブスクリプション
- Storage操作

## 設定例（予定）

```json
{
  "name": "supabase",
  "type": "mcp",
  "config": {
    "url": "${SUPABASE_URL}",
    "anon_key": "${SUPABASE_ANON_KEY}",
    "service_role_key": "${SUPABASE_SERVICE_ROLE_KEY}"
  }
}
```

## 参考

- [Supabase公式](https://supabase.com/)
- [Supabase MCP (community)](https://github.com/supabase-community)

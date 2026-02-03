---
name: catalog-maintainer
description: catalog.yamlのメンテナンススキル。新規スキル/サブエージェント/MCP追加、整合性チェック、推奨マッピング更新を支援。Tool Store管理者向け。
---

# Catalog Maintainer

Tool Storeのcatalog.yamlを保守するためのスキル。

---

## 機能

1. **新規ツール追加** - スキル、サブエージェント、MCP、ワークフロー
2. **整合性チェック** - パス存在確認、必須フィールド検証
3. **推奨マッピング更新** - キーワード→ツール関連付け

---

## 1. 新規スキル追加

### 手順

1. スキルファイル作成
```
domains/[domain]/[category]/skills/[skill-id]/SKILL.md
```

2. catalog.yamlに追加
```yaml
domains:
  [domain]:
    [category]:
      skills:
        - id: [skill-id]                    # 一意のID（ケバブケース）
          name: "[表示名]"                   # 日本語OK
          path: "domains/[domain]/[category]/skills/[skill-id]"
          description: "[説明]"
          tags: [tag1, tag2, tag3]          # 検索用タグ
          dependencies: [other-skill-id]    # 依存スキル（任意）
```

3. 推奨マッピングに追加（必要に応じて）
```yaml
recommendations:
  - keywords: [関連キーワード1, 関連キーワード2]
    suggest:
      skills: [[skill-id]]
```

### 例: 新規スキル「flutter-animation」追加

```yaml
# domains.mobile.flutter.skills に追加
- id: flutter-animation
  name: "Flutterアニメーション"
  path: "domains/mobile/flutter/skills/flutter-animation"
  description: "暗黙的・明示的アニメーション、Rive、Lottie統合"
  tags: [animation, rive, lottie, motion]
  dependencies: [flutter-development]

# recommendations に追加
- keywords: [アニメーション, animation, モーション, rive, lottie]
  suggest:
    skills: [flutter-animation]
```

---

## 2. 新規サブエージェント追加

### 手順

1. サブエージェントファイル作成
```
domains/[domain]/[category]/subagents/[subagent-id].md
```

2. catalog.yamlに追加
```yaml
domains:
  [domain]:
    [category]:
      subagents:
        - id: [subagent-id]
          name: "[表示名]"
          path: "domains/[domain]/[category]/subagents/[subagent-id].md"
          description: "[役割説明]"
          model: sonnet | opus              # 推奨モデル
```

---

## 3. 新規MCP追加

### 手順

1. MCPフォルダ作成
```
mcps/[category]/[mcp-id]/README.md
```

2. catalog.yamlに追加
```yaml
mcps:
  [category]:
    - id: [mcp-id]
      name: "[表示名]"
      path: "mcps/[category]/[mcp-id]"
      description: "[説明]"
      status: placeholder | implemented
```

---

## 4. 新規ドメイン追加

### 例: Webドメイン追加

1. フォルダ構造作成
```bash
mkdir -p domains/web/react/{skills,subagents,workflows}
mkdir -p domains/web/nextjs/{skills,subagents,workflows}
```

2. catalog.yamlに追加
```yaml
domains:
  web:
    react:
      name: "React"
      description: "Reactフロントエンド開発"
      path: "domains/web/react"
      skills: []
      subagents: []
      workflows: []
      
    nextjs:
      name: "Next.js"
      description: "Next.jsフルスタック開発"
      path: "domains/web/nextjs"
      skills: []
      subagents: []
      workflows: []
```

---

## 5. 整合性チェック

### チェック項目

| 項目 | 検証内容 |
|------|---------|
| パス存在 | pathで指定したファイル/フォルダが存在するか |
| ID重複 | 同一カテゴリ内でIDが重複していないか |
| 必須フィールド | id, name, path, descriptionが存在するか |
| 依存関係 | dependenciesで指定したスキルが存在するか |
| タグ形式 | tagsが配列形式になっているか |

### チェックコマンド例

```bash
# パス存在チェック（PowerShell）
$catalog = Get-Content catalog.yaml -Raw | ConvertFrom-Yaml
foreach ($skill in $catalog.domains.mobile.flutter.skills) {
    if (-not (Test-Path $skill.path)) {
        Write-Warning "Missing: $($skill.path)"
    }
}
```

---

## 6. 推奨マッピング設計ガイドライン

### キーワード選定

```yaml
# ✅ 良い例: 具体的で多角的
- keywords: [flutter, dart, mobile, クロスプラットフォーム, モバイルアプリ]

# ❌ 悪い例: 曖昧すぎる
- keywords: [アプリ, 開発]
```

### 推奨ツールの優先順位

```yaml
suggest:
  # 1. 必須スキル（最初に読むべき）
  common: [ai-flutter-guidelines]
  
  # 2. メインスキル（直接関連）
  skills: [flutter-development, flutter-tdd]
  
  # 3. サブエージェント（作業担当）
  subagents: [flutter-developer]
  
  # 4. MCP（外部連携が必要な場合のみ）
  mcps: []
```

---

## 7. バージョン管理

### catalog.yaml更新時

```yaml
# ヘッダーを更新
version: "1.x"                    # マイナーバージョンアップ
last_updated: "YYYY-MM-DD"        # 更新日
```

### 破壊的変更時

```yaml
version: "2.0"                    # メジャーバージョンアップ
# 変更履歴コメント追加
# BREAKING: skill path format changed from X to Y
```

---

## チェックリスト

新規ツール追加時:
- [ ] ファイル/フォルダ作成
- [ ] catalog.yamlにエントリ追加
- [ ] 必須フィールド（id, name, path, description）記入
- [ ] tags設定
- [ ] 依存関係（dependencies）設定
- [ ] 推奨マッピング更新
- [ ] last_updated更新
- [ ] 整合性チェック実行
- [ ] Git commit & push

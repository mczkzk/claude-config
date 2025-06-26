# Claude Code のユーザー設定

このリポジトリは、Claude Code のユーザー設定とドキュメントを管理するためのものです。

## 含まれるファイル

- `CLAUDE.md` - Claude Code のユーザー指示設定
- `docs/` - ルールとガイドライン
  - `investigation.md` - 調査時のガイドライン
  - `commands.md` - コマンド実行ガイドライン
- `commands/` - カスタムコマンド定義
  - `commit.md` - Git コミット作成コマンド
  - `plan.md` - 実装計画作成コマンド
  - `tdd.md` - テスト駆動開発コマンド
- `settings.json` - Claude Codeの設定ファイル

## 別のPCで設定を同期する方法

既存の`~/.claude`ディレクトリがある場合、以下の手順で設定ファイルのみを同期できます：

```bash
# .claudeディレクトリに移動
cd ~/.claude

# gitリポジトリを初期化
git init

# リモートリポジトリを追加
git remote add origin https://github.com/mczkzk/claude-config.git

# リモートから取得
git fetch origin

# ローカルブランチを作成してリモートのmainブランチを追跡
git checkout -b main origin/main

# 必要に応じて個別にチェックアウト
git checkout origin/main -- docs/
git checkout origin/main -- commands/
git checkout origin/main -- CLAUDE.md
git checkout origin/main -- settings.json
git checkout origin/main -- .gitignore
```

## 注意事項

以下のディレクトリは各PC固有のデータのため、同期対象外です：
- `ide/` - IDE関連の一時ファイル
- `projects/` - プロジェクト履歴
- `statsig/` - 統計データ
- `todos/` - TODO履歴

これらは`.gitignore`により除外されているため、同期時に影響を受けません。
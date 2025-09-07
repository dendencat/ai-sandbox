# スクリプト説明ドキュメント

このディレクトリには、フィーチャー開発ワークフローを管理するためのBashスクリプトが含まれています。これらのスクリプトは、AIエージェントとの協働開発を支援する自動化ツールです。

## スクリプト一覧

### 1. common.sh
**目的**: 全スクリプトで共有される関数と変数を提供するライブラリファイル

**主な機能**:
- リポジトリルートの取得
- 現在のブランチ名の取得
- フィーチャーブランチの妥当性チェック（`001-feature-name`形式）
- フィーチャーディレクトリパスの生成
- 標準ファイルパスの定義（spec.md, plan.md, tasks.md等）
- ファイル/ディレクトリ存在チェック機能

**使用方法**:
```bash
# 他のスクリプトから読み込み
source "$SCRIPT_DIR/common.sh"

# パス設定の取得
eval $(get_feature_paths)
```

**依存関係**: なし（他のスクリプトの基盤となる）

---

### 2. create-new-feature.sh
**目的**: 新しいフィーチャーのブランチ、ディレクトリ構造、テンプレートを作成

**主な機能**:
- 次のフィーチャー番号の自動生成（3桁ゼロパディング）
- フィーチャー説明からブランチ名の生成
- 新しいフィーチャーブランチの作成と切り替え
- フィーチャーディレクトリの作成
- spec-template.mdからspec.mdの作成

**使用方法**:
```bash
# 基本使用法
./create-new-feature.sh "機能の説明"

# JSON出力モード
./create-new-feature.sh --json "機能の説明"
```

**出力例**:
```
BRANCH_NAME: 001-user-authentication
SPEC_FILE: /path/to/specs/001-user-authentication/spec.md
FEATURE_NUM: 001
```

**依存関係**: git, templates/spec-template.md

---

### 3. get-feature-paths.sh
**目的**: 現在のフィーチャーブランチのパス情報を取得（ファイル作成なし）

**主な機能**:
- フィーチャーブランチの妥当性確認
- フィーチャー関連ファイルのパス一覧表示
- 既存ファイルの検索に使用

**使用方法**:
```bash
./get-feature-paths.sh
```

**出力例**:
```
REPO_ROOT: /path/to/repo
BRANCH: 001-user-auth
FEATURE_DIR: /path/to/specs/001-user-auth
FEATURE_SPEC: /path/to/specs/001-user-auth/spec.md
IMPL_PLAN: /path/to/specs/001-user-auth/plan.md
TASKS: /path/to/specs/001-user-auth/tasks.md
```

**依存関係**: common.sh

---

### 4. setup-plan.sh
**目的**: 現在のブランチの実装プラン構造をセットアップ

**主な機能**:
- フィーチャーディレクトリの作成
- plan-template.mdからplan.mdの作成
- 実装プラン生成に必要なパス情報の提供

**使用方法**:
```bash
# 基本使用法
./setup-plan.sh

# JSON出力モード
./setup-plan.sh --json
```

**出力例**:
```
FEATURE_SPEC: /path/to/specs/001-user-auth/spec.md
IMPL_PLAN: /path/to/specs/001-user-auth/plan.md
SPECS_DIR: /path/to/specs/001-user-auth
BRANCH: 001-user-auth
```

**依存関係**: common.sh, templates/plan-template.md

---

### 5. check-task-prerequisites.sh
**目的**: タスク生成の前提条件をチェックし、利用可能なドキュメントを確認

**主な機能**:
- フィーチャーブランチの妥当性確認
- フィーチャーディレクトリの存在確認
- 必須ファイル（plan.md）の存在確認
- オプションドキュメントの検出
  - research.md（調査資料）
  - data-model.md（データモデル）
  - contracts/（API契約）
  - quickstart.md（クイックスタート）

**使用方法**:
```bash
# 基本使用法
./check-task-prerequisites.sh

# JSON出力モード
./check-task-prerequisites.sh --json
```

**出力例**:
```
FEATURE_DIR:/path/to/specs/001-user-auth
AVAILABLE_DOCS:
  ✓ research.md
  ✗ data-model.md
  ✓ contracts/
  ✗ quickstart.md
```

**依存関係**: common.sh

---

### 6. update-agent-context.sh
**目的**: 新しいフィーチャープランに基づいてエージェントコンテキストファイルを増分更新

**主な機能**:
- プランファイルからテクノロジー情報の抽出
- エージェントコンテキストファイルの更新
  - CLAUDE.md（Claude Code用）
  - GEMINI.md（Gemini CLI用）
  - .github/copilot-instructions.md（GitHub Copilot用）
- 新しいテクノロジースタックの追加
- プロジェクト構造の更新
- 最新変更履歴の管理

**使用方法**:
```bash
# 全ての既存ファイルを更新
./update-agent-context.sh

# 特定のエージェントのみ更新
./update-agent-context.sh claude
./update-agent-context.sh gemini
./update-agent-context.sh copilot
```

**抽出される情報**:
- Language/Version（プログラミング言語）
- Primary Dependencies（主要な依存関係）
- Testing（テスト手法）
- Storage（ストレージ/データベース）
- Project Type（プロジェクトタイプ）

**依存関係**: plan.md, templates/agent-file-template.md, Python3

## ワークフロー

これらのスクリプトは通常、以下の順序で使用されます：

1. `create-new-feature.sh` - 新しいフィーチャーを開始
2. `setup-plan.sh` - 実装プランの準備
3. `check-task-prerequisites.sh` - 前提条件の確認
4. `get-feature-paths.sh` - パス情報の取得
5. `update-agent-context.sh` - エージェントコンテキストの更新

## 共通パターン

- 全スクリプトは`--json`オプションをサポート（機械読み取り可能な出力）
- `common.sh`の関数を活用して一貫性を保持
- フィーチャーブランチ名は`NNN-feature-name`形式を前提
- エラー時は適切な終了コードを返す
- `set -e`により途中でエラーが発生した場合は処理を停止
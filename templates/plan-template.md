# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

## Execution Flow (/plan command scope)
```
1. 機能仕様を入力パスから読み込む
   → 見つからない場合: ERROR "No feature spec at {path}"
2. 技術コンテキストを埋める (NEEDS CLARIFICATION をスキャン)
   → コンテキストからプロジェクトタイプを検出 (web=frontend+backend, mobile=app+api)
   → プロジェクトタイプに基づいて構造決定を設定
3. 下記の憲法チェックセクションを評価
   → 違反が存在する場合: 複雑さ追跡に文書化
   → 正当化が不可能な場合: ERROR "Simplify approach first"
   → 進捗追跡を更新: Initial Constitution Check
4. Phase 0 を実行 → research.md
   → NEEDS CLARIFICATION が残っている場合: ERROR "Resolve unknowns"
5. Phase 1 を実行 → contracts, data-model.md, quickstart.md, エージェント固有のテンプレートファイル (例: Claude Code 用 `CLAUDE.md`, GitHub Copilot 用 `.github/copilot-instructions.md`, Gemini CLI 用 `GEMINI.md`)
6. 憲法チェックセクションを再評価
   → 新しい違反がある場合: 設計をリファクタリングし、Phase 1 に戻る
   → 進捗追跡を更新: Post-Design Constitution Check
7. Phase 2 を計画 → タスク生成アプローチを記述 (tasks.md を作成しない)
8. STOP - /tasks コマンドの準備完了
```

**IMPORTANT**: /plan コマンドはステップ7で停止します。Phase 2-4 は他のコマンドによって実行されます:
- Phase 2: /tasks コマンドが tasks.md を作成
- Phase 3-4: 実装実行 (手動またはツール経由)

## Summary
[機能仕様から抽出: 主な要件 + 研究からの技術アプローチ]

## Technical Context
**Language/Version**: [例: Python 3.11, Swift 5.9, Rust 1.75 または NEEDS CLARIFICATION]  
**Primary Dependencies**: [例: FastAPI, UIKit, LLVM または NEEDS CLARIFICATION]  
**Storage**: [該当する場合、例: PostgreSQL, CoreData, files または N/A]  
**Testing**: [例: pytest, XCTest, cargo test または NEEDS CLARIFICATION]  
**Target Platform**: [例: Linux server, iOS 15+, WASM または NEEDS CLARIFICATION]
**Project Type**: [single/web/mobile - ソース構造を決定]  
**Performance Goals**: [ドメイン固有、例: 1000 req/s, 10k lines/sec, 60 fps または NEEDS CLARIFICATION]  
**Constraints**: [ドメイン固有、例: <200ms p95, <100MB memory, offline-capable または NEEDS CLARIFICATION]  
**Scale/Scope**: [ドメイン固有、例: 10k users, 1M LOC, 50 screens または NEEDS CLARIFICATION]

## Constitution Check
*GATE: Phase 0 研究前に合格する必要あり。Phase 1 設計後に再チェック。*

**Simplicity**:
- Projects: [#] (最大3 - 例: api, cli, tests)
- フレームワークを直接使用? (ラッパークラスなし)
- 単一のデータモデル? (シリアライズが異なる場合を除きDTOなし)
- パターンを避ける? (証明された必要性なしでRepository/UoWなし)

**Architecture**:
- すべての機能をライブラリとして? (直接のアプリコードなし)
- ライブラリ一覧: [各々の名前 + 目的]
- ライブラリごとのCLI: [--help/--version/--format 付きコマンド]
- ライブラリドキュメント: llms.txt 形式を計画?

**Testing (NON-NEGOTIABLE)**:
- RED-GREEN-Refactor サイクルを強制? (テストは最初に失敗する必要あり)
- Git コミットで実装前にテストを表示?
- 順序: Contract→Integration→E2E→Unit を厳密に遵守?
- 実際の依存関係を使用? (実際のDB、モックなし)
- 統合テスト対象: 新しいライブラリ、契約変更、共有スキーマ?
- FORBIDDEN: テスト前の実装、RED フェーズのスキップ

**Observability**:
- 構造化ログを含める?
- フロントエンドログ → バックエンド? (統合ストリーム)
- エラーコンテキストは十分?

**Versioning**:
- バージョン番号を割り当て? (MAJOR.MINOR.BUILD)
- すべての変更でBUILD をインクリメント?
- 破壊的変更を処理? (並行テスト、移行計画)

## Project Structure

### Documentation (this feature)
```
specs/[###-feature]/
├── plan.md              # This file (/plan command output)
├── research.md          # Phase 0 output (/plan command)
├── data-model.md        # Phase 1 output (/plan command)
├── quickstart.md        # Phase 1 output (/plan command)
├── contracts/           # Phase 1 output (/plan command)
└── tasks.md             # Phase 2 output (/tasks command - NOT created by /plan)
```

### Source Code (repository root)
```
# Option 1: Single project (DEFAULT)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# Option 2: Web application (when "frontend" + "backend" detected)
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# Option 3: Mobile + API (when "iOS/Android" detected)
api/
└── [same as backend above]

ios/ or android/
└── [platform-specific structure]
```

**Structure Decision**: [Technical Context が web/mobile アプリを示さない限り Option 1 をデフォルト]

## Phase 0: Outline & Research
1. **上記の Technical Context から不明点を抽出**:
   - 各 NEEDS CLARIFICATION → 研究タスク
   - 各依存関係 → ベストプラクティスタスク
   - 各統合 → パターンタスク

2. **研究エージェントを生成して派遣**:
   ```
   Technical Context の各不明点に対して:
     Task: "Research {unknown} for {feature context}"
   各技術選択に対して:
     Task: "Find best practices for {tech} in {domain}"
   ```

3. **研究結果を `research.md` に統合** 形式を使用:
   - Decision: [選択されたもの]
   - Rationale: [選択理由]
   - Alternatives considered: [評価された他の選択肢]

**Output**: すべての NEEDS CLARIFICATION を解決した research.md

## Phase 1: Design & Contracts
*Prerequisites: research.md 完了*

1. **機能仕様からエンティティを抽出** → `data-model.md`:
   - エンティティ名、フィールド、リレーションシップ
   - 要件からの検証ルール
   - 該当する場合の状態遷移

2. **機能要件から API 契約を生成**:
   - 各ユーザーアクション → エンドポイント
   - 標準 REST/GraphQL パターンを使用
   - OpenAPI/GraphQL スキーマを `/contracts/` に出力

3. **契約から契約テストを生成**:
   - エンドポイントごとに1つのテストファイル
   - リクエスト/レスポンススキーマをアサート
   - テストは失敗する必要あり (実装なし)

4. **ユーザーストーリーからテストシナリオを抽出**:
   - 各ストーリー → 統合テストシナリオ
   - Quickstart テスト = ストーリー検証ステップ

5. **エージェントファイルをインクリメンタルに更新** (O(1) 操作):
   - `/scripts/update-agent-context.sh [claude|gemini|copilot]` を実行して AI アシスタント用
   - 存在する場合: 現在の計画から新しい技術のみ追加
   - マーカー間の手動追加を保持
   - 最近の変更を更新 (最後の3つを保持)
   - トークン効率のために150行未満に保つ
   - リポジトリルートに出力

**Output**: data-model.md, /contracts/*, 失敗するテスト, quickstart.md, エージェント固有ファイル

## Phase 2: Task Planning Approach
*このセクションは /tasks コマンドが何をするかを記述 - /plan 中に実行しない*

**Task Generation Strategy**:
- `/templates/tasks-template.md` をベースとして読み込み
- Phase 1 設計ドキュメント (contracts, data model, quickstart) からタスクを生成
- 各契約 → 契約テストタスク [P]
- 各エンティティ → モデル作成タスク [P] 
- 各ユーザーストーリー → 統合テストタスク
- テストをパスさせるための実装タスク

**Ordering Strategy**:
- TDD 順序: 実装前にテスト 
- 依存順序: モデル → サービス → UI
- [P] で並行実行をマーク (独立ファイル)

**Estimated Output**: tasks.md の 25-30 の番号付き順序付きタスク

**IMPORTANT**: このフェーズは /tasks コマンドによって実行され、/plan によってではない

## Phase 3+: Future Implementation
*これらのフェーズは /plan コマンドの範囲外*

**Phase 3**: タスク実行 (/tasks コマンドが tasks.md を作成)  
**Phase 4**: 実装 (憲法原則に従って tasks.md を実行)  
**Phase 5**: 検証 (テスト実行, quickstart.md 実行, パフォーマンス検証)

## Complexity Tracking
*Constitution Check に違反があり正当化が必要な場合のみ記入*

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [例: 4番目のプロジェクト] | [現在の必要性] | [3つのプロジェクトが不十分な理由] |
| [例: Repository パターン] | [特定の課題] | [直接DBアクセスが不十分な理由] |


## Progress Tracking
*このチェックリストは実行フロー中に更新*

**Phase Status**:
- [ ] Phase 0: Research complete (/plan command)
- [ ] Phase 1: Design complete (/plan command)
- [ ] Phase 2: Task planning complete (/plan command - describe approach only)
- [ ] Phase 3: Tasks generated (/tasks command)
- [ ] Phase 4: Implementation complete
- [ ] Phase 5: Validation passed

**Gate Status**:
- [ ] Initial Constitution Check: PASS
- [ ] Post-Design Constitution Check: PASS
- [ ] All NEEDS CLARIFICATION resolved
- [ ] Complexity deviations documented

---
*Based on Constitution v2.1.1 - See `/memory/constitution.md`*
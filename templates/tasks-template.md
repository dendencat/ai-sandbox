# Tasks: [FEATURE NAME]

**入力**: `/specs/[###-feature-name]/` からの設計ドキュメント
**前提条件**: plan.md (必須), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. 機能ディレクトリから plan.md を読み込み
   → 見つからない場合: ERROR "No implementation plan found"
   → 抽出: 技術スタック、ライブラリ、構造
2. オプションの設計ドキュメントを読み込み:
   → data-model.md: エンティティを抽出 → モデルタスク
   → contracts/: 各ファイル → 契約テストタスク
   → research.md: 決定を抽出 → セットアップタスク
3. カテゴリごとにタスクを生成:
   → Setup: プロジェクト初期化、依存関係、リンティング
   → Tests: 契約テスト、統合テスト
   → Core: モデル、サービス、CLI コマンド
   → Integration: DB、ミドルウェア、ロギング
   → Polish: ユニットテスト、パフォーマンス、ドキュメント
4. タスクルールを適用:
   → 異なるファイル = [P] で並行実行をマーク
   → 同じファイル = 順次実行 ( [P] なし)
   → 実装前にテスト (TDD)
5. タスクを順次番号付け (T001, T002...)
6. 依存関係グラフを生成
7. 並行実行例を作成
8. タスクの完全性を検証:
   → すべての契約にテストがあるか？
   → すべてのエンティティにモデルがあるか？
   → すべてのエンドポイントが実装されているか？
9. 戻り値: SUCCESS (タスクが実行準備完了)
```

## Format: `[ID] [P?] Description`
- **[P]**: 並行して実行可能 (異なるファイル、依存関係なし)
- 説明に正確なファイルパスを含める

## Path Conventions
- **単一プロジェクト**: リポジトリルートに `src/`, `tests/`
- **Webアプリ**: `backend/src/`, `frontend/src/`
- **モバイル**: `api/src/`, `ios/src/` または `android/src/`
- 以下のパスは単一プロジェクトを想定 - plan.md の構造に基づいて調整

## Phase 3.1: Setup
- [ ] T001 plan.md に従ってプロジェクト構造を作成
- [ ] T002 [language] プロジェクトを [framework] 依存関係で初期化
- [ ] T003 [P] リンターとフォーマッターツールを設定

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**重要: これらのテストは実装前に書き込み、失敗させる必要がある**
- [ ] T004 [P] tests/contract/test_users_post.py で POST /api/users の契約テスト
- [ ] T005 [P] tests/contract/test_users_get.py で GET /api/users/{id} の契約テスト
- [ ] T006 [P] tests/integration/test_registration.py でユーザー登録の統合テスト
- [ ] T007 [P] tests/integration/test_auth.py で認証フローの統合テスト

## Phase 3.3: Core Implementation (ONLY after tests are failing)
- [ ] T008 [P] src/models/user.py でユーザーモデル
- [ ] T009 [P] src/services/user_service.py で UserService CRUD
- [ ] T010 [P] src/cli/user_commands.py で CLI --create-user
- [ ] T011 POST /api/users エンドポイント
- [ ] T012 GET /api/users/{id} エンドポイント
- [ ] T013 入力検証
- [ ] T014 エラーハンドリングとログ

## Phase 3.4: Integration
- [ ] T015 UserService を DB に接続
- [ ] T016 認証ミドルウェア
- [ ] T017 リクエスト/レスポンスログ
- [ ] T018 CORS とセキュリティヘッダー

## Phase 3.5: Polish
- [ ] T019 [P] tests/unit/test_validation.py で検証のユニットテスト
- [ ] T020 パフォーマンステスト (<200ms)
- [ ] T021 [P] docs/api.md を更新
- [ ] T022 重複を削除
- [ ] T023 manual-testing.md を実行

## Dependencies
- テスト (T004-T007) を実装 (T008-T014) より前に
- T008 が T009, T015 をブロック
- T016 が T018 をブロック
- 実装をポリッシュ (T019-T023) より前に

## Parallel Example
```
# Launch T004-T007 together:
Task: "Contract test POST /api/users in tests/contract/test_users_post.py"
Task: "Contract test GET /api/users/{id} in tests/contract/test_users_get.py"
Task: "Integration test registration in tests/integration/test_registration.py"
Task: "Integration test auth in tests/integration/test_auth.py"
```

## Notes
- [P] タスク = 異なるファイル、依存関係なし
- 実装前にテストが失敗することを確認
- 各タスク後にコミット
- 避ける: 曖昧なタスク、同じファイルの競合

## Task Generation Rules
*main() 実行中に適用*

1. **契約から**:
   - 各契約ファイル → 契約テストタスク [P]
   - 各エンドポイント → 実装タスク
   
2. **データモデルから**:
   - 各エンティティ → モデル作成タスク [P]
   - 関係 → サービスレイヤータスク
   
3. **ユーザーストーリーから**:
   - 各ストーリー → 統合テスト [P]
   - クイックスタートシナリオ → 検証タスク

4. **順序**:
   - セットアップ → テスト → モデル → サービス → エンドポイント → ポリッシュ
   - 依存関係が並行実行をブロック

## Validation Checklist
*GATE: main() が返す前にチェック*

- [ ] すべての契約にテストがある
- [ ] すべてのエンティティにモデルタスクがある
- [ ] すべてのテストが実装より前にある
- [ ] 並行タスクが本当に独立している
- [ ] 各タスクが正確なファイルパスを指定している
- [ ] 他の [P] タスクと同じファイルを変更しない
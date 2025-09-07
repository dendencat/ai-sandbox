# Constitution Update Checklist

When amending the constitution (`/memory/constitution.md`), ensure all dependent documents are updated to maintain consistency.

## Templates to Update

### When adding/modifying ANY article:
- [ ] `/templates/plan-template.md` - 憲法チェックセクションを更新
- [ ] `/templates/spec-template.md` - 要件/範囲に影響がある場合に更新
- [ ] `/templates/tasks-template.md` - 新しいタスクタイプが必要な場合に更新
- [ ] `/.claude/commands/plan.md` - 計画プロセスが変更された場合に更新
- [ ] `/.claude/commands/tasks.md` - タスク生成に影響がある場合に更新
- [ ] `/CLAUDE.md` - ランタイム開発ガイドラインを更新

### Article-specific updates:

#### Article I (Library-First):
- [ ] テンプレートがライブラリ作成を強調することを確認
- [ ] CLIコマンド例を更新
- [ ] llms.txtドキュメント要件を追加

#### Article II (CLI Interface):
- [ ] テンプレート内のCLIフラグ要件を更新
- [ ] テキストI/Oプロトコルのリマインダーを追加

#### Article III (Test-First):
- [ ] すべてのテンプレートでテスト順序を更新
- [ ] TDD要件を強調
- [ ] テスト承認ゲートを追加

#### Article IV (Integration Testing):
- [ ] 統合テストトリガーをリスト
- [ ] テストタイプの優先順位を更新
- [ ] 実際の依存関係要件を追加

#### Article V (Observability):
- [ ] テンプレートにログ要件を追加
- [ ] マルチティアログストリーミングを含める
- [ ] パフォーマンス監視セクションを更新

#### Article VI (Versioning):
- [ ] バージョンインクリメントのリマインダーを追加
- [ ] 破壊的変更手順を含める
- [ ] 移行要件を更新

#### Article VII (Simplicity):
- [ ] プロジェクト数制限を更新
- [ ] パターン禁止の例を追加
- [ ] YAGNIリマインダーを含める

## Validation Steps

1. **Before committing constitution changes:**
   - [ ] すべてのテンプレートが新しい要件を参照している
   - [ ] 例が新しいルールに一致するように更新されている
   - [ ] 文書間に矛盾がない

2. **After updating templates:**
   - [ ] サンプル実装計画を実行する
   - [ ] すべての憲法要件が対応されていることを確認する
   - [ ] テンプレートが自己完結していることを確認する（憲法なしで読める）

3. **Version tracking:**
   - [ ] 憲法バージョン番号を更新
   - [ ] テンプレートフッターにバージョンを記載
   - [ ] 憲法履歴に改正を追加

## Common Misses

Watch for these often-forgotten updates:
- コマンドドキュメント（`/commands/*.md`）を更新
- テンプレート内のチェックリスト項目
- 例のコード/コマンド
- ドメイン固有のバリエーション（ウェブ vs モバイル vs CLI）
- 文書間の相互参照

## Template Sync Status

Last sync check: 2025-07-16
- Constitution version: 2.1.1
- Templates aligned: ❌ (missing versioning, observability details)

---

*This checklist ensures the constitution's principles are consistently applied across all project documentation.*
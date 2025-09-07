# Plan how to implement the specified feature

指定された機能をどのように実装するかを計画してください。

これは、Spec-Driven Developmentライフサイクルの2番目のステップです。

引数として提供された実装詳細に基づいて、以下のことを行ってください：

1. リポジトリのルートから `scripts/setup-plan.sh --json` を実行し、JSONを解析して FEATURE_SPEC、IMPL_PLAN、SPECS_DIR、BRANCH を取得します。今後のすべてのファイルパスは絶対パスでなければなりません。
2. 機能仕様を読み取り、分析して以下の点を理解します：
   - 機能要件とユーザーストーリー
   - 機能要件と非機能要件
   - 成功基準と受け入れ基準
   - 言及されている技術的制約や依存関係

3. `/memory/constitution.md` の憲法を読み取り、憲法上の要件を理解します。

4. 実装計画テンプレートを実行します：
   - `/templates/plan-template.md` をロードします（すでに IMPL_PLAN パスにコピー済み）
   - 入力パスを FEATURE_SPEC に設定します
   - Execution Flow (main) 関数のステップ1-10を実行します
   - テンプレートは自己完結型で実行可能です
   - 指定されたエラーハンドリングとゲートチェックに従います
   - $SPECS_DIR でのアーティファクト生成をテンプレートに任せます：
     * Phase 0 は research.md を生成します
     * Phase 1 は data-model.md、contracts/、quickstart.md を生成します
     * Phase 2 は tasks.md を生成します
   - 引数から提供されたユーザーの詳細を Technical Context: $ARGUMENTS に組み込みます
   - 各フェーズを完了するごとに Progress Tracking を更新します

5. 実行が完了したことを確認します：
   - Progress Tracking がすべてのフェーズが完了していることを確認します
   - すべての必要なアーティファクトが生成されたことを確認します
   - 実行に ERROR 状態がないことを確認します

6. ブランチ名、ファイルパス、生成されたアーティファクトとともに結果を報告します。

パス問題を避けるため、すべてのファイル操作でリポジトリルートからの絶対パスを使用してください。


# Start a new feature by creating a specification and feature branch

新しい機能を仕様書と機能ブランチを作成して開始します。

これはSpec-Driven Developmentライフサイクルの最初のステップです。

引数として提供された機能の説明に基づいて、以下のことを行います：

1. リポジトリのルートからスクリプト `scripts/create-new-feature.sh --json "$ARGUMENTS"` を実行し、そのJSON出力を解析してBRANCH_NAMEとSPEC_FILEを取得します。すべてのファイルパスは絶対パスでなければなりません。
2. `templates/spec-template.md` を読み込んで、必要なセクションを理解します。
3. テンプレート構造を使用してSPEC_FILEに仕様書を書き込み、プレースホルダーを機能の説明（引数）から導き出された具体的な詳細に置き換え、セクションの順序と見出しを保持します。
4. 完了をブランチ名、仕様書ファイルのパス、次のフェーズの準備状況とともに報告します。

注：スクリプトは新しいブランチを作成してチェックアウトし、書き込み前に仕様書ファイルを初期化します。


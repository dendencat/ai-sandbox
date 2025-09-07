# [PROJECT_NAME] Constitution
<!-- 例: Spec Constitution, TaskFlow Constitution, など。 -->

## Core Principles

### [PRINCIPLE_1_NAME]
<!-- 例: I. Library-First -->
[PRINCIPLE_1_DESCRIPTION]
<!-- 例: すべての機能はスタンドアロンのライブラリから始まる；ライブラリは自己完結型で、独立してテスト可能、文書化されている；明確な目的が必要 - 組織専用のライブラリはなし -->

### [PRINCIPLE_2_NAME]
<!-- 例: II. CLI Interface -->
[PRINCIPLE_2_DESCRIPTION]
<!-- 例: すべてのライブラリはCLI経由で機能を公開；テキスト入出力プロトコル: stdin/args → stdout, エラー → stderr；JSON + 人間可読形式をサポート -->

### [PRINCIPLE_3_NAME]
<!-- 例: III. Test-First (NON-NEGOTIABLE) -->
[PRINCIPLE_3_DESCRIPTION]
<!-- 例: TDD必須: テストを書く → ユーザーが承認 → テストが失敗 → 実装；Red-Green-Refactorサイクルを厳格に実施 -->

### [PRINCIPLE_4_NAME]
<!-- 例: IV. Integration Testing -->
[PRINCIPLE_4_DESCRIPTION]
<!-- 例: 統合テストが必要な焦点領域: 新しいライブラリ契約テスト、契約変更、サービス間通信、共有スキーマ -->

### [PRINCIPLE_5_NAME]
<!-- 例: V. Observability, VI. Versioning & Breaking Changes, VII. Simplicity -->
[PRINCIPLE_5_DESCRIPTION]
<!-- 例: テキストI/Oでデバッグ可能性を確保；構造化ログが必要；または: MAJOR.MINOR.BUILD形式；または: シンプルに始める、YAGNI原則 -->

## [SECTION_2_NAME]
<!-- 例: Additional Constraints, Security Requirements, Performance Standards, など。 -->

[SECTION_2_CONTENT]
<!-- 例: テクノロジースタックの要件、コンプライアンス基準、デプロイメントポリシー、など。 -->

## [SECTION_3_NAME]
<!-- 例: Development Workflow, Review Process, Quality Gates, など。 -->

[SECTION_3_CONTENT]
<!-- 例: コードレビューの要件、テストゲート、デプロイメント承認プロセス、など。 -->

## Governance
<!-- 例: Constitutionは他のすべての慣行を上書き；改正には文書化、承認、移行計画が必要 -->

[GOVERNANCE_RULES]
<!-- 例: すべてのPR/レビューはコンプライアンスを確認；複雑さは正当化される；ランタイム開発ガイダンスには[GUIDANCE_FILE]を使用 -->

**Version**: [CONSTITUTION_VERSION] | **Ratified**: [RATIFICATION_DATE] | **Last Amended**: [LAST_AMENDED_DATE]
<!-- 例: Version: 2.1.1 | Ratified: 2025-06-13 | Last Amended: 2025-07-16 -->
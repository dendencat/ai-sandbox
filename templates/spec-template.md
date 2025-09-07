# Feature Specification: [FEATURE NAME]

**Feature Branch**: `[###-feature-name]`  
**Created**: [DATE]  
**Status**: Draft  
**Input**: User description: "$ARGUMENTS"

## Execution Flow (main)
```
1. 入力からユーザーの説明を解析
   → 空の場合: ERROR "機能の説明が提供されていません"
2. 説明から主要な概念を抽出
   → 識別: アクター、アクション、データ、制約
3. 各不明な側面について:
   → [NEEDS CLARIFICATION: 具体的な質問] でマーク
4. ユーザーシナリオとテストセクションを埋める
   → 明確なユーザーフローがない場合: ERROR "ユーザーシナリオを決定できません"
5. 機能要件を生成
   → 各要件はテスト可能でなければならない
   → 曖昧な要件をマーク
6. キーエンティティを特定 (データが関わる場合)
7. レビューチェックリストを実行
   → [NEEDS CLARIFICATION]がある場合: WARN "仕様に不確実性があります"
   → 実装の詳細が見つかった場合: ERROR "技術的な詳細を削除してください"
8. 戻る: SUCCESS (計画のための仕様が準備完了)
```

---

## ⚡ Quick Guidelines
- ✅ ユーザーが何を必要とし、なぜかを重視
- ❌ どのように実装するかを避ける (技術スタック、API、コード構造なし)
- 👥 ビジネスステークホルダー向けに書かれ、開発者向けではない

### Section Requirements
- **Mandatory sections**: すべての機能で完了する必要があります
- **Optional sections**: 機能に関連する場合のみ含める
- セクションが適用されない場合、完全に削除する ("N/A" のままにしない)

### For AI Generation
When creating this spec from a user prompt:
1. **Mark all ambiguities**: 必要とする仮定に対して [NEEDS CLARIFICATION: 具体的な質問] を使用
2. **Don't guess**: プロンプトが何かを指定していない場合 (例: 認証方法なしの "ログインシステム")、マークする
3. **Think like a tester**: すべての曖昧な要件は "テスト可能で曖昧でない" チェックリスト項目に失敗するはず
4. **Common underspecified areas**:
   - ユーザータイプと権限
   - データ保持/削除ポリシー
   - パフォーマンスターゲットとスケール
   - エラーハンドリング動作
   - 統合要件
   - セキュリティ/コンプライアンスニーズ

---

## User Scenarios & Testing *(mandatory)*

### Primary User Story
[メインのユーザー体験を平易な言葉で記述]

### Acceptance Scenarios
1. **Given** [初期状態], **When** [アクション], **Then** [期待される結果]
2. **Given** [初期状態], **When** [アクション], **Then** [期待される結果]

### Edge Cases
- [境界条件] の場合、何が起こるか?
- システムは [エラーシナリオ] をどのように処理するか?

## Requirements *(mandatory)*

### Functional Requirements
- **FR-001**: システムは [特定の機能、例: "ユーザーがアカウントを作成できるようにする"] をしなければならない
- **FR-002**: システムは [特定の機能、例: "メールアドレスを検証する"] をしなければならない
- **FR-003**: ユーザーは [主要なインタラクション、例: "パスワードをリセットする"] ことができる必要がある
- **FR-004**: システムは [データ要件、例: "ユーザーの設定を保持する"] をしなければならない
- **FR-005**: システムは [動作、例: "すべてのセキュリティイベントをログに記録する"] をしなければならない

*曖昧な要件をマークする例:*
- **FR-006**: システムは [NEEDS CLARIFICATION: 認証方法が指定されていない - email/password, SSO, OAuth?] を介してユーザーを認証しなければならない
- **FR-007**: システムは [NEEDS CLARIFICATION: 保持期間が指定されていない] の間ユーザーデータを保持しなければならない

### Key Entities *(include if feature involves data)*
- **[Entity 1]**: [何を表すか、実装なしの主要な属性]
- **[Entity 2]**: [何を表すか、他のエンティティとの関係]

---

## Review & Acceptance Checklist
*GATE: main() 実行中に自動チェックが実行されます*

### Content Quality
- [ ] 実装の詳細なし (言語、フレームワーク、API)
- [ ] ユーザー価値とビジネスニーズに焦点を当てた
- [ ] 非技術的なステークホルダー向けに書かれた
- [ ] すべての必須セクションが完了

### Requirement Completeness
- [ ] [NEEDS CLARIFICATION] マーカーが残っていない
- [ ] 要件はテスト可能で曖昧でない
- [ ] 成功基準は測定可能
- [ ] スコープは明確に境界付けられている
- [ ] 依存関係と仮定が特定されている

---

## Execution Status
*処理中に main() によって更新されます*

- [ ] ユーザーの説明が解析された
- [ ] 主要な概念が抽出された
- [ ] 曖昧さがマークされた
- [ ] ユーザーシナリオが定義された
- [ ] 要件が生成された
- [ ] エンティティが特定された
- [ ] レビューチェックリストが合格

---


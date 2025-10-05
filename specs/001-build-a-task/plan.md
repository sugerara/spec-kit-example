
# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

## Execution Flow (/plan command scope)
```
1. Load feature spec from Input path
   → If not found: ERROR "No feature spec at {path}"
2. Fill Technical Context (scan for NEEDS CLARIFICATION)
   → Detect Project Type from file system structure or context (web=frontend+backend, mobile=app+api)
   → Set Structure Decision based on project type
3. Fill the Constitution Check section based on the content of the constitution document.
4. Evaluate Constitution Check section below
   → If violations exist: Document in Complexity Tracking
   → If no justification possible: ERROR "Simplify approach first"
   → Update Progress Tracking: Initial Constitution Check
5. Execute Phase 0 → research.md
   → If NEEDS CLARIFICATION remain: ERROR "Resolve unknowns"
6. Execute Phase 1 → contracts, data-model.md, quickstart.md, agent-specific template file (e.g., `CLAUDE.md` for Claude Code, `.github/copilot-instructions.md` for GitHub Copilot, `GEMINI.md` for Gemini CLI, `QWEN.md` for Qwen Code, or `AGENTS.md` for all other agents).
7. Re-evaluate Constitution Check section
   → If new violations: Refactor design, return to Phase 1
   → Update Progress Tracking: Post-Design Constitution Check
8. Plan Phase 2 → Describe task generation approach (DO NOT create tasks.md)
9. STOP - Ready for /tasks command
```

**IMPORTANT**: The /plan command STOPS at step 7. Phases 2-4 are executed by other commands:
- Phase 2: /tasks command creates tasks.md
- Phase 3-4: Implementation execution (manual or via tools)

## Summary
````markdown
# 実装計画: [FEATURE]

**Branch**: `[###-feature-name]` | **日付**: [DATE] | **Spec**: [link]
**入力**: 機能仕様（`/specs/[###-feature-name]/spec.md` から）

## 実行フロー（/plan コマンドの範囲）
```
1. 入力パスから機能仕様を読み込む
   → 見つからない場合: ERROR "No feature spec at {path}"
2. 技術コンテキストを埋める（NEEDS CLARIFICATION をスキャン）
   → ファイル構成やコンテキストからプロジェクトタイプを検出（web=frontend+backend, mobile=app+api）
   → プロジェクトタイプに基づき構成方針を決定
3. 憲法（constitution）ドキュメントの内容に基づき Constitution Check セクションを埋める
4. 以下の Constitution Check セクションを評価
   → 違反がある場合: Complexity Tracking に記録
   → 正当化できない場合: ERROR "Simplify approach first"
   → 進捗トラッキングを更新: Initial Constitution Check
5. フェーズ0 を実行 → research.md を生成
   → NEEDS CLARIFICATION が残る場合: ERROR "Resolve unknowns"
6. フェーズ1 を実行 → contracts, data-model.md, quickstart.md, agent 固有テンプレート（例: `CLAUDE.md`, `.github/copilot-instructions.md`, `GEMINI.md`, `QWEN.md`, または `AGENTS.md`）
7. Constitution Check を再評価
   → 新たな違反があれば: 設計をリファクタし、フェーズ1 に戻る
   → 進捗トラッキングを更新: Post-Design Constitution Check
8. フェーズ2 を計画 → タスク生成アプローチを記述（注意: tasks.md は作らない）
9. 停止 - /tasks コマンドの準備完了
```

**重要**: /plan コマンドはステップ7で停止します。フェーズ2-4 は別のコマンドで実行されます:
- フェーズ2: `/tasks` コマンドが `tasks.md` を生成
- フェーズ3-4: 実装の実行（手動またはツールを使用）

## 要約
[機能仕様から抽出: 主要要件 + 調査に基づく技術方針]

## 技術コンテキスト
**言語/バージョン**: React + TypeScript (フロントエンド), Node.js (バックエンド)
**主要依存関係**: React, TypeScript, Node.js, express/fastify 等, PostgreSQL
**ストレージ**: PostgreSQL
**テスト**: ユニット: jest / vitest、統合: supertest / Playwright（NEEDS CLARIFICATION で選定確定）
**ターゲットプラットフォーム**: Web (Desktop, Mobile browsers) + iOS/Android（モバイルサポート）
**プロジェクトタイプ**: web + mobile
**パフォーマンス目標**: [NEEDS CLARIFICATION]
**制約**: リアルタイム要件（低レイテンシ）とオフライン同期待ち合わせ（NEEDS CLARIFICATION）
**スケール/範囲**: [NEEDS CLARIFICATION]

## 憲法チェック
*GATE: フェーズ0 調査前に合格する必要があります。フェーズ1 設計後に再チェックします。*

[憲法ファイルに基づき決定されるゲート]

## プロジェクト構成

### ドキュメント（この機能）
```
specs/[###-feature]/
├── plan.md              # このファイル（/plan コマンド出力）
├── research.md          # フェーズ0 出力（/plan コマンド）
├── data-model.md        # フェーズ1 出力（/plan コマンド）
├── quickstart.md        # フェーズ1 出力（/plan コマンド）
├── contracts/           # フェーズ1 出力（/plan コマンド）
└── tasks.md             # フェーズ2 出力（/tasks コマンド - /plan では作成しない）
```

### ソースコード（リポジトリルート）
<!--
  ACTION REQUIRED: 下のプレースホルダツリーをこの機能用の具体的構成に置換してください。
  不要なオプションは削除し、選択した構成を実際のパスで展開してください（例: apps/admin, packages/something）。
  返却される計画に Option ラベルを含めないでください。
-->
```
# フロントエンド + バックエンド構成（推奨）
frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

shared/
└── types/ (共有型定義や契約)
```

**構成方針**: Web フロントエンド（React + TypeScript）と Node.js バックエンドを分離した標準的な
フロントバック構成を採用します。共有型は `shared/types` に配置し、契約に基づく型安全性を確保します。

## フェーズ0: 概要と調査
1. **技術コンテキストから不明点を抽出**:
   - 各 NEEDS CLARIFICATION → 調査タスク
   - 各依存 → ベストプラクティス調査タスク
   - 各統合 → パターン調査タスク

2. **調査エージェントの生成と起動**:
```
For each unknown in Technical Context:
  Task: "Research {unknown} for {feature context}"
For each technology choice:
  Task: "Find best practices for {tech} in {domain}"
```

3. **調査結果を `research.md` に統合**（フォーマット）:
   - Decision: [選択した案]
   - Rationale: [選択理由]
   - Alternatives considered: [検討した代替案]

**出力**: 全ての NEEDS CLARIFICATION が解決された `research.md`

## フェーズ1: 設計と契約
*前提: `research.md` 完了*

1. **機能仕様からエンティティを抽出** → `data-model.md`:
   - エンティティ名、フィールド、リレーション
   - 要件に基づくバリデーションルール
   - 状態遷移（該当する場合）

2. **機能要件から API 契約を生成**:
   - 各ユーザー操作 → エンドポイント
   - 標準的な REST / GraphQL パターンを使用
   - OpenAPI / GraphQL スキーマを `/contracts/` に出力

3. **契約テストを生成**:
   - エンドポイントごとにテストファイルを作成
   - リクエスト/レスポンススキーマを検証
   - 実装が未完のためテストは失敗する想定

4. **ユーザーストーリーからテストシナリオを抽出**:
   - 各ストーリー → 統合テストシナリオ
   - Quickstart テスト = ストーリーの検証手順

5. **エージェント用ファイルを段階的に更新** (O(1) 操作):
   - `.specify/scripts/bash/update-agent-context.sh copilot` を実行
     **重要**: 上記の通り正確に実行してください。引数を追加・削除しないでください。
   - 既存ファイルがある場合は今回の技術のみを追加
   - 手動の追記部分は保持する
   - 変更履歴は直近3件を反映
   - 出力はリポジトリルート

**出力**: `data-model.md`, `/contracts/*`, 失敗するテスト群, `quickstart.md`, エージェント固有ファイル

## フェーズ2: タスク計画アプローチ
*このセクションは /tasks コマンドの動作を説明します - /plan 中に tasks.md を作成しないでください*

**タスク生成戦略**:
- `.specify/templates/tasks-template.md` をベースに読み込む
- フェーズ1 の設計ドキュメント（contracts, data model, quickstart）からタスクを生成
- 各契約 → 契約テストタスク [P]
- 各エンティティ → モデル作成タスク [P]
- 各ユーザーストーリー → 統合テストタスク
- テストをパスさせるための実装タスク

**並び順戦略**:
- TDD 順: テストの先行作成 → 実装
- 依存順: モデル → サービス → UI
- [P] のタスクは並列実行可（異なるファイル）

**想定出力**: `tasks.md` に 25-30 件程度の番号付きタスク

**重要**: フェーズ2 は `/tasks` コマンドで実行されるため、ここでは説明のみに留めます

## フェーズ3+: 将来の実装
*これらのフェーズは /plan コマンドの範囲外です*

**フェーズ3**: タスク実行（/tasks コマンドが tasks.md を生成）
**フェーズ4**: 実装（tasks.md の指示に従って実装を行う）
**フェーズ5**: 検証（テスト実行、quickstart.md の検証、性能検証）

## 複雑性の追跡
*憲法チェックで正当化が必要な違反がある場合のみ記入してください*

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |


## 進捗トラッキング
*このチェックリストは実行フロー中に更新されます*

**フェーズ状況**:
- [ ] Phase 0: Research complete (/plan command)
- [ ] Phase 1: Design complete (/plan command)
- [ ] Phase 2: Task planning complete (/plan command - describe approach only)
- [ ] Phase 3: Tasks generated (/tasks command)
- [ ] Phase 4: Implementation complete
- [ ] Phase 5: Validation passed

**ゲート状況**:
- [ ] Initial Constitution Check: PASS
- [ ] Post-Design Constitution Check: PASS
- [ ] All NEEDS CLARIFICATION resolved
- [ ] Complexity deviations documented

---
*Based on Constitution v2.1.1 - See `/memory/constitution.md`*

```
   - リクエスト/レスポンススキーマを検証

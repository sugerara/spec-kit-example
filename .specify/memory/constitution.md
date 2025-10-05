<!--
Sync Impact Report

- Version change: template -> 0.1.0
- Modified principles:
	- [PRINCIPLE_1_NAME] -> Library-First
	- [PRINCIPLE_2_NAME] -> CLI Interface
	- [PRINCIPLE_3_NAME] -> Test-First (NON-NEGOTIABLE)
	- [PRINCIPLE_4_NAME] -> Integration Testing
	- [PRINCIPLE_5_NAME] -> Observability & Versioning
- Added sections: Filled `Additional Constraints` and `Development Workflow`
- Removed sections: none
- Templates reviewed (checked for alignment):
	- .specify/templates/plan-template.md ✅ checked
	- .specify/templates/spec-template.md ✅ checked
	- .specify/templates/tasks-template.md ✅ checked
	- .specify/templates/agent-file-template.md ✅ checked
	- .specify/templates/commands/*.md ⚠ pending (no command files present)
- Runtime docs:
	- README.md ⚠ missing - create or update README with constitution reference
- Follow-up TODOs:
	- RATIFICATION_DATE: TODO(RATIFICATION_DATE): please confirm the original adoption date of this constitution
	- Verify agent-specific command files (if added) do not reference vendor-specific agent names
-->

```markdown
# spec-kit-example 憲法

## 中核となる原則

### ライブラリ第一（Library-First）
すべての機能は独立したライブラリとして開始されます。ライブラリは自己完結し、独立して
テスト可能で、文書化されていなければなりません。各ライブラリは明確で単一の目的を持つ
ことが必須です。組織専用のライブラリは、Complexity Tracking に記録され明示的に承認され
ない限り禁止されます。

### CLI インターフェイス
プロジェクトのツールやライブラリは、可能な場合コマンドラインインターフェイス（CLI）を通じ
て機能を公開するべきです。テキスト I/O のプロトコルは stdin/args → stdout、エラー → stderr
に従う必要があります。出力は自動化向けの JSON と、デバッグ向けの人間可読形式の両方を
サポートしなければなりません。

### テストファースト（Test-First, 非交渉）
テスト駆動開発（TDD）は必須です：テストは実装前に作成・コミットされなければなりません。
テストは初めは失敗している必要があり、その後実装を行ってテストを通す（Red-Green-Refactor）
流れを踏襲します。本原則は本番向けコードや重要なスクリプトに対して非交渉的です。

### 統合テスト
統合テストは、ライブラリ契約、契約変更、サービス間通信、および共有スキーマをカバーしなけ
ればなりません。プロジェクト横断的、またはランタイム挙動に影響する変更には、適切な統合
テストの追加が必須です。

### 可観測性とバージョニング
本番で稼働するコンポーネントは構造化ログおよび文脈情報付きのエラーデータを提供する必要が
あります。運用性が実質的に向上する場合、メトリクスやトレーシングを追加するべきです。リリース
はセマンティックバージョニングに従い、破壊的変更はガバナンスに従った移行手順を必ず実施してく
ださい。

## 追加制約
技術選定や制約は各機能の `plan.md` に記録することが必須です。既定と要件は次の通りです：

- シェル自動化: 自動化スクリプトは POSIX 互換の Bash を標準とします。
- プロトコル: 構造化交換には JSON を用いるテキスト I/O を優先します。
- セキュリティおよびコンプライアンス要件は `plan.md` に明記し、Phase 0 で解決してください。

不明な制約がある場合は、`plan.md` に `TODO` と記載して Phase 0 の調査で解決してください。

## 開発ワークフロー
- `src/`, `scripts/`, `.specify/` に対する変更はコードレビューを必須とします。
- プルリクエストには短い「Constitution Check」要約と、準拠を示す該当する plan/spec の参照を含
	む必要があります。
- 複雑性の例外は Complexity Tracking に記録し、少なくとも一名のシニアメンテナーの承認を得る
	必要があります。
- リリースは `vMAJOR.MINOR.PATCH` のタグを使用し、破壊的変更には移行ガイダンスを含む変更履歴
	を必ず添付してください。

## ガバナンス
この憲法はプロジェクトの規範、最低要件、および改訂手順に関する最終的な根拠です。改訂は以下の
セマンティックルールに従って行います。

改訂手順：
1. 憲法（`.specify/memory/constitution.md`）を更新する PR を作成し、理由と移行計画を添えること。
2. 変更を分類する：MAJOR（原則の削除や意味の再定義）、MINOR（新しい原則または実質的な追記）、
	 PATCH（文言の明確化、誤字修正など）。
3. 少なくとも2名のレビュアー（うち1名はメンテナー）の承認を得ること。
4. マージ後に最終改定日を更新すること。

バージョニング方針：
- MAJOR: ガバナンスや原則の後方互換性を壊す変更／再定義。
- MINOR: 新しい原則や実質的なガイダンスの追加。
- PATCH: 文言の明確化、誤字訂正、非意味的な微修正。

コンプライアンスレビューの期待：
- 本番挙動に影響を与える PR には必ず Constitution Check の要約を含めること。
- CI は可能な範囲で自動化された Constitution Check（フォーマット、準拠声明の存在等）を検証
	することが望ましい。

**バージョン**: 0.1.0 | **採択日**: 2025-10-05 | **最終改定**: 2025-10-05
```

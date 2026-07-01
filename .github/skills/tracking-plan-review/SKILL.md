---
name: tracking-plan-review
description: Design, review, and output BTCC/Sensors event tracking plans based on the Lark field-level tracking-plan instruction workbook and 神策自定义埋点事件采集提需模板. Use when Codex needs to create 埋点方案, produce an Excel 提需模板, define events/event properties/user properties, review teammates' 埋点方案, audit naming/trigger/upload/platform/version fields, or convert PRD/product flows into behavior analytics tracking requirements for CEX, BI, funnels, dashboards, or user behavior analysis.
---

# Tracking Plan Review

## Overview

Use this skill to design, audit, and output BTCC 埋点方案 according to:

- Field-level rules from `BTCC_埋点方案文档填写说明（字段级说明）.xlsx`, extracted in `references/field-rules.md`.
- The generic deliverable workbook template `assets/sensors-custom-event-request-template.xlsx`, documented in `references/output-template.md`.
- The business-scenario deliverable workbook template `assets/business-scenario-sensors-tracking-template.xlsx`, documented in `references/output-template.md`.

## Workflow

1. Determine whether the task is design, review, revision, or Excel template output.
2. Read `references/field-rules.md` before judging or generating field-level content.
3. Read `references/output-template.md` when the user asks for a final 提需模板, Excel deliverable, 神策导入表, or a table intended to be pasted into that template.
4. Separate event/event-property requirements from logged-in user ID/user-property requirements.
5. Anchor events to real product flow, PRD steps, modules, and user behavior triggers.
6. Design for downstream BI, funnels, dashboards, user behavior analysis, and governance reuse.
7. Return structured output in Chinese unless the user asks otherwise.

## Design Mode

When creating a tracking plan:

- Start from business goal, page/module, user action, and trigger timing.
- Merge redundant events when the same behavior appears in multiple pages and can be distinguished by event properties.
- Prefer reusable event properties for common dimensions such as source page, entry, button, position, result, error reason, country, channel, order/trade/deposit context.
- Choose upload method by accuracy needs: server-side for key result events, front-end for PV/exposure/click/UI interaction events.
- Mark platform scope clearly for Android, iOS, Web/JavaScript, mini program, or server-side.
- Include screenshots or screenshot requirements when UI location, button position, category hierarchy, or version context may be ambiguous.
- If the user wants an Excel deliverable, choose the matching workbook template and use the columns and sheet rules from `references/output-template.md`.

## Excel Output Mode

When producing a final 神策埋点提需模板:

- Copy `assets/sensors-custom-event-request-template.xlsx` for a generic/simple plan, or `assets/business-scenario-sensors-tracking-template.xlsx` when the request benefits from a richer scenario template with event rows, reusable property dictionary, traffic-slot/location dictionary, APP page dictionary, or logged-in user profile examples. Use judgment based on the business scenario and downstream analysis needs, not only on the module name.
- Preserve the selected template's sheets, styling, merged cells, validations, and guidance text.
- Populate the main `（埋点事件+事件级变量）` sheet with one row per event-property binding.
- Add all used event properties to `事件级属性列表`; avoid duplicating equivalent reusable properties.
- Put logged-in user ID and user profile attributes in the login-user sheet, not in the event-property sheet. Some templates name it `登录用户ID&登录用户变量（可不填）`; the business-scenario template names it `登录用户ID&登录用户变量`.
- Update `change_long` with the plan version and summary of added/changed/deprecated events or properties.
- Before delivery, verify required fields are filled, dropdown values are valid, and the main sheet has no event property missing from `事件级属性列表`.

## Review Mode

When reviewing a teammate's plan, return:

- Overall verdict: `通过`, `需修改后通过`, or `不通过`.
- Critical blockers: missing required fields, duplicate/invalid identifiers, unclear triggers, wrong upload method, unusable property type, or missing platform scope.
- Issue table: `字段/问题/影响/建议改法/优先级`.
- Governance suggestions: event merging, property reuse, value enumeration, naming consistency, screenshots, version tracking, and owner traceability.
- Revised examples: provide corrected identifiers, names, descriptions, property types, value examples, or trigger wording where helpful.
- If the reviewed artifact is in the 神策提需模板, also check sheet integrity: main-sheet fields, property dictionary coverage, user-property placement, change log, screenshot placeholders, and platform/dropdown values.

## Severity

- Critical: causes data not to collect, collect at wrong time, become impossible to analyze, or break unique identifier governance.
- Major: causes ambiguous implementation, hard-to-filter data, poor metric reuse, or weak iteration traceability.
- Minor: affects clarity, naming polish, or implementation convenience without blocking data validity.

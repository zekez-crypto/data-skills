# 神策自定义埋点事件采集提需模板

Use this reference when the user asks for a deliverable 埋点方案, 提需模板, Excel output, 神策导入表, or anything that should be written into the bundled workbook template.

Source assets:

- Generic template: `assets/sensors-custom-event-request-template.xlsx`
- Business-scenario template: `assets/business-scenario-sensors-tracking-template.xlsx`

Use the generic template for simple or clean-slate deliverables. Use the business-scenario template when the request benefits from a richer workbook with example event rows, reusable property dictionary, traffic-slot/location dictionary, APP page dictionary, or logged-in user profile examples. Decide by the structure needed for implementation and analysis, not only by the module name.

## Workbook Structure

Keep these sheets and their purposes:

| Sheet | Purpose |
|---|---|
| `change_long` | Version change log. Record every event/property add, delete, definition change, or naming change. |
| `BTCC埋点介绍` | Usage notes. Usually keep unchanged unless the user asks to revise instructions. |
| `用户运营_弹窗TOAST曝光（埋点事件+事件级变量）` | Main event and event-property binding sheet. Rename the sheet to match the feature or business module when producing a new plan, but keep the suffix `（埋点事件+事件级变量）`. |
| `事件级属性列表` | Dictionary of reusable event properties. Every new event property used in the main sheet must appear here. |
| `登录用户ID&登录用户变量（可不填）` | Logged-in user ID and user properties. Fill only when the plan needs user profile properties or ID setup. |

## Business-Scenario Template Structure

Asset: `assets/business-scenario-sensors-tracking-template.xlsx`

Source example: `交易运营-神策埋点需求 (1).xlsx`. Although the included sheet names come from a trading-operations plan, this template can be reused for other scenarios with similar tracking-plan needs. Rename scenario-specific sheets when appropriate while preserving the workbook structure and guidance.

Keep these sheets and their purposes:

| Sheet | Purpose |
|---|---|
| `change_long` | Version change log. Row 1 is guidance; append version rows with version, change summary, and date. |
| `BTCC埋点介绍` | Usage notes. Usually keep unchanged. |
| `交易运营（埋点事件+事件级变量）` | Main event and event-property binding sheet from the source example. For other modules, rename to the business module while keeping the suffix `（埋点事件+事件级变量）`. |
| `流量位说明-首页` | Traffic-slot or location dictionary. Use for dimensions such as `area_var`, `position_var`, `trafficName_var`, `trafficID_var`, screenshots, and placement remarks; rename if the scenario is not homepage traffic. |
| `APP页面说明` | APP/page dictionary. Use for `pageType_var`, `pageName_var`, and page screenshot references; can also serve as a page/module mapping sheet for non-APP scenarios. |
| `登录用户ID&登录用户变量` | Logged-in user ID and user properties. Fill only when the plan needs user profile properties or ID setup. |
| `事件级属性列表` | Dictionary of reusable event properties. Every event property used in the main sheet must appear here. |

In the business-scenario template, the main sheet starts data rows at row 3 and uses the same main event columns A-M as the generic template. It may contain example rows; update, append, or clear rows according to the user's requested output while preserving useful headers, validations, widths, and guidance text.

Template residue cleanup is mandatory for every final Excel deliverable:

- Remove inherited screenshots, image objects, charts, shapes, or other drawings from the template unless the user explicitly asks to keep them.
- Do not keep template example screenshots as placeholders. Use text placeholders such as `待补充：APP截图/位置标注` and `待补充：Web截图/位置标注` unless real feature screenshots are intentionally inserted.
- Clear template sample rows that are not part of the requested plan.
- Unmerge populated data rows and dictionary rows so each row can be filtered, sorted, copied, and maintained independently. Keep only intentional header merges such as the main instruction row or screenshot header spanning APP/Web columns.
- Check that old template formatting does not make new content unreadable, hidden, clipped, or visually misleading. If needed, clear data-area formats and reapply simple readable formatting.

## Main Event Sheet Columns

The main sheet starts data rows at row 3. Preserve row 1 instructions and row 2 headers.

| Column | Header | Fill Rule |
|---|---|---|
| A | `序号` | Continuous integer sequence. Each event-property binding occupies one row, so one event with 3 properties has 3 sequence rows. |
| B | `app端对应截图（埋点涉及到哪个端就截哪个图）` | Screenshot or placeholder. If not available, write `待补充：APP截图/位置标注`. |
| C | `web端对应截图（埋点涉及到哪个端就截哪个图）` | Screenshot or placeholder. If not available, write `待补充：Web截图/位置标注`. |
| D | `事件英文名称` | Event identifier. Follow `field-rules.md` identifier rules. Template examples use snake/lower camel with action suffixes such as `_view`, `_click`, `_submit`, `_success`, `_fail`; keep one convention per workbook. |
| E | `事件中文名称` | Chinese event name, max 30 chars, aligned with the identifier and actual UI action. |
| F | `属性英文名称` | Event property identifier. Must already exist in `事件级属性列表`; if the event has no property, fill `#`. |
| G | `属性中文名称` | Chinese property name. If no property, fill `#`. |
| H | `数据格式` | One of `Bool`, `String`, `Datetime`, `List`, `Number`. Use `String` for dimension-like codes, page names, positions, and enums unless numeric aggregation is required. |
| I | `属性值示例枚举或说明` | Enumerate known values or provide clear examples. For non-exhaustive values, include examples plus `等`. For positions, state whether numbering starts from 1. |
| J | `上传方式（前端、后端）` | Use `前端` for PV, exposure, click, UI interaction; use `后端` for critical result events requiring accuracy, such as registration success, payment success, order completion, deposit/withdraw result. |
| K | `事件触发时机` | Clear trigger condition. Distinguish exposure/click/submit/success/fail. If multiple triggers share one event, list them and state `或`/`且`. |
| L | `应埋点平台（JavaScript指代web端）` | Use `Android`, `iOS`, `JavaScript`, `小程序`, or `服务端`; list all applicable platforms. |
| M | `备注信息` | Optional implementation notes, dependencies, owner, version, or pending confirmation. |

## Event Property Dictionary

Sheet: `事件级属性列表`

Required columns:

| Column | Header | Fill Rule |
|---|---|---|
| A | `属性英文名称*` | Unique event property identifier. Prefer reusable properties such as `pageName_var`, `sourcePage_var`, `buttonName_var`, `position_var`, `result_var`, `errorReason_var`. New properties must follow the `_var` suffix rule. |
| B | `属性中文名称*` | Chinese property name aligned with the English identifier. |

Rules:

- Before adding a new property, check whether a semantically equivalent property already exists.
- The main event sheet must not reference properties missing from this dictionary.
- Keep existing reusable properties unless the user explicitly asks to clean the dictionary. For a cleaner deliverable, it is acceptable to keep only properties used by the current plan plus newly defined properties.

## Logged-In User ID And User Properties

Sheet: `登录用户ID&登录用户变量（可不填）` in the generic template, or `登录用户ID&登录用户变量` in the business-scenario template.

Use this sheet when the request includes user attributes, profile properties, ID mapping, segmentation tags, VIP/KYC/channel/invite/KOL attributes, or other values that should be set on the user profile rather than attached to a single event.

Data starts at row 7:

| Column | Header | Fill Rule |
|---|---|---|
| A | `标识符*` | User property identifier. Use `_ppl` suffix for non-preset properties. |
| B | `名称*` | Chinese user property name. |
| C | `字段类型*` | One of `字符串`, `整数`, `日期`. |
| D | `描述` | Value examples or enum definition. |
| E | `触发时机` | Usually `登录时获取`, `每次打开客户端时...`, `后台标签导入`, or `用户登录时或此变量值发生变化时触发`, depending on source. |
| F | `备注` | Optional implementation/source notes. |
| G | `埋点优先级` | `高`, `中`, or `低`. |

## Change Log

Sheet: `change_long`

- Row 1 is the instruction. Keep it.
- Append version rows with `版本` and `调整项`.
- Use `v1.0` for a new plan unless the user provides an existing version.
- Mention added/changed/deprecated events and properties, and any user-property changes.

## Output Behavior

When asked to produce a final Excel deliverable:

1. Copy the selected source template to the requested output location: use `assets/sensors-custom-event-request-template.xlsx` for a generic/simple plan, or `assets/business-scenario-sensors-tracking-template.xlsx` for a richer scenario plan.
2. Rename the main event sheet to the business module if helpful, keeping `（埋点事件+事件级变量）`. In the business-scenario template, rename `交易运营（埋点事件+事件级变量）` when the output is for another module.
3. Clear or update sample rows from the main event sheet after preserving headers, validations, merges, widths, and styling. For scenario-template outputs, keep useful existing example rows only when they are part of the requested plan.
4. Populate rows from the designed tracking plan.
5. Add every used event property to `事件级属性列表`, including reused and newly defined properties.
6. Fill the login-user sheet only when user properties are needed; otherwise keep the sheet and its guidance intact.
7. Do not add, rename, or populate extra dictionary/page-description sheets by default, including scenario-specific `字典说明`, `流量位说明-首页`, `APP页面说明`, or `APP&Web页面说明`. Keep concise enum and page/source guidance in the main event sheet's `属性值示例枚举或说明` and `备注信息` columns. Only populate these extra sheets when the user explicitly asks for a dictionary/page mapping sheet, or when the plan has enough reusable page/location/traffic-slot values that a separate dictionary is necessary for implementation.
8. Remove inherited template images/drawings across all sheets unless explicitly requested; verify the exported workbook has no unintended `xl/media` or `xl/drawings` entries.
9. Unmerge populated data/dictionary ranges. Verify dictionary sheets such as page, location, traffic-slot, property dictionary, and user-property sheets do not contain nonessential merged cells.
10. Extend data validations when populated rows exceed the template's sample validation ranges, especially `数据格式`, `应埋点平台`, and user-property `字段类型`.
11. Update `change_long`.
12. Visually or structurally verify that headers remain, required fields are populated, dropdown values are valid, the main sheet does not reference missing properties, template example screenshots are not retained, and populated rows remain readable and filterable.

If the user asks only for a Markdown plan or review, do not create an Excel file unless explicitly requested. Still follow these columns when presenting a table meant to be pasted into the template.

# 神策自定义埋点事件采集提需模板

Use this reference when the user asks for a deliverable 埋点方案, 提需模板, Excel output, 神策导入表, or anything that should be written into the bundled workbook template.

Source asset: `assets/sensors-custom-event-request-template.xlsx`

## Workbook Structure

Keep these sheets and their purposes:

| Sheet | Purpose |
|---|---|
| `change_long` | Version change log. Record every event/property add, delete, definition change, or naming change. |
| `BTCC埋点介绍` | Usage notes. Usually keep unchanged unless the user asks to revise instructions. |
| `用户运营_弹窗TOAST曝光（埋点事件+事件级变量）` | Main event and event-property binding sheet. Rename the sheet to match the feature or business module when producing a new plan, but keep the suffix `（埋点事件+事件级变量）`. |
| `事件级属性列表` | Dictionary of reusable event properties. Every new event property used in the main sheet must appear here. |
| `登录用户ID&登录用户变量（可不填）` | Logged-in user ID and user properties. Fill only when the plan needs user profile properties or ID setup. |

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

Sheet: `登录用户ID&登录用户变量（可不填）`

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

1. Copy `assets/sensors-custom-event-request-template.xlsx` to the requested output location.
2. Rename the main event sheet to the business module if helpful, keeping `（埋点事件+事件级变量）`.
3. Clear sample rows from the main event sheet after preserving headers, validations, merges, widths, and styling.
4. Populate rows from the designed tracking plan.
5. Add every used event property to `事件级属性列表`, including reused and newly defined properties.
6. Fill `登录用户ID&登录用户变量（可不填）` only when user properties are needed; otherwise keep the sheet and its guidance intact.
7. Extend data validations when populated rows exceed the template's sample validation ranges, especially `数据格式`, `应埋点平台`, and user-property `字段类型`.
8. Update `change_long`.
9. Visually or structurally verify that headers remain, required fields are populated, dropdown values are valid, and the main sheet does not reference missing properties.

If the user asks only for a Markdown plan or review, do not create an Excel file unless explicitly requested. Still follow these columns when presenting a table meant to be pasted into the template.

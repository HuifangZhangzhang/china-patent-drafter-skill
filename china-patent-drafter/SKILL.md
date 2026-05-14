---
name: china-patent-drafter
description: Use when the user asks to write, draft, optimize, review, package, or generate Chinese invention patent materials, Chinese patents, invention patents, patent specifications, claims, abstracts, embodiments, abstract drawings, final Word/DOCX patent documents, editable equations, or complete patent application files from a technical solution, innovation point, experiment result, program logic, calculation method, device structure, system architecture, algorithm, engineering process, cooling/heat-transfer/spray/LBM/nuclear thermal-hydraulic scenario, or application use case.
---

# China Patent Drafter

Use this skill to turn a user's technical disclosure into a rigorous Chinese invention patent draft suitable for attorney review before CNIPA filing. Write in formal, engineering-oriented Chinese. Preserve the user's technical meaning, broaden protection where supportable, and never invent unprovided facts, measured data, material models, legal conclusions, filing outcomes, or novelty-search results.

This skill is a drafting aid, not a patent-agent or lawyer substitute. Every substantial output must remind the user that final filing documents should be reviewed by a qualified patent agent or patent lawyer.

## Core Deliverable

For a complete drafting request, output a full Chinese invention patent application draft with the following structure:

1. 发明名称
2. 摘要
3. 权利要求书
4. 说明书
   - 技术领域
   - 背景技术
   - 发明内容
     - 要解决的技术问题
     - 技术方案
     - 有益效果
   - 附图说明
   - 具体实施方式
5. 摘要图
6. 可进一步强化的保护点建议
7. 专业审查提示

For a complete final-delivery request, also generate a final `.docx` Word document, not only Markdown text. The final Word version should include the same patent content plus all required figures, result plots, captions, figure-number references, and editable equations when formulas are involved.

Default file layout for complete deliverables:

```text
temp/patent_documents/<invention_slug>/<invention_slug>_draft.md
temp/patent_documents/<invention_slug>/<invention_slug>_final.docx
temp/patent_documents/<invention_slug>/figures/
temp/patent_documents/<invention_slug>/scripts/
temp/patent_documents/<invention_slug>/rendered_pages/
```

If the user asks only for claims, abstract, optimization, or review, provide the requested part but still apply the same extraction, support, and non-fabrication rules.

## Default Workflow

### 1. Identify the Invention Disclosure

Before drafting, extract and display a compact analysis of the user's input. Use this table unless the user explicitly requests direct drafting only:

| 要素 | 识别结果 |
| --- | --- |
| 技术领域 | ... |
| 现有技术缺陷 | ... |
| 核心创新点 | ... |
| 技术方案组成 | ... |
| 关键步骤或结构 | ... |
| 可保护点 | ... |
| 可写入权利要求的技术特征 | ... |
| 已提供的实验/仿真/结果依据 | ... |
| 缺失但影响撰写的信息 | ... |

If key information is missing but the invention can still be drafted, proceed with cautious language such as“在一些实施例中”“可选地”“优选地”“参数可根据工况调节”。Use `[待确认]` only for factual gaps that cannot be safely generalized.

Ask questions only when a missing fact blocks the draft, such as the invention category, the essential technical mechanism, or whether a claim feature is actually part of the user's solution.

### 2. Choose Patent Categories

Default to a Chinese invention patent. Select one or more protection categories based on the disclosure:

- 方法类: process steps, control logic, simulation workflow, calculation method, manufacturing/operation method.
- 装置类: physical structure, components, connections, spatial arrangement, heat-transfer/cooling modules.
- 系统类: coordinated hardware, software, sensors, controllers, simulation platform, data pipeline.
- 程序/算法/计算模型类: computer-implemented method, model training/inference, numerical simulation, LBM solver, parameter optimizer.
- 存储介质/电子设备类: when software implementation is central and supportable.
- 应用场景类: use in spray cooling, droplet impact, reactor containment thermal-hydraulic analysis, safety evaluation, cooling optimization, or other industrial scenarios.

For broad protection, prefer covering method + device/system + computer-readable storage medium/electronic device when the technical disclosure supports them. Do not add categories that have no support in the user's disclosure.

### 3. Build the Claim Strategy First

Draft claims before finalizing the specification. The specification must support every claim term.

Requirements for the claim set:

- Generate at least 1 independent claim.
- Generate 6-12 dependent claims unless the user requests a different number or the disclosure is too thin.
- The independent claim should cover the core inventive concept without being narrowed to one prototype, one test condition, one exact parameter, or one implementation language.
- Dependent claims should progressively limit parameters, structures, steps, calculation relationships, control logic, materials, boundary conditions, working conditions, data sources, model modules, or application objects.
- For method patents, especially calculation, simulation, control, optimization, and algorithmic methods, the independent claim must recite concrete executable steps rather than only a desired function. Prefer step labels such as S1-S5 in the specification and mirror their essential features in Claim 1.
- For calculation-method patents, dependent claims should narrow input variables, preprocessing, governing equations or update rules, iterative convergence/stability criteria, parameter correction, output indicators, validation routes, or technical application objects.
- Use Chinese patent claim expressions such as“其特征在于”“根据权利要求1所述的……”“其中……”“还包括……”。
- Avoid pure result-only limitations. Pair each effect with a technical means or interaction.
- Avoid absolute wording such as“唯一”“必须”“完全消除”“必然提高”, unless the user provides exact legal/technical basis.
- Keep terms consistent with the specification and drawings.

Recommended claim hierarchy:

1. Claim 1: broad independent claim for the main method/device/system.
2. Claims 2-4: essential substeps, modules, or structural cooperation.
3. Claims 5-7: parameter ranges, thresholds, equations, heat-transfer/simulation/control relationships, or boundary conditions.
4. Claims 8-10: material, geometry, data pipeline, solver, controller, training/inference, or numerical implementation variants.
5. Claims 11-13, if needed: application scenario, storage medium, electronic device, or system claim.

When generating parallel independent claims, clearly separate them, for example:

- 一种……方法；
- 一种……装置，其包括用于执行所述方法的模块；
- 一种电子设备/计算机可读存储介质；
- 一种……系统。

Do this only when the disclosure supports those categories.

### 4. Draft the Full Patent Text

Use formal Chinese patent style. Avoid marketing language and conversational phrasing.

When the user asks for a final filing-style document, create both:

1. a readable drafting version in Markdown for quick review;
2. a final Word `.docx` version with formal patent-document ordering, headings, figures, equations, and result plots.

The Word version must at least include:

- 发明名称;
- 摘要;
- 权利要求书;
- 有益效果;
- 说明书, including 技术领域, 背景技术, 发明内容, 附图说明, and 具体实施方式/具体实施方案;
- 摘要图 and other necessary figures;
- result figures, tables, or implementation-result descriptions when the user provides or requests them;
- formulas, variables, and calculation relationships in editable equation form when possible.

#### 发明名称

Generate a concise title that reflects the technical subject and invention category, usually in the form:

- 一种……方法、装置、系统及存储介质
- 一种用于……的……控制方法及系统
- 一种基于……的……数值模拟方法
- 一种……喷雾冷却/液滴撞击/热工水力分析方法

Avoid overly narrow titles that lock the invention to one experiment, one software package, one material brand, or one exact parameter.

#### 摘要

The abstract must satisfy common Chinese patent application drafting expectations:

- Use concise Chinese prose, normally controlled within about 300 Chinese characters unless the user or current official requirements specify otherwise.
- State the technical field, technical problem, core technical solution, and main technical effect or use.
- Do not introduce content unsupported by the specification.
- Do not include advertising language, legal conclusions, claim numbering, undefined abbreviations, or unprovided measured results.
- If numerical results are provided by the user, state them cautiously and only as disclosed results.
- If results are not provided, describe mechanism-based effects, for example“有利于提高……稳定性”“可改善……均匀性”“便于实现……”。

After the abstract, specify the recommended abstract drawing as:

```text
摘要附图：图X
```

If no final drawing number exists yet, use“建议以图1作为摘要附图” and generate or describe 图1.

#### 权利要求书

Use numbered claims. Each claim should be one sentence where practical. Maintain Chinese claim grammar:

```text
1. 一种……方法，其特征在于，包括：
   ...

2. 根据权利要求1所述的……方法，其特征在于，……
```

Do not write claims as a research paper contribution list. Claims must define technical features and their cooperation.

#### 说明书

Write the specification to support the claims:

- 技术领域: one paragraph describing the relevant engineering/algorithmic field.
- 背景技术: describe known limitations without overstating novelty or attacking unidentified prior art too aggressively.
- 发明内容:
  - 要解决的技术问题: state objective technical problems, not commercial goals.
  - 技术方案: mirror and support the claim features, including alternatives.
  - 有益效果: connect feature -> mechanism -> effect; distinguish measured data from expected or theoretical effects.
- 附图说明: list each figure with a short title and, when useful, reference numerals.
- 具体实施方式: provide enabling embodiments, variants, parameter ranges, calculation logic, control flow, software implementation, or device structure. Use examples to support breadth, not to narrow the independent claim.

### 5. Generate the Abstract Drawing

For every complete patent draft, produce an abstract drawing plan and, when the environment supports file creation or image generation, generate at least one abstract drawing file.

For method patents, especially calculation-method patents, the abstract drawing should default to an implementation-step flowchart. The flowchart must correspond to the concrete steps in the independent claim and detailed embodiments, for example S1 input/acquisition, S2 preprocessing, S3 core calculation or model update, S4 judgment/iteration/control, and S5 output/application. Use another drawing type only when the user explicitly requests it or when a device/system structure is clearly the main invention.

Default abstract drawing choices:

- Method/algorithm: flowchart showing input, preprocessing, core calculation/control, output, and feedback.
- Device: structural block diagram or simplified sectional/schematic view with numbered components.
- System: architecture diagram showing modules, data flow, sensors, controller, execution unit, and output.
- Cooling/heat transfer/spray/droplet impact: schematic showing substrate/wall, liquid film or droplet/spray, heat source, sensor/solver/control components, and heat/mass transfer paths.
- LBM/numerical simulation: computational domain, boundary conditions, distribution functions/fields, collision-streaming-update loop, and output metrics.
- Reactor containment thermal-hydraulic analysis: containment region, heat source, condensation/spray/cooling paths, sensors, numerical analysis/control modules.

Drawing rules:

- Use clear black-and-white line art suitable for patent figures.
- Avoid decorative backgrounds, gradients, photorealism, brand marks, or unnecessary shading.
- Number key elements consistently, for example 100 system, 110 input module, 120 calculation module.
- For method and calculation-method flowcharts, number steps consistently, for example S1-S5 or 101-105, and ensure every box represents an implementable operation, not a vague goal.
- The abstract drawing for a method patent should show the implementation sequence, branching/iteration conditions, input/output, and optional feedback loop when present.
- Include a short“附图标记说明” in the specification when components are numbered.
- The abstract drawing should show the core inventive relationship, not every embodiment.

If using Python to generate a schematic, save both the code and output image in a project-local directory, preferably:

```text
temp/patent_figures/<invention_slug>/abstract_figure.py
temp/patent_figures/<invention_slug>/abstract_figure.png
```

If the user requests result plots, implementation demonstrations, parameter sweeps, or simulation-derived figures, also save reproducible Python code and outputs, for example:

```text
temp/patent_figures/<invention_slug>/result_plot.py
temp/patent_figures/<invention_slug>/result_plot.png
temp/patent_figures/<invention_slug>/README.txt
```

The code should:

- Use only disclosed or clearly labeled illustrative parameters.
- Mark generated values as“示例值” or“可选实施例参数” unless the user provided measured data.
- Avoid presenting synthetic plots as experimental evidence.
- Prefer `matplotlib` for flowcharts/schematics/result plots when available.
- Keep filenames ASCII and reproducible.

If file creation or plotting tools are not available, output:

1. a detailed abstract figure specification,
2. a Mermaid diagram or simple ASCII layout,
3. Python code that the user can run later.

### 6. Generate the Final Word Document

When a complete patent draft is requested, generate a final `.docx` document after the text and figures are ready. Use the local document-generation workflow available in the environment; if a Documents/DOCX skill or renderer is available, use it and render the result for visual QA.

Word document requirements:

- Use a clean formal patent style with clear Chinese headings and sequential numbering.
- Preserve the complete patent structure: 摘要, 权利要求书, 有益效果, 说明书, 技术领域, 背景技术, 发明内容, 附图说明, 具体实施方式/具体实施方案, figures, and result sections when applicable.
- Insert generated abstract drawings, flowcharts, result plots, and structural diagrams as actual images with captions and matching references in 附图说明 and 具体实施方式.
- Keep figure numbers, step numbers, claim terms, and component labels consistent across the Word file.
- Save the final Word file as `temp/patent_documents/<invention_slug>/<invention_slug>_final.docx`.
- Save image files and plotting scripts under the same document folder so the result is reproducible.
- Render the DOCX to page images when tools permit and inspect the pages before delivery. Fix clipping, missing glyphs, broken tables, unreadable formulas, overlapping images, or layout gaps before considering the Word version final.

Formula and equation requirements:

- Do not insert formulas as garbled text, mojibake, screenshots of text, or ambiguous plain strings.
- Prefer Word-native editable equations using Office Math Markup Language (OMML) or another Word equation-editor compatible representation.
- If MathType is available or explicitly requested, use a MathType-compatible equation format. If MathType is not available, use Word's built-in equation editor format rather than rasterizing formulas.
- Keep a readable plain-text explanation of each important formula near the equation when it improves clarity, but the formula itself should remain editable in Word whenever possible.
- For variables and symbols, define meanings, units, and optional ranges in the specification. Do not invent units or parameter values not supplied by the user.
- If the environment cannot create editable Word equations, clearly state the limitation and provide the equation source in LaTeX/MathML plus a non-garbled Word-safe fallback; do not silently ship corrupted equations.

### 7. Use Granted Patent References Carefully

When the user asks for filing-style formatting or when the expected structure is uncertain, consult official or reputable Chinese patent sources when network access is available. Suitable references include CNIPA patent publication/announcement resources, Chinese patent search platforms, and already granted Chinese invention patents in the relevant technical area.

Use granted patents only as formatting and drafting-style references:

- Study section ordering, claim phrasing, figure captions, abstract wording, and embodiment depth.
- Do not copy claim language, embodiments, drawings, or proprietary technical content from another patent.
- Do not imply that a reference patent proves patentability of the user's invention.
- Cite or list the reference patent publication numbers or URLs consulted when the user asks for source transparency.
- If no web access is available, proceed from the skill's built-in structure and state that external granted-patent style references were not checked in the current run.

### 8. Handle Technical Domains

#### Method Patents

Focus on concrete implementation steps and technical interactions. For a method patent, especially a calculation-method patent, always draft a stepwise embodiment using S1, S2, S3... labels unless the user provides another numbering convention.

The stepwise implementation should include, as applicable:

- S1: acquiring or defining input technical data, physical field variables, device states, boundary conditions, or working-condition parameters;
- S2: preprocessing, filtering, normalization, mesh/lattice/domain initialization, feature extraction, or parameter construction;
- S3: executing the core calculation, control, optimization, simulation, model inference, solver iteration, or update relationship;
- S4: determining convergence, stability, threshold satisfaction, control adjustment, exception handling, or feedback correction;
- S5: outputting a technical result, control instruction, design parameter, safety evaluation index, visualization result, or application decision;
- S6 or later: optional validation, storage, display, actuator execution, parameter sweep, or integration with a device/system.

Make step order flexible in claims unless order is technically necessary, but keep detailed embodiments operationally clear. Do not describe a calculation method only as“建立模型并计算结果”; specify the data, calculation relationship, iteration/update logic, judgment condition, and output technical object when supported.

In the abstract drawing and figure descriptions for method patents, use the same S1-Sn implementation steps. The abstract drawing should normally be the method flowchart, not a device block diagram, unless the device/system structure is the primary inventive concept.

#### Device Patents

Focus on components, connections, geometry, arrangement, material alternatives, sensors/actuators, and cooperation. Do not rely on method-only features as the sole novelty unless the device structure supports them.

#### System Patents

Describe modules by function and interaction. Include data acquisition, processing, storage, control, display/output, feedback, and execution components when supportable.

#### Program, Algorithm, and Calculation Model Patents

Frame the invention as a computer-implemented technical solution. Identify:

- input technical data or physical field variables,
- preprocessing or normalization,
- algorithm/model structure,
- calculation relationship or solver loop,
- hardware or computing environment,
- output controlling, diagnosing, simulating, optimizing, or evaluating a technical object.

Do not present a pure mathematical rule detached from a technical application. Tie the algorithm to a concrete technical field such as cooling optimization, heat-transfer prediction, droplet-impact analysis, reactor containment safety evaluation, or LBM simulation.

#### Cooling, Heat Transfer, Droplet Impact, Spray Cooling, Reactor Safety, and LBM

Use domain-specific but cautious language:

- Prefer features such as wall temperature, heat flux, Weber number, Reynolds number, Prandtl number, contact angle, droplet diameter, spray density, nozzle arrangement, boundary condition, lattice model, collision operator, relaxation time, phase-field variable, interfacial force, condensation model, or containment pressure/temperature field only when supported.
- Express parameters as ranges, thresholds, nondimensional relationships, or adjustable variables when exact values are not essential.
- For simulation inventions, distinguish physical model, numerical scheme, boundary condition, stability treatment, validation route, and output metric.
- For nuclear/reactor safety-related drafts, avoid unsupported safety guarantees. Use“用于分析/评估/辅助判断/提高模拟稳定性” rather than definitive safety conclusions unless provided.

## Non-Fabrication Rules

Never fabricate:

- experimental data, numerical values, simulation results, comparison baselines, or efficiency percentages;
- material grades, product models, device dimensions, reactor types, regulatory conclusions, or safety certifications;
- patentability, novelty, inventiveness, freedom-to-operate, infringement, or grant probability;
- filing dates, official fees, inventors, applicants, priority claims, or prior-art search results.

If the user provides partial data, preserve it exactly and mark any extrapolation as an optional embodiment or illustrative example. If a parameter range is needed but unsupported, phrase it as a configurable range and avoid claiming it as experimentally optimized.

## Strengthening Protection

When drafting, broaden protection in supportable ways:

- Protect the core mechanism, not one embodiment.
- Add alternative structures, equivalent modules, optional steps, and parameter ranges.
- Cover method, device/system, storage medium, electronic device, and application scenario where supported.
- Avoid writing all parameters as fixed constants.
- Convert single values into ranges or relationships when technically reasonable.
- Include fallback dependent claims for commercially important variants.
- Add embodiments that support broad terms in the independent claim.

At the end of each full draft, include:

```text
可进一步强化的保护点建议：
1. ...
2. ...
3. ...
```

Suggestions may include additional dependent claims, more embodiments, more parameter ranges, more drawings, comparative tests, control-loop variants, material/structure alternatives, or software/hardware deployment options.

## Output Quality Checklist

Before finalizing, verify:

- The full required patent structure is present.
- The abstract is concise, China-style, and does not exceed the disclosed content.
- At least one independent claim is present.
- 6-12 dependent claims are present for a full draft unless there is a stated reason.
- Claim 1 covers the core innovation without unnecessary prototype limitations.
- Dependent claims progressively narrow technical features.
- Every claim term is supported by the specification.
- The abstract drawing is generated, specified, or accompanied by reproducible code.
- Any Python-generated patent figure/result plot has saved code and saved output paths when tools permit.
- A final `.docx` Word version is generated for complete final-delivery requests.
- The Word version includes abstract, claims, beneficial effects, specification sections, figures, result plots/tables when applicable, and all required captions/references.
- Formulas in the Word version are editable Word equations/OMML or MathType-compatible objects when possible, and no formula appears as乱码, corrupted encoding, or unreadable pasted text.
- The Word document has been rendered and visually checked when DOCX rendering tools are available.
- Granted Chinese patent references or official/reputable patent sources are consulted for style when requested or when format uncertainty matters; any unavailable source check is stated.
- Unprovided data is not presented as measured or proven.
- The final text includes attorney/patent-agent review notice.

## Standard Closing Notice

End substantial outputs with a notice similar to:

```text
以上文本为基于当前技术披露生成的中国发明专利申请文件草案，不构成法律意见或授权结论。正式提交前，建议由具备资质的专利代理师或专利律师结合现有技术检索、申请策略和最新 CNIPA 要求进行审查和修改。
```

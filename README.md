# china-patent-drafter

Codex Skill for drafting and packaging Chinese invention patent application documents from technical disclosures, innovation points, experimental results, program logic, calculation methods, device structures, system architectures, and engineering application scenarios.

## Contents

- `china-patent-drafter/SKILL.md`
- `china-patent-drafter/agents/openai.yaml`

## Install

Copy the `china-patent-drafter` folder into a Codex skill directory such as:

```text
~/.agents/skills/china-patent-drafter
```

or a project-local skill directory used by your Codex configuration.

## Usage

Example prompt:

```text
Use $china-patent-drafter to generate a Chinese invention patent application draft from this technical solution: ...
```

## Scope

This skill defaults to complete delivery: for complete patent-application requests it generates both a Markdown draft and a final Word/DOCX package, including title, abstract, claims, beneficial effects, specification, abstract drawing guidance, figures, result plots, editable equations, and optional Python code for patent figures or result plots. It skips DOCX generation only when the user explicitly asks for Markdown-only or text-only output.

It is not legal advice. Final filing documents should be reviewed by a qualified patent agent or patent lawyer before submission.

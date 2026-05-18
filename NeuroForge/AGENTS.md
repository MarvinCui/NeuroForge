# Codex Agent Instructions

When working in this repository, start from `SKILL.md`.

When the user provides data, first run `scripts/inspect_input.py` to classify the input safely. Use `scripts/route_workflow.py` and `scripts/build_plan.py` to route and plan. Use `workflows/` for end-to-end workflow templates. Use `graph/skill_graph_summary.tsv` for tool-concept routing. Use `skills/<tool>/SKILL.md` before reading detailed references.

Do not execute heavy tools without explicit user approval. Do not modify raw input data unless explicitly asked. Do not rely on changelogs, test examples, or generated pattern-detection metadata as primary evidence.

The scripts in `scripts/` are safe inspection and planning helpers only. They may suggest commands as text, but they must not execute fMRIPrep, QSIPrep, FreeSurfer, MRtrix3, AFNI, MNE preprocessing pipelines, PyMC sampling, Docker, Snakemake, or Nipype workflows.

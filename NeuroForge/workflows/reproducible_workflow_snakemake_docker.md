# Reproducible Snakemake and Docker Workflow

## Scope
Workflow assistance for reproducible Psychology and Neuroscience pipelines using Docker environments, Snakemake rules, BIDS inputs, derivatives outputs, logging, and provenance.

## Input Requirements
- BIDS input dataset or another documented raw-data root.
- Tool commands, scripts, or notebooks to orchestrate.
- Dockerfile or container image definition with pinned dependencies where possible.
- Expected derivative outputs and QC artifacts.

## Main Steps
1. Define the BIDS input root, derivatives output root, logs directory, and config file.
2. Build a Docker image or container specification with required neuroimaging, behavioral, or statistics tools.
3. Write Snakemake rules with explicit inputs, outputs, params, logs, threads, and container declarations.
4. Add per-rule QC outputs and provenance capture, including versions and command logs.
5. Run dry-runs and DAG inspection before full execution.
6. Archive outputs in BIDS derivatives style with clear naming and metadata.

## Relevant Tools
- `snakemake`
- `bids-specification`
- `fmriprep`
- `qsiprep`
- `nilearn`
- `pymc`

## Common Failure Points
- Rules depend on hidden side effects instead of declared outputs.
- Container versions are not pinned.
- Logs are overwritten across subjects or sessions.
- BIDS derivatives are written without metadata or provenance.
- Workflow reruns produce different outputs because random seeds or environments are not fixed.

## Quality Checks
- `snakemake --dry-run` and DAG review succeed.
- Every rule has logs and expected outputs.
- Container image, package versions, and command lines are recorded.
- Failed jobs leave inspectable logs.
- Outputs can be regenerated from config, inputs, and workflow code.

## Expected Outputs
- Snakefile, config, logs, and container definition.
- BIDS derivatives tree.
- QC reports and provenance files.
- Reproducible run instructions.

## Search Terms For This Corpus
`Snakemake`, `rule`, `Snakefile`, `workflow`, `DAG`, `docker`, `container`, `Dockerfile`, `BIDS`, `derivatives`, `provenance`, `environment`, `version`

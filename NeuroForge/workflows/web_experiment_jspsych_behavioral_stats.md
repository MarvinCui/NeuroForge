# jsPsych Behavioral Experiment to Statistics Workflow

## Scope
Browser-based behavioral experiment assistance from jsPsych timeline design through trial data export, reaction time and accuracy cleaning, and PyMC statistical modeling.

## Input Requirements
- jsPsych experiment with timeline variables, plugins, stimuli, response fields, and browser compatibility expectations.
- Trial-level data export including condition labels, reaction time, accuracy, response, stimulus identifiers, and participant/session metadata.
- Statistical question expressed as contrasts, regression terms, hierarchical effects, or Bayesian model structure.

## Main Steps
1. Define jsPsych timeline structure, plugin sequence, instructions, practice trials, and trial metadata.
2. Record trial data with condition, stimulus, response, accuracy, reaction time, and browser/session fields.
3. Clean data for invalid responses, anticipatory reaction times, timeouts, and participant exclusion rules.
4. Summarize behavioral outcomes by participant, condition, and trial block.
5. Fit Bayesian models in PyMC, depending on the study question.
6. Report effect estimates, uncertainty, diagnostics, and reproducible analysis code.

## Relevant Tools
- `jspsych`
- `psychopy`
- `pymc`
- `snakemake`

## Common Failure Points
- Trial metadata not saved with every response.
- Browser timing limitations ignored for stimulus classes that require tight timing.
- Reaction time filtering rules chosen after inspecting effects.
- Accuracy and missing-response coding mixed together.
- Bayesian models reported without posterior predictive checks or convergence diagnostics.

## Quality Checks
- Inspect raw trial rows before aggregation.
- Confirm timeline conditions match the experimental design.
- Plot reaction time distributions and accuracy by condition.
- Check model residuals, posterior diagnostics, or convergence summaries.
- Preserve analysis scripts, package versions, and exclusion criteria.

## Expected Outputs
- jsPsych experiment files and trial data.
- Cleaned behavioral table with participant and condition labels.
- Reaction time and accuracy summaries.
- PyMC posterior summaries with diagnostics.

## Search Terms For This Corpus
`jsPsych`, `timeline`, `plugin`, `jsPsych.run`, `browser`, `html-keyboard-response`, `reaction time`, `accuracy`, `trial`, `condition`, `pymc`, `posterior`, `regression`

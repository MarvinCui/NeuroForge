---
name: pymc
description: Use this skill for Bayesian model planning, priors, posteriors, MCMC diagnostics, ArviZ summaries, and hierarchical modeling.
domain: Bayesian modeling
source: cleaned local skill corpus
---

# PyMC Skill

## Purpose

This standalone skill helps Codex reason about Bayesian modeling within psychology and neuroscience research workflows. It is designed for inspection, routing, planning, and safe command suggestion around user-provided data or analysis questions.

Use it to understand what this tool is good for, which local references are likely worth reading first, which workflows it supports, and which cautions apply before any processing is attempted. The wider collection provides cross-tool routing and workflow templates, but this file is complete enough to use this `pymc` skill folder independently.

## Use This Skill When

- A user asks for Bayesian modeling of behavioral, imaging, or summary data.
- You need to plan priors, likelihoods, diagnostics, posterior summaries, or hierarchical models.
- You need to explain safe PyMC command suggestions without running sampling automatically.

## Do Not Use This Skill As Primary Evidence For

- General medical, diagnostic, or clinical interpretation questions.
- Tasks where another skill is the direct source of truth, such as BIDS layout questions or tool-specific output interpretation.
- Evidence that should come from current official documentation when version-specific behavior matters.
- Architecture claims based only on generated metadata, tests, changelogs, or pattern-detection output.

## High-Value References

- `references/documentation/api/data.rst`: API reference for data.rst.
- `references/documentation/api/model.rst`: API reference for model.rst.
- `references/documentation/api/gp.rst`: API reference for gp.rst.
- `references/documentation/api/cov.rst`: API reference for cov.rst.
- `references/documentation/api/ode.rst`: API reference for ode.rst.
- `references/documentation/api/smc.rst`: API reference for smc.rst.
- `references/documentation/api/core.rst`: API reference for core.rst.
- `references/documentation/api/dims.rst`: API reference for dims.rst.
- `references/documentation/api/math.rst`: API reference for math.rst.
- `references/documentation/api/mean.rst`: API reference for mean.rst.
- `references/documentation/api/misc.rst`: API reference for misc.rst.
- `references/documentation/api/util.rst`: API reference for util.rst.

## Common Workflows

- Plan Bayesian model structure
- Choose priors and likelihood families
- Specify diagnostics and posterior checks
- Route behavioral or imaging summaries into models

## Search Terms

- `PyMC`
- `posterior`
- `prior`
- `MCMC`
- `NUTS`
- `ArviZ`
- `trace`
- `hierarchical model`
- `posterior predictive`
- `sampling`
- `credible interval`
- `diagnostics`

## Related Skills

- `nilearn`
- `jspsych`
- `psychopy`

## Cautions

- Do not run sampling automatically; ask before executing MCMC or long posterior predictive workflows.
- Check priors, likelihoods, convergence diagnostics, and posterior predictive checks before interpreting results.
- Treat this skill as planning and documentation support, not permission to run heavy processing automatically.
- Do not modify raw user data unless the user explicitly asks for that operation.
- Prefer documentation, tutorials, examples, and workflow templates over changelogs, tests, or generated metadata.
- Check modality, file format, space, and metadata assumptions before suggesting commands.

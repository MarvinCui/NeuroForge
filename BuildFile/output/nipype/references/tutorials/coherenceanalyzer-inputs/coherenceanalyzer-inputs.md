# How To: Coherenceanalyzer Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CoherenceAnalyzer inputs

## Prerequisites

**Required Modules:**
- `analysis`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(NFFT=dict(usedefault=True), TR=dict(), figure_type=dict(usedefault=True), frequency_range=dict(usedefault=True), in_TS=dict(), in_file=dict(extensions=None, requires=('TR',)), n_overlap=dict(usedefault=True), output_csv_file=dict(extensions=None), output_figure_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(NFFT=dict(usedefault=True), TR=dict(), figure_type=dict(usedefault=True), frequency_range=dict(usedefault=True), in_TS=dict(), in_file=dict(extensions=None, requires=('TR',)), n_overlap=dict(usedefault=True), output_csv_file=dict(extensions=None), output_figure_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_CoherenceAnalyzer.py:6 | Complexity: Beginner | Last updated: 2026-05-18*
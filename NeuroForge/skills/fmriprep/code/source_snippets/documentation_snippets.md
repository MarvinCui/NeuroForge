# fmriprep Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Faq #3

- Kind: `documentation`
- Source: `references/documentation/other/faq.rst`
- Note: Documentation code block extracted for implementation use.

```bash
recon-all
recon-all -autorecon2-volonly -openmp 8 -subjid sub-020 -sd /outputs/freesurfer -nogcareg -nocanorm -nocareg -nonormalization2 -nomaskbfs -nosegmentation -nofill
$ python -m pip install -U templateflow
$ python -c "from templateflow.api import get; get(['MNI152NLin2009cAsym', 'MNI152NLin6Asym', 'OASIS30ANTs', 'MNIPediatricAsym', 'MNIInfant'])"
```

## 2. Workflows #2

- Kind: `documentation`
- Source: `references/documentation/other/workflows.rst`
- Note: Documentation code block extracted for implementation use.

```text
spaces=SpatialReferences([
wf = init_anat_preproc_wf(
skull_strip_template=Reference('MNI152NLin2009cAsym'),
```

## 3. Changes

- Kind: `documentation`
- Source: `references/documentation/overview/CHANGES.rst`
- Note: Documentation code block extracted for implementation use.

```bash
recon-all
N4BiasFieldCorrection
antsBrainExtraction
`antsBrainExtraction.sh` workflow distributed by ANTs.
```

## 4. Faq #2

- Kind: `documentation`
- Source: `references/documentation/other/faq.rst`
- Note: Documentation code block extracted for implementation use.

```text
$ python -c "from templateflow.api import get; get(['MNI152NLin2009cAsym', 'MNI152NLin6Asym', 'OASIS30ANTs', 'MNIPediatricAsym', 'MNIInfant'])"
```

## 5. Installation #2

- Kind: `documentation`
- Source: `references/documentation/other/installation.rst`
- Note: Documentation code block extracted for implementation use.

```bash
$ python -m pip install fmriprep-docker
$ python -m pip install fmriprep
```

## 6. Workflows #1

- Kind: `documentation`
- Source: `references/documentation/other/workflows.rst`
- Note: Documentation code block extracted for implementation use.

```text
wf = init_single_subject_wf('01')
```

## 7. Workflows #3

- Kind: `documentation`
- Source: `references/documentation/other/workflows.rst`
- Note: Documentation code block extracted for implementation use.

```text
wf = init_brain_extraction_wf()
```

## 8. Faq #1

- Kind: `documentation`
- Source: `references/documentation/other/faq.rst`
- Note: Documentation code block extracted for implementation use.

```text
$ python -m pip install -U templateflow
```

## 9. Installation #1

- Kind: `documentation`
- Source: `references/documentation/other/installation.rst`
- Note: Documentation code block extracted for implementation use.

```text
$ python -m pip install fmriprep
```

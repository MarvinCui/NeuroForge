# mne-python Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Design Philosophy #2

- Kind: `documentation`
- Source: `references/documentation/other/design_philosophy.rst`
- Note: Documentation code block extracted for implementation use.

```text
from mne.preprocessing import eog
eog.peak_finder(...)
eog.find_eog_events(...)
eog.create_eog_epochs(...)
```

## 2. Design Philosophy #1

- Kind: `documentation`
- Source: `references/documentation/other/design_philosophy.rst`
- Note: Documentation code block extracted for implementation use.

```text
import mne
mne.preprocessing.eog.peak_finder(...)
mne.preprocessing.eog.find_eog_events(...)
mne.preprocessing.eog.create_eog_epochs(...)
```

## 3. Cookbook #2

- Kind: `documentation`
- Source: `references/documentation/other/cookbook.rst`
- Note: Documentation code block extracted for implementation use.

```text
>>> reject = dict(grad=4000e-13, mag=4e-12, eog=150e-6)  # doctest: +SKIP
>>> epochs = mne.Epochs(raw, events, event_id=1, tmin=-0.2, tmax=0.5,  # doctest: +SKIP
>>>                     proj=True, picks=picks, baseline=(None, 0),  # doctest: +SKIP
>>>                     preload=True, reject=reject)  # doctest: +SKIP
```

## 4. Memory #3

- Kind: `documentation`
- Source: `references/documentation/other/memory.rst`
- Note: Documentation code block extracted for implementation use.

```bash
data_path = sample.data_path()
raw = io.read_raw_fif(raw_fname, preload=False)
events = mne.find_events(raw)
picks = mne.pick_types(raw.info, meg=True, eeg=True, stim=False, eog=True)
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, picks=picks,
```

## 5. Memory #2

- Kind: `documentation`
- Source: `references/documentation/other/memory.rst`
- Note: Documentation code block extracted for implementation use.

```text
events = mne.find_events(raw)
picks = mne.pick_types(raw.info, meg=True, eeg=True, stim=False, eog=True)
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, picks=picks,
```

## 6. Migrating

- Kind: `documentation`
- Source: `references/documentation/other/migrating.rst`
- Note: Documentation code block extracted for implementation use.

```bash
EEG = pop_fileio(fname);
EEG = pop_eegfiltnew(EEG, l_freq, h_freq);
EEG= pop_averef;
pop_select.m
EEG = pop_runica(EEG, 'pca', n);
EEG = pop_binica(EEG, 'pca', n);
pop_compprop( EEG, comp_num, winhandle);
pop_selectcomps()
Epochs = pop_epochs(EEG, event_id, [tmin, tmax]);
Epochs = pop_epochs(EEG_epochs, {cond2});
pop_timtopo(EEG_epochs, ...);
pop_compareerps(EEG_epochs1, EEG_epochs2);
```

## 7. Ged #1

- Kind: `documentation`
- Source: `references/documentation/other/ged.rst`
- Note: Documentation code block extracted for implementation use.

```text
_, ref_evecs, mask = mne.cov._smart_eigh(C_ref, ..., proj_subspace=True, ...)
restr_mat = ref_evecs[mask]
```

## 8. Faq #3

- Kind: `documentation`
- Source: `references/documentation/other/faq.rst`
- Note: Documentation code block extracted for implementation use.

```text
>>> import os
>>> num_cpu = '4' # Set as a string
>>> os.environ['OMP_NUM_THREADS'] = num_cpu
```

## 9. Faq #2

- Kind: `documentation`
- Source: `references/documentation/other/faq.rst`
- Note: Documentation code block extracted for implementation use.

```text
import appnope
  appnope.nope()
```

## 10. Contributing #2

- Kind: `documentation`
- Source: `references/documentation/other/contributing.rst`
- Note: Documentation code block extracted for implementation use.

```text
$ cd mne-python
$ git remote add upstream https://github.com/mne-tools/mne-python.git
$ git fetch --all
$ git config --local blame.ignoreRevsFile .git-blame-ignore-revs
```

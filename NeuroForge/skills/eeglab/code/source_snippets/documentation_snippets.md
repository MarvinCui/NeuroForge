# eeglab Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. AGENTS.md #2

- Kind: `documentation`
- Source: `references/documentation/overview/AGENTS.md`
- Note: Documentation code block extracted for implementation use.

```matlab
% 1. Load data
EEG = pop_loadset('filename', 'data.set', 'filepath', '/path/');
% or: EEG = pop_fileio('/path/to/data.edf');
% or: [STUDY, ALLEEG] = pop_importbids(bidspath, 'studyName', 'MyStudy');

% 2. Import channel locations (if not already present)
EEG = pop_chanedit(EEG, 'lookup', 'standard-10-5-cap385.elp');

% 3. Remove non-EEG channels (EMG, EOG, ECG, GSR, etc.)
EEG = pop_select(EEG, 'nochannel', {'EXG1','EXG2','EXG3','ECG','EMG'});

% 4. Average reference (before artifact cleaning)
EEG = pop_reref(EEG, []);

% 5. Clean data: remove bad channels, reject bad segments (clean_rawdata)
EEG = pop_clean_rawdata(EEG, ...
    'FlatlineCriterion', 5, ...
    'ChannelCriterion', 0.8, ...
    'LineNoiseCriterion', 4, ...
    'Highpass', [0.25 0.75], ...
    'BurstCriterion', 20, ...
    'WindowCriterion', 0.25, ...
    'BurstRejection', 'on', ...
    'Distance', 'Euclidian', ...
    'WindowCriterionTolerances', [-Inf 7]);

% 6. Re-reference again (after bad channel removal)
EEG = pop_reref(EEG, []);

% 7. Run ICA (pca -1 = auto-reduce for rank-deficient data)
% 'pca', -1 indicate to reduce the dimension by 1 to account for rank decrease by average reference in 6
EEG = pop_runica(EEG, 'icatype', 'runica', 'options', {'pca', -1});

% 8. Classify and flag artifact components (ICLabel)
EEG = pop_iclabel(EEG, 'default');
EEG = pop_icflag(EEG, [NaN NaN; 0.9 1; 0.9 1; NaN NaN; NaN NaN; NaN NaN; NaN NaN]);
%                       Brain   Muscle  Eye    Heart  LineNoise ChanNoise Other

% 9. Remove flagged components
EEG = pop_subcomp(EEG, find(EEG.reject.gcompreject), 0);

% 10. Extract epochs
EEG = pop_epoch(EEG, {'xxx','yyy'}, [-1 2], 'epochinfo', 'yes');
EEG = eeg_checkset(EEG);

% 11. Remove baseline
EEG = pop_rmbase(EEG, [-1000 0]);

% 12. Save
EEG = pop_saveset(EEG, 'filename', 'processed.set', 'filepath', '/path/');
```

## 2. AGENTS.md #1

- Kind: `documentation`
- Source: `references/documentation/overview/AGENTS.md`
- Note: Documentation code block extracted for implementation use.

```matlab
% plugin_askinstall(plugin_name, plugin_function, interactive)
% interactive: 0 = install silently, 1 = prompt user
plugin_askinstall('ICLabel', 'iclabel', 0);        % install ICLabel
plugin_askinstall('clean_rawdata', 'clean_artifacts', 0);
plugin_askinstall('firfilt', 'pop_eegfiltnew', 0);
plugin_askinstall('picard', 'picard', 0);
plugin_askinstall('dipfit', 'pop_dipfit_settings', 0);
```

## 3. AGENTS.md #3

- Kind: `documentation`
- Source: `references/documentation/overview/AGENTS.md`
- Note: Documentation code block extracted for implementation use.

```matlab
EEG = pop_iclabel(EEG, 'default');
% Results in: EEG.etc.ic_classification.ICLabel.classifications  (N_components x 7 matrix)
% Columns:    [Brain, Muscle, Eye, Heart, LineNoise, ChannelNoise, Other]
% Each row sums to 1.0
```

## 4. What is EEGLAB? #3

- Kind: `documentation`
- Source: `references/documentation/overview/README.md`
- Note: Documentation code block extracted for implementation use.

```bash
git clone --recurse-submodules https://github.com/sccn/eeglab.git
git submodule update --init --recursive --remote
git pull --recurse-submodules
```

## 5. What is EEGLAB? #2

- Kind: `documentation`
- Source: `references/documentation/overview/README.md`
- Note: Documentation code block extracted for implementation use.

```text
git submodule update --init --recursive --remote
git pull --recurse-submodules
```

## 6. What is EEGLAB? #1

- Kind: `documentation`
- Source: `references/documentation/overview/README.md`
- Note: Documentation code block extracted for implementation use.

```text
git clone --recurse-submodules https://github.com/sccn/eeglab.git
```

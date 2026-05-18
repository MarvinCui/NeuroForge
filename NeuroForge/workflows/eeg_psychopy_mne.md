# EEG PsychoPy to MNE Workflow

## Scope
EEG or MEG task workflow assistance from PsychoPy task design and trigger logging through MNE preprocessing, epoching, evoked responses, time-frequency analysis, and statistics.

## Input Requirements
- PsychoPy experiment with stable trial conditions, keyboard or response logging, and synchronized trigger/event output.
- Raw EEG/MEG data with sampling rate, channel metadata, event markers, and acquisition notes.
- Channel location, montage, or digitization metadata when source analysis is planned.

## Main Steps
1. Build or inspect the PsychoPy task design, routines, stimuli, TrialHandler loops, response logging, and trigger timing.
2. Import raw EEG/MEG data into MNE and verify channel types, sampling frequency, montage, and event markers.
3. Apply filtering, notch filtering, bad-channel marking, rereferencing, and artifact inspection.
4. Run ICA or other artifact correction with clear component review criteria.
5. Create epochs from events with `event_id`, `tmin`, `tmax`, and baseline settings.
6. Compute evoked responses, time-frequency representations, or decoding features.
7. Export subject-level measures for statistics or group analysis.

## Relevant Tools
- `psychopy`
- `mne-python`
- `eeglab`

## Common Failure Points
- PsychoPy timestamps not synchronized with EEG triggers.
- Trigger codes reused ambiguously across conditions.
- Filtering choices that distort epochs or baseline windows.
- ICA components removed without review.
- Epoch rejection thresholds applied inconsistently across subjects.

## Quality Checks
- Verify event counts against trial logs.
- Plot raw data before and after filtering.
- Review bad channels, ICA components, and epoch rejection summaries.
- Confirm evoked response polarity, timing, and condition labels.
- Check TFR baseline and frequency ranges before statistics.

## Expected Outputs
- Cleaned raw data or preprocessing reports.
- Epoch files, evoked responses, TFR objects, and exported summary tables.
- Event-log audit linking PsychoPy trials to EEG/MEG events.
- Statistical-ready condition-level measures.

## Search Terms For This Corpus
`PsychoPy`, `TrialHandler`, `stimulus`, `keyboard`, `raw`, `filter`, `ICA`, `events`, `epochs`, `event_id`, `tmin`, `tmax`, `baseline`, `TFR`, `morlet`

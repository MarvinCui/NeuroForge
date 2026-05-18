# How To: Audioclip Rms

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the RMS method of `AudioClip`. Just check if the function give back
values that are correctly formatted given the input data.

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.sound`


## Step-by-Step Guide

### Step 1: 'Test the RMS method of `AudioClip`. Just check if the function give back\n    values that are correctly formatted given the input data.\n    '

```python
'Test the RMS method of `AudioClip`. Just check if the function give back\n    values that are correctly formatted given the input data.\n    '
```

**Verification:**
```python
assert caughtChannelParamError, 'Did not catch expected error related to specifying the wrong value when specifying `channel` to RMS.'
```

### Step 2: Assign audioClipStereo = AudioClip.sine(...)

```python
audioClipStereo = AudioClip.sine(duration=1.0, sampleRateHz=SAMPLE_RATE_48kHz, channels=AUDIO_CHANNELS_STEREO)
```

**Verification:**
```python
assert isinstance(rmsResultStereo, np.ndarray) and len(rmsResultStereo) == audioClipStereo.channels
```

### Step 3: Assign caughtChannelParamError = False

```python
caughtChannelParamError = False
```

**Verification:**
```python
assert isinstance(rmsResultMono, np.float32)
```

### Step 4: Assign rmsResultStereo = audioClipStereo.rms(...)

```python
rmsResultStereo = audioClipStereo.rms()
```

**Verification:**
```python
assert isinstance(rmsResultStereo, np.ndarray) and len(rmsResultStereo) == audioClipStereo.channels
```

### Step 5: Assign audioClipMono = audioClipStereo.asMono(...)

```python
audioClipMono = audioClipStereo.asMono()
```

### Step 6: Assign rmsResultMono = audioClipMono.rms(...)

```python
rmsResultMono = audioClipMono.rms()
```

**Verification:**
```python
assert isinstance(rmsResultMono, np.float32)
```

### Step 7: Call audioClipStereo.rms()

```python
audioClipStereo.rms(-1)
```

### Step 8: Assign caughtChannelParamError = True

```python
caughtChannelParamError = True
```


## Complete Example

```python
# Workflow
'Test the RMS method of `AudioClip`. Just check if the function give back\n    values that are correctly formatted given the input data.\n    '
audioClipStereo = AudioClip.sine(duration=1.0, sampleRateHz=SAMPLE_RATE_48kHz, channels=AUDIO_CHANNELS_STEREO)
caughtChannelParamError = False
try:
    audioClipStereo.rms(-1)
except AssertionError:
    caughtChannelParamError = True
assert caughtChannelParamError, 'Did not catch expected error related to specifying the wrong value when specifying `channel` to RMS.'
rmsResultStereo = audioClipStereo.rms()
assert isinstance(rmsResultStereo, np.ndarray) and len(rmsResultStereo) == audioClipStereo.channels
audioClipMono = audioClipStereo.asMono()
rmsResultMono = audioClipMono.rms()
assert isinstance(rmsResultMono, np.float32)
```

## Next Steps


---

*Source: test_audioclip.py:292 | Complexity: Advanced | Last updated: 2026-05-18*
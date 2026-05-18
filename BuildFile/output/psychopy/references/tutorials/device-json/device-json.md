# How To: Device Json

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Configuration example: test device JSON

## Prerequisites

**Required Modules:**
- `threading`
- `psychopy`
- `psychopy.hardware`
- `psychopy.tests`
- `pathlib`
- `json`
- `asyncio`
- `time`
- `psychopy.hardware.keyboard`
- `psychopy.visual`


## Step-by-Step Guide

### Step 1: Assign cases = value

```python
cases = {'testMic': 'psychopy.hardware.microphone.MicrophoneDevice', 'testPhotodiode': 'psychopy.hardware.lightsensor.ScreenBufferSampler', 'testButtonBox': 'psychopy.hardware.button.KeyboardButtonBox'}
```


## Complete Example

```python
# Workflow
cases = {'testMic': 'psychopy.hardware.microphone.MicrophoneDevice', 'testPhotodiode': 'psychopy.hardware.lightsensor.ScreenBufferSampler', 'testButtonBox': 'psychopy.hardware.button.KeyboardButtonBox'}
```

## Next Steps


---

*Source: test_Liaison.py:239 | Complexity: Beginner | Last updated: 2026-05-18*
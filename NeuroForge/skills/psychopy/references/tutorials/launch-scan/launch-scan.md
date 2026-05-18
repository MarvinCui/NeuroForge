# How To: Launch Scan

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that launchScan successfully adds sync keys to the buffer.

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `pytest`
- `psychopy`
- `psychopy.hardware`
- `psychopy.hardware.emulator`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: 'Test that launchScan successfully adds sync keys to the buffer.'

```python
'Test that launchScan successfully adds sync keys to the buffer.'
```

**Verification:**
```python
assert 0 < self.globalClock.getTime() < 0.05
```

### Step 2: Assign MR_settings = value

```python
MR_settings = self.MR_settings
```

**Verification:**
```python
assert vol == MR_settings['volumes'] == len(onsets)
```

### Step 3: Assign onsets = value

```python
onsets = [0.0]
```

### Step 4: Assign sync_key = value

```python
sync_key = MR_settings['sync']
```

### Step 5: Assign vol = launchScan(...)

```python
vol = launchScan(self.win, MR_settings, globalClock=self.globalClock, mode='Test', wait_timeout=5, log=False)
```

**Verification:**
```python
assert 0 < self.globalClock.getTime() < 0.05
```

### Step 6: Assign duration = value

```python
duration = MR_settings['volumes'] * MR_settings['TR']
```

**Verification:**
```python
assert vol == MR_settings['volumes'] == len(onsets)
```

### Step 7: Assign allKeys = event.getKeys(...)

```python
allKeys = event.getKeys(timeStamped=True)
```

### Step 8: Call onsets.append()

```python
onsets.append(key_tuple[1])
```


## Complete Example

```python
# Workflow
'Test that launchScan successfully adds sync keys to the buffer.'
MR_settings = self.MR_settings
onsets = [0.0]
sync_key = MR_settings['sync']
vol = launchScan(self.win, MR_settings, globalClock=self.globalClock, mode='Test', wait_timeout=5, log=False)
assert 0 < self.globalClock.getTime() < 0.05
duration = MR_settings['volumes'] * MR_settings['TR']
while self.globalClock.getTime() < duration:
    allKeys = event.getKeys(timeStamped=True)
    for key_tuple in allKeys:
        if key_tuple[0] == sync_key:
            vol += 1
            onsets.append(key_tuple[1])
assert vol == MR_settings['volumes'] == len(onsets)
```

## Next Steps


---

*Source: test_emulator.py:32 | Complexity: Advanced | Last updated: 2026-05-18*
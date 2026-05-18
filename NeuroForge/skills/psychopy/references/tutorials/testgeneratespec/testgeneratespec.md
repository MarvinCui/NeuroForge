# How To: Testgeneratespec

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: testGenerateSpec

## Prerequisites

**Required Modules:**
- `pytest`
- `re`
- `psychopy`


## Step-by-Step Guide

### Step 1: Assign base = open.read(...)

```python
base = open(preferences.__folder__ / 'baseNoArch.spec').read()
```

**Verification:**
```python
assert all(("theme = string(default='PsychopyDark')" in target for target in [darwin, freeBSD, linux, windows]))
```

### Step 2: Assign base = re.sub(...)

```python
base = re.sub("(?<=theme = string\\(default=')PsychopyLight(?='\\))", 'PsychopyDark', base)
```

**Verification:**
```python
assert all(("theme = string(default='PsychopyLight')" not in target for target in [darwin, freeBSD, linux, windows]))
```

### Step 3: Call preferences.generateSpec()

```python
preferences.generateSpec(baseSpec=base)
```

**Verification:**
```python
assert prefs.app['theme'] == 'PsychopyDark'
```

### Step 4: Assign darwin = open.read(...)

```python
darwin = open(preferences.__folder__ / 'Darwin.spec').read()
```

### Step 5: Assign freeBSD = open.read(...)

```python
freeBSD = open(preferences.__folder__ / 'FreeBSD.spec').read()
```

### Step 6: Assign linux = open.read(...)

```python
linux = open(preferences.__folder__ / 'Linux.spec').read()
```

### Step 7: Assign windows = open.read(...)

```python
windows = open(preferences.__folder__ / 'Windows.spec').read()
```

**Verification:**
```python
assert all(("theme = string(default='PsychopyDark')" in target for target in [darwin, freeBSD, linux, windows]))
```

### Step 8: Assign prefs = preferences.Preferences(...)

```python
prefs = preferences.Preferences()
```

### Step 9: Call prefs.resetPrefs()

```python
prefs.resetPrefs()
```

**Verification:**
```python
assert prefs.app['theme'] == 'PsychopyDark'
```


## Complete Example

```python
# Workflow
base = open(preferences.__folder__ / 'baseNoArch.spec').read()
base = re.sub("(?<=theme = string\\(default=')PsychopyLight(?='\\))", 'PsychopyDark', base)
preferences.generateSpec(baseSpec=base)
darwin = open(preferences.__folder__ / 'Darwin.spec').read()
freeBSD = open(preferences.__folder__ / 'FreeBSD.spec').read()
linux = open(preferences.__folder__ / 'Linux.spec').read()
windows = open(preferences.__folder__ / 'Windows.spec').read()
assert all(("theme = string(default='PsychopyDark')" in target for target in [darwin, freeBSD, linux, windows]))
assert all(("theme = string(default='PsychopyLight')" not in target for target in [darwin, freeBSD, linux, windows]))
prefs = preferences.Preferences()
prefs.resetPrefs()
assert prefs.app['theme'] == 'PsychopyDark'
```

## Next Steps


---

*Source: test_prefs.py:6 | Complexity: Advanced | Last updated: 2026-05-18*
# How To: Invalid Headers

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that invalid headers raise exceptions.

## Prerequisites

**Required Modules:**
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io.nedf`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test that invalid headers raise exceptions.'

```python
'Test that invalid headers raise exceptions.'
```

### Step 2: Assign tpl = b'<nedf>\n        <NEDFversion>1.3</NEDFversion>\n        <EEGSettings>\n            %s\n            <EEGMontage><C>A</C><C>B</C><C>C</C><C>D</C></EEGMontage>\n        </EEGSettings>\n    </nedf>\x00'

```python
tpl = b'<nedf>\n        <NEDFversion>1.3</NEDFversion>\n        <EEGSettings>\n            %s\n            <EEGMontage><C>A</C><C>B</C><C>C</C><C>D</C></EEGMontage>\n        </EEGSettings>\n    </nedf>\x00'
```

### Step 3: Assign nchan = b'<TotalNumberOfChannels>4</TotalNumberOfChannels>'

```python
nchan = b'<TotalNumberOfChannels>4</TotalNumberOfChannels>'
```

### Step 4: Assign sr = b'<EEGSamplingRate>500</EEGSamplingRate>'

```python
sr = b'<EEGSamplingRate>500</EEGSamplingRate>'
```

### Step 5: Assign hdr = value

```python
hdr = {'null': b'No null terminator', 'Unknown additional': b'<a><NEDFversion>1.3</NEDFversion>' + b'<AdditionalChannelStatus>???</AdditionalChannelStatus></a>\x00', 'No EEG channels found': b'<a><NEDFversion>1.3</NEDFversion></a>\x00', 'TotalNumberOfChannels not found': tpl % b'No nchan.', '!= channel count': tpl % (sr + b'<TotalNumberOfChannels>52</TotalNumberOfChannels>'), 'EEGSamplingRate not found': tpl % nchan, 'NumberOfRecordsOfEEG not found': tpl % (sr + nchan)}
```

### Step 6: Assign sus_hdrs = value

```python
sus_hdrs = {'unsupported': b'<a><NEDFversion>25</NEDFversion></a>\x00', 'tested': b'<a><NEDFversion>1.3</NEDFversion><stepDetails>' + b'<DeviceClass>STARSTIM</DeviceClass></stepDetails></a>\x00'}
```

### Step 7: Call _parse_nedf_header()

```python
_parse_nedf_header(invalid_hdr)
```

### Step 8: Call _parse_nedf_header()

```python
_parse_nedf_header(sus_hdr)
```


## Complete Example

```python
# Workflow
'Test that invalid headers raise exceptions.'
tpl = b'<nedf>\n        <NEDFversion>1.3</NEDFversion>\n        <EEGSettings>\n            %s\n            <EEGMontage><C>A</C><C>B</C><C>C</C><C>D</C></EEGMontage>\n        </EEGSettings>\n    </nedf>\x00'
nchan = b'<TotalNumberOfChannels>4</TotalNumberOfChannels>'
sr = b'<EEGSamplingRate>500</EEGSamplingRate>'
hdr = {'null': b'No null terminator', 'Unknown additional': b'<a><NEDFversion>1.3</NEDFversion>' + b'<AdditionalChannelStatus>???</AdditionalChannelStatus></a>\x00', 'No EEG channels found': b'<a><NEDFversion>1.3</NEDFversion></a>\x00', 'TotalNumberOfChannels not found': tpl % b'No nchan.', '!= channel count': tpl % (sr + b'<TotalNumberOfChannels>52</TotalNumberOfChannels>'), 'EEGSamplingRate not found': tpl % nchan, 'NumberOfRecordsOfEEG not found': tpl % (sr + nchan)}
for match, invalid_hdr in hdr.items():
    with pytest.raises(RuntimeError, match=match):
        _parse_nedf_header(invalid_hdr)
sus_hdrs = {'unsupported': b'<a><NEDFversion>25</NEDFversion></a>\x00', 'tested': b'<a><NEDFversion>1.3</NEDFversion><stepDetails>' + b'<DeviceClass>STARSTIM</DeviceClass></stepDetails></a>\x00'}
for match, sus_hdr in sus_hdrs.items():
    with pytest.warns(RuntimeWarning, match=match):
        with pytest.raises(RuntimeError, match='No EEG channels found'):
            _parse_nedf_header(sus_hdr)
```

## Next Steps


---

*Source: test_nedf.py:58 | Complexity: Advanced | Last updated: 2026-05-18*
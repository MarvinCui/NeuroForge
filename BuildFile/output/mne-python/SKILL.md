---
name: mne-python
description: Local codebase analysis for mne-python
doc_version: 
---

# mne-python Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `mne-python`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

### 🎨 Design Patterns Detected

*From C3.1 codebase analysis (confidence > 0.7)*

- **Observer**: 2 instances

*Total: 2 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: Test adjacency equivalence for lattice adjacency.** (complexity: 1.00)

```python
'Test adjacency equivalence for lattice adjacency.'
from sklearn.feature_extraction import grid_to_graph
sk_shape = shape if len(shape) > 1 else shape + (1,)
conn_sk = grid_to_graph(*sk_shape).toarray()
conn = combine_adjacency(*shape)
want_shape = (np.prod(shape),) * 2
assert conn.shape == conn_sk.shape == want_shape
assert (conn.data == 1.0).all()
conn = conn.toarray()
assert np.isin(conn, [0, 1, 2, 3]).all()
assert conn.shape == conn_sk.shape
assert_array_equal(conn, conn_sk)
```

**Workflow: Test the get_data method for Evoked.** (complexity: 1.00)

```python
'Test the get_data method for Evoked.'
evoked = read_evokeds(fname, 0)
d1 = evoked.get_data()
d2 = evoked.data
assert_array_equal(d1, d2)
eeg_idxs = np.array([i == 'eeg' for i in evoked.get_channel_types()])
assert_array_equal(evoked.data[eeg_idxs], evoked.get_data(picks='eeg'))
d3 = evoked.get_data(tmin=0)
assert np.all(d3.shape[1] == evoked.data.shape[1] - np.nonzero(evoked.times == 0)[0])
assert evoked.get_data(tmin=0, tmax=0).size == 0
with pytest.raises(TypeError, match='tmin .* float, None'):
    evoked.get_data(tmin=[1], tmax=1)
with pytest.raises(TypeError, match='tmax .* float, None'):
    evoked.get_data(tmin=1, tmax=np.ones(5))
d1 = evoked.get_data(picks='eeg', units=None)
d2 = evoked.get_data(picks='eeg', units='V')
assert_array_equal(d1, d2)
d3 = evoked.get_data(picks='eeg', units='µV')
assert_array_equal(d1 * 1000000.0, d3)
```

**Workflow: Test savgol filtering.** (complexity: 1.00)

```python
'Test savgol filtering.'
h_freq = 10.0
evoked = read_evokeds(fname, 0)
freqs = fftpack.fftfreq(len(evoked.times), 1.0 / evoked.info['sfreq'])
data = np.abs(fftpack.fft(evoked.data))
match_mask = np.logical_and(freqs >= 0, freqs <= h_freq / 2.0)
mismatch_mask = np.logical_and(freqs >= h_freq * 2, freqs < 50.0)
pytest.raises(ValueError, evoked.savgol_filter, evoked.info['sfreq'])
evoked_sg = evoked.copy().savgol_filter(h_freq)
data_filt = np.abs(fftpack.fft(evoked_sg.data))
assert_allclose(np.mean(data[:, match_mask], 0), np.mean(data_filt[:, match_mask], 0), rtol=0.0001, atol=0.01)
assert np.mean(data[:, mismatch_mask]) > np.mean(data_filt[:, mismatch_mask]) * 5
assert_allclose(data, np.abs(fftpack.fft(evoked.data)), atol=1e-16)
```

**Workflow: Test evoked Pandas exporter.** (complexity: 1.00)

```python
'Test evoked Pandas exporter.'
pytest.importorskip('pandas')
ave = read_evokeds(fname, 0)
with pytest.raises(ValueError, match='options. Valid index options are'):
    ave.to_data_frame(index=['foo', 'bar'])
with pytest.raises(ValueError, match='"qux" is not a valid option'):
    ave.to_data_frame(index='qux')
with pytest.raises(TypeError, match='index must be `None` or a string or'):
    ave.to_data_frame(index=np.arange(400))
df = ave.to_data_frame(index='time')
assert 'time' not in df.columns
assert 'time' in df.index.names
df_wide = ave.to_data_frame()
assert all(np.isin(ave.ch_names, df_wide.columns))
df_long = ave.to_data_frame(long_format=True)
expected = ('time', 'channel', 'ch_type', 'value')
assert set(expected) == set(df_long.columns)
assert set(ave.ch_names) == set(df_long['channel'])
assert len(df_long) == ave.data.size
del df_wide, df_long
df = ave.to_data_frame(index='time')
assert (df.columns == ave.ch_names).all()
assert_array_equal(df.values[:, 0], ave.data[0] * 10000000000000.0)
assert_array_equal(df.values[:, 2], ave.data[2] * 1000000000000000.0)
```

**Workflow: Test channels-dropping functionality.** (complexity: 1.00)

```python
'Test channels-dropping functionality.'
evoked = read_evokeds(fname, condition=0, proj=True)
drop_ch = evoked.ch_names[:3]
ch_names = evoked.ch_names[3:]
ch_names_orig = evoked.ch_names
dummy = evoked.copy().drop_channels(drop_ch)
assert_equal(ch_names, dummy.ch_names)
assert_equal(ch_names_orig, evoked.ch_names)
assert_equal(len(ch_names_orig), len(evoked.data))
dummy2 = evoked.copy().drop_channels([drop_ch[0]])
assert_equal(dummy2.ch_names, ch_names_orig[1:])
evoked.drop_channels(drop_ch)
assert_equal(ch_names, evoked.ch_names)
assert_equal(len(ch_names), len(evoked.data))
for ch_names in ([1, 2], 'fake', ['fake']):
    pytest.raises(ValueError, evoked.drop_channels, ch_names)
```

**Workflow: Test channel-picking functionality.** (complexity: 1.00)

```python
'Test channel-picking functionality.'
evoked = read_evokeds(fname, condition=0, proj=True)
ch_names = evoked.ch_names[:3]
ch_names_orig = evoked.ch_names
dummy = evoked.copy().pick(ch_names)
assert_equal(ch_names, dummy.ch_names)
assert_equal(ch_names_orig, evoked.ch_names)
assert_equal(len(ch_names_orig), len(evoked.data))
evoked.pick(ch_names)
assert_equal(ch_names, evoked.ch_names)
assert_equal(len(ch_names), len(evoked.data))
evoked = read_evokeds(fname, condition=0, proj=True)
assert 'meg' in evoked
assert 'eeg' in evoked
evoked.pick(picks='eeg')
assert 'meg' not in evoked
assert 'eeg' in evoked
assert len(evoked.ch_names) == 60
```

**Workflow: Test checking of bad markings.** (complexity: 1.00)

```python
'Test checking of bad markings.'
raw = readerfn(fname)
_fnirs_check_bads(raw.info)
raw = optical_density(raw)
_fnirs_check_bads(raw.info)
raw = beer_lambert_law(raw)
_fnirs_check_bads(raw.info)
raw = readerfn(fname)
nfreqs = len(set(_channel_frequencies(raw.info)))
raw.info['bads'] = raw.ch_names[0:nfreqs]
_fnirs_check_bads(raw.info)
raw = optical_density(raw)
_fnirs_check_bads(raw.info)
raw = beer_lambert_law(raw)
_fnirs_check_bads(raw.info)
raw = readerfn(fname)
raw.info['bads'] = raw.ch_names[0:1]
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
with pytest.raises(RuntimeError, match='bad labelling'):
    raw = optical_density(raw)
raw.info['bads'] = []
raw = optical_density(raw)
raw.info['bads'] = raw.ch_names[0:1]
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
with pytest.raises(RuntimeError, match='bad labelling'):
    raw = beer_lambert_law(raw)
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
```

**Workflow: Test checking of bad markings.** (complexity: 1.00)

```python
'Test checking of bad markings.'
raw = readerfn(fname)
nfreqs = len(set(_channel_frequencies(raw.info)))
raw.info['bads'] = [raw.ch_names[0]]
info = _fnirs_spread_bads(raw.info)
assert info['bads'] == raw.ch_names[:nfreqs]
raw_od = optical_density(raw)
bads = [raw_od.ch_names[nfreqs * ii + ii] for ii in range(nfreqs)]
expected_bads = raw_od.ch_names[:nfreqs ** 2]
raw_od.info['bads'] = bads
info = _fnirs_spread_bads(raw_od.info)
assert info['bads'] == sorted(expected_bads)
raw_hb = beer_lambert_law(raw_od)
raw_hb.info['bads'] = [raw_hb.ch_names[x] for x in [1, 8]]
info = _fnirs_spread_bads(raw_hb.info)
assert info['bads'] == [info.ch_names[x] for x in [0, 1, 8, 9]]
```

**Workflow: Ensure fNIRS channel checking on manually created data.** (complexity: 1.00)

```python
'Ensure fNIRS channel checking on manually created data.'
data = np.random.normal(size=(6, 10))
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D1 760', 'S2_D1 850', 'S3_D1 760', 'S3_D1 850']
ch_types = np.repeat('fnirs_od', 6)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
freqs = np.tile([760, 850], 3)
for idx, f in enumerate(freqs):
    raw.info['chs'][idx]['loc'][9] = f
freqs = np.unique(_channel_frequencies(raw.info))
picks = _check_channels_ordered(raw.info, freqs)
assert len(picks) == len(raw.ch_names)
assert len(picks) == 6
ch_names = ['S1_D1 760', 'S2_D1 760', 'S3_D1 760', 'S1_D1 850', 'S2_D1 850', 'S3_D1 850']
ch_types = np.repeat('fnirs_od', 6)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
freqs = np.repeat([760, 850], 3)
for idx, f in enumerate(freqs):
    raw.info['chs'][idx]['loc'][9] = f
_check_channels_ordered(raw.info, [760, 850])
raw.pick(picks=[0, 3, 1, 4, 2, 5])
_check_channels_ordered(raw.info, [760, 850])
ch_names = ['S1_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw2 = RawArray(data, info, verbose=True)
raw.add_channels([raw2])
with pytest.raises(ValueError, match='does not support a combination'):
    _check_channels_ordered(raw.info, [760, 850])
```

**Workflow: Ensure fNIRS channel checking on manually created data.** (complexity: 1.00)

```python
'Ensure fNIRS channel checking on manually created data.'
data = np.random.RandomState(0).randn(6, 10)
ch_names = ['S1_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
chroma = np.unique(_channel_chromophore(raw.info))
picks = _check_channels_ordered(raw.info, chroma)
assert len(picks) == len(raw.ch_names)
assert len(picks) == 6
ch_names = ['S1_D1 hbo', 'S2_D1 hbo', 'S3_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbr', 'S3_D1 hbr']
ch_types = np.repeat(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
raw.pick(picks=[0, 3, 1, 4, 2, 5])
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
with pytest.raises(ValueError, match='chromophore in info'):
    _check_channels_ordered(raw.info, ['hbb', 'hbr'])
ch_names = ['S1_D1 hbb', 'S1_D1 hbr', 'S2_D1 hbb', 'S2_D1 hbr', 'S3_D1 hbb', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
with pytest.raises(ValueError, match='naming conventions'):
    _check_channels_ordered(raw.info, ['hbo', 'hbr'])
ch_names = ['S1_DX hbo', 'S1_DX hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
with pytest.raises(ValueError, match='can not be parsed'):
    _check_channels_ordered(raw.info, ['hbo', 'hbr'])
```

*See `references/test_examples/` for all extracted examples*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 146
**Categories:** 6

### Overview

- **README.rst** (`README.rst`)

### Api

- **connectivity.rst** (`doc/api/connectivity.rst`)
- **covariance.rst** (`doc/api/covariance.rst`)
- **creating_from_arrays.rst** (`doc/api/creating_from_arrays.rst`)
- **datasets.rst** (`doc/api/datasets.rst`)
- **decoding.rst** (`doc/api/decoding.rst`)
- *...and 19 more*

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

### Other

- **CONTRIBUTING.md** (`.github/CONTRIBUTING.md`)
- **PULL_REQUEST_TEMPLATE.md** (`.github/PULL_REQUEST_TEMPLATE.md`)
- **bem_model.rst** (`doc/_includes/bem_model.rst`)
- **channel_interpolation.rst** (`doc/_includes/channel_interpolation.rst`)
- **channel_types.rst** (`doc/_includes/channel_types.rst`)
- *...and 110 more*

### Security

- **SECURITY.md** (`SECURITY.md`)

### Templates

- **class.rst** (`doc/_templates/autosummary/class.rst`)
- **class_no_inherited_members.rst** (`doc/_templates/autosummary/class_no_inherited_members.rst`)
- **class_no_members.rst** (`doc/_templates/autosummary/class_no_members.rst`)
- **function.rst** (`doc/_templates/autosummary/function.rst`)

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis

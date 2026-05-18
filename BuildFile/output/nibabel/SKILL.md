---
name: nibabel
description: Local codebase analysis for nibabel
doc_version: 
---

# nibabel Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `nibabel`
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

- **Adapter**: 7 instances

*Total: 7 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: test origin affine** (complexity: 1.00)

```python
hdr = Spm99AnalyzeHeader()
aff = hdr.get_origin_affine()
assert_array_equal(aff, hdr.get_base_affine())
hdr.set_data_shape((3, 5, 7))
hdr.set_zooms((3, 2, 1))
assert hdr.default_x_flip
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
hdr['origin'][:3] = [3, 4, 5]
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 6.0], [0.0, 2.0, 0.0, -6.0], [0.0, 0.0, 1.0, -4.0], [0.0, 0.0, 0.0, 1.0]])
hdr['origin'] = 0
hdr.set_data_shape((3, 5))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -0.0], [0.0, 0.0, 0.0, 1.0]])
hdr.set_data_shape((3, 5, 7))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

**Workflow: test data scaling** (complexity: 1.00)

```python
hdr = self.header_class()
hdr.set_data_shape((1, 2, 3))
hdr.set_data_dtype(np.int16)
S3 = BytesIO()
data = np.arange(6, dtype=np.float64).reshape((1, 2, 3))
hdr.data_to_fileobj(data, S3)
data_back = hdr.data_from_fileobj(S3)
assert_array_almost_equal(data, data_back, 4)
assert not np.all(data == data_back)
data_back2 = hdr.data_from_fileobj(S3)
assert_array_equal(data_back, data_back2, 4)
hdr.data_to_fileobj(data, S3, rescale=True)
data_back = hdr.data_from_fileobj(S3)
assert_array_almost_equal(data, data_back, 4)
assert not np.all(data == data_back)
with np.errstate(invalid='ignore'):
    hdr.data_to_fileobj(data, S3, rescale=False)
data_back = hdr.data_from_fileobj(S3)
assert np.all(data == data_back)
```

**Workflow: test origin checks** (complexity: 1.00)

```python
HC = self.header_class
hdr = HC()
hdr.data_shape = [1, 1, 1]
hdr['origin'][0] = 101
fhdr, message, raiser = self.log_chk(hdr, 20)
assert fhdr == hdr
assert message == 'very large origin values relative to dims; leaving as set, ignoring for affine'
pytest.raises(*raiser)
dxer = self.header_class.diagnose_binaryblock
assert dxer(hdr.binaryblock) == 'very large origin values relative to dims'
```

**Workflow: test header scaling** (complexity: 1.00)

```python
img_class = self.image_class
hdr_class = img_class.header_class
if not hdr_class.has_data_slope:
    return
arr = np.arange(24, dtype=np.int16).reshape((2, 3, 4))
invalid_slopes = (0, np.nan, np.inf, -np.inf)
for slope in (1,) + invalid_slopes:
    self.assert_null_scaling(arr, slope, None)
if not hdr_class.has_data_intercept:
    return
invalid_inters = (np.nan, np.inf, -np.inf)
invalid_pairs = tuple(itertools.product(invalid_slopes, invalid_inters))
bad_slopes_good_inter = tuple(itertools.product(invalid_slopes, (0, 1)))
good_slope_bad_inters = tuple(itertools.product((1, 2), invalid_inters))
for slope, inter in invalid_pairs + bad_slopes_good_inter + good_slope_bad_inters:
    self.assert_null_scaling(arr, slope, inter)
```

**Workflow: test nan2zero range ok** (complexity: 1.00)

```python
img_class = self.image_class
arr = np.arange(24, dtype=np.float32).reshape((2, 3, 4))
arr[0, 0, 0] = np.nan
arr[1, 0, 0] = 256
img = img_class(arr, np.eye(4))
rt_img = bytesio_round_trip(img)
assert_array_equal(rt_img.get_fdata(), arr)
img.set_data_dtype(np.uint8)
with np.errstate(invalid='ignore'):
    rt_img = bytesio_round_trip(img)
assert rt_img.get_fdata()[0, 0, 0] == 0
```

**Workflow: test checks** (complexity: 1.00)

```python
hdr_t = self.header_class()
assert self._dxer(hdr_t) == ''
hdr = hdr_t.copy()
hdr['sizeof_hdr'] = 1
with suppress_warnings():
    assert self._dxer(hdr) == 'sizeof_hdr should be ' + str(self.sizeof_hdr)
hdr = hdr_t.copy()
hdr['datatype'] = 0
assert self._dxer(hdr) == 'data code 0 not supported\nbitpix does not match datatype'
hdr = hdr_t.copy()
hdr['bitpix'] = 0
assert self._dxer(hdr) == 'bitpix does not match datatype'
```

**Workflow: test log checks** (complexity: 1.00)

```python
HC = self.header_class
hdr = HC()
with suppress_warnings():
    hdr['sizeof_hdr'] = 350
    fhdr, message, raiser = self.log_chk(hdr, 30)
assert fhdr['sizeof_hdr'] == self.sizeof_hdr
assert message == f'sizeof_hdr should be {self.sizeof_hdr}; set sizeof_hdr to {self.sizeof_hdr}'
pytest.raises(*raiser)
hdr = HC()
hdr.set_data_dtype('RGB')
fhdr, message, raiser = self.log_chk(hdr, 0)
hdr = HC()
hdr['datatype'] = -1
with suppress_warnings():
    fhdr, message, raiser = self.log_chk(hdr, 40)
assert message == 'data code -1 not recognized; not attempting fix'
pytest.raises(*raiser)
hdr['datatype'] = 255
fhdr, message, raiser = self.log_chk(hdr, 40)
assert message == 'data code 255 not supported; not attempting fix'
pytest.raises(*raiser)
hdr = HC()
hdr['datatype'] = 16
hdr['bitpix'] = 16
fhdr, message, raiser = self.log_chk(hdr, 10)
assert fhdr['bitpix'] == 32
assert message == 'bitpix does not match datatype; setting bitpix to match datatype'
pytest.raises(*raiser)
```

**Workflow: test pixdim log checks** (complexity: 1.00)

```python
HC = self.header_class
hdr = HC()
hdr['pixdim'][1] = -2
fhdr, message, raiser = self.log_chk(hdr, 35)
assert fhdr['pixdim'][1] == 2
assert message == 'pixdim[1,2,3] should be positive; setting to abs of pixdim values'
pytest.raises(*raiser)
hdr = HC()
hdr['pixdim'][1] = 0
fhdr, message, raiser = self.log_chk(hdr, 30)
assert fhdr['pixdim'][1] == 1
assert message == PIXDIM0_MSG
pytest.raises(*raiser)
hdr = HC()
hdr['pixdim'][1] = 0
hdr['pixdim'][2] = -2
fhdr, message, raiser = self.log_chk(hdr, 35)
assert fhdr['pixdim'][1] == 1
assert fhdr['pixdim'][2] == 2
assert message == 'pixdim[1,2,3] should be non-zero and pixdim[1,2,3] should be positive; setting 0 dims to 1 and setting to abs of pixdim values'
pytest.raises(*raiser)
```

**Workflow: test logger error** (complexity: 1.00)

```python
HC = self.header_class
hdr = HC()
str_io = StringIO()
logger = logging.getLogger('test.logger')
logger.addHandler(logging.StreamHandler(str_io))
hdr['datatype'] = 16
hdr['bitpix'] = 16
logger.setLevel(10)
log_cache = (imageglobals.logger, imageglobals.error_level)
try:
    imageglobals.logger = logger
    hdr.copy().check_fix()
    assert str_io.getvalue() == 'bitpix does not match datatype; setting bitpix to match datatype\n'
    imageglobals.error_level = 10
    with pytest.raises(HeaderDataError):
        hdr.copy().check_fix()
finally:
    imageglobals.logger, imageglobals.error_level = log_cache
```

**Workflow: test data dtype** (complexity: 1.00)

```python
all_supported_types = ((2, np.uint8), (4, np.int16), (8, np.int32), (16, np.float32), (32, np.complex64), (64, np.float64), (128, np.dtype([('R', 'u1'), ('G', 'u1'), ('B', 'u1')])))
all_unsupported_types = (np.void, 'none', 'all', 0)

def assert_set_dtype(dt_spec, np_dtype):
    hdr = self.header_class()
    hdr.set_data_dtype(dt_spec)
    assert_dt_equal(hdr.get_data_dtype(), np_dtype)
for code, npt in all_supported_types:
    assert_set_dtype(code, npt)
    assert_set_dtype(npt, npt)
    assert_set_dtype(np.dtype(npt), npt)
for npt in self.supported_np_types:
    assert_set_dtype(npt, npt)
    assert_set_dtype(np.dtype(npt), npt)
    assert_set_dtype(np.dtype(npt).newbyteorder(), npt)
    assert_set_dtype(np.dtype(npt).str, npt)
    if np.dtype(npt).str[0] in '=|<>':
        assert_set_dtype(np.dtype(npt).str[1:], npt)
assert_set_dtype(float, np.float64)
np_sys_int = np.dtype(int).type
if issubclass(self.header_class, Nifti1Header):
    with pytest.raises(ValueError):
        hdr = self.header_class()
        hdr.set_data_dtype(int)
elif np_sys_int in self.supported_np_types:
    assert_set_dtype(int, np_sys_int)
hdr = self.header_class()
for inp in all_unsupported_types:
    with pytest.raises(HeaderDataError):
        hdr.set_data_dtype(inp)
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 12
**Total Settings:** 241
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 12 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 73
**Categories:** 3

### Overview

- **README.rst** (`README.rst`)

### Workflows

- **workflow_failure.md** (`.github/workflows/workflow_failure.md`)

### Other

- **CODE_OF_CONDUCT.md** (`.github/CODE_OF_CONDUCT.md`)
- **CONTRIBUTING.md** (`.github/CONTRIBUTING.md`)
- **README.rst** (`doc/README.rst`)
- **api.rst** (`doc/source/api.rst`)
- **changelog.rst** (`doc/source/changelog.rst`)
- *...and 66 more*

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

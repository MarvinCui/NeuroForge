---
name: afni
description: Local codebase analysis for afni
doc_version: 
---

# afni Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `afni`
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

- **Strategy**: 2 instances
- **Factory**: 1 instances
- **Adapter**: 1 instances

*Total: 4 high-confidence patterns*

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
assert_true(hdr.default_x_flip)
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
hdr['origin'][:3] = [3, 4, 5]
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 6.0], [0.0, 2.0, 0.0, -6.0], [0.0, 0.0, 1.0, -4.0], [0.0, 0.0, 0.0, 1.0]])
hdr['origin'] = 0
hdr.set_data_shape((3, 5))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -0.0], [0.0, 0.0, 0.0, 1.0]])
hdr.set_data_shape((3, 5, 7))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

**Workflow: test scaling** (complexity: 1.00)

```python
hdr = self.header_class()
hdr.set_data_shape((1, 2, 3))
hdr.set_data_dtype(np.int16)
S3 = BytesIO()
data = np.arange(6, dtype=np.float64).reshape((1, 2, 3))
hdr.data_to_fileobj(data, S3)
data_back = hdr.data_from_fileobj(S3)
assert_array_almost_equal(data, data_back, 4)
data_back2 = hdr.data_from_fileobj(S3)
assert_array_equal(data_back, data_back2, 4)
```

**Workflow: test origin checks** (complexity: 1.00)

```python
HC = self.header_class
hdr = HC()
hdr.data_shape = [1, 1, 1]
hdr['origin'][0] = 101
fhdr, message, raiser = self.log_chk(hdr, 20)
assert_equal(fhdr, hdr)
assert_equal(message, 'very large origin values relative to dims; leaving as set, ignoring for affine')
assert_raises(*raiser)
dxer = self.header_class.diagnose_binaryblock
assert_equal(dxer(hdr.binaryblock), 'very large origin values relative to dims')
```

**Workflow: test spm scale checks** (complexity: 1.00)

```python
hdr = self.header_class()
hdr['scl_slope'] = np.nan
fhdr, message, raiser = self.log_chk(hdr, 30)
assert_equal(fhdr['scl_slope'], 1)
assert_equal(message, 'scale slope is %s; should be finite; setting scalefactor "scl_slope" to 1' % np.nan)
assert_raises(*raiser)
dxer = self.header_class.diagnose_binaryblock
assert_equal(dxer(hdr.binaryblock), 'scale slope is %s; should be finite' % np.nan)
hdr['scl_slope'] = np.inf
assert_equal(dxer(hdr.binaryblock), 'scale slope is %s; should be finite' % np.inf)
```

**test origin affine** (complexity: 1.00)

```python
assert_true(hdr.default_x_flip)
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

**test origin affine** (complexity: 1.00)

```python
hdr.set_data_shape((3, 5))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -0.0], [0.0, 0.0, 0.0, 1.0]])
```

**test origin affine** (complexity: 1.00)

```python
hdr.set_data_shape((3, 5, 7))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

**Workflow: test inverse** (complexity: 1.00)

```python
args = call_init_args(init_args)
inp = inp_arg_gen()
dtype = klass(*args).get_supported_dtypes()[0]
args = call_init_args(init_args)
node = klass(*args, dtype=dtype)
_train_if_necessary(inp, node, sup_arg_gen)
extra = [execute_arg_gen(inp)] if execute_arg_gen else []
out = node.execute(inp, *extra)
rec = node.inverse(out)
inp = inp.astype(dtype)
assert_array_almost_equal_diff(rec, inp, decimal - 3)
assert rec.dtype == dtype
```

**Workflow: test FANode** (complexity: 1.00)

```python
d = 10
N = 5000
k = 4
mu = uniform((1, d)) * 3.0 + 2.0
sigma = uniform((d,)) * 0.01
A = numx_rand.normal(size=(k, d))
y = numx_rand.normal(0.0, 1.0, size=(N, k))
noise = numx_rand.normal(0.0, 1.0, size=(N, d)) * sigma
x = mult(y, A) + mu + noise
fa = mdp.nodes.FANode(output_dim=k, dtype='d')
fa.train(x)
fa.stop_training()
assert_array_almost_equal(fa.mu[0, :], mean(x, axis=0), 5)
assert_array_almost_equal(fa.sigma, std(noise, axis=0) ** 2, 2)
AA = numx.concatenate((A, fa.A.T), axis=0)
u, s, vh = utils.svd(AA)
assert sum(s / max(s) > 0.01) == k, 'A and its estimation do not span the same subspace'
y = fa.execute(x)
fa.generate_input()
fa.generate_input(10)
fa.generate_input(y)
fa.generate_input(y, noise=True)
est = fa.generate_input(numx.zeros((N, k)), noise=True)
est -= fa.mu
assert_array_almost_equal(numx.diag(numx.cov(est, rowvar=0)), fa.sigma, 3)
assert_almost_equal(numx.amax(abs(numx.mean(est, axis=0)), axis=None), 0.0, 3)
est = fa.generate_input(100000)
assert_array_almost_equal_diff(numx.cov(est, rowvar=0), mdp.utils.mult(fa.A, fa.A.T), 1)
```

**Workflow: test NIPALSNode** (complexity: 1.00)

```python
line_x = numx.zeros((1000, 2), 'd')
line_y = numx.zeros((1000, 2), 'd')
line_x[:, 0] = numx.linspace(-1, 1, num=1000, endpoint=1)
line_y[:, 1] = numx.linspace(-0.2, 0.2, num=1000, endpoint=1)
mat = numx.concatenate((line_x, line_y))
des_var = std(mat, axis=0)
utils.rotate(mat, uniform() * 2 * numx.pi)
mat += uniform(2)
pca = mdp.nodes.NIPALSNode(conv=1e-15, max_it=1000)
pca.train(mat)
act_mat = pca.execute(mat)
assert_array_almost_equal(mean(act_mat, axis=0), [0, 0], decimal)
assert_array_almost_equal(std(act_mat, axis=0), des_var, decimal)
pca.inverse(act_mat[:, :1])
pca2 = mdp.nodes.PCANode()
pca2.train(mat)
pca2.stop_training()
assert_array_almost_equal(pca2.d, pca.d, decimal)
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 19
**Total Settings:** 121
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 19 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 16
**Categories:** 2

### Overview

- **README.rst** (`README.rst`)

### Other

- **connectionstoc1.rst** (`doc/macaque_sphinx/connectionstoc1.rst`)
- **glossary.rst** (`doc/macaque_sphinx/glossary.rst`)
- **index.rst** (`doc/macaque_sphinx/index.rst`)
- **ROI_45a.rst** (`doc/macaque_sphinx/macaque/ROI_45a.rst`)
- **ROI_45a_connections.rst** (`doc/macaque_sphinx/macaque/ROI_45a_connections.rst`)
- *...and 10 more*

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

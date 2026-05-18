# nilearn Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_save_glm_to_bids_infer_filenames

- Kind: `test-workflow`
- Source: `nilearn/nilearn/glm/tests/test_io.py:483`
- Note: Workflow: Check that output filenames can be inferred from BIDS input.

```python
'Check that output filenames can be inferred from BIDS input.'
n_sub = 1
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2], n_voxels=20)
models, imgs, events, _ = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
model = models[0]
run_imgs = imgs[0]
events = events[0]
model.minimize_memory = False
model.fit(run_imgs=run_imgs, events=events)
assert len(model._reporting_data['run_imgs']) == 4
if kwargs == {'height_control': None}:
    with pytest.warns(FutureWarning, match="the default 'threshold' will be set to"):
        model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], **kwargs)
else:
    model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], **kwargs)
EXPECTED_FILENAME_ENDINGS = ['sub-01_task-main_space-MNI_contrast-c0_stat-z_statmap.nii.gz', 'sub-01_task-main_space-MNI_contrast-c0_clusters.tsv', 'sub-01_task-main_space-MNI_contrast-c0_clusters.json', 'sub-01_ses-01_task-main_run-01_space-MNI_stat-rsquared_statmap.nii.gz', 'sub-01_ses-02_task-main_run-02_space-MNI_design.tsv', 'sub-01_ses-01_task-main_run-02_space-MNI_design.json', 'sub-01_task-main_space-MNI_mask.nii.gz']
if is_matplotlib_installed():
    EXPECTED_FILENAME_ENDINGS.extend(['sub-01_ses-02_task-main_run-01_space-MNI_design.png', 'sub-01_ses-02_task-main_run-01_space-MNI_corrdesign.png', 'sub-01_ses-01_task-main_run-02_space-MNI_contrast-c0_design.png'])
for fname in EXPECTED_FILENAME_ENDINGS:
    assert (tmp_path / 'output' / 'sub-01' / fname).exists()
with (tmp_path / 'output' / 'sub-01' / 'sub-01_task-main_space-MNI_contrast-c0_clusters.json').open('r') as f:
    metadata = json.load(f)
expected_keys = ['Cluster size threshold (voxels)', 'Minimum distance (mm)']
if 'height_control' not in kwargs:
    expected_keys.extend(['Height control', 'Threshold (computed)'])
else:
    expected_keys.extend(['Height control', 'Threshold Z'])
for key in expected_keys:
    assert key in metadata
```

## 2. test_check_output_2d

- Kind: `test-workflow`
- Source: `nilearn/nilearn/maskers/tests/test_surface_labels_masker.py:565`
- Note: Workflow: Check actual content of the transform and inverse_transform when we have multiple timepoints. - Use a label mask with more than one label. - Use data with known content and expected mean. and background label data has random value. - Check that output data is properly averaged, even when labels are spread across hemispheres.

```python
'Check actual content of the transform and inverse_transform when\n    we have multiple timepoints.\n\n    - Use a label mask with more than one label.\n    - Use data with known content and expected mean.\n      and background label data has random value.\n    - Check that output data is properly averaged,\n      even when labels are spread across hemispheres.\n    '
surf_label_img = SurfaceImage(surf_mesh, polydata_labels)
masker = SurfaceLabelsMasker(labels_img=surf_label_img, standardize=None)
masker = masker.fit()
data = {'left': np.asarray([data_left_1d_with_expected_mean - 1, data_left_1d_with_expected_mean + 1]).T, 'right': np.asarray([data_right_1d_with_expected_mean - 1, data_right_1d_with_expected_mean + 1]).T}
surf_img_2d = SurfaceImage(surf_mesh, data)
signal = masker.transform(surf_img_2d)
assert signal.shape == (surf_img_2d.shape[1], masker.n_elements_)
expected_signal = np.asarray([expected_signal - 1, expected_signal + 1])
assert_array_equal(signal, expected_signal)
assert masker.labels_ == [0, 1, 2, 10, 20]
assert masker.lut_['name'].to_list() == ['Background', '1', '2', '10', '20']
assert masker.region_names_ == {0: '1', 1: '2', 2: '10', 3: '20'}
assert masker.region_ids_ == {'background': 0, 0: 1, 1: 2, 2: 10, 3: 20}
img = masker.inverse_transform(signal)
assert img.shape[0] == surf_img_2d.shape[0]
expected_inverse_data = {'left': np.asarray([[expected_mean_value['2'] - 1, 0.0, expected_mean_value['10'] - 1, expected_mean_value['1'] - 1], [expected_mean_value['2'] + 1, 0.0, expected_mean_value['10'] + 1, expected_mean_value['1'] + 1]]).T, 'right': np.asarray([[expected_mean_value['10'] - 1, expected_mean_value['1'] - 1, expected_mean_value['20'] - 1, expected_mean_value['20'] - 1, 0.0], [expected_mean_value['10'] + 1, expected_mean_value['1'] + 1, expected_mean_value['20'] + 1, expected_mean_value['20'] + 1, 0.0]]).T}
assert_array_equal(img.data.parts['left'], expected_inverse_data['left'])
assert_array_equal(img.data.parts['right'], expected_inverse_data['right'])
```

## 3. test_explicit_fixed_effects

- Kind: `test-workflow`
- Source: `nilearn/nilearn/glm/tests/test_first_level.py:168`
- Note: Workflow: Test the fixed effects performed manually/explicitly.

```python
'Test the fixed effects performed manually/explicitly.'
shapes, rk = ([(*shape_3d_default, 4), (*shape_3d_default, 5)], 3)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
contrast = np.eye(rk)[1]
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[:1])
dic1 = multi_run_model.compute_contrast(contrast, output_type='all')
multi_run_model.fit(fmri_data[1], design_matrices=design_matrices[1:])
dic2 = multi_run_model.compute_contrast(contrast, output_type='all')
multi_run_model.fit(fmri_data, design_matrices=design_matrices)
fixed_fx_dic = multi_run_model.compute_contrast(contrast, output_type='all')
contrasts = [dic1['effect_size'], dic2['effect_size']]
variance = [dic1['effect_variance'], dic2['effect_variance']]
fixed_fx_contrast, fixed_fx_variance, fixed_fx_stat, _ = compute_fixed_effects(contrasts, variance, mask)
assert_almost_equal(get_data(fixed_fx_contrast), get_data(fixed_fx_dic['effect_size']))
assert_almost_equal(get_data(fixed_fx_variance), get_data(fixed_fx_dic['effect_variance']))
assert_almost_equal(get_data(fixed_fx_stat), get_data(fixed_fx_dic['stat']))
with pytest.raises(ValueError, match='The number of contrast images .* differs from the number of variance images'):
    compute_fixed_effects(contrasts * 2, variance, mask)
with pytest.raises(ValueError, match='degrees of freedom .* differs .* contrast images'):
    compute_fixed_effects(contrasts, variance, mask, dofs=[100])
```

## 4. test_multi_nifti_labels_masker

- Kind: `test-workflow`
- Source: `nilearn/nilearn/maskers/tests/test_multi_nifti_labels_masker.py:72`
- Note: Workflow: Check working of shape/affine checks.

```python
'Check working of shape/affine checks.'
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
signals11 = masker11.fit_transform(fmri11_img)
assert signals11.shape == (length, n_regions)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
masker11.fit()
masker11.inverse_transform(signals11)
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask11_img, resampling_target=None, keep_masked_labels=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals11 = masker11.fit_transform(fmri11_img)
assert signals11.shape == (length, n_regions)
signals_input = [fmri11_img, fmri11_img]
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals11_list = masker11.fit_transform(signals_input)
for signals in signals11_list:
    assert signals.shape == (length, n_regions)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
signals11_list = masker11.fit_transform(signals_input)
for signals in signals11_list:
    assert signals.shape == (length, n_regions)
for signals in signals11_list:
    fmri11_img_r = masker11.inverse_transform(signals)
    assert fmri11_img_r.shape == fmri11_img.shape
    assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
```

## 5. test_rena_clustering

- Kind: `test-workflow`
- Source: `nilearn/nilearn/regions/tests/test_rena_clustering.py:86`
- Note: Workflow: test rena clustering

```python
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=5)
data = get_data(data_img)
mask = get_data(mask_img)
X = np.empty((data.shape[3], int(mask.sum())))
for i in range(data.shape[3]):
    X[i, :] = np.copy(data[:, :, :, i])[get_data(mask_img) != 0]
nifti_masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
n_voxels = nifti_masker.transform(data_img).shape[1]
rena = ReNA(mask_img, n_clusters=10)
X_red = rena.fit_transform(X)
X_compress = rena.inverse_transform(X_red)
assert rena.n_clusters_ == 10
assert X.shape == X_compress.shape
memory = Memory(location=None)
rena = ReNA(mask_img, n_clusters=-2, memory=memory)
with pytest.raises(ValueError):
    rena.fit(X)
rena = ReNA(mask_img, n_clusters=10, scaling=True)
X_red = rena.fit_transform(X)
X_compress = rena.inverse_transform(X_red)
for n_iter in [-2, 0]:
    rena = ReNA(mask_img, n_iter=n_iter, memory=memory)
    with pytest.raises(ValueError):
        rena.fit(X)
for n_clusters in [1, 2, 4, 8]:
    rena = ReNA(mask_img, n_clusters=n_clusters, n_iter=1, memory=memory).fit(X)
    assert n_clusters != rena.n_clusters_
del n_voxels, X_red, X_compress
```

## 6. test_check_output_1d

- Kind: `test-workflow`
- Source: `nilearn/nilearn/maskers/tests/test_surface_labels_masker.py:456`
- Note: Workflow: Check actual content of the transform and inverse_transform. - Use a label mask with more than one label. - Use data with known content and expected mean. and background label data has random value. - Check that output data is properly averaged, even when labels are spread across hemispheres.

```python
'Check actual content of the transform and inverse_transform.\n\n    - Use a label mask with more than one label.\n    - Use data with known content and expected mean.\n      and background label data has random value.\n    - Check that output data is properly averaged,\n      even when labels are spread across hemispheres.\n    '
surf_label_img = SurfaceImage(surf_mesh, polydata_labels)
masker = SurfaceLabelsMasker(labels_img=surf_label_img, standardize=None)
masker = masker.fit()
data = {'left': data_left_1d_with_expected_mean, 'right': data_right_1d_with_expected_mean}
surf_img_1d = SurfaceImage(surf_mesh, data)
signal = masker.transform(surf_img_1d)
assert_array_equal(signal, np.asarray(expected_signal))
assert masker.labels_ == [0, 1, 2, 10, 20]
assert masker.lut_['name'].to_list() == ['Background', '1', '2', '10', '20']
assert masker.region_names_ == {0: '1', 1: '2', 2: '10', 3: '20'}
assert masker.region_ids_ == {'background': 0, 0: 1, 1: 2, 2: 10, 3: 20}
img = masker.inverse_transform(signal)
assert img.shape[0] == surf_img_1d.shape[0]
expected_inverse_data = {'left': np.asarray(inverse_data_left_1d_with_expected_mean).T, 'right': np.asarray(inverse_data_right_1d_with_expected_mean).T}
assert_array_equal(img.data.parts['left'], expected_inverse_data['left'])
assert_array_equal(img.data.parts['right'], expected_inverse_data['right'])
```

## 7. test_nifti_labels_masker_errors

- Kind: `test-workflow`
- Source: `nilearn/nilearn/maskers/tests/test_nifti_labels_masker.py:122`
- Note: Workflow: Check working of shape/affine checks.

```python
'Check working of shape/affine checks.'
masker = NiftiLabelsMasker(standardize=None)
with pytest.raises(TypeError, match='input should be a NiftiLike object'):
    masker.fit()
shape1 = (*shape_3d_default, length)
shape2 = (12, 10, 14, length)
affine2 = np.diag((1, 2, 3, 1))
fmri12_img, mask12_img = generate_random_img(shape1, affine=affine2)
fmri21_img, mask21_img = generate_random_img(shape2, affine=affine_eye)
labels11_img = generate_labeled_regions(shape1[:3], affine=affine_eye, n_regions=n_regions)
masker11 = NiftiLabelsMasker(labels11_img, resampling_target=None, standardize=None)
masker11.fit()
with pytest.raises(ValueError, match='Images have different affine matrices.'):
    masker11.transform(fmri12_img)
with pytest.raises(ValueError, match='Images have incompatible shapes.'):
    masker11.transform(fmri21_img)
masker11 = NiftiLabelsMasker(labels11_img, mask_img=mask12_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker11.fit()
masker11 = NiftiLabelsMasker(labels11_img, mask_img=mask21_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker11.fit()
```

## 8. test_multi_nifti_maps_masker

- Kind: `test-workflow`
- Source: `nilearn/nilearn/maskers/tests/test_multi_nifti_maps_masker.py:72`
- Note: Workflow: Check basic functions of MultiNiftiMapsMasker. - fit, transform, fit_transform, inverse_transform. - 4D and list[4D] inputs

```python
'Check basic functions of MultiNiftiMapsMasker.\n\n    - fit, transform, fit_transform, inverse_transform.\n    - 4D and list[4D] inputs\n    '
fmri11_img, mask11_img = generate_fake_fmri(shape_3d_default, affine=affine_eye, length=length)
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask11_img, resampling_target=None, keep_masked_maps=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed in version 0\\.15'):
    signals11 = masker.fit_transform(fmri11_img)
assert signals11.shape == (length, n_regions)
MultiNiftiMapsMasker(img_maps, standardize=None).fit_transform(fmri11_img)
signals_input = [fmri11_img, fmri11_img]
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    signals11_list = masker.fit_transform(signals_input)
for signals in signals11_list:
    assert signals.shape == (length, n_regions)
for signals in signals11_list:
    fmri11_img_r = masker.inverse_transform(signals)
    assert fmri11_img_r.shape == fmri11_img.shape
    assert_almost_equal(fmri11_img_r.affine, fmri11_img.affine)
masker = MultiNiftiMapsMasker(img_maps, resampling_target=None, standardize=None)
masker.fit()
masker.inverse_transform(signals)
```

## 9. test_inverse_transform

- Kind: `test-workflow`
- Source: `nilearn/nilearn/maskers/tests/test_nifti_spheres_masker.py:281`
- Note: Workflow: Applying the sphere_extraction example from above backwards.

```python
'Applying the sphere_extraction example from above backwards.'
data = rng.random((3, 3, 3, 5))
img = Nifti1Image(data, affine_eye)
masker = NiftiSpheresMasker([(1, 1, 1)], radius=1, standardize=None)
masker.fit()
signal = masker.transform(img)
with pytest.raises(ValueError, match='Please provide mask_img'):
    masker.inverse_transform(signal)
mask_img = np.zeros((3, 3, 3))
mask_img[1, :, :] = 1
mask_img = Nifti1Image(mask_img, affine_eye)
masker = NiftiSpheresMasker([(1, 1, 1)], radius=1, mask_img=mask_img, standardize=None)
masker.fit()
s = masker.transform(img)
mask = np.zeros((3, 3, 3), dtype=bool)
mask[:, 1, 1] = True
mask[1, :, 1] = True
mask[1, 1, :] = True
array_mask = np.logical_and(mask, get_data(mask_img))
inverse_map = masker.inverse_transform(s)
assert_array_equal(np.mean(get_data(inverse_map), axis=-1) != 0, array_mask)
assert_array_equal(get_data(inverse_map)[array_mask].mean(0), s[:, 0])
assert_array_equal(inverse_map.shape[:3], mask_img.shape)
```

## 10. test_signal_extraction_with_maps_and_labels

- Kind: `test-workflow`
- Source: `nilearn/nilearn/regions/tests/test_signal_extraction.py:524`
- Note: Workflow: test signal extraction with maps and labels

```python
labels = list(range(N_REGIONS + 1))
labels_data = get_data(labeled_regions)
maps_data = np.zeros((*shape_3d_default, N_REGIONS))
for n, l in enumerate(labels):
    if n == 0:
        continue
    maps_data[labels_data == l, n - 1] = 1
maps_img = Nifti1Image(maps_data, labeled_regions.affine)
maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, keep_masked_maps=True)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, keep_masked_labels=True)
assert_almost_equal(maps_signals, labels_signals)
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=True)
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, mask_img=mask_img, keep_masked_maps=True)
assert_almost_equal(maps_signals, labels_signals)
assert maps_signals.shape[1] == N_REGIONS
assert maps_labels == list(range(len(maps_labels)))
assert labels_signals.shape == (N_TIMEPOINTS, N_REGIONS)
assert labels_labels == labels[1:]
labels_img_r = signals_to_img_labels(labels_signals, labeled_regions, mask_img=mask_img)
assert labels_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
maps_img_r = signals_to_img_maps(maps_signals, maps_img, mask_img=mask_img)
assert maps_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
```

## 11. test_dict_learning

- Kind: `test-workflow`
- Source: `nilearn/nilearn/decomposition/tests/test_dict_learning.py:48`
- Note: Workflow: Check content of components_img_.

```python
'Check content of components_img_.'
masker = NiftiMasker(mask_img=decomposition_mask_img).fit()
mask = get_data(decomposition_mask_img) != 0
flat_mask = mask.ravel()
masked_components = canica_components[:, flat_mask]
dict_init = masker.inverse_transform(masked_components)
smoothing_fwhm = None
dict_learning = DictLearning(n_components=4, random_state=RANDOM_STATE, dict_init=dict_init, mask=decomposition_mask_img, smoothing_fwhm=smoothing_fwhm, standardize='zscore_sample', alpha=1)
dict_learning_auto_init = DictLearning(n_components=4, random_state=RANDOM_STATE, mask=decomposition_mask_img, n_epochs=10, smoothing_fwhm=smoothing_fwhm, standardize='zscore_sample', alpha=1)
maps = {}
for estimator in [dict_learning, dict_learning_auto_init]:
    estimator.fit(canica_data)
    check_decomposition_estimator(dict_learning, data_type)
    maps[estimator] = get_data(estimator.components_img_)
    maps[estimator] = np.reshape(np.rollaxis(maps[estimator], 3, 0)[:, mask], (4, flat_mask.sum()))
for this_dict_learning in [dict_learning]:
    these_maps = maps[this_dict_learning]
    S = np.sqrt(np.sum(masked_components ** 2, axis=1))
    S[S == 0] = 1
    masked_components /= S[:, np.newaxis]
    S = np.sqrt(np.sum(these_maps ** 2, axis=1))
    S[S == 0] = 1
    these_maps /= S[:, np.newaxis]
    K = np.abs(masked_components.dot(these_maps.T))
    recovered_maps = np.sum(K > 0.9)
    assert recovered_maps >= 2
```

## 12. test_fmri_inputs_errors

- Kind: `test-workflow`
- Source: `nilearn/nilearn/glm/tests/test_non_parametric_inference.py:125`
- Note: Workflow: Test several errors with non_parametric_inference.

```python
'Test several errors with non_parametric_inference.'
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design([shape_4d_default], rk=1)
flm = FirstLevelModel(subject_label='01').fit(fmri_data, design_matrices=design_matrices)
p, q = (80, 10)
X = rng.standard_normal(size=(p, q))
sdes = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
shape_3d = [(*shape_3d_default, 1)]
_, fmri_data, _ = generate_fake_fmri_data_and_design(shape_3d)
fmri_data = fmri_data[0]
niimgs = [fmri_data, fmri_data, fmri_data]
niimg_4d = concat_imgs(niimgs)
match = 'No second-level contrast is specified.'
with pytest.raises(ValueError, match=match):
    non_parametric_inference(niimgs, None, sdes)
with pytest.raises(ValueError, match=match):
    non_parametric_inference(niimgs, confounds, sdes)
with pytest.raises(ValueError, match=match):
    non_parametric_inference(niimg_4d, None, sdes)
with pytest.raises(TypeError, match='second_level_input must be'):
    non_parametric_inference(flm)
with pytest.raises(TypeError, match='at least two'):
    non_parametric_inference([fmri_data])
with pytest.raises(ValueError, match='require a design matrix'):
    non_parametric_inference(niimgs)
with pytest.raises(TypeError):
    non_parametric_inference([*niimgs, []], confounds)
with pytest.raises(ValueError, match='File not found: .*'):
    non_parametric_inference('random string object')
```

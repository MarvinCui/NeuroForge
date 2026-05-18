# nilearn Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Save Glm To Bids Infer Filenames

- Kind: `tutorial`
- Source: `references/tutorials/save-glm-to-bids-infer-filenames/save-glm-to-bids-infer-filenames.md`
- Note: Workflow: Check that output filenames can be inferred from BIDS input.

```python
# Setup
# Fixtures: tmp_path, kwargs

# Workflow
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

## 2. How To: Check Output 2D

- Kind: `tutorial`
- Source: `references/tutorials/check-output-2d/check-output-2d.md`
- Note: Workflow: Check actual content of the transform and inverse_transform when we have multiple timepoints. - Use a label mask with more than one label. - Use data with known content and expected mean. and background label d

```python
# Setup
# Fixtures: surf_mesh, polydata_labels, expected_mean_value, expected_signal, data_left_1d_with_expected_mean, data_right_1d_with_expected_mean

# Workflow
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

## 3. How To: Check Output 1D

- Kind: `tutorial`
- Source: `references/tutorials/check-output-1d/check-output-1d.md`
- Note: Workflow: Check actual content of the transform and inverse_transform. - Use a label mask with more than one label. - Use data with known content and expected mean. and background label data has random value. - Check tha

```python
# Setup
# Fixtures: surf_mesh, polydata_labels, expected_signal, data_left_1d_with_expected_mean, data_right_1d_with_expected_mean, inverse_data_left_1d_with_expected_mean, inverse_data_right_1d_with_expected_mean

# Workflow
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

## 4. How To: Multi Nifti Labels Masker

- Kind: `tutorial`
- Source: `references/tutorials/multi-nifti-labels-masker/multi-nifti-labels-masker.md`
- Note: Workflow: Check working of shape/affine checks.

```python
# Setup
# Fixtures: affine_eye, n_regions, shape_3d_default, length, img_labels

# Workflow
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

## 5. How To: Explicit Fixed Effects

- Kind: `tutorial`
- Source: `references/tutorials/explicit-fixed-effects/explicit-fixed-effects.md`
- Note: Workflow: Test the fixed effects performed manually/explicitly.

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
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

## 6. How To: Label Image No Background Missing Regions

- Kind: `tutorial`
- Source: `references/tutorials/label-image-no-background-missing-regions/label-image-no-background-missing-regions.md`
- Note: Workflow: Test label image with no background. Compare behavior when background is present in label image (background_label=1) or not (background_label=0). Regression test for https://github.com/nilearn/nilearn/issues/55

```python
# Setup
# Fixtures: surf_mesh, surf_img_2d, background_label, n_expected_regions, kwargs

# Workflow
'Test label image with no background.\n\n    Compare behavior when background is present in label image\n    (background_label=1) or not (background_label=0).\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5596\n    '
data = {'left': np.asarray([3, 3, 1, 1]), 'right': np.asarray([1, 1, 3, 2, 3])}
label_img = SurfaceImage(surf_mesh, data)
labels_masker = SurfaceLabelsMasker(labels_img=label_img, background_label=background_label, standardize=None, **kwargs).fit()
if 'lut' in kwargs:
    assert list(kwargs['lut'].columns) == list(labels_masker.lut_.columns)
masked_data = labels_masker.transform(surf_img_2d(2))
assert masked_data.shape[1] == n_expected_regions
assert len(labels_masker.region_names_) == n_expected_regions
if background_label == 1:
    assert 'Background' in labels_masker.lut_['name'].to_list()
    assert len(labels_masker.labels_) == n_expected_regions + 1
    assert len(labels_masker.region_ids_) == n_expected_regions + 1
else:
    assert 'Background' not in labels_masker.lut_['name'].to_list()
    assert len(labels_masker.labels_) == n_expected_regions
    assert len(labels_masker.region_ids_) == n_expected_regions
```

## 7. How To: Rena Clustering

- Kind: `tutorial`
- Source: `references/tutorials/rena-clustering/rena-clustering.md`
- Note: Workflow: test rena clustering

```python
# Workflow
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

## 8. How To: Multi Nifti Labels Masker Resampling Target

- Kind: `tutorial`
- Source: `references/tutorials/multi-nifti-labels-masker-resampling-target/multi-nifti-labels-masker-resampling-target.md`
- Note: Workflow: Test labels masker with resampling target in 'data', 'labels'. Must return resampled labels having number of labels equal with transformed shape of 2nd dimension. This tests are added based on issue #1673 in Ni

```python
# Workflow
"Test labels masker with resampling target in 'data', 'labels'.\n\n    Must return resampled labels having number of labels\n    equal with transformed shape of 2nd dimension.\n\n    This tests are added based on issue #1673 in Nilearn.\n    "
shape = (13, 11, 12)
affine = np.eye(4) * 2
fmri_img, _ = generate_fake_fmri(shape, affine=affine, length=21)
labels_img = generate_labeled_regions((9, 8, 6), affine=np.eye(4), n_regions=10)
for resampling_target in ['data', 'labels']:
    masker = MultiNiftiLabelsMasker(labels_img=labels_img, resampling_target=resampling_target, keep_masked_labels=True, standardize=None)
    if resampling_target == 'data':
        with pytest.warns(UserWarning, match='After resampling the label image to the data image, the following labels were removed'), pytest.warns(FutureWarning, match='In version 0.15.0, "keep_masked_labels" parameter will be removed'):
            signals = masker.fit_transform(fmri_img)
    else:
        with pytest.warns(FutureWarning, match='In version 0.15.0, "keep_masked_labels" parameter will be removed'):
            signals = masker.fit_transform(fmri_img)
    resampled_labels_img = masker.labels_img_
    n_resampled_labels = len(np.unique(get_data(resampled_labels_img)))
    assert n_resampled_labels - 1 == signals.shape[1]
    compressed_img = masker.inverse_transform(signals)
    with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
        signals2 = masker.fit_transform(fmri_img)
    compressed_img2 = masker.inverse_transform(signals2)
    assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

## 9. How To: Save Glm To Bids Second Level

- Kind: `tutorial`
- Source: `references/tutorials/save-glm-to-bids-second-level/save-glm-to-bids-second-level.md`
- Note: Workflow: Test save_glm_to_bids on a SecondLevelModel. This test reuses code from nilearn.glm.tests.test_second_level.test_high_level_glm_with_paths.

```python
# Setup
# Fixtures: tmp_path_factory, prefix

# Workflow
'Test save_glm_to_bids on a SecondLevelModel.\n\n    This test reuses code from\n    nilearn.glm.tests.test_second_level.test_high_level_glm_with_paths.\n    '
tmpdir = tmp_path_factory.mktemp('test_save_glm_to_bids_second_level')
EXPECTED_FILENAMES = ['contrast-effectsOfInterest_stat-F_statmap.nii.gz', 'contrast-effectsOfInterest_stat-effect_statmap.nii.gz', 'contrast-effectsOfInterest_stat-p_statmap.nii.gz', 'contrast-effectsOfInterest_stat-variance_statmap.nii.gz', 'contrast-effectsOfInterest_stat-z_statmap.nii.gz', 'contrast-effectsOfInterest_clusters.tsv', 'contrast-effectsOfInterest_clusters.json', 'design.tsv', 'stat-errorts_statmap.nii.gz', 'stat-rsquared_statmap.nii.gz', 'statmap.json', 'mask.nii.gz', 'report.html']
if is_matplotlib_installed():
    EXPECTED_FILENAMES.extend(['design.png', 'contrast-effectsOfInterest_design.png'])
shapes = ((3, 3, 3, 1),)
rk = 3
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes, rk)
fmri_data = fmri_data[0]
model = SecondLevelModel(mask_img=mask, minimize_memory=False)
Y = [fmri_data] * 2
X = pd.DataFrame([[1]] * 2, columns=['intercept'])
model = model.fit(Y, design_matrix=X)
contrasts = {'effects of interest': np.eye(len(model.design_matrix_.columns))[0]}
contrast_types = {'effects of interest': 'F'}
save_glm_to_bids(model=model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmpdir, prefix=prefix, **KWARGS)
assert (tmpdir / 'dataset_description.json').exists()
for fname in EXPECTED_FILENAMES:
    assert (tmpdir / 'group' / f'{prefix}_{fname}').exists()
```

## 10. How To: Nifti Labels Masker Errors

- Kind: `tutorial`
- Source: `references/tutorials/nifti-labels-masker-errors/nifti-labels-masker-errors.md`
- Note: Workflow: Check working of shape/affine checks.

```python
# Setup
# Fixtures: affine_eye, shape_3d_default, n_regions, length

# Workflow
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

## 11. How To: Multi Nifti Maps Masker

- Kind: `tutorial`
- Source: `references/tutorials/multi-nifti-maps-masker/multi-nifti-maps-masker.md`
- Note: Workflow: Check basic functions of MultiNiftiMapsMasker. - fit, transform, fit_transform, inverse_transform. - 4D and list[4D] inputs

```python
# Setup
# Fixtures: affine_eye, length, n_regions, shape_3d_default, img_maps

# Workflow
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

## 12. How To: Signal Extraction With Maps And Labels

- Kind: `tutorial`
- Source: `references/tutorials/signal-extraction-with-maps-and-labels/signal-extraction-with-maps-and-labels.md`
- Note: Workflow: test signal extraction with maps and labels

```python
# Setup
# Fixtures: labeled_regions, fmri_img, shape_3d_default

# Workflow
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

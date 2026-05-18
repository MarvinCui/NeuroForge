# nilearn Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Functional Connectomes #1

- Kind: `documentation`
- Source: `references/documentation/other/functional_connectomes.rst`
- Note: Documentation code block extracted for implementation use.

```text
from nilearn import plotting
plotting.plot_roi(atlas_filename)
```

## 2. Readme #1

- Kind: `documentation`
- Source: `references/documentation/other/README.md`
- Note: Documentation code block extracted for implementation use.

```python
import numpy as np
from nilearn.surface import surface

for n in [10, 20, 40, 80, 160]:
    ball_cloud = surface._uniform_ball_cloud(n_points=n)
    np.savetxt(f"./ball_cloud_{b}_samples.csv", ball_cloud)
```

## 3. First Level Model

- Kind: `documentation`
- Source: `references/documentation/other/first_level_model.rst`
- Note: Documentation code block extracted for implementation use.

```bash
design_matrices = make_first_level_design_matrix(frame_times, events,
seed_masker = NiftiSpheresMasker([pcc_coords], radius=10)
seed_time_series = seed_masker.fit_transform(adhd_dataset.func[0])
fmri_glm = FirstLevelModel()
fmri_glm = fmri_glm.fit(subject_data, design_matrices=design_matrices)
observed_timeseries = masker.fit_transform(fmri_img)
predicted_timeseries = masker.fit_transform(fmri_glm.predicted[0])
```

## 4. Index

- Kind: `documentation`
- Source: `references/documentation/other/index.rst`
- Note: Documentation code block extracted for implementation use.

```bash
display = plotting.plot_stat_map(img)
display = plotting.plot_epi(...)
img = datasets.fetch_localizer_button_task()["tmap"]
view = plotting.view_img_on_surf(img, threshold="90%", surf_mesh="fsaverage")
destrieux = datasets.fetch_atlas_surf_destrieux()
fsaverage = datasets.fetch_surf_fsaverage()
view = plotting.view_surf(
motor_images = datasets.load_sample_motor_activation_image()
mesh = surface.load_surf_mesh(fsaverage.pial_right)
map = surface.vol_to_surf(motor_images.images[0], mesh)
fig = plotting.plot_surf_stat_map(
view = plotting.view_connectome(correlation_matrix, coords, edge_threshold="90%")
```

## 5. Input Output

- Kind: `documentation`
- Source: `references/documentation/other/input_output.rst`
- Note: Documentation code block extracted for implementation use.

```bash
data = nilearn.image.get_data(img)
smoothed_img = image.smooth_img("/path/to/project")
result_img = smooth_img(["dataset/subject1.nii", "dataset/subject2.nii"])
result_img = smooth_img("dataset/subject_*.nii")
result_img = smooth_img("~/dataset/subject_01.nii")
haxby_dataset = datasets.fetch_haxby()
labels = pd.read_csv(haxby_dataset.session_target[0], sep=" ")
```

## 6. Manual Pipeline

- Kind: `documentation`
- Source: `references/documentation/other/manual_pipeline.rst`
- Note: Documentation code block extracted for implementation use.

```bash
dataset = datasets.fetch_haxby()
masker = NiftiMasker(mask_img=mask_filename, standardize=True)
fmri_masked = masker.fit_transform(fmri_filename)
prediction = svc.predict(fmri_masked)
coef_img = masker.inverse_transform(coef_)
```

## 7. Connectome Extraction

- Kind: `documentation`
- Source: `references/documentation/other/connectome_extraction.rst`
- Note: Documentation code block extracted for implementation use.

```bash
estimator = GraphicalLassoCV()
measure = ConnectivityMeasure(kind="tangent")
connectivities = measure.fit([time_series_1, time_series_2, ...])
```

## 8. Gpu Usage

- Kind: `documentation`
- Source: `references/documentation/other/gpu_usage.rst`
- Note: Documentation code block extracted for implementation use.

```bash
estimator = Ridge(alpha=100.0, solver="svd")
param_grid = dict(alpha=np.logspace(-6, 6, 100))
search_cv_cpu = GridSearchCV(estimator, param_grid)
fmri_data_cupy = cp.asarray(fmri_data)
stimuli_cupy = cp.asarray(stimuli)
search_cv_gpu = GridSearchCV(estimator, param_grid)
fmri_data_torch = torch.from_numpy(fmri_data)
stimuli_torch = torch.from_numpy(stimuli)
```

## 9. Manipulating Images

- Kind: `documentation`
- Source: `references/documentation/other/manipulating_images.rst`
- Note: Documentation code block extracted for implementation use.

```text
>>> import numpy as np
>>> target_affine = np.diag((3, 3, 3))
```

## 10. Readme

- Kind: `documentation`
- Source: `references/documentation/overview/README.rst`
- Note: Documentation code block extracted for implementation use.

```bash
python3 -m venv /
python -m pip install -U nilearn
```

# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: 3D Images | references/tutorials/3d-images/3d-images.md | Workflow: Test that the MultiNiftiMasker works with 3D images. Note that fit() requires all images in list to have the same affine. | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: 3X3 Affine Bbox | references/tutorials/3x3-affine-bbox/3x3-affine-bbox.md | Workflow: Test that the bounding-box is properly computed when transforming with a negative affine component. This is specifically to test for a change in behavior between scipy < 0.18 and scipy >= 0.18, which is an inte | copy, math, os, sys, pathlib |
| How To: 4D Affine Bounding Box Error | references/tutorials/4d-affine-bounding-box-error/4d-affine-bounding-box-error.md | Workflow: test 4d affine bounding box error | copy, math, os, sys, pathlib |
| How To: Add Absolute Paths | references/tutorials/add-absolute-paths/add-absolute-paths.md | Workflow: Test _add_absolute_paths. | hashlib, json, os, re, stat |
| How To: Add Metadata To Bids Derivatives With Json Path | references/tutorials/add-metadata-to-bids-derivatives-with-json-path/add-metadata-to-bids-derivatives-with-json-path.md | Workflow: test add metadata to bids derivatives with json path | json, numpy, pandas, pytest, nibabel |
| How To: Affine Output Mask | references/tutorials/affine-output-mask/affine-output-mask.md | Workflow: test affine output mask | pathlib, numpy, pandas, pytest, nibabel |
| How To: All Resolution Inference | references/tutorials/all-resolution-inference/all-resolution-inference.md | Workflow: test all resolution inference | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: All Resolution Inference One Sided | references/tutorials/all-resolution-inference-one-sided/all-resolution-inference-one-sided.md | Workflow: test all resolution inference one sided | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: All Resolution Inference One Voxel | references/tutorials/all-resolution-inference-one-voxel/all-resolution-inference-one-voxel.md | Workflow: test all resolution inference one voxel | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: All Resolution Inference Surface | references/tutorials/all-resolution-inference-surface/all-resolution-inference-surface.md | Workflow: Check cluster_level_inference that runs on each hemisphere. | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: All Resolution Inference Surface Mask | references/tutorials/all-resolution-inference-surface-mask/all-resolution-inference-surface-mask.md | Workflow: Check cluster_level_inference that runs on each hemisphere. Here mask excludes the right hemisphere. | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: All Resolution Inference With Mask | references/tutorials/all-resolution-inference-with-mask/all-resolution-inference-with-mask.md | Workflow: test all resolution inference with mask | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: Anisotropic Sphere Extraction | references/tutorials/anisotropic-sphere-extraction/anisotropic-sphere-extraction.md | Workflow: Test non anisotropic sphere extraction. | numpy, pytest, nibabel, numpy.testing, sklearn.utils.estimator_checks |
| How To: Apply Mask | references/tutorials/apply-mask/apply-mask.md | Workflow: Test smoothing of timeseries extraction. | re, warnings, numpy, pytest, nibabel |
| How To: Apply Mask 3D Accepted | references/tutorials/apply-mask-3d-accepted/apply-mask-3d-accepted.md | Workflow: Check that 3D data is accepted. | re, warnings, numpy, pytest, nibabel |
| How To: Apply Mask Nan | references/tutorials/apply-mask-nan/apply-mask-nan.md | Workflow: Check that NaNs in the data do not propagate. | re, warnings, numpy, pytest, nibabel |
| How To: Are Array Identical | references/tutorials/are-array-identical/are-array-identical.md | Workflow: test are array identical | pathlib, numpy, pytest, nilearn._utils.numpy_conversions |
| How To: As Ndarray | references/tutorials/as-ndarray/as-ndarray.md | Workflow: test as ndarray | pathlib, numpy, pytest, nilearn._utils.numpy_conversions |
| How To: As Ndarray Memmap | references/tutorials/as-ndarray-memmap/as-ndarray-memmap.md | Workflow: test as ndarray memmap | pathlib, numpy, pytest, nilearn._utils.numpy_conversions |
| How To: As Ndarray More | references/tutorials/as-ndarray-more/as-ndarray-more.md | Workflow: test as ndarray more | pathlib, numpy, pytest, nilearn._utils.numpy_conversions |
| How To: Bad Inputs | references/tutorials/bad-inputs/bad-inputs.md | Workflow: test bad inputs | numpy, pytest, nilearn._utils.segmentation |
| How To: Base Estimator Invalid L1 Ratio | references/tutorials/base-estimator-invalid-l1-ratio/base-estimator-invalid-l1-ratio.md | Workflow: Check that 0 < L1 ratio < 1. | functools, numpy, pytest, numpy.testing, scipy |
| How To: Bids Dataset No Run Entity | references/tutorials/bids-dataset-no-run-entity/bids-dataset-no-run-entity.md | Workflow: n_runs = 0 produces files without the run entity. | json, numpy, pandas, pytest, nibabel |
| How To: Bids Dataset No Session | references/tutorials/bids-dataset-no-session/bids-dataset-no-session.md | Workflow: n_ses = 0 prevent creation of a session folder. | json, numpy, pandas, pytest, nibabel |
| How To: Cache Mixin Without Expand User | references/tutorials/cache-mixin-without-expand-user/cache-mixin-without-expand-user.md | Workflow: test cache mixin without expand user | shutil, pathlib, pytest, joblib, nilearn |
| How To: Cache Shelving | references/tutorials/cache-shelving/cache-shelving.md | Workflow: test cache shelving | shutil, pathlib, pytest, joblib, nilearn |
| How To: Calculate Tfce | references/tutorials/calculate-tfce/calculate-tfce.md | Workflow: Test calculate_tfce. | math, numpy, pytest, numpy.testing, scipy.ndimage |
| How To: Calculate Tr | references/tutorials/calculate-tr/calculate-tr.md | Workflow: Test the TR calculation. | warnings, numpy, pytest, numpy.testing, nilearn.glm.first_level.hemodynamic_models |
| How To: Canica Square Img | references/tutorials/canica-square-img/canica-square-img.md | Workflow: Check content of components. | numpy, pytest, numpy.testing, nilearn._utils.helpers, nilearn.decomposition.canica |
| How To: Carousel Several Runs | references/tutorials/carousel-several-runs/carousel-several-runs.md | Workflow: Check that a carousel is present when there is more than 1 run. | pathlib, numpy, pandas, pytest, nilearn._utils.data_gen |
| How To: Check Embedded Masker Attribute Forwarding | references/tutorials/check-embedded-masker-attribute-forwarding/check-embedded-masker-attribute-forwarding.md | Workflow: Check attribute forwarding. | numpy, pytest, joblib, nibabel, sklearn.base |
| How To: Check Events | references/tutorials/check-events/check-events.md | Workflow: test check events | pathlib, numpy, pandas, pytest, numpy.testing |
| How To: Check Events Errors | references/tutorials/check-events-errors/check-events-errors.md | Workflow: Test the function which tests that the events data describes a valid experimental paradigm. | pathlib, numpy, pandas, pytest, numpy.testing |
| How To: Check Events Warnings | references/tutorials/check-events-warnings/check-events-warnings.md | Workflow: Test the function which tests that the events data describes a valid experimental paradigm. | pathlib, numpy, pandas, pytest, numpy.testing |
| How To: Check Inputs Length | references/tutorials/check-inputs-length/check-inputs-length.md | Workflow: test check inputs length | collections, numbers, warnings, numpy, pytest |
| How To: Check Memory | references/tutorials/check-memory/check-memory.md | Workflow: test check memory | shutil, pathlib, pytest, joblib, nilearn |
| How To: Check Mesh And Data | references/tutorials/check-mesh-and-data/check-mesh-and-data.md | Workflow: test check mesh and data | warnings, pathlib, numpy, pytest, nibabel |
| How To: Check Output 1D | references/tutorials/check-output-1d/check-output-1d.md | Workflow: Check actual content of the transform and inverse_transform. - Use a label mask with more than one label. - Use data with known content and expected mean. and background label data has random value. - Check tha | numpy, pandas, pytest, numpy.testing, sklearn.utils.estimator_checks |
| How To: Check Output 2D | references/tutorials/check-output-2d/check-output-2d.md | Workflow: Check actual content of the transform and inverse_transform when we have multiple timepoints. - Use a label mask with more than one label. - Use data with known content and expected mean. and background label d | numpy, pandas, pytest, numpy.testing, sklearn.utils.estimator_checks |
| How To: Check Param Grid Replacement | references/tutorials/check-param-grid-replacement/check-param-grid-replacement.md | Workflow: test check param grid replacement | collections, numbers, warnings, numpy, pytest |
| How To: Check Parameters Transform | references/tutorials/check-parameters-transform/check-parameters-transform.md | Workflow: test check parameters transform | warnings, numpy, pandas, pytest, nibabel |
| How To: Check Threshold For Error | references/tutorials/check-threshold-for-error/check-threshold-for-error.md | Workflow: Tests nilearn._utils.param_validation.check_threshold for errors. | numpy, pytest, scipy.stats, nilearn._utils.extmath, nilearn._utils.param_validation |
| How To: Check Values Epoch Argument Smoke | references/tutorials/check-values-epoch-argument-smoke/check-values-epoch-argument-smoke.md | Workflow: Smoke test to check different values of the epoch argument. | numpy, pytest, nilearn.decomposition.dict_learning, nilearn.decomposition.tests.conftest, nilearn.image |
| How To: Clean Confounds Detrending | references/tutorials/clean-confounds-detrending/clean-confounds-detrending.md | Workflow: Test detrending. No trend should exist in the output. | pathlib, typing, numpy, pytest, scipy.signal |
| How To: Clean Confounds Inputs | references/tutorials/clean-confounds-inputs/clean-confounds-inputs.md | Workflow: Check several types of supported inputs. | pathlib, typing, numpy, pytest, scipy.signal |
| How To: Clean Detrending | references/tutorials/clean-detrending/clean-detrending.md | Workflow: Check effect of clean with detrending. This test is inspired from Scipy docstring of detrend function. - clean should not modify inputs - check effect when fintie results requested | pathlib, typing, numpy, pytest, scipy.signal |
| How To: Cluster Level | references/tutorials/cluster-level/cluster-level.md | Workflow: Test non-parametric inference with cluster-level inference. | numpy, pandas, pytest, nibabel, numpy.testing |
| How To: Cluster Level Parameters Smoke | references/tutorials/cluster-level-parameters-smoke/cluster-level-parameters-smoke.md | Workflow: Test combinations of parameters related to cluster-level inference. | warnings, numpy, pytest, nibabel, numpy.testing |
| How To: Cluster Level With Covariates | references/tutorials/cluster-level-with-covariates/cluster-level-with-covariates.md | Workflow: Test non-parametric inference with cluster-level inference in the context of covariates. | numpy, pandas, pytest, nibabel, numpy.testing |
| How To: Cluster Level With Single Covariates | references/tutorials/cluster-level-with-single-covariates/cluster-level-with-single-covariates.md | Workflow: Test non-parametric inference with cluster-level inference in the context of covariates. | numpy, pandas, pytest, nibabel, numpy.testing |
| How To: Cluster Nearest Neighbor | references/tutorials/cluster-nearest-neighbor/cluster-nearest-neighbor.md | Workflow: Check that _cluster_nearest_neighbor preserves within-cluster voxels, projects voxels to the correct cluster, and handles singleton clusters. | warnings, copy, numpy, pandas, pytest |
| How To: Cmap As Lookup Table With Background | references/tutorials/cmap-as-lookup-table-with-background/cmap-as-lookup-table-with-background.md | Workflow: Ensure that the background color is dropped from lut. regression test for https://github.com/nilearn/nilearn/issues/5934 | matplotlib.pyplot, numpy, pandas, pytest, nibabel |
| How To: Cmap With One Level | references/tutorials/cmap-with-one-level/cmap-with-one-level.md | Workflow: Test we can handle cmap with only 1 level. Regression test for https://github.com/nilearn/nilearn/issues/4255 | matplotlib.pyplot, numpy, pandas, pytest, nibabel |
| How To: Coef Shape | references/tutorials/coef-shape/coef-shape.md | Workflow: test coef shape | numpy, pytest, nibabel, numpy.testing, sklearn.datasets |
| How To: Compare Design Matrix To Spm | references/tutorials/compare-design-matrix-to-spm/compare-design-matrix-to-spm.md | Workflow: test compare design matrix to spm | pathlib, numpy, pandas, pytest, numpy.testing |
| How To: Compute Background Mask | references/tutorials/compute-background-mask/compute-background-mask.md | Workflow: Test compute_background_mask. | re, warnings, numpy, pytest, nibabel |
| How To: Compute Background Mask Errors Warnings | references/tutorials/compute-background-mask-errors-warnings/compute-background-mask-errors-warnings.md | Workflow: Check that we get a ValueError for incorrect shape. | re, warnings, numpy, pytest, nibabel |
| How To: Compute Brain Mask | references/tutorials/compute-brain-mask/compute-brain-mask.md | Workflow: Test compute_brain_mask. | re, warnings, numpy, pytest, nibabel |
| How To: Compute Epi Mask | references/tutorials/compute-epi-mask/compute-epi-mask.md | Workflow: Test compute_epi_mask. | re, warnings, numpy, pytest, nibabel |
| How To: Compute Epi Mask Errors Warnings | references/tutorials/compute-epi-mask-errors-warnings/compute-epi-mask-errors-warnings.md | Workflow: Check that we get a ValueError for incorrect shape. | re, warnings, numpy, pytest, nibabel |

## Snippets Extracted

- `references/tutorials/save-glm-to-bids-infer-filenames/save-glm-to-bids-infer-filenames.md`: How To: Save Glm To Bids Infer Filenames
- `references/tutorials/check-output-2d/check-output-2d.md`: How To: Check Output 2D
- `references/tutorials/check-output-1d/check-output-1d.md`: How To: Check Output 1D
- `references/tutorials/multi-nifti-labels-masker/multi-nifti-labels-masker.md`: How To: Multi Nifti Labels Masker
- `references/tutorials/explicit-fixed-effects/explicit-fixed-effects.md`: How To: Explicit Fixed Effects
- `references/tutorials/label-image-no-background-missing-regions/label-image-no-background-missing-regions.md`: How To: Label Image No Background Missing Regions
- `references/tutorials/rena-clustering/rena-clustering.md`: How To: Rena Clustering
- `references/tutorials/multi-nifti-labels-masker-resampling-target/multi-nifti-labels-masker-resampling-target.md`: How To: Multi Nifti Labels Masker Resampling Target
- `references/tutorials/save-glm-to-bids-second-level/save-glm-to-bids-second-level.md`: How To: Save Glm To Bids Second Level
- `references/tutorials/nifti-labels-masker-errors/nifti-labels-masker-errors.md`: How To: Nifti Labels Masker Errors
- `references/tutorials/multi-nifti-maps-masker/multi-nifti-maps-masker.md`: How To: Multi Nifti Maps Masker
- `references/tutorials/signal-extraction-with-maps-and-labels/signal-extraction-with-maps-and-labels.md`: How To: Signal Extraction With Maps And Labels

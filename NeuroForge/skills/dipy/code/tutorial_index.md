# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: 3D Points | references/tutorials/3d-points/3d-points.md | Workflow: test 3D points | itertools, numpy, numpy.testing, dipy.segment.clustering, dipy.segment.featurespeed |
| How To: 3D Segments | references/tutorials/3d-segments/3d-segments.md | Workflow: test 3D segments | itertools, numpy, numpy.testing, dipy.segment.clustering, dipy.segment.featurespeed |
| How To: 4D Moving | references/tutorials/4d-moving/4d-moving.md | Workflow: test 4D moving | logging, pathlib, tempfile, nibabel, numpy |
| How To: 4D Static | references/tutorials/4d-static/4d-static.md | Workflow: test 4D static | logging, pathlib, tempfile, nibabel, numpy |
| How To: Add Noise | references/tutorials/add-noise/add-noise.md | Workflow: test add noise | numpy, numpy.testing, dipy.core.gradients, dipy.data, dipy.io.gradients |
| How To: Adjacency Calc | references/tutorials/adjacency-calc/adjacency-calc.md | Workflow: Test adjacency_calc function, which calculates indices of adjacent voxels | numpy, numpy.testing, dipy.utils.volume |
| How To: Affine | references/tutorials/affine/affine.md | Workflow: test affine | logging, pathlib, tempfile, nibabel, numpy |
| How To: Affreg All Transforms | references/tutorials/affreg-all-transforms/affreg-all-transforms.md | Workflow: test affreg all transforms | numpy, numpy.linalg, numpy.testing, dipy.align, dipy.align.imaffine |
| How To: Afq Profile | references/tutorials/afq-profile/afq-profile.md | Workflow: test afq profile | numpy, numpy.testing, dipy.stats.analysis, dipy.tracking.streamline |
| How To: All Constant | references/tutorials/all-constant/all-constant.md | Workflow: test all constant | random, numpy, numpy.testing, dipy.core.gradients, dipy.core.sphere |
| How To: All Zeros | references/tutorials/all-zeros/all-zeros.md | Workflow: test all zeros | random, numpy, numpy.testing, dipy.core.gradients, dipy.core.sphere |
| How To: Anisotropic Reduced Mse | references/tutorials/anisotropic-reduced-mse/anisotropic-reduced-mse.md | Workflow: test anisotropic reduced MSE | warnings, numpy, numpy.testing, pytest, scipy.integrate |
| How To: Apply Post Processing Shift Intensity No Op When Baselines Match | references/tutorials/apply-post-processing-shift-intensity-no-op-when-baselines-match/apply-post-processing-shift-intensity-no-op-when-baselines-match.md | Workflow: test apply post processing shift intensity no op when baselines match | warnings, numpy, numpy.testing, pytest, dipy.core.gradients |
| How To: Approx Ei Traj | references/tutorials/approx-ei-traj/approx-ei-traj.md | Workflow: test approx ei traj | warnings, numpy, numpy.testing, dipy.data, dipy.io.streamline |
| How To: Approx Mdl Traj | references/tutorials/approx-mdl-traj/approx-mdl-traj.md | Workflow: test approx mdl traj | warnings, numpy, numpy.testing, dipy.data, dipy.io.streamline |
| How To: Argmax From Countarrs | references/tutorials/argmax-from-countarrs/argmax-from-countarrs.md | Workflow: test argmax from countarrs | numpy, numpy.testing, dipy.reconst.recspeed |
| How To: As Native | references/tutorials/as-native/as-native.md | Workflow: test as native | sys, numpy, numpy.testing, dipy.testing, dipy.testing.decorators |
| How To: Ascm Accuracy | references/tutorials/ascm-accuracy/ascm-accuracy.md | Workflow: test ascm accuracy | nibabel, numpy, numpy.testing, dipy.data, dipy.denoise.adaptive_soft_matching |
| How To: Ascm Random Noise | references/tutorials/ascm-random-noise/ascm-random-noise.md | Workflow: test ascm random noise | nibabel, numpy, numpy.testing, dipy.data, dipy.denoise.adaptive_soft_matching |
| How To: Ascm Rmse With Nlmeans | references/tutorials/ascm-rmse-with-nlmeans/ascm-rmse-with-nlmeans.md | Workflow: test ascm rmse with nlmeans | nibabel, numpy, numpy.testing, dipy.data, dipy.denoise.adaptive_soft_matching |
| How To: Ascm Static | references/tutorials/ascm-static/ascm-static.md | Workflow: test ascm static | nibabel, numpy, numpy.testing, dipy.data, dipy.denoise.adaptive_soft_matching |
| How To: Assert | references/tutorials/assert/assert.md | Workflow: test assert | sys, warnings, numpy, numpy.testing, dipy.testing |
| How To: Auto Response Ssst | references/tutorials/auto-response-ssst/auto-response-ssst.md | Workflow: test auto response ssst | warnings, numpy, numpy.testing, numpy.testing, dipy.core.gradients |
| How To: B0 Threshold Greater Than0 | references/tutorials/b0-threshold-greater-than0/b0-threshold-greater-than0.md | Workflow: Added test case for default b0_threshold set to 50. Checks if error is thrown correctly. | warnings, numpy, numpy.testing, pytest, dipy.core.gradients |
| How To: B0S | references/tutorials/b0s/b0s.md | Workflow: test b0s | warnings, numpy, numpy.testing, pytest, dipy.core.geometry |
| How To: Bdg Get Direction | references/tutorials/bdg-get-direction/bdg-get-direction.md | Workflow: This tests the direction found by the bootstrap direction getter. | warnings, numpy, numpy.testing, dipy.core.geometry, dipy.core.gradients |
| How To: Bdg Initial Direction | references/tutorials/bdg-initial-direction/bdg-initial-direction.md | Workflow: This tests the number of initial directions." | warnings, numpy, numpy.testing, dipy.core.geometry, dipy.core.gradients |
| How To: Bingham Fit | references/tutorials/bingham-fit/bingham-fit.md | Workflow: Tests for bingham function and single Bingham fit | warnings, numpy, numpy.testing, dipy.core.gradients, dipy.data |
| How To: Bingham From Sh | references/tutorials/bingham-from-sh/bingham-from-sh.md | Workflow: test bingham from sh | warnings, numpy, numpy.testing, dipy.core.gradients, dipy.data |
| How To: Blockwise 3D Sigma Map Not Reduced To Global Mean | references/tutorials/blockwise-3d-sigma-map-not-reduced-to-global-mean/blockwise-3d-sigma-map-not-reduced-to-global-mean.md | Workflow: Blockwise 3D sigma maps should affect denoising beyond a global mean. | time, numpy, numpy.testing, pytest, dipy.denoise.denspeed |
| How To: Blockwise Sigma Array Support | references/tutorials/blockwise-sigma-array-support/blockwise-sigma-array-support.md | Workflow: Test that blockwise method supports different sigma input formats. | time, numpy, numpy.testing, pytest, dipy.denoise.denspeed |
| How To: Bootstrap Array | references/tutorials/bootstrap-array/bootstrap-array.md | Workflow: test bootstrap array | warnings, numpy, numpy.linalg, numpy.testing, numpy.testing |
| How To: Bounding Box | references/tutorials/bounding-box/bounding-box.md | Workflow: test bounding box | warnings, numpy, numpy.testing, pytest, scipy.ndimage |
| How To: Bounds X0 | references/tutorials/bounds-x0/bounds-x0.md | Workflow: Test to check if setting bounds for signal where initial value is higher than subsequent values works. These values are from the IVIM dataset which can be obtained by using the `read_ivim` function from dipy.da | warnings, numpy, numpy.testing, pytest, dipy.core.gradients |
| How To: Bspline Design Matrix Row Sums | references/tutorials/bspline-design-matrix-row-sums/bspline-design-matrix-row-sums.md | Workflow: test bspline design matrix row sums | numpy, pytest, dipy.core.gradients, dipy.denoise.bias_correction, dipy.segment.mask |
| How To: Bspline Design Matrix Shape | references/tutorials/bspline-design-matrix-shape/bspline-design-matrix-shape.md | Workflow: test bspline design matrix shape | numpy, pytest, dipy.core.gradients, dipy.denoise.bias_correction, dipy.segment.mask |
| How To: Btable Prepare | references/tutorials/btable-prepare/btable-prepare.md | Workflow: test btable prepare | warnings, numpy, numpy.testing, pytest, dipy.core.geometry |
| How To: Buan Profile | references/tutorials/buan-profile/buan-profile.md | Workflow: test buan profile | numpy, numpy.testing, dipy.stats.analysis, dipy.tracking.streamline |
| How To: Bundle Shape Profile | references/tutorials/bundle-shape-profile/bundle-shape-profile.md | Workflow: test bundle shape profile | numpy.testing, pytest, dipy.align.streamwarp, dipy.data, dipy.tracking.streamline |
| How To: Bundles Distances Mam | references/tutorials/bundles-distances-mam/bundles-distances-mam.md | Workflow: test bundles distances mam | warnings, numpy, numpy.testing, dipy.data, dipy.io.streamline |
| How To: Bundlewarp | references/tutorials/bundlewarp/bundlewarp.md | Workflow: test bundlewarp | numpy.testing, pytest, dipy.align.streamwarp, dipy.data, dipy.tracking.streamline |
| How To: Bundlewarp Vector Filed | references/tutorials/bundlewarp-vector-filed/bundlewarp-vector-filed.md | Workflow: test bundlewarp vector filed | numpy.testing, pytest, dipy.align.streamwarp, dipy.data, dipy.tracking.streamline |
| How To: Callablearray | references/tutorials/callablearray/callablearray.md | Workflow: test CallableArray | functools, numpy, numpy.testing, dipy.core.sphere, dipy.reconst.multi_voxel |
| How To: Calling Cartesian Laplacian With Precomputed Matrices | references/tutorials/calling-cartesian-laplacian-with-precomputed-matrices/calling-cartesian-laplacian-with-precomputed-matrices.md | Workflow: test calling cartesian laplacian with precomputed matrices | warnings, numpy, numpy.testing, pytest, scipy.integrate |
| How To: Calling Spherical Laplacian With Precomputed Matrices | references/tutorials/calling-spherical-laplacian-with-precomputed-matrices/calling-spherical-laplacian-with-precomputed-matrices.md | Workflow: test calling spherical laplacian with precomputed matrices | warnings, numpy, numpy.testing, pytest, scipy.integrate |
| How To: Carlson Rd | references/tutorials/carlson-rd/carlson-rd.md | Workflow: test carlson rd | random, warnings, numpy, numpy.testing, dipy.core.geometry |
| How To: Carlson Rf | references/tutorials/carlson-rf/carlson-rf.md | Workflow: test carlson rf | random, warnings, numpy, numpy.testing, dipy.core.geometry |
| How To: Cart Distance | references/tutorials/cart-distance/cart-distance.md | Workflow: test cart distance | itertools, random, numpy, numpy.testing, dipy.core.geometry |
| How To: Cartesian Normalization | references/tutorials/cartesian-normalization/cartesian-normalization.md | Workflow: test cartesian normalization | warnings, numpy, numpy.testing, pytest, scipy.integrate |
| How To: Cc 2D | references/tutorials/cc-2d/cc-2d.md | Workflow: Test 2D SyN with CC metric Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good quality. | nibabel.eulerangles, numpy, numpy.testing, dipy.align, dipy.align.imwarp |
| How To: Cc 3D | references/tutorials/cc-3d/cc-3d.md | Workflow: Test 3D SyN with CC metric Register a volume created by stacking copies of a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registratio | nibabel.eulerangles, numpy, numpy.testing, dipy.align, dipy.align.imwarp |
| How To: Cc Factors 2D | references/tutorials/cc-factors-2d/cc-factors-2d.md | Workflow: Compares the output of the optimized function to compute the cross- correlation factors against a direct (not optimized, but less error prone) implementation. | numpy, numpy.testing, dipy.align, dipy.testing.decorators |
| How To: Cc Factors 3D | references/tutorials/cc-factors-3d/cc-factors-3d.md | Workflow: Compares the output of the optimized function to compute the cross- correlation factors against a direct (not optimized, but less error prone) implementation. | numpy, numpy.testing, dipy.align, dipy.testing.decorators |
| How To: Center And Transform | references/tutorials/center-and-transform/center-and-transform.md | Workflow: test center and transform | types, warnings, numpy, numpy.linalg, numpy.testing |
| How To: Change Range | references/tutorials/change-range/change-range.md | Workflow: Test change_range method in PeaksTab. | unittest.mock, numpy, pytest, dipy.direction.peaks, dipy.testing.decorators |
| How To: Change Slice | references/tutorials/change-slice/change-slice.md | Workflow: Test change_slice method in PeaksTab. | unittest.mock, numpy, pytest, dipy.direction.peaks, dipy.testing.decorators |
| How To: Check Directions | references/tutorials/check-directions/check-directions.md | Workflow: test check directions | numpy, numpy.testing, dipy.core.gradients, dipy.data, dipy.io.gradients |
| How To: Check Img Dtype | references/tutorials/check-img-dtype/check-img-dtype.md | Workflow: test check img dtype | numpy, numpy.testing, dipy.direction.peaks, dipy.testing.decorators, dipy.viz.horizon.util |
| How To: Check Img Shapes | references/tutorials/check-img-shapes/check-img-shapes.md | Workflow: test check img shapes | numpy, numpy.testing, dipy.direction.peaks, dipy.testing.decorators, dipy.viz.horizon.util |
| How To: Check Md5 Error Message Contains Checksums | references/tutorials/check-md5-error-message-contains-checksums/check-md5-error-message-contains-checksums.md | Workflow: test check md5 error message contains checksums | http.server, importlib, logging, os, pathlib |

## Snippets Extracted

- `references/tutorials/affreg-all-transforms/affreg-all-transforms.md`: How To: Affreg All Transforms
- `references/tutorials/em-2d-demons/em-2d-demons.md`: How To: Em 2D Demons
- `references/tutorials/em-2d-gauss-newton/em-2d-gauss-newton.md`: How To: Em 2D Gauss Newton
- `references/tutorials/bdg-get-direction/bdg-get-direction.md`: How To: Bdg Get Direction
- `references/tutorials/validate-patch-radius-and-version/validate-patch-radius-and-version.md`: How To: Validate Patch Radius And Version
- `references/tutorials/streamline-registration/streamline-registration.md`: How To: Streamline Registration
- `references/tutorials/mapmri-isotropic-static-scale-factor/mapmri-isotropic-static-scale-factor.md`: How To: Mapmri Isotropic Static Scale Factor
- `references/tutorials/cc-3d/cc-3d.md`: How To: Cc 3D
- `references/tutorials/mcsd-model-delta/mcsd-model-delta.md`: How To: Mcsd Model Delta
- `references/tutorials/diffeomorphic-map-simplification-2d/diffeomorphic-map-simplification-2d.md`: How To: Diffeomorphic Map Simplification 2D
- `references/tutorials/cc-2d/cc-2d.md`: How To: Cc 2D
- `references/tutorials/mapmri-metrics-anisotropic/mapmri-metrics-anisotropic.md`: How To: Mapmri Metrics Anisotropic

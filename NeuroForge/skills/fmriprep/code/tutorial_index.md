# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: Baseline Found As Str | references/tutorials/baseline-found-as-str/baseline-found-as-str.md | Workflow: test baseline found as str | pathlib, pytest, fmriprep.utils |
| How To: Bids Filter File | references/tutorials/bids-filter-file/bids-filter-file.md | Workflow: test bids filter file | argparse, contextlib, pytest, packaging.version, tests.test_config |
| How To: Bidssourcefile | references/tutorials/bidssourcefile/bidssourcefile.md | Workflow: Test the BIDSSourceFile interface | pytest, fmriprep.interfaces.bids, fmriprep.interfaces.bids |
| How To: Bidsuri | references/tutorials/bidsuri/bidsuri.md | Workflow: Test the BIDSURI interface. | pytest, fmriprep.interfaces.bids, fmriprep.interfaces.bids |
| How To: Bold Native Precomputes | references/tutorials/bold-native-precomputes/bold-native-precomputes.md | Workflow: Test as many combinations of precomputed files and input configurations as possible. | pathlib, nibabel, numpy, pytest, nipype.pipeline.engine.utils |
| How To: Bold Wf | references/tutorials/bold-wf/bold-wf.md | Workflow: Test as many combinations of precomputed files and input configurations as possible. | pathlib, nibabel, numpy, pytest, nipype.pipeline.engine.utils |
| How To: Clip | references/tutorials/clip/clip.md | Workflow: test Clip | nibabel, numpy, nipype.pipeline, fmriprep.interfaces.maths |
| How To: Config Spaces | references/tutorials/config-spaces/config-spaces.md | Workflow: Check that all necessary spaces are recorded in the config. | os, unittest.mock, pytest, niworkflows.utils.spaces, toml |
| How To: Convertaffine | references/tutorials/convertaffine/convertaffine.md | Workflow: test ConvertAffine | nitransforms, numpy, nibabel.tmpdirs, fmriprep.interfaces |
| How To: Derivatives | references/tutorials/derivatives/derivatives.md | Workflow: Check the correct parsing of the derivatives argument. | argparse, contextlib, pytest, packaging.version, tests.test_config |
| How To: Filterdropped | references/tutorials/filterdropped/filterdropped.md | Workflow: test FilterDropped | pathlib, numpy, pandas, nipype.pipeline, fmriprep.interfaces |
| How To: Fmriprep Wf Heterogeneous Sessions | references/tutorials/fmriprep-wf-heterogeneous-sessions/fmriprep-wf-heterogeneous-sessions.md | Workflow: Test on a heterogeneous sessions layout, and test track_sessions behavior | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Framewisedisplacement | references/tutorials/framewisedisplacement/framewisedisplacement.md | Workflow: test FramewiseDisplacement | pathlib, numpy, pandas, nipype.pipeline, fmriprep.interfaces |
| How To: Fsl6 Long Filenames | references/tutorials/fsl6-long-filenames/fsl6-long-filenames.md | Workflow: test fsl6 long filenames | shutil, pathlib, pytest, templateflow.api, looseversion |
| How To: Fslmotionparams | references/tutorials/fslmotionparams/fslmotionparams.md | Workflow: test FSLMotionParams | pathlib, numpy, pandas, nipype.pipeline, fmriprep.interfaces |
| How To: Fslrmsdeviation | references/tutorials/fslrmsdeviation/fslrmsdeviation.md | Workflow: test FSLRMSDeviation | pathlib, numpy, pandas, nipype.pipeline, fmriprep.interfaces |
| How To: Get Estimator B0Field And Intendedfor | references/tutorials/get-estimator-b0field-and-intendedfor/get-estimator-b0field-and-intendedfor.md | Workflow: test get estimator b0field and intendedfor | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Get Estimator Intendedfor | references/tutorials/get-estimator-intendedfor/get-estimator-intendedfor.md | Workflow: test get estimator intendedfor | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Get Estimator Multiple B0Fields | references/tutorials/get-estimator-multiple-b0fields/get-estimator-multiple-b0fields.md | Workflow: test get estimator multiple b0fields | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Get Estimator Overlapping Specs | references/tutorials/get-estimator-overlapping-specs/get-estimator-overlapping-specs.md | Workflow: test get estimator overlapping specs | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Init Fmriprep Wf Sanitize Fmaps | references/tutorials/init-fmriprep-wf-sanitize-fmaps/init-fmriprep-wf-sanitize-fmaps.md | Workflow: test init fmriprep wf sanitize fmaps | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Init Fmriprep Wf Sanitize Plus | references/tutorials/init-fmriprep-wf-sanitize-plus/init-fmriprep-wf-sanitize-plus.md | Workflow: test init fmriprep wf sanitize plus | pathlib, unittest.mock, bids, nibabel, numpy |
| How To: Memory Arg | references/tutorials/memory-arg/memory-arg.md | Workflow: Check the correct parsing of the memory argument. | argparse, contextlib, pytest, packaging.version, tests.test_config |
| How To: Parser Valid | references/tutorials/parser-valid/parser-valid.md | Workflow: Check valid arguments. | argparse, contextlib, pytest, packaging.version, tests.test_config |
| How To: Renameacompcor | references/tutorials/renameacompcor/renameacompcor.md | Workflow: test RenameACompCor | pathlib, numpy, pandas, nipype.pipeline, fmriprep.interfaces |
| How To: Reuse Config | references/tutorials/reuse-config/reuse-config.md | Workflow: test reuse config | argparse, contextlib, pytest, packaging.version, tests.test_config |
| How To: Slice Time Ref | references/tutorials/slice-time-ref/slice-time-ref.md | Workflow: test slice time ref | argparse, contextlib, pytest, packaging.version, tests.test_config |
| How To: Transforms Found As Str | references/tutorials/transforms-found-as-str/transforms-found-as-str.md | Workflow: test transforms found as str | pathlib, pytest, fmriprep.utils |
| How To: Use Syn Sdc | references/tutorials/use-syn-sdc/use-syn-sdc.md | Workflow: test use syn sdc | argparse, contextlib, pytest, packaging.version, tests.test_config |

## Snippets Extracted

- `references/tutorials/bidsuri/bidsuri.md`: How To: Bidsuri
- `references/tutorials/convertaffine/convertaffine.md`: How To: Convertaffine
- `references/tutorials/reuse-config/reuse-config.md`: How To: Reuse Config
- `references/tutorials/derivatives/derivatives.md`: How To: Derivatives
- `references/tutorials/config-spaces/config-spaces.md`: How To: Config Spaces
- `references/tutorials/bidssourcefile/bidssourcefile.md`: How To: Bidssourcefile
- `references/tutorials/bold-wf/bold-wf.md`: How To: Bold Wf
- `references/tutorials/clip/clip.md`: How To: Clip
- `references/tutorials/fmriprep-wf-heterogeneous-sessions/fmriprep-wf-heterogeneous-sessions.md`: How To: Fmriprep Wf Heterogeneous Sessions
- `references/tutorials/bold-native-precomputes/bold-native-precomputes.md`: How To: Bold Native Precomputes
- `references/tutorials/get-estimator-multiple-b0fields/get-estimator-multiple-b0fields.md`: How To: Get Estimator Multiple B0Fields
- `references/tutorials/bids-filter-file/bids-filter-file.md`: How To: Bids Filter File

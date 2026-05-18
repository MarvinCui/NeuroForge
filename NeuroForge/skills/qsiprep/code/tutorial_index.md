# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: Collect Data | references/tutorials/collect-data/collect-data.md | Workflow: Test qsiprep.utils.bids.collect_data. | pytest, niworkflows.utils.testing, re, bids.layout, qsiprep |
| How To: Complex Relpaths Dataset | references/tutorials/complex-relpaths-dataset/complex-relpaths-dataset.md | Workflow: Create a BIDS dataset with complex relative paths for testing. | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Cuda | references/tutorials/cuda/cuda.md | Workflow: Was in CUDATest.sh. XXX: Not called in CircleCI. This tests the following features: - Blip-up + Blip-down DWI series for TOPUP/Eddy - Eddy is run on a CPU - Denoising is skipped Inputs ------ - DSDTI BIDS data | os, shutil, sys, pathlib, unittest.mock |
| How To: Drbuddi Rpe | references/tutorials/drbuddi-rpe/drbuddi-rpe.md | Workflow: Was in DRBUDDI_eddy_rpe_series.sh. This tests the following features: - Blip-up + Blip-down DWI series for TOPUP/Eddy - Eddy is run on a CPU - Denoising is skipped Inputs: ------- - qsiprep single shell results | os, shutil, sys, pathlib, unittest.mock |
| How To: Drbuddi Shoreline Epi | references/tutorials/drbuddi-shoreline-epi/drbuddi-shoreline-epi.md | Workflow: Test EPI fieldmap correction with SHORELine + DRBUDDI. Was in DRBUDDI_SHORELine_epi.sh. This tests the following features: - SHORELine (here, just b=0 registration) motion correction | os, shutil, sys, pathlib, unittest.mock |
| How To: Drbuddi Tensorline Epi | references/tutorials/drbuddi-tensorline-epi/drbuddi-tensorline-epi.md | Workflow: Test EPI fieldmap correction with TENSORLine + DRBUDDI. Was in DRBUDDI_TENSORLine_epi.sh. This tests the following features: - TENSORLine (tensor-based) motion correction | os, shutil, sys, pathlib, unittest.mock |
| How To: Dscsdsi | references/tutorials/dscsdsi/dscsdsi.md | Workflow: DSCSDSI test Was in DSCSDSI.sh. This tests the following features: - Whether the --anat-only workflow is successful - Whether the regular qsiprep workflow can resume using the working directory from --anat-only | os, shutil, sys, pathlib, unittest.mock |
| How To: Dscsdsi Fmap | references/tutorials/dscsdsi-fmap/dscsdsi-fmap.md | Workflow: Run AllFieldmaps test on DSCSDSI data. Was in AllFieldmapsTests.sh. I split it between this and the DSDTI test. XXX: Not called in CircleCI. Instead of running full workflows, this test checks that workflows ca | os, shutil, sys, pathlib, unittest.mock |
| How To: Dsdti Fmap | references/tutorials/dsdti-fmap/dsdti-fmap.md | Workflow: Run AllFieldmaps test on DSDTI data. Was in AllFieldmapsTests.sh. I split it between this and the DSCSDSI test. XXX: Not called in CircleCI. Instead of running full workflows, this test checks that workflows ca | os, shutil, sys, pathlib, unittest.mock |
| How To: Dsdti Nofmap | references/tutorials/dsdti-nofmap/dsdti-nofmap.md | Workflow: DSCDTI_nofmap test. Was in DSDTI_nofmap.sh. This tests the following features: - A workflow with no distortion correction followed by eddy - Eddy is run on a CPU - Denoising is skipped Inputs ------ - DSDTI BID | os, shutil, sys, pathlib, unittest.mock |
| How To: Dsdti Synfmap | references/tutorials/dsdti-synfmap/dsdti-synfmap.md | Workflow: DSCDTI_synfmap test Was in DSDTI_synfmap.sh. This tests the following features: - A workflow with no distortion correction followed by eddy - Eddy is run on a CPU - Denoising is skipped Inputs ------ - DSDTI BI | os, shutil, sys, pathlib, unittest.mock |
| How To: Dwidenoise | references/tutorials/dwidenoise/dwidenoise.md | Workflow: Test qsiprep.interfaces.mrtrix.DWIDenoise. | os, nibabel, qsiprep.interfaces |
| How To: Get Entity Groups With Multipartid | references/tutorials/get-entity-groups-with-multipartid/get-entity-groups-with-multipartid.md | Workflow: Test the get_entity_groups function. | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Get Entity Groups Without Multipartid | references/tutorials/get-entity-groups-without-multipartid/get-entity-groups-without-multipartid.md | Workflow: Test the get_entity_groups function. | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Get Fieldmaps B0Fields | references/tutorials/get-fieldmaps-b0fields/get-fieldmaps-b0fields.md | Workflow: Test the get_fieldmaps function. | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Get Fieldmaps Bidsuri | references/tutorials/get-fieldmaps-bidsuri/get-fieldmaps-bidsuri.md | Workflow: test get fieldmaps bidsuri | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Get Fieldmaps Relpaths | references/tutorials/get-fieldmaps-relpaths/get-fieldmaps-relpaths.md | Workflow: Test the get_fieldmaps function. | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Get Fsl Motion Params Identity Transform | references/tutorials/get-fsl-motion-params-identity-transform/get-fsl-motion-params-identity-transform.md | Workflow: Test end-to-end motion parameter extraction using c3d_affine_tool. | os, shutil, nibabel, numpy, pytest |
| How To: Group Dwi Scans With Complex B0Fields | references/tutorials/group-dwi-scans-with-complex-b0fields/group-dwi-scans-with-complex-b0fields.md | Workflow: Test the group_dwi_scans function. In the test dataset, we have the following:: fmap/ sub-01_dir-AP_epi.nii.gz sub-01_dir-PA_epi.nii.gz dwi/ sub-01_dir-AP_run-1_dwi.nii.gz sub-01_dir-AP_run-2_dwi.nii.gz sub-01_ | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Intramodal Template | references/tutorials/intramodal-template/intramodal-template.md | Workflow: IntramodalTemplate test A two-session dataset is used to create an intramodal template. This tests the following features: - Blip-up + Blip-down DWI series for TOPUP/Eddy - Eddy is run on a CPU - dwidenoise is | os, shutil, sys, pathlib, unittest.mock |
| How To: Patch2Self | references/tutorials/patch2self/patch2self.md | Workflow: Test qsiprep.interfaces.dipy.Patch2Self. | os, nibabel, qsiprep.interfaces |
| How To: Simple Multiped Dataset | references/tutorials/simple-multiped-dataset/simple-multiped-dataset.md | Workflow: Create a BIDS dataset with multiple DWI series. | os, pprint, pytest, bids.layout, niworkflows.utils.testing |
| How To: Synthseg Interface | references/tutorials/synthseg-interface/synthseg-interface.md | Workflow: Test qsiprep.interfaces.freesurfer.SynthSeg. | os, shutil, nibabel, numpy, pytest |
| How To: Synthstrip Interface | references/tutorials/synthstrip-interface/synthstrip-interface.md | Workflow: Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip. | os, shutil, nibabel, numpy, pytest |

## Snippets Extracted

- `references/tutorials/group-dwi-scans-with-complex-b0fields/group-dwi-scans-with-complex-b0fields.md`: How To: Group Dwi Scans With Complex B0Fields
- `references/tutorials/dscsdsi/dscsdsi.md`: How To: Dscsdsi
- `references/tutorials/collect-data/collect-data.md`: How To: Collect Data
- `references/tutorials/dsdti-nofmap/dsdti-nofmap.md`: How To: Dsdti Nofmap
- `references/tutorials/dsdti-synfmap/dsdti-synfmap.md`: How To: Dsdti Synfmap
- `references/tutorials/dscsdsi-fmap/dscsdsi-fmap.md`: How To: Dscsdsi Fmap
- `references/tutorials/dsdti-fmap/dsdti-fmap.md`: How To: Dsdti Fmap
- `references/tutorials/cuda/cuda.md`: How To: Cuda
- `references/tutorials/intramodal-template/intramodal-template.md`: How To: Intramodal Template
- `references/tutorials/patch2self/patch2self.md`: How To: Patch2Self
- `references/tutorials/get-fieldmaps-relpaths/get-fieldmaps-relpaths.md`: How To: Get Fieldmaps Relpaths
- `references/tutorials/drbuddi-shoreline-epi/drbuddi-shoreline-epi.md`: How To: Drbuddi Shoreline Epi

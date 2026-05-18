# mrtrix3 Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Ismrm Hcp Tutorial

- Kind: `documentation`
- Source: `references/documentation/other/ismrm_hcp_tutorial.rst`
- Note: Documentation code block extracted for implementation use.

```bash
mrconvert data.nii.gz DWI.mif -fslgrad bvecs bvals -datatype float32 -strides 0,0,0,1
dwi2response msmt_5tt DWI.mif 5TT.mif RF_WM.txt RF_GM.txt RF_CSF.txt -voxels RF_voxels.mif
mrview meanb0.mif -overlay.load RF_voxels.mif -overlay.opacity 0.5
dwi2fod msmt_csd DWI.mif RF_WM.txt WM_FODs.mif RF_GM.txt GM.mif RF_CSF.txt CSF.mif -mask nodif_brain_mask.nii.gz
mrconvert WM_FODs.mif - -coord 3 0 | mrcat CSF.mif GM.mif - tissueRGB.mif -axis 3
mrview tissueRGB.mif -odf.load_sh WM_FODs.mif
tckgen WM_FODs.mif 100M.tck -act 5TT.mif -backtrack -crop_at_gmwmi -seed_dynamic WM_FODs.mif -maxlength 250 -select 100M -cutoff 0.06
tcksift 100M.tck WM_FODs.mif 10M_SIFT.tck -act 5TT.mif -term_number 10M
tckedit 100M.tck 50M.tck -number 50M
tck2connectome 10M_SIFT.tck nodes_fixSGM.mif connectome.csv
mrview nodes_fixSGM.mif -connectome.init nodes_fixSGM.mif -connectome.load connectome.csv
``mrconvert data.nii.gz DWI.mif -fslgrad bvecs bvals -datatype float32 -strides 0,0,0,1``
```

## 2. Dicom Handling

- Kind: `documentation`
- Source: `references/documentation/other/dicom_handling.rst`
- Note: Documentation code block extracted for implementation use.

```bash
mrconvert: [done] scanning DICOM folder "DICOM_folder/"
mrconvert: [100%] reading DICOM series "t1_mpr_1mm iso qk"
mrconvert: [100%] copying from "TOURNIER D...BRI) [MR] t1_mpr_1mm iso qk" to "T1_anat.nii"
$ mrconvert DICOM/ out.nii
mrconvert: [SYSTEM FATAL CODE: SIGSEGV (11)] Segmentation fault: Invalid memory access
$ dwi2tensor DICOM/ dt.mif
dwi2tensor: [done] scanning DICOM folder "DICOM/"
dwi2tensor: [100%] reading DICOM series "DWI_60"
dwi2tensor: [ERROR] no diffusion encoding information found in image "Joe Bloggs [MR] DWI_60"
$ mrconvert DICOM/ data.mif
mrconvert: [done] scanning folder "DICOM/" for DICOM data
mrconvert: [100%] Reading DICOM series "SeriesDescription"
```

## 3. Dw Scheme

- Kind: `documentation`
- Source: `references/documentation/other/dw_scheme.rst`
- Note: Documentation code block extracted for implementation use.

```bash
mrconvert
$ mrconvert DICOM/ dwi.nii.gz -export_grad_fsl bvecs bvals
mrconvert: [done] scanning DICOM folder "DICOM/"
mrconvert: [100%] reading DICOM series "BRI 64 directions ep2d_diff_3scan_trace_p2"
mrconvert: [100%] reformatting DICOM mosaic images
mrconvert: [100%] copying from "DICOM data...ns ep2d_diff_3scan_trace_p2" to "dwi.nii.gz"
mrconvert: [100%] compressing image "dwi.nii.gz"
``mrconvert``, or at the point of use. For example:
$ mrconvert dwi.nii -fslgrad dwi_bvecs dwi_bvals dwi.mif
$ dwi2tensor DICOM/ -grad encoding.b tensor.nii
```

## 4. Command Line #2

- Kind: `documentation`
- Source: `references/documentation/other/command_line.rst`
- Note: Documentation code block extracted for implementation use.

```bash
mrconvert
dwi2tensor
dwi2mask
$ mrconvert input.mif -coord 3 0:2:end output.mif
$ mrconvert -debug in.mif out.nii.gz
$ mrconvert -de in.mif out.nii.gz
$ mrconvert -d in.mif out.nii.gz
$ dwi2tensor /data/DICOM_folder/ - | tensor2metric - -vector ev.mif
dwi2tensor: [done] scanning DICOM folder "/data/DICOM_folder/"
dwi2tensor: [100%] reading DICOM series "ep2d_diff"...
dwi2tensor: [100%] reformatting DICOM mosaic images...
dwi2tensor: [100%] loading data for image "ACME (hm) [MR] ep2d_diff"...
```

## 5. Index

- Kind: `documentation`
- Source: `references/documentation/other/index.rst`
- Note: Documentation code block extracted for implementation use.

```bash
fixel-based analysis of apparent fibre density and fibre cross-section
fixel_based_analysis/st_fibre_density_cross-section
fixel_based_analysis/mt_fibre_density_cross-section
fixel_based_analysis/fixel_directory_format
fixel_based_analysis/mitigating_brain_cropping
fixel_based_analysis/computing_effect_size_wrt_controls
fixel_based_analysis/displaying_results_with_streamlines
```

## 6. Response Function Estimation

- Kind: `documentation`
- Source: `references/documentation/other/response_function_estimation.rst`
- Note: Documentation code block extracted for implementation use.

```bash
dwi2fod csd
tckglobal
dwi2response tournier dwi.mif wm_response.txt
dwi2response dhollander dwi.mif wm_response.txt gm_response.txt csf_response.txt
dwi2response tournier dwi.mif wm_response.txt -voxels voxels.mif
dwi2response fa dwi.mif response.txt
dwi2response msmt_5tt dwi.mif 5tt.mif wm_response.txt gm_response.txt csf_response.txt -sfwm_fa_threshold 0.7
```

## 7. Multi Shell Multi Tissue Csd

- Kind: `documentation`
- Source: `references/documentation/other/multi_shell_multi_tissue_csd.rst`
- Note: Documentation code block extracted for implementation use.

```bash
dwi2response tournier
dwi2fod csd
dwi2fod msmt_csd
dwi2fod msmt_csd dwi.mif wm_response.txt wmfod.mif gm_response.txt gm.mif csf_response.txt csf.mif
dwi2fod msmt_csd -mask mask.mif dwi.mif wm_response.txt wmfod.mif gm_response.txt gm.mif csf_response.txt csf.mif
mrconvert -coord 3 0 wm.mif - | mrcat csf.mif gm.mif - vf.mif
mrview vf.mif -odf.load_sh wm.mif
```

## 8. Mrview #2

- Kind: `documentation`
- Source: `references/documentation/api/mrview.rst`
- Note: Documentation code block extracted for implementation use.

```bash
mrview [ options ] [ image ... ]
$ mrview -load image1.mif -interpolation 0 -load image2.mif -interpolation 0
$ mrview image1.mif image2.mif -interpolation 0 -select_image 2 -interpolation 0
fixel.load image** *(multiple uses permitted)* Load a fixel file (any file inside a fixel directory, or an old .msf / .msh legacy format file) into the fixel tool.
```

## 9. Tck2Fixel #2

- Kind: `documentation`
- Source: `references/documentation/api/tck2fixel.rst`
- Note: Documentation code block extracted for implementation use.

```bash
tck2fixel
tck2fixel [ options ] tracks fixel_folder_in fixel_folder_out fixel_data_out
fixel_folder_in*: the input fixel folder. Used to define the fixels and their directions
fixel_folder_out*: the fixel folder to which the output will be written. This can be the same as the input folder if desired
fixel_data_out*: the name of the fixel data image.
```

## 10. Statistics #1

- Kind: `documentation`
- Source: `references/documentation/other/statistics.rst`
- Note: Documentation code block extracted for implementation use.

```text
fixelcfestats fd_smooth/ files.txt design_matrix.txt contrast_matrix.txt matrix/ stats_fd/
 fixelcfestats log_fc_smooth/ files.txt design_matrix.txt contrast_matrix.txt matrix/ stats_log_fc/
 fixelcfestats fdc_smooth/ files.txt design_matrix.txt contrast_matrix.txt matrix/ stats_fdc/
```

---
name: freesurfer
description: Use for FreeSurfer documentation tasks involving FreeSurfer, recon-all, neuroimaging, structural MRI analysis, cortical surface reconstruction, brain segmentation, FreeSurfer statistics tables, installation/licensing, SUBJECTS_DIR setup, Freeview/tkmedit/tksurfer output inspection, coordinate transforms, file formats, and troubleshooting FreeSurfer processing errors.
doc_version: "FreeSurfer wiki snapshot in references/"
---

# FreeSurfer Documentation Guide

Use this skill when the user asks about FreeSurfer documentation or workflows: installing FreeSurfer, setting `FREESURFER_HOME` or `SUBJECTS_DIR`, running or resuming `recon-all`, understanding recon-all outputs, inspecting cortical surfaces or segmentations, extracting stats, answering common FreeSurfer questions, or troubleshooting errors from FreeSurfer commands.

Do not use this skill for unrelated MRI tools unless the user is specifically connecting them to FreeSurfer outputs, registration, file formats, or neuroimaging workflows.

## Grounding Rules

- Treat `references/documentation/overview/` as the source of truth. Do not invent flags, file names, runtime expectations, or quality-control advice that is not supported by those files.
- Do not paste long documentation excerpts into the answer. Give the workflow, the relevant commands, and the reference file to consult.
- For current release, download URL availability, course dates, or platform support that may have changed since the references were captured, say the local docs state the captured fact and recommend checking the official FreeSurfer site if the user needs current details.
- Prefer the subject's own `$SUBJECTS_DIR/<subject>/scripts/recon-all.log` over generic tables when diagnosing an actual run. The reference table explicitly says the log has the exact commands and flags used for a dataset.
- When advising a study, keep versions consistent across subjects. The local install and FAQ references warn against processing a dataset with mixed FreeSurfer versions/platforms.

## Reference Map

- `references/documentation/overview/FreeSurferWiki.md`: overview of what FreeSurfer does and links to installation, tutorials, citation, and support.
- `references/documentation/overview/DownloadAndInstall.md`: release/download notes, platform/package notes, license requirement, version consistency warning.
- `references/documentation/overview/QuickInstall.md`: moved page; use `DownloadAndInstall.md`.
- `references/documentation/overview/ReconAllTable.md`: how to use recon-all tables and why the subject's `scripts/recon-all.log` is authoritative for an actual run.
- `references/documentation/overview/ReconAllTableStableV6.0.md`: detailed stable v6.0 `recon-all` steps, command lines, inputs, and outputs.
- `references/documentation/overview/FAQ.md`: common FreeSurfer questions, recon-all resume/rerun advice, error fixes, output interpretation, and analysis questions.
- `references/documentation/overview/FileFormats.md`: FreeSurfer native and external file-format overview.
- `references/documentation/overview/Glossary.md`: definitions for surfaces, volumes, segmentation, labels, topology, voxels, and related MRI terms.
- `references/documentation/overview/CoordinateSystems.md`: coordinate transform use cases between surface, volume, scanner RAS, MNI305/MNI152, CRS, and registration spaces.
- `references/documentation/overview/FreeSurferCommandsRegistration.md`: registration command families such as `mri_robust_register`, `mri_robust_template`, `bbregister`, `mri_cvs_register`, `mri_em_register`, and `mri_ca_register`.
- `references/documentation/overview/FreeSurferSupport.md`: support channels and how to ask/search for help.
- `references/documentation/overview/FreeSurferMethodsCitation.md`: method descriptions and citations.
- `references/documentation/overview/Tutorials.md`: tutorial/course entry points and version-specific tutorial pointers.

## Standard Answer Pattern

1. Identify the user's task: install, setup, run, resume, inspect output, extract stats, transform coordinates, troubleshoot, or cite methods.
2. Open the relevant reference file(s), usually with `rg` first:

   ```sh
   rg -n "term|command|error|file" references/documentation/overview
   ```

3. Answer with:
   - the smallest reliable command workflow,
   - what files/directories to check,
   - the source reference file names,
   - any caveat about version-specific behavior.

## Installation And Environment

Use `DownloadAndInstall.md` for installation claims.

Key supported facts:
- The local docs identify FreeSurfer as requiring a free `license.txt` key file for tools to operate.
- The license file should be copied to the FreeSurfer installation directory, the same location defined by `FREESURFER_HOME`.
- The local docs mention Linux RPM/DEB and MacOS installer packages for release 7 downloads, and point Windows users to WSL instructions.
- The local docs state that when processing a study group, all subjects should be processed with the same FreeSurfer version and same OS platform/vendor, and for safety the same OS version.

Typical setup skeleton, adapting paths to the user's install:

```sh
export FREESURFER_HOME=/path/to/freesurfer
source "$FREESURFER_HOME/SetUpFreeSurfer.sh"
export SUBJECTS_DIR=/path/to/freesurfer_subjects
```

Verification commands:

```sh
recon-all -version
echo "$FREESURFER_HOME"
echo "$SUBJECTS_DIR"
test -f "$FREESURFER_HOME/license.txt"
```

If the user asks for the latest installer or current release, explain that the local reference says v7.4.1 was the latest v7 release in June 2023, but that release status may have changed and should be checked against the official FreeSurfer download page.

## SUBJECTS_DIR Workflow

Use `$SUBJECTS_DIR` as the root directory where processed subjects live. A typical completed subject has subdirectories such as:

```text
$SUBJECTS_DIR/<subject>/
  mri/
  surf/
  label/
  stats/
  scripts/
```

When diagnosing an existing subject, ask for or inspect:

```sh
ls "$SUBJECTS_DIR/<subject>"
ls "$SUBJECTS_DIR/<subject>/scripts"
tail -n 80 "$SUBJECTS_DIR/<subject>/scripts/recon-all.log"
```

Do not assume the subject directory path from the subject id alone; confirm `SUBJECTS_DIR` or use an explicit path supplied by the user.

## recon-all Workflows

For a straightforward T1 structural run:

```sh
recon-all -s <subject_id> -i <input_T1> -all
```

For multiple input volumes, the stable v6 table shows repeated input conversion steps, so use repeated `-i` inputs only when the user's FreeSurfer version supports the intended invocation. If uncertain, direct them to `recon-all -help` for their installed version and to the subject `recon-all.log` after running.

For a long-running SSH session, the FAQ gives this detached pattern:

```sh
recon-all -s <subject_id> -all > /dev/null 2>&1 < /dev/null & disown -a
```

For an interrupted run, the FAQ suggests:

```sh
recon-all -make all -s <subject_id>
```

Also check for an `IsRunning` file under the subject's `scripts/` directory and remove it only when you are sure no `recon-all` process is still running for that subject.

For rerunning after manual edits, use the earliest affected stage and let later stages follow. The FAQ says that if both white-matter and pial edits were made, `-autorecon2-wm` is enough to restart before the pial-related steps, but the user should still run `-autorecon3` afterward:

```sh
recon-all -autorecon2-wm -autorecon3 -s <subject_id>
```

For already skull-stripped data, the FAQ supports this only if the skull-stripped volume still includes the cerebellum:

```sh
recon-all -autorecon1 -noskullstrip -s <subject_id>
# then create/check brainmask.auto.mgz and brainmask.mgz as described in FAQ.md
recon-all -autorecon2 -autorecon3 -s <subject_id>
```

Note: the local FAQ text contains a typo `-autrecon2`; use the standard spelling `-autorecon2`.

## Outputs And Quality Checks

Use `ReconAllTableStableV6.0.md`, `FAQ.md`, `FileFormats.md`, and `Glossary.md`.

Common outputs:
- `mri/orig.mgz`: conformed original MRI volume.
- `mri/T1.mgz`: intensity-normalized T1 volume.
- `mri/brainmask.mgz`: skull-stripped brain mask volume.
- `mri/wm.mgz`: white-matter segmentation volume used for edits.
- `mri/aseg.mgz`: automatic segmentation.
- `mri/aparc+aseg.mgz`: cortical parcellation plus segmentation volume.
- `mri/wmparc.mgz`: white-matter parcellation.
- `surf/?h.white`: gray/white boundary surface.
- `surf/?h.pial`: gray/CSF boundary surface.
- `surf/?h.thickness`: cortical thickness values.
- `label/?h.aparc.annot`, `label/?h.aparc.a2009s.annot`, `label/?h.aparc.DKTatlas.annot`: cortical annotation files.
- `stats/?h.aparc.stats`, `stats/?h.aparc.a2009s.stats`, `stats/?h.aparc.DKTatlas.stats`: cortical parcellation stats.
- `stats/aseg.stats`: segmentation stats.
- `stats/wmparc.stats`: white-matter parcellation stats.

Interpret `?h` as hemisphere-specific `lh` and `rh`.

For an actual processing question, inspect:

```sh
tail -n 80 "$SUBJECTS_DIR/<subject>/scripts/recon-all.log"
ls "$SUBJECTS_DIR/<subject>/mri"
ls "$SUBJECTS_DIR/<subject>/surf"
ls "$SUBJECTS_DIR/<subject>/stats"
```

If the user asks whether a surface is acceptable, use `FAQ.md` guidance: compare with the sample subject `bert` when available, inspect nofix surfaces for large defects in unusually long runs, and remember that medial wall/hippocampus/amygdala surface placement is generally unreliable for thickness studies and should be excluded with `?h.cortex.label`.

## Stats Tables And Measures

Use `ReconAllTableStableV6.0.md` and `FAQ.md`.

Generated stats files to collect from each subject include:

```text
$SUBJECTS_DIR/<subject>/stats/lh.aparc.stats
$SUBJECTS_DIR/<subject>/stats/rh.aparc.stats
$SUBJECTS_DIR/<subject>/stats/lh.aparc.a2009s.stats
$SUBJECTS_DIR/<subject>/stats/rh.aparc.a2009s.stats
$SUBJECTS_DIR/<subject>/stats/lh.aparc.DKTatlas.stats
$SUBJECTS_DIR/<subject>/stats/rh.aparc.DKTatlas.stats
$SUBJECTS_DIR/<subject>/stats/aseg.stats
$SUBJECTS_DIR/<subject>/stats/wmparc.stats
```

Stats-file workflow:

```sh
ls "$SUBJECTS_DIR/<subject>/stats"
sed -n '1,40p' "$SUBJECTS_DIR/<subject>/stats/aseg.stats"
sed -n '1,40p' "$SUBJECTS_DIR/<subject>/stats/lh.aparc.stats"
```

Regenerating documented stats from the stable v6 table:

```sh
recon-all -parcstats -s <subject_id>
recon-all -parcstats2 -s <subject_id>
recon-all -parcstats3 -s <subject_id>
recon-all -segstats -s <subject_id>
recon-all -wmparc -s <subject_id>
```

The stable v6 table shows cortical parcellation stats being produced by `mris_anatomical_stats`, and `aseg.stats`/`wmparc.stats` being produced by `mri_segstats`.

Supported extraction/analysis guidance from the references:
- `mris_anatomical_stats -l <label file>` can be used for ROI cortical thickness/statistics from a saved label.
- `aseg.stats` accounts for partial voluming, so summed individual subcortical structures may not equal the provided subcortical volume.
- For global mean cortical thickness across hemispheres, the FAQ suggests weighting each hemisphere's mean thickness by that hemisphere's surface area.
- `sulc` reflects displacement/depth relative to an average surface; `curv` reflects curvature; `jacobian_white` reflects distortion needed to register a subject to the atlas.

If the user asks for group-level table export commands such as `aparcstats2table` or `asegstats2table`, first search the references. These command names are not described in the provided files, so answer cautiously and use the installed FreeSurfer help for that local version:

```sh
aparcstats2table --help
asegstats2table --help
```

## Troubleshooting Playbooks

Use `FAQ.md` first, then the subject's `scripts/recon-all.log`.

Initial triage:

```sh
recon-all -version
echo "$FREESURFER_HOME"
echo "$SUBJECTS_DIR"
tail -n 120 "$SUBJECTS_DIR/<subject>/scripts/recon-all.log"
ls "$SUBJECTS_DIR/<subject>/scripts"
```

Interrupted run:

```sh
recon-all -make all -s <subject_id>
```

Very long run:
- Compare with other subjects processed on the same machine.
- Inspect `surf/?h.inflated.nofix` or `surf/?h.orig.nofix` for large defects.
- Inspect `mri/filled.mgz` for attached cerebellum/skull, and check pons/corpus callosum detection.

Watershed error `GLOBAL region of the brain empty`:

```sh
recon-all -skullstrip -no-wsgcaatlas -s <subject_id>
recon-all -autorecon2 -autorecon3 -s <subject_id>
```

Talairach failure detection:

```sh
tkregister2 --mgz --s <subject_id> --fstal
```

If the green lines align with the anatomy, the FAQ says the subject may be rerun with:

```sh
recon-all -all -s <subject_id> -notal-check
```

If the lines do not align, fix the Talairach transform rather than bypassing the check. For ANALYZE images, the FAQ warns that orientation information is not retained, so verify orientation.

Pial surface includes cerebellum:
- For supported versions in the FAQ, edit `brain.finalsurfs.mgz`, not `brainmask.mgz`.
- Remove the cerebellum portions affecting surfaces, save, then run:

```sh
recon-all -make all -s <subject_id>
```

Missing/corrupt output file:
- Find the first recon-all step that creates the file in `ReconAllTableStableV6.0.md`.
- Rerun that step for the subject. The FAQ example says recreating `norm.mgz` requires:

```sh
recon-all -canorm -s <subject_id>
```

## Coordinates, Registration, And Formats

Use `CoordinateSystems.md` for formulas and worked coordinate-space cases. Do not recreate formulas from memory.

Use `FreeSurferCommandsRegistration.md` to choose registration command families:
- `mri_robust_register`: robust registration.
- `mri_robust_template`: within-subject template creation.
- `bbregister`: rigid cross-modality registration that needs surfaces.
- `mri_cvs_register`: combined volumetric and surface-based registration.
- `mri_em_register` and `mri_ca_register`: registration commands used in the processing stream.

Use `FileFormats.md` when explaining formats. It lists FreeSurfer native formats including `mgh`, `mgz`, `gca`, `bshort`, `bfloat`, `COR`, surface, `curv`, `w`, `annot`, `patch`, `gcs`, `dat`, `xfm`, `m3d`, and `lta`, plus external formats including MINC, Analyze, DICOM, and NIfTI.

## Common User Questions

**What is FreeSurfer?**  
Use `FreeSurferWiki.md`: it is a software package for analysis and visualization of structural and functional neuroimaging data from cross-sectional or longitudinal studies, with structural MRI tools for skull stripping, bias correction, gray-white segmentation, cortical surface reconstruction, cortical/subcortical labeling, surface registration, and morphometry statistics.

**Where is the log?**  
`$SUBJECTS_DIR/<subject>/scripts/recon-all.log`.

**Where are the stats?**  
`$SUBJECTS_DIR/<subject>/stats/`.

**Where are surfaces?**  
`$SUBJECTS_DIR/<subject>/surf/`, with `lh.*` and `rh.*` files.

**Where are segmentations and MRI volumes?**  
`$SUBJECTS_DIR/<subject>/mri/`.

**Can I mix FreeSurfer versions in one dataset?**  
No. The references say this is not a good idea and that all cases in a dataset should be processed with the same version.

**Can I use skull-stripped input?**  
Only with care. The FAQ says no if the cerebellum is absent; if the cerebellum is present, use the `-autorecon1 -noskullstrip` workflow and manually set/check `brainmask.auto.mgz` and `brainmask.mgz` before later stages.

**How do I cite methods?**  
Use `FreeSurferMethodsCitation.md`; cite only the method(s) relevant to the user's analysis.

**Where should users get help?**  
Use `FreeSurferSupport.md`: search mailing-list archives first, then subscribe/ask on the relevant list when the archive does not answer the question.

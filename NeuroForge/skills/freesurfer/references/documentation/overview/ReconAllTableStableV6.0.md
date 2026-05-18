<div id="header">

<div id="logo">

[![FreeSurfer](https://surfer.nmr.mgh.harvard.edu/wiki/fswiki_htdocs/common/fslogosmall.png)](FreeSurferWiki.html)

</div>

<div>

Search:

</div>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV6.0?action=login"
  id="login" rel="nofollow">Login</a>

<div id="locationline">

- [ReconAllTableStableV6.0](ReconAllTableStableV6.0.html)

</div>

- [FreeSurferWiki](FreeSurferWiki.html)
- [RecentChanges](https://surfer.nmr.mgh.harvard.edu/fswiki/RecentChanges)
- [FindPage](https://surfer.nmr.mgh.harvard.edu/fswiki/FindPage)
- [HelpContents](https://surfer.nmr.mgh.harvard.edu/fswiki/HelpContents)
- [ReconAllTableStableV6.0](ReconAllTableStableV6.0.html)

<div id="pageline">

------------------------------------------------------------------------

</div>

- <span class="disabled">Immutable Page</span>

- <a href="ReconAllTableStableV6.0.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV6.0?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV6.0?action=AttachFile"
  class="nbattachments" rel="nofollow">Attachments</a>

- <div>

  More Actions: Raw Text Print View Render as Docbook Delete Cache
  ------------------------ Check Spelling Like Pages Local Site Map
  ------------------------ Rename Page Delete Page
  ------------------------ Subscribe User ------------------------
  Remove Spam Revert to this revision Package Pages Sync Pages
  ------------------------ Load Save SlideShow

  </div>

</div>

<div id="page" lang="en" dir="ltr">

<div id="content" dir="ltr" lang="en">

<span id="top" class="anchor"></span> <span id="line-1"
class="anchor"></span>

<a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV7"
class="nonexistent">ReconAllTableStableV7</a> <span id="line-2"
class="anchor"></span><span id="line-3" class="anchor"></span>

This table shows the recon-all steps for the **stable**, publicly
released, **version 6.0** of FreeSurfer [(available
here)](DownloadAndInstall.html). <span id="line-4"
class="anchor"></span><span id="line-5" class="anchor"></span>

See also the
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/OtherUsefulFlags"
class="https">OtherUsefulFlags</a> for other recon-all options.
<span id="line-6" class="anchor"></span>

<div>

<table style="text-align:left;                     ; text-align:left">
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>recon-all step</strong></p></td>
<td><p><strong>Individual Flag</strong></p></td>
<td><p><strong>Input</strong></p></td>
<td><p><strong>Command Line</strong></p></td>
<td><p><strong>Output</strong></p></td>
</tr>
<tr>
<td rowspan="19" style="text-align: left;"><span id="line-7"
class="anchor"></span>
<p><strong><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="https">recon-all</a> -autorecon1 -subjid
&lt;subjid&gt;</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-8" class="anchor"></span>
<p>-i &lt;invol1&gt;</p></td>
<td><p>invol1.dcm <em>or .nii or .mgz</em></p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> invol1.dcm orig/001.mgz</p></td>
<td><p>orig/001.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-9" class="anchor"></span>
<p>-i &lt;invol2&gt; <em>optional</em></p></td>
<td><p>invol2.dcm <em>or .nii or .mgz</em></p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> invol2.dcm orig/002.mgz</p></td>
<td><p>orig/002.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-10" class="anchor"></span>
<p>-T2 &lt;invol&gt; <em>or</em> -FLAIR &lt;invol&gt;
<em>optional</em></p></td>
<td style="text-align: left;"><p>invol.dcm <em>or .nii or
.mgz</em></p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> --no_scale 1 invol.dcm orig/T2raw.mgz
<em>(or orig/FLAIRraw.mgz)</em></p></td>
<td style="text-align: left;"><p>orig/T2raw.mgz <em>(or
orig/FLAIRraw.mgz)</em></p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-11"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/motioncor"
class="https">motioncor</a></p></td>
<td><p>orig/001.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_robust_template"
class="https">mri_robust_template</a> --mov 001.mgz 002.mgz --average 1
--template rawavg.mgz --satit --inittp 1 --fixtp --noit --iscale
--iscaleout --subsample 200 --lta</p></td>
<td rowspan="2" style="text-align: left;"><p>rawavg.mgz</p></td>
</tr>
<tr>
<td><span id="line-12" class="anchor"></span>
<p>orig/002.mgz</p></td>
</tr>
<tr>
<td><span id="line-13" class="anchor"></span>
<p>rawavg.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> rawavg.mgz orig.mgz --conform</p></td>
<td><p>orig.mgz</p></td>
</tr>
<tr>
<td><span id="line-14" class="anchor"></span>
<p>orig.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_add_xform_to_header"
class="https">mri_add_xform_to_header</a> -c transforms/talairach.xfm
orig.mgz orig.mgz</p></td>
<td><p>orig.mgz</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-15"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/talairach"
class="https">talairach</a></p></td>
<td><p>orig.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_nu_correct.mni"
class="https">mri_nu_correct.mni</a> --n 1 --proto-iters 1000 --distance
50 --no-rescale --i orig.mgz --o orig_nu.mgz</p></td>
<td><p>orig_nu.mgz</p></td>
</tr>
<tr>
<td><span id="line-16" class="anchor"></span>
<p>orig_nu.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/talairach_avi"
class="https">talairach_avi</a> --i orig_nu.mgz --xfm
transforms/talairach.auto.xfm</p></td>
<td><p>transforms/talairach.auto.xfm</p></td>
</tr>
<tr>
<td><span id="line-17" class="anchor"></span>
<p>transforms/talairach.auto.xfm</p></td>
<td><p>cp transforms/talairach.auto.xfm
transforms/talairach.xfm</p></td>
<td><p>transforms/talairach.xfm</p></td>
</tr>
<tr>
<td><span id="line-18" class="anchor"></span>
<p>transforms/talairach.xfm</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/talairach_afd"
class="https">talairach_afd</a> -T 0.005 -xfm
transforms/talairach.xfm</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-19" class="anchor"></span></td>
<td><p>awk -f $FREESURFER_HOME/bin/extract_talairach_avi_QA.awk
transforms/talairach_avi.log</p></td>
<td><p>transforms/talairach_avi.log</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-20"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/nuintensitycor"
class="https">nuintensitycor</a></p></td>
<td><p>orig.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_nu_correct.mni"
class="https">mri_nu_correct.mni</a> --i orig.mgz --o nu.mgz --uchar
transforms/talairach.xfm --n 2</p></td>
<td rowspan="2" style="text-align: left;"><p>nu.mgz</p></td>
</tr>
<tr>
<td><span id="line-21" class="anchor"></span>
<p>talairach.xfm</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-22" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/normalization"
class="https">normalization</a></p></td>
<td><p>nu.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_normalize"
class="https">mri_normalize</a> -g 1 -mprage nu.mgz T1.mgz</p></td>
<td><p>T1.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-23"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/skullstrip"
class="https">skullstrip</a></p></td>
<td><p>nu.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_em_register"
class="https">mri_em_register</a> -skull nu.mgz
$FREESURFER_HOME/average/RB_all_withskull_2016-05-10.vc700.gca
transforms/talairach_with_skull.lta</p></td>
<td><p>transforms/talairach_with_skull.lta</p></td>
</tr>
<tr>
<td><span id="line-24" class="anchor"></span>
<p>T1.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_watershed"
class="https">mri_watershed</a> -T1 -brain_atlas
$FREESURFER_HOME/average/RB_all_withskull_2016-05-10.vc700.gca
transforms/talairach_with_skull.lta T1.mgz brainmask.auto.mgz</p></td>
<td><p>brainmask.auto.mgz</p></td>
</tr>
<tr>
<td><span id="line-25" class="anchor"></span>
<p>brainmask.auto.mgz</p></td>
<td><p>cp brainmask.auto.mgz brainmask.mgz</p></td>
<td><p>brainmask.mgz</p></td>
</tr>
</tbody>
</table>

</div>

<span id="line-26" class="anchor"></span><span id="line-27"
class="anchor"></span><span id="line-28" class="anchor"></span>

<div>

<table style="text-align:left;                     ; text-align:left">
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>recon-all step</strong></p></td>
<td><p><strong>Individual Flag</strong></p></td>
<td><p><strong>Input</strong></p></td>
<td><p><strong>Command Line</strong></p></td>
<td><p><strong>Output</strong></p></td>
</tr>
<tr>
<td rowspan="62" style="text-align: left;"><span id="line-29"
class="anchor"></span>
<p><strong><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="https">recon-all</a> -autorecon2 -subjid
&lt;subjid&gt;</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-30"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/gcareg"
class="https">gcareg</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_em_register"
class="https">mri_em_register</a> -uns 3 -mask brainmask.mgz nu.mgz
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
transforms/talairach.lta</p></td>
<td rowspan="2"
style="text-align: left;"><p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td><span id="line-31" class="anchor"></span>
<p>nu.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-32"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/canorm"
class="https">canorm</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_normalize"
class="https">mri_ca_normalize</a> -c ctrl_pts.mgz -mask brainmask.mgz
nu.mgz $FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
transforms/talairach.lta norm.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-33" class="anchor"></span>
<p>nu.mgz</p></td>
</tr>
<tr>
<td><span id="line-34" class="anchor"></span>
<p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-35"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/careg"
class="https">careg</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_register"
class="https">mri_ca_register</a> -align-after -nobigventricles -mask
brainmask.mgz -T transforms/talairach.lta norm.mgz
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
transforms/talairach.m3z</p></td>
<td rowspan="3"
style="text-align: left;"><p>transforms/talairach.m3z</p></td>
</tr>
<tr>
<td><span id="line-36" class="anchor"></span>
<p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td><span id="line-37" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-38"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/calabel"
class="https">calabel</a></p></td>
<td><p>norm.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_label"
class="https">mri_ca_label</a> -relabel_unlikely 9 .3 -prior 0.5 -align
norm.mgz transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
aseg.auto_noCCseg.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>aseg.auto_noCCseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-39" class="anchor"></span>
<p>transforms/talairach.m3z</p></td>
</tr>
<tr>
<td><span id="line-40" class="anchor"></span>
<p>aseg.auto_noCCseg.mgz</p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_cc"
class="https">mri_cc</a> -lta &lt;subjid&gt;/mri/transforms/cc_up.lta
-aseg aseg.auto_noCCseg.mgz -o aseg.auto.mgz &lt;subjid&gt;</p></td>
<td><p>aseg.auto.mgz</p></td>
</tr>
<tr>
<td><span id="line-41" class="anchor"></span>
<p>aseg.auto.mgz</p></td>
<td><p>cp aseg.auto.mgz aseg.presurf.mgz</p></td>
<td><p>aseg.presurf.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-42"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/normalization2"
class="https">normalization2</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_normalize"
class="https">mri_normalize</a> -mprage -aseg aseg.presurf.mgz -mask
brainmask.mgz norm.mgz brain.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>brain.mgz</p></td>
</tr>
<tr>
<td><span id="line-43" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-44" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-45"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/maskbfs"
class="https">maskbfs</a></p></td>
<td><p>brain.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_mask"
class="https">mri_mask</a> -T 5 brain.mgz brainmask.mgz
brain.finalsurfs.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td><span id="line-46" class="anchor"></span>
<p>brainmask.mgz</p></td>
</tr>
<tr>
<td rowspan="6" style="text-align: left;"><span id="line-47"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/segmentation"
class="https">segmentation</a></p></td>
<td><p>brain.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_segment"
class="https">mri_segment</a> -mprage brain.mgz wm.seg.mgz</p></td>
<td><p>wm.seg.mgz</p></td>
</tr>
<tr>
<td><span id="line-48" class="anchor"></span>
<p>wm.seg.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_edit_wm_with_aseg"
class="https">mri_edit_wm_with_aseg</a> wm.seg.mgz brain.mgz
aseg.presurf.mgz wm.asegedit.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>wm.asegedit.mgz</p></td>
</tr>
<tr>
<td><span id="line-49" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
</tr>
<tr>
<td><span id="line-50" class="anchor"></span>
<p>brain.mgz</p></td>
</tr>
<tr>
<td><span id="line-51" class="anchor"></span>
<p>wm.asegedit.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_pretess"
class="https">mri_pretess</a> wm.asegedit.mgz wm norm.mgz
wm.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>wm.mgz</p></td>
</tr>
<tr>
<td><span id="line-52" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-53"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/fill"
class="https">fill</a></p></td>
<td><p>wm.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_fill"
class="https">mri_fill</a> -a ../scripts/ponscc.cut.log -xform
transforms/talairach.lta -segmentation aseg.auto_noCCseg.mgz wm.mgz
filled.mgz</p></td>
<td><p>filled.mgz</p></td>
</tr>
<tr>
<td><span id="line-54" class="anchor"></span>
<p>aseg.auto_noCCseg.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>../scripts/ponscc.cut.log</p></td>
</tr>
<tr>
<td><span id="line-55" class="anchor"></span>
<p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td rowspan="8" style="text-align: left;"><span id="line-56"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/tessellate"
class="https">tessellate</a></p></td>
<td><p>filled.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_pretess"
class="https">mri_pretess</a> filled.mgz 255 norm.mgz
filled-pretess255.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>filled-pretess255.mgz</p></td>
</tr>
<tr>
<td><span id="line-57" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-58" class="anchor"></span>
<p>filled-pretess255.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_tessellate"
class="https">mri_tessellate</a> filled-pretess255.mgz 255
lh.orig.nofix</p></td>
<td><p>lh.orig.nofix</p></td>
</tr>
<tr>
<td><span id="line-59" class="anchor"></span>
<p>filled.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_pretess"
class="https">mri_pretess</a> filled.mgz 127 norm.mgz
filled-pretess127.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>filled-pretess127.mgz</p></td>
</tr>
<tr>
<td><span id="line-60" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-61" class="anchor"></span>
<p>filled-pretess127.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_tessellate"
class="https">mri_tessellate</a> filled-pretess127.mgz 127
rh.orig.nofix</p></td>
<td><p>rh.orig.nofix</p></td>
</tr>
<tr>
<td><span id="line-62" class="anchor"></span>
<p>?h.orig.nofix</p></td>
<td><p>mris_extract_main_component ?h.orig.nofix ?h.orig.nofix</p></td>
<td><p>?h.orig.nofix</p></td>
</tr>
<tr>
<td><span id="line-63" class="anchor"></span></td>
<td><p>rm -f filled-pretess255.mgz filled-pretess127.mgz</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-64" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/smooth"
class="https">smooth1</a></p></td>
<td><p>?h.orig.nofix</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_smooth"
class="https">mris_smooth</a> -nw ?h.orig.nofix
?h.smoothwm.nofix</p></td>
<td><p>?h.smoothwm.nofix</p></td>
</tr>
<tr>
<td><span id="line-65" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/inflate"
class="https">inflate1</a></p></td>
<td><p>?h.smoothwm.nofix</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_inflate"
class="https">mris_inflate</a> -no-save-sulc ?h.smoothwm.nofix
?h.inflated.nofix</p></td>
<td><p>?h.inflated.nofix</p></td>
</tr>
<tr>
<td><span id="line-66" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/qsphere"
class="https">qsphere</a></p></td>
<td><p>?h.inflated.nofix</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_sphere"
class="https">mris_sphere</a> -q ?h.inflated.nofix
?h.qsphere.nofix</p></td>
<td><p>?h.qsphere.nofix</p></td>
</tr>
<tr>
<td rowspan="6" style="text-align: left;"><span id="line-67"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/fix"
class="https">fix</a></p></td>
<td><p>?h.orig.nofix</p></td>
<td><p>cp ?h.orig.nofix ?h.orig</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-68" class="anchor"></span>
<p>?h.inflated.nofix</p></td>
<td><p>cp ?h.inflated.nofix ?h.inflated</p></td>
<td><p>?h.inflated</p></td>
</tr>
<tr>
<td><span id="line-69" class="anchor"></span>
<p>?h.qsphere.nofix</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_fix_topology"
class="https">mris_fix_topology</a> -mgz -sphere qsphere.nofix -ga
&lt;subjid&gt; ?h</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-70" class="anchor"></span>
<p>?h.orig</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_euler_number"
class="https">mris_euler_number</a> ?h.orig</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-71" class="anchor"></span>
<p>?h.orig</p></td>
<td><p>mris_remove_intersection ?h.orig ?h.orig</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-72" class="anchor"></span></td>
<td><p>rm ?h.inflated</p></td>
<td></td>
</tr>
<tr>
<td rowspan="8" style="text-align: left;"><span id="line-73"
class="anchor"></span>
<p>-white</p></td>
<td style="text-align: left;"><p>aseg.presurf.mgz</p></td>
<td rowspan="8" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_make_surfaces"
class="https">mris_make_surfaces</a> -aseg ../mri/aseg.presurf
-whiteonly -noaparc -mgz -T1 brain.finalsurfs &lt;subjid&gt; ?h</p></td>
<td rowspan="4" style="text-align: left;"><p>?h.white.preaparc</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-74" class="anchor"></span>
<p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-75" class="anchor"></span>
<p>wm.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-76" class="anchor"></span>
<p>filled.mgz</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-77"
class="anchor"></span>
<p>?h.orig</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-78" class="anchor"></span>
<p>?h.curv</p></td>
</tr>
<tr>
<td><span id="line-79" class="anchor"></span>
<p>?h.area</p></td>
</tr>
<tr>
<td><span id="line-80" class="anchor"></span>
<p>?h.cortex.label</p></td>
</tr>
<tr>
<td><span id="line-81" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/smooth"
class="https">smooth2</a></p></td>
<td><p>?h.white.preaparc</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_smooth"
class="https">mris_smooth</a> -n 3 -nw ?h.white.preaparc
?h.smoothwm</p></td>
<td><p>?h.smoothwm</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-82"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/inflate"
class="https">inflate2</a></p></td>
<td rowspan="2" style="text-align: left;"><p>?h.smoothwm</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_inflate"
class="https">mris_inflate</a> ?h.smoothwm ?h.inflated</p></td>
<td><p>?h.inflated</p></td>
</tr>
<tr>
<td><span id="line-83" class="anchor"></span>
<p>?h.sulc</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-84"
class="anchor"></span>
<p>-curvHK</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.white.preaparc</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_curvature"
class="https">mris_curvature</a> -w ?h.white.preaparc</p></td>
<td style="text-align: left;"><p>?h.white.H</p></td>
</tr>
<tr>
<td><span id="line-85" class="anchor"></span>
<p>?h.white.K</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-86"
class="anchor"></span>
<p>?h.inflated</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_curvature"
class="https">mris_curvature</a> -thresh .999 -n -a 5 -w -distances 10
10 ?h.inflated</p></td>
<td style="text-align: left;"><p>?h.inflated.H</p></td>
</tr>
<tr>
<td><span id="line-87" class="anchor"></span>
<p>?h.inflated.K</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-88"
class="anchor"></span>
<p>-curvstats</p></td>
<td style="text-align: left;"><p>?h.smoothwm</p></td>
<td rowspan="3" style="text-align: left;"><p>mris_curvature_stats -m
--writeCurvatureFiles -G -o ../stats/?h.curv.stats -F smoothwm
&lt;subjid&gt; ?h curv sulc</p></td>
<td rowspan="3"
style="text-align: left;"><p>stats/?h.curv.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-89" class="anchor"></span>
<p>?h.curv</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-90" class="anchor"></span>
<p>?h.sulc</p></td>
</tr>
</tbody>
</table>

</div>

<span id="line-91" class="anchor"></span><span id="line-92"
class="anchor"></span><span id="line-93" class="anchor"></span>

<div>

<table style="text-align:left;                     ; text-align:left">
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>recon-all step</strong></p></td>
<td><p><strong>Individual Flag</strong></p></td>
<td><p><strong>Input</strong></p></td>
<td><p><strong>Command Line</strong></p></td>
<td><p><strong>Output</strong></p></td>
</tr>
<tr>
<td rowspan="84" style="text-align: left;"><span id="line-94"
class="anchor"></span>
<p><strong><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="https">recon-all</a> -autorecon3 -subjid
&lt;subjid&gt;</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-95"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/sphere"
class="https">sphere</a></p></td>
<td><p>?h.inflated</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_sphere"
class="https">mris_sphere</a> ?h.inflated ?h.sphere</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.sphere</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-96" class="anchor"></span>
<p>?h.smoothwm</p></td>
</tr>
<tr>
<td><span id="line-97" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/surfreg"
class="https">surfreg</a></p></td>
<td><p>?h.sphere</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_register"
class="https">mris_register</a> -curv ?h.sphere
$FREESURFER_HOME/average/?h.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif
?h.sphere.reg</p></td>
<td><p>?h.sphere.reg</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-98"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/jacobian_white"
class="https">jacobian_white</a></p></td>
<td><p>?h.white.preaparc</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_jacobian"
class="https">mris_jacobian</a> ?h.white.preaparc ?h.sphere.reg
?h.jacobian_white</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.jacobian_white</p></td>
</tr>
<tr>
<td><span id="line-99" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td><span id="line-100" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/avgcurv"
class="https">avgcurv</a></p></td>
<td><p>?h.sphere.reg</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mrisp_paint"
class="https">mrisp_paint</a> -a 5
$FREESURFER_HOME/average/?h.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif#6
?h.sphere.reg ?h.avg_curv</p></td>
<td><p>?h.avg_curv</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-101"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortparc"
class="https">cortparc</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_ca_label"
class="https">mris_ca_label</a> -l ../label/?h.cortex.label -aseg
mri/aseg.presurf.mgz &lt;subjid&gt; ?h ?h.sphere.reg
$FREESURFER_HOME/average/?h.curvature.buckner40.filled.desikan_killiany.2007-06-20.gcs
?h.aparc.annot</p></td>
<td rowspan="3"
style="text-align: left;"><p>label/?h.aparc.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-102" class="anchor"></span>
<p>?h.cortex.label</p></td>
</tr>
<tr>
<td><span id="line-103" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td rowspan="8" style="text-align: left;"><span id="line-104"
class="anchor"></span>
<p>-pial</p></td>
<td style="text-align: left;"><p>aseg.presurf.mgz</p></td>
<td rowspan="8" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_make_surfaces"
class="https">mris_make_surfaces</a> -orig_white white.preaparc
-orig_pial white.preaparc -aseg ../mri/aseg.presurf -mgz -T1
brain.finalsurfs &lt;subjid&gt; ?h</p></td>
<td rowspan="4" style="text-align: left;"><p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-105" class="anchor"></span>
<p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td><span id="line-106" class="anchor"></span>
<p>wm.mgz</p></td>
</tr>
<tr>
<td><span id="line-107" class="anchor"></span>
<p>filled.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-108"
class="anchor"></span>
<p>?h.orig</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-109" class="anchor"></span>
<p>?h.curv.pial</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-110" class="anchor"></span>
<p>?h.area.pial</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-111" class="anchor"></span>
<p>label/?h.aparc.annot</p></td>
<td><p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="17" style="text-align: left;"><span id="line-112"
class="anchor"></span>
<p>-T2pial <em>or</em><br />
-FLAIRpial <em>optional</em></p></td>
<td><p>orig/T2raw.mgz</p></td>
<td><p>bbregister --s &lt;subjid&gt; --mov mri/orig/T2raw.mgz --lta
mri/transforms/T2raw.lta --init-fsl --T2</p></td>
<td><p>transforms/T2raw.lta</p></td>
</tr>
<tr>
<td><span id="line-113" class="anchor"></span>
<p>orig/T2raw.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>mri_convert -odt float -at
mri/transforms/T2raw.lta -rt cubic -ns 1 -rl mri/orig.mgz
mri/orig/T2raw.mgz mri/T2.prenorm.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>T2.prenorm.mgz</p></td>
</tr>
<tr>
<td><span id="line-114" class="anchor"></span>
<p>transforms/T2raw.lta</p></td>
</tr>
<tr>
<td><span id="line-115" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>mri_normalize -sigma 0.5
-nonmax_suppress 0 -min_dist 1 -aseg mri/aseg.presurf.mgz -surface
surf/rh.white identity.nofile -surface surf/lh.white identity.nofile
mri/T2.prenorm.mgz mri/T2.norm.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>T2.norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-116" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-117" class="anchor"></span>
<p>T2.prenorm.mgz</p></td>
</tr>
<tr>
<td><span id="line-118" class="anchor"></span>
<p>T2.norm.mgz</p></td>
<td rowspan="2" style="text-align: center;"><p>mri_mask mri/T2.norm.mgz
mri/brainmask.mgz mri/T2.mgz</p></td>
<td rowspan="2" style="text-align: center;"><p>T2.mgz</p></td>
</tr>
<tr>
<td><span id="line-119" class="anchor"></span>
<p>brainmask.mgz</p></td>
</tr>
<tr>
<td><span id="line-120" class="anchor"></span>
<p>?h.pial</p></td>
<td><p>cp -v surf/?h.pial surf/?h.woT2.pial</p></td>
<td><p>?h.woT2.pial</p></td>
</tr>
<tr>
<td><span id="line-121" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
<td rowspan="9" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_make_surfaces">mris_make_surfaces</a>
-orig_white white -orig_pial woT2.pial -aseg ../mri/aseg.presurf
-nowhite -mgz -T1 brain.finalsurfs -T2 ../mri/T2 -nsigma_above 2
-nsigma_below 5 &lt;subjid&gt; ?h</p></td>
<td rowspan="3" style="text-align: left;"><p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-122" class="anchor"></span>
<p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td><span id="line-123" class="anchor"></span>
<p>wm.mgz</p></td>
</tr>
<tr>
<td><span id="line-124" class="anchor"></span>
<p>filled.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.curv.pial</p></td>
</tr>
<tr>
<td><span id="line-125" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-126" class="anchor"></span>
<p>label/?h.aparc.annot</p></td>
<td style="text-align: left;"><p>?h.area.pial</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-127" class="anchor"></span>
<p>T2.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>?h.thickness</p></td>
</tr>
<tr>
<td><span id="line-128" class="anchor"></span>
<p>?h.woT2.pial</p></td>
</tr>
<tr>
<td><span id="line-129" class="anchor"></span></td>
<td></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-130"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortribbon"
class="https">cortribbon</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_volmask"
class="https">mris_volmask</a> --aseg_name aseg.presurf
--label_left_white 2 --label_left_ribbon 3 --label_right_white 41
--label_right_ribbon 42 --save_ribbon &lt;subjid&gt;</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-131" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-132" class="anchor"></span>
<p>?h.pial</p></td>
<td style="text-align: left;"><p>ribbon.mgz</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-133"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/parcstats"
class="https">parcstats</a></p></td>
<td style="text-align: left;"><p>label/?h.aparc.annot</p></td>
<td rowspan="5" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_anatomical_stats"
class="https">mris_anatomical_stats</a> -th3 -mgz -cortex
../label/?h.cortex.label -f stats/?h.aparc.stats -b -a
label/?h.aparc.annot -c label/aparc.annot.ctab &lt;subjid&gt; ?h
&lt;white or pial&gt;</p></td>
<td><p>stats/?h.aparc.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-134" class="anchor"></span>
<p>wm.mgz, ribbon.mgz</p></td>
<td rowspan="4"
style="text-align: left;"><p>label/aparc.annot.ctab</p></td>
</tr>
<tr>
<td><span id="line-135" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-136" class="anchor"></span>
<p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-137" class="anchor"></span>
<p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-138"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortparc"
class="https">cortparc2</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_ca_label"
class="https">mris_ca_label</a> -l ../label/?h.cortex.label -aseg
aseg.presurf.mgz &lt;subjid&gt; ?h ?h.sphere.reg
$FREESURFER_HOME/average/?h.destrieux.simple.2009-07-29.gcs
label/?h.aparc.a2009s.annot</p></td>
<td rowspan="3"
style="text-align: left;"><p>label/?h.aparc.a2009s.annot</p></td>
</tr>
<tr>
<td><span id="line-139" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td><span id="line-140" class="anchor"></span>
<p>label/?h.cortex.label</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-141"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/parcstats"
class="https">parcstats2</a></p></td>
<td style="text-align: left;"><p>label/?h.aparc.a2009s.annot</p></td>
<td rowspan="5" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_anatomical_stats"
class="https">mris_anatomical_stats</a> -th3 -mgz -cortex
../label/?h.cortex.label -f stats/?h.aparc.a2009s.stats -b -a
label/?h.aparc.a2009s.annot -c label/aparc.annot.a2009s.ctab
&lt;subjid&gt; ?h</p></td>
<td><p>stats/?h.aparc.a2009s.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-142" class="anchor"></span>
<p>wm.mgz, ribbon.mgz</p></td>
<td rowspan="4"
style="text-align: left;"><p>label/aparc.annot.a2009s.ctab</p></td>
</tr>
<tr>
<td><span id="line-143" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-144" class="anchor"></span>
<p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-145" class="anchor"></span>
<p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-146"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortparc"
class="https">cortparc3</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_ca_label"
class="https">mris_ca_label</a> -l ../label/?h.cortex.label -aseg
aseg.presurf.mgz &lt;subjid&gt; ?h ?h.sphere.reg
$FREESURFER_HOME/average/?h.DKTatlas.2016-03-20.gcs
../label/?h.aparc.DKTatlas.annot</p></td>
<td rowspan="3"
style="text-align: left;"><p>label/?h.aparc.DKTatlas.annot</p></td>
</tr>
<tr>
<td><span id="line-147" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td><span id="line-148" class="anchor"></span>
<p>label/?h.cortex.label</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-149"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/parcstats"
class="https">parcstats3</a></p></td>
<td style="text-align: left;"><p>label/?h.aparc.DKTatlas.annot</p></td>
<td rowspan="5" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_anatomical_stats"
class="https">mris_anatomical_stats</a> -th3 -mgz -cortex
../label/?h.cortex.label -f stats/?h.aparc.DKTatlas.stats -b -a
label/?h.aparc.DKTatlas.annot -c label/aparc.annot.DKTatlas.ctab
&lt;subjid&gt; ?h</p></td>
<td><p>stats/?h.aparc.DKTatlas.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-150" class="anchor"></span>
<p>wm.mgz, ribbon.mgz</p></td>
<td rowspan="4"
style="text-align: left;"><p>label/aparc.annot.DKTatlas.ctab</p></td>
</tr>
<tr>
<td><span id="line-151" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-152" class="anchor"></span>
<p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-153" class="anchor"></span>
<p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-154"
class="anchor"></span>
<p>-pctsurfcon</p></td>
<td><p>rawavg.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p>pctsurfcon --s
&lt;subjid&gt; --?h-only</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.w-g.pct.mgh</p></td>
</tr>
<tr>
<td><span id="line-155" class="anchor"></span>
<p>orig.mgz</p></td>
</tr>
<tr>
<td><span id="line-156" class="anchor"></span>
<p>?h.cortex.label</p></td>
<td rowspan="2"
style="text-align: left;"><p>stats/?h.w-g.pct.stats</p></td>
</tr>
<tr>
<td><span id="line-157" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-158"
class="anchor"></span>
<p>-hyporelabel</p></td>
<td style="text-align: left;"><p>aseg.presurf.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>mri_relabel_hypointensities
aseg.presurf.mgz ../surf aseg.presurf.hypos.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>aseg.presurf.hypos.mgz</p></td>
</tr>
<tr>
<td><span id="line-159" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td rowspan="12" style="text-align: left;"><span id="line-160"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/aparc2aseg"
class="https">aparc2aseg</a></p></td>
<td><p>aseg.presurf.hypos.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --volmask --aseg
aseg.presurf.hypos --relabel mri/norm.mgz mri/transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
mri/aseg.auto_noCCseg.label_intensities.txt</p></td>
<td rowspan="4" style="text-align: left;"><p>aparc+aseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-161" class="anchor"></span>
<p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-162" class="anchor"></span>
<p>label/?h.aparc.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-163" class="anchor"></span>
<p>ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-164" class="anchor"></span>
<p>aseg.presurf.hypos.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --volmask --annot
aparc.a2009s --aseg aseg.presurf.hypos --relabel mri/norm.mgz
mri/transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
mri/aseg.auto_noCCseg.label_intensities.txt</p></td>
<td rowspan="4"
style="text-align: left;"><p>aparc.a2009s+aseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-165" class="anchor"></span>
<p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-166" class="anchor"></span>
<p>label/?h.aparc.a2009s.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-167" class="anchor"></span>
<p>ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-168" class="anchor"></span>
<p>aseg.presurf.hypos.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --volmask --annot
aparc.DKTatlas --aseg aseg.presurf.hypos --relabel mri/norm.mgz
mri/transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
mri/aseg.auto_noCCseg.label_intensities.txt</p></td>
<td rowspan="4"
style="text-align: left;"><p>aparc.DKTatlas+aseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-169" class="anchor"></span>
<p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-170" class="anchor"></span>
<p>label/?h.aparc.DKTatlas.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-171" class="anchor"></span>
<p>ribbon.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-172" class="anchor"></span>
<p>-apas2aseg</p></td>
<td><p>aparc+aseg.mgz</p></td>
<td style="text-align: left;"><p>apas2aseg --i aparc+aseg.mgz --o
aseg.mgz</p></td>
<td style="text-align: left;"><p>aseg.mgz</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-173"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/segstats"
class="https">segstats</a></p></td>
<td><p>brainmask.mgz, norm.mgz, aseg.mgz, aseg.presurf.mgz,
ribbon.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_segstats"
class="https">mri_segstats</a> --seg mri/aseg.mgz --sum stats/aseg.stats
--pv mri/norm.mgz --empty --brainmask mri/brainmask.mgz
--brain-vol-from-seg --excludeid 0 --excl-ctxgmwm --supratent
--subcortgray --in mri/norm.mgz --in-intensity-name norm
--in-intensity-units MR --etiv --surf-wm-vol --surf-ctx-vol --totalgray
--euler --ctab $FREESURFER_HOME/ASegStatsLUT.txt --subject
&lt;subjid&gt;</p></td>
<td rowspan="2" style="text-align: left;"><p>stats/aseg.stats</p></td>
</tr>
<tr>
<td><span id="line-174" class="anchor"></span>
<p>?h.orig.nofix, ?h.white, ?h.pial</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-175"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/wmparc"
class="https">wmparc</a></p></td>
<td><p>aparc+aseg.mgz</p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --labelwm
--hypo-as-wm --rip-unknown --volmask --o mri/wmparc.mgz --ctxseg
aparc+aseg.mgz</p></td>
<td style="text-align: left;"><p>wmparc.mgz</p></td>
</tr>
<tr>
<td><span id="line-176" class="anchor"></span>
<p>talairach.xfm, brainmask.mgz, norm.mgz, ribbon.mgz, wmparc.mgz,
aseg.presurf.mgz, ?h.white, ?h.pial</p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_segstats"
class="https">mri_segstats</a> --seg mri/wmparc.mgz --sum
stats/wmparc.stats --pv mri/norm.mgz --excludeid 0 --brainmask
mri/brainmask.mgz --in mri/norm.mgz --in-intensity-name norm
--in-intensity-units MR --etiv --subject &lt;subjid&gt; --surf-wm-vol
--ctab $FREESURFER_HOME/WMParcStatsLUT.txt</p></td>
<td style="text-align: left;"><p>stats/wmparc.stats</p></td>
</tr>
<tr>
<td><span id="line-177" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/BrodmannAreaMaps"
class="https">balabels</a></p></td>
<td><p>?h.sphere.reg</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_label2label"
class="https">mri_label2label</a> --srcsubject fsaverage --srclabel
fsaverage/label/?h.BA*.label --trgsubject &lt;subjid&gt; --trglabel
?h.BA*.label --hemi ?h --regmethod surface</p></td>
<td><p>label/?h.BA*_exvivo.label label/?h.perirhinal_exvivo.label
label/?h.entorhinal_exvivo.label</p></td>
</tr>
</tbody>
</table>

</div>

<span id="line-178" class="anchor"></span><span id="line-179"
class="anchor"></span><span id="line-180"
class="anchor"></span><span id="line-181"
class="anchor"></span><span id="line-182"
class="anchor"></span><span id="line-183" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-184"
class="anchor"></span>—————————————————————————————————
<span id="line-185" class="anchor"></span>

# ReconAllTableStable7.1.1

<span id="line-186" class="anchor"></span><span id="line-187"
class="anchor"></span>

This table shows the recon-all steps for the **stable**, publicly
released, **version 7.1.1** of FreeSurfer [(available
here)](DownloadAndInstall.html). <span id="line-188"
class="anchor"></span><span id="line-189" class="anchor"></span>

See also the
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/OtherUsefulFlags"
class="https">OtherUsefulFlags</a> for other recon-all options.
<span id="line-190" class="anchor"></span>

<div>

<table style="text-align:left;                     ; text-align:left">
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>recon-all step</strong></p></td>
<td><p><strong>Individual Flag</strong></p></td>
<td><p><strong>Input</strong></p></td>
<td><p><strong>Command Line</strong></p></td>
<td><p><strong>Output</strong></p></td>
</tr>
<tr>
<td rowspan="19" style="text-align: left;"><span id="line-191"
class="anchor"></span>
<p><strong><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="https">recon-all</a> -autorecon1 -subjid
&lt;subjid&gt;</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-192" class="anchor"></span>
<p>-i &lt;invol1&gt;</p></td>
<td><p>invol1.dcm <em>or .nii or .mgz</em></p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> invol1.dcm orig/001.mgz</p></td>
<td><p>orig/001.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-193" class="anchor"></span>
<p>-i &lt;invol2&gt; <em>optional</em></p></td>
<td><p>invol2.dcm <em>or .nii or .mgz</em></p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> invol2.dcm orig/002.mgz</p></td>
<td><p>orig/002.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-194" class="anchor"></span>
<p>-T2 &lt;invol&gt; <em>or</em> -FLAIR &lt;invol&gt;
<em>optional</em></p></td>
<td style="text-align: left;"><p>invol.dcm <em>or .nii or
.mgz</em></p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> --no_scale 1 invol.dcm orig/T2raw.mgz
<em>(or orig/FLAIRraw.mgz)</em></p></td>
<td style="text-align: left;"><p>orig/T2raw.mgz <em>(or
orig/FLAIRraw.mgz)</em></p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-195"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/motioncor"
class="https">motioncor</a></p></td>
<td><p>orig/001.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_robust_template"
class="https">mri_robust_template</a> --mov 001.mgz 002.mgz --average 1
--template rawavg.mgz --satit --inittp 1 --fixtp --noit --iscale
--iscaleout --subsample 200 --lta</p></td>
<td rowspan="2" style="text-align: left;"><p>rawavg.mgz</p></td>
</tr>
<tr>
<td><span id="line-196" class="anchor"></span>
<p>orig/002.mgz</p></td>
</tr>
<tr>
<td><span id="line-197" class="anchor"></span>
<p>rawavg.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_convert"
class="https">mri_convert</a> rawavg.mgz orig.mgz --conform</p></td>
<td><p>orig.mgz</p></td>
</tr>
<tr>
<td><span id="line-198" class="anchor"></span>
<p>orig.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_add_xform_to_header"
class="https">mri_add_xform_to_header</a> -c transforms/talairach.xfm
orig.mgz orig.mgz</p></td>
<td><p>orig.mgz</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-199"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/talairach"
class="https">talairach</a></p></td>
<td><p>orig.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_nu_correct.mni"
class="https">mri_nu_correct.mni</a> --n 1 --proto-iters 1000 --distance
50 --no-rescale --i orig.mgz --o orig_nu.mgz</p></td>
<td><p>orig_nu.mgz</p></td>
</tr>
<tr>
<td><span id="line-200" class="anchor"></span>
<p>orig_nu.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/talairach_avi"
class="https">talairach_avi</a> --i orig_nu.mgz --xfm
transforms/talairach.auto.xfm</p></td>
<td><p>transforms/talairach.auto.xfm</p></td>
</tr>
<tr>
<td><span id="line-201" class="anchor"></span>
<p>transforms/talairach.auto.xfm</p></td>
<td><p>cp transforms/talairach.auto.xfm
transforms/talairach.xfm</p></td>
<td><p>transforms/talairach.xfm</p></td>
</tr>
<tr>
<td><span id="line-202" class="anchor"></span>
<p>transforms/talairach.xfm</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/talairach_afd"
class="https">talairach_afd</a> -T 0.005 -xfm
transforms/talairach.xfm</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-203" class="anchor"></span></td>
<td><p>awk -f $FREESURFER_HOME/bin/extract_talairach_avi_QA.awk
transforms/talairach_avi.log</p></td>
<td><p>transforms/talairach_avi.log</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-204"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/nuintensitycor"
class="https">nuintensitycor</a></p></td>
<td><p>orig.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_nu_correct.mni"
class="https">mri_nu_correct.mni</a> --i orig.mgz --o nu.mgz --uchar
transforms/talairach.xfm --n 2</p></td>
<td rowspan="2" style="text-align: left;"><p>nu.mgz</p></td>
</tr>
<tr>
<td><span id="line-205" class="anchor"></span>
<p>talairach.xfm</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-206" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/normalization"
class="https">normalization</a></p></td>
<td><p>nu.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_normalize"
class="https">mri_normalize</a> -g 1 -mprage nu.mgz T1.mgz</p></td>
<td><p>T1.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-207"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/skullstrip"
class="https">skullstrip</a></p></td>
<td><p>nu.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_em_register"
class="https">mri_em_register</a> -skull nu.mgz
$FREESURFER_HOME/average/RB_all_withskull_2016-05-10.vc700.gca
transforms/talairach_with_skull.lta</p></td>
<td><p>transforms/talairach_with_skull.lta</p></td>
</tr>
<tr>
<td><span id="line-208" class="anchor"></span>
<p>T1.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_watershed"
class="https">mri_watershed</a> -T1 -brain_atlas
$FREESURFER_HOME/average/RB_all_withskull_2016-05-10.vc700.gca
transforms/talairach_with_skull.lta T1.mgz brainmask.auto.mgz</p></td>
<td><p>brainmask.auto.mgz</p></td>
</tr>
<tr>
<td><span id="line-209" class="anchor"></span>
<p>brainmask.auto.mgz</p></td>
<td><p>cp brainmask.auto.mgz brainmask.mgz</p></td>
<td><p>brainmask.mgz</p></td>
</tr>
</tbody>
</table>

</div>

<span id="line-210" class="anchor"></span><span id="line-211"
class="anchor"></span><span id="line-212" class="anchor"></span>

<div>

<table style="text-align:left;                     ; text-align:left">
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>recon-all step</strong></p></td>
<td><p><strong>Individual Flag</strong></p></td>
<td><p><strong>Input</strong></p></td>
<td><p><strong>Command Line</strong></p></td>
<td><p><strong>Output</strong></p></td>
</tr>
<tr>
<td rowspan="62" style="text-align: left;"><span id="line-213"
class="anchor"></span>
<p><strong><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="https">recon-all</a> -autorecon2 -subjid
&lt;subjid&gt;</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-214"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/gcareg"
class="https">gcareg</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_em_register"
class="https">mri_em_register</a> -uns 3 -mask brainmask.mgz nu.mgz
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
transforms/talairach.lta</p></td>
<td rowspan="2"
style="text-align: left;"><p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td><span id="line-215" class="anchor"></span>
<p>nu.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-216"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/canorm"
class="https">canorm</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_normalize"
class="https">mri_ca_normalize</a> -c ctrl_pts.mgz -mask brainmask.mgz
nu.mgz $FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
transforms/talairach.lta norm.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-217" class="anchor"></span>
<p>nu.mgz</p></td>
</tr>
<tr>
<td><span id="line-218" class="anchor"></span>
<p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-219"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/careg"
class="https">careg</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_register"
class="https">mri_ca_register</a> -align-after -nobigventricles -mask
brainmask.mgz -T transforms/talairach.lta norm.mgz
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
transforms/talairach.m3z</p></td>
<td rowspan="3"
style="text-align: left;"><p>transforms/talairach.m3z</p></td>
</tr>
<tr>
<td><span id="line-220" class="anchor"></span>
<p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td><span id="line-221" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-222"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/calabel"
class="https">calabel</a></p></td>
<td><p>norm.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_label"
class="https">mri_ca_label</a> -relabel_unlikely 9 .3 -prior 0.5 -align
norm.mgz transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
aseg.auto_noCCseg.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>aseg.auto_noCCseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-223" class="anchor"></span>
<p>transforms/talairach.m3z</p></td>
</tr>
<tr>
<td><span id="line-224" class="anchor"></span>
<p>aseg.auto_noCCseg.mgz</p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_cc"
class="https">mri_cc</a> -lta &lt;subjid&gt;/mri/transforms/cc_up.lta
-aseg aseg.auto_noCCseg.mgz -o aseg.auto.mgz &lt;subjid&gt;</p></td>
<td><p>aseg.auto.mgz</p></td>
</tr>
<tr>
<td><span id="line-225" class="anchor"></span>
<p>aseg.auto.mgz</p></td>
<td><p>cp aseg.auto.mgz aseg.presurf.mgz</p></td>
<td><p>aseg.presurf.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-226"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/normalization2"
class="https">normalization2</a></p></td>
<td><p>brainmask.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_normalize"
class="https">mri_normalize</a> -mprage -aseg aseg.presurf.mgz -mask
brainmask.mgz norm.mgz brain.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>brain.mgz</p></td>
</tr>
<tr>
<td><span id="line-227" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-228" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-229"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/maskbfs"
class="https">maskbfs</a></p></td>
<td><p>brain.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_mask"
class="https">mri_mask</a> -T 5 brain.mgz brainmask.mgz
brain.finalsurfs.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td><span id="line-230" class="anchor"></span>
<p>brainmask.mgz</p></td>
</tr>
<tr>
<td rowspan="6" style="text-align: left;"><span id="line-231"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/segmentation"
class="https">segmentation</a></p></td>
<td><p>brain.mgz</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_segment"
class="https">mri_segment</a> -mprage brain.mgz wm.seg.mgz</p></td>
<td><p>wm.seg.mgz</p></td>
</tr>
<tr>
<td><span id="line-232" class="anchor"></span>
<p>wm.seg.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_edit_wm_with_aseg"
class="https">mri_edit_wm_with_aseg</a> wm.seg.mgz brain.mgz
aseg.presurf.mgz wm.asegedit.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>wm.asegedit.mgz</p></td>
</tr>
<tr>
<td><span id="line-233" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
</tr>
<tr>
<td><span id="line-234" class="anchor"></span>
<p>brain.mgz</p></td>
</tr>
<tr>
<td><span id="line-235" class="anchor"></span>
<p>wm.asegedit.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_pretess"
class="https">mri_pretess</a> wm.asegedit.mgz wm norm.mgz
wm.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>wm.mgz</p></td>
</tr>
<tr>
<td><span id="line-236" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-237"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/fill"
class="https">fill</a></p></td>
<td><p>wm.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_fill"
class="https">mri_fill</a> -a ../scripts/ponscc.cut.log -xform
transforms/talairach.lta -segmentation aseg.auto_noCCseg.mgz wm.mgz
filled.mgz</p></td>
<td><p>filled.mgz</p></td>
</tr>
<tr>
<td><span id="line-238" class="anchor"></span>
<p>aseg.auto_noCCseg.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>../scripts/ponscc.cut.log</p></td>
</tr>
<tr>
<td><span id="line-239" class="anchor"></span>
<p>transforms/talairach.lta</p></td>
</tr>
<tr>
<td rowspan="8" style="text-align: left;"><span id="line-240"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/tessellate"
class="https">tessellate</a></p></td>
<td><p>filled.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_pretess"
class="https">mri_pretess</a> filled.mgz 255 norm.mgz
filled-pretess255.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>filled-pretess255.mgz</p></td>
</tr>
<tr>
<td><span id="line-241" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-242" class="anchor"></span>
<p>filled-pretess255.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_tessellate"
class="https">mri_tessellate</a> filled-pretess255.mgz 255
lh.orig.nofix</p></td>
<td><p>lh.orig.nofix</p></td>
</tr>
<tr>
<td><span id="line-243" class="anchor"></span>
<p>filled.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_pretess"
class="https">mri_pretess</a> filled.mgz 127 norm.mgz
filled-pretess127.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>filled-pretess127.mgz</p></td>
</tr>
<tr>
<td><span id="line-244" class="anchor"></span>
<p>norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-245" class="anchor"></span>
<p>filled-pretess127.mgz</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_tessellate"
class="https">mri_tessellate</a> filled-pretess127.mgz 127
rh.orig.nofix</p></td>
<td><p>rh.orig.nofix</p></td>
</tr>
<tr>
<td><span id="line-246" class="anchor"></span>
<p>?h.orig.nofix</p></td>
<td><p>mris_extract_main_component ?h.orig.nofix ?h.orig.nofix</p></td>
<td><p>?h.orig.nofix</p></td>
</tr>
<tr>
<td><span id="line-247" class="anchor"></span></td>
<td><p>rm -f filled-pretess255.mgz filled-pretess127.mgz</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-248" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/smooth"
class="https">smooth1</a></p></td>
<td><p>?h.orig.nofix</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_smooth"
class="https">mris_smooth</a> -nw ?h.orig.nofix
?h.smoothwm.nofix</p></td>
<td><p>?h.smoothwm.nofix</p></td>
</tr>
<tr>
<td><span id="line-249" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/inflate"
class="https">inflate1</a></p></td>
<td><p>?h.smoothwm.nofix</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_inflate"
class="https">mris_inflate</a> -no-save-sulc ?h.smoothwm.nofix
?h.inflated.nofix</p></td>
<td><p>?h.inflated.nofix</p></td>
</tr>
<tr>
<td><span id="line-250" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/qsphere"
class="https">qsphere</a></p></td>
<td><p>?h.inflated.nofix</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_sphere"
class="https">mris_sphere</a> -q ?h.inflated.nofix
?h.qsphere.nofix</p></td>
<td><p>?h.qsphere.nofix</p></td>
</tr>
<tr>
<td rowspan="6" style="text-align: left;"><span id="line-251"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/fix"
class="https">fix</a></p></td>
<td><p>?h.orig.nofix</p></td>
<td><p>cp ?h.orig.nofix ?h.orig</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-252" class="anchor"></span>
<p>?h.inflated.nofix</p></td>
<td><p>cp ?h.inflated.nofix ?h.inflated</p></td>
<td><p>?h.inflated</p></td>
</tr>
<tr>
<td><span id="line-253" class="anchor"></span>
<p>?h.qsphere.nofix</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_fix_topology"
class="https">mris_fix_topology</a> -mgz -sphere qsphere.nofix -ga
&lt;subjid&gt; ?h</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-254" class="anchor"></span>
<p>?h.orig</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_euler_number"
class="https">mris_euler_number</a> ?h.orig</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-255" class="anchor"></span>
<p>?h.orig</p></td>
<td><p>mris_remove_intersection ?h.orig ?h.orig</p></td>
<td><p>?h.orig</p></td>
</tr>
<tr>
<td><span id="line-256" class="anchor"></span></td>
<td><p>rm ?h.inflated</p></td>
<td></td>
</tr>
<tr>
<td rowspan="8" style="text-align: left;"><span id="line-257"
class="anchor"></span>
<p>-white</p></td>
<td style="text-align: left;"><p>aseg.presurf.mgz</p></td>
<td rowspan="8" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_make_surfaces"
class="https">mris_make_surfaces</a> -aseg ../mri/aseg.presurf
-whiteonly -noaparc -mgz -T1 brain.finalsurfs &lt;subjid&gt; ?h</p></td>
<td rowspan="4" style="text-align: left;"><p>?h.white.preaparc</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-258" class="anchor"></span>
<p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-259" class="anchor"></span>
<p>wm.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-260" class="anchor"></span>
<p>filled.mgz</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-261"
class="anchor"></span>
<p>?h.orig</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-262" class="anchor"></span>
<p>?h.curv</p></td>
</tr>
<tr>
<td><span id="line-263" class="anchor"></span>
<p>?h.area</p></td>
</tr>
<tr>
<td><span id="line-264" class="anchor"></span>
<p>?h.cortex.label</p></td>
</tr>
<tr>
<td><span id="line-265" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/smooth"
class="https">smooth2</a></p></td>
<td><p>?h.white.preaparc</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_smooth"
class="https">mris_smooth</a> -n 3 -nw ?h.white.preaparc
?h.smoothwm</p></td>
<td><p>?h.smoothwm</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-266"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/inflate"
class="https">inflate2</a></p></td>
<td rowspan="2" style="text-align: left;"><p>?h.smoothwm</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_inflate"
class="https">mris_inflate</a> ?h.smoothwm ?h.inflated</p></td>
<td><p>?h.inflated</p></td>
</tr>
<tr>
<td><span id="line-267" class="anchor"></span>
<p>?h.sulc</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-268"
class="anchor"></span>
<p>-curvHK</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.white.preaparc</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_curvature"
class="https">mris_curvature</a> -w ?h.white.preaparc</p></td>
<td style="text-align: left;"><p>?h.white.H</p></td>
</tr>
<tr>
<td><span id="line-269" class="anchor"></span>
<p>?h.white.K</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-270"
class="anchor"></span>
<p>?h.inflated</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_curvature"
class="https">mris_curvature</a> -thresh .999 -n -a 5 -w -distances 10
10 ?h.inflated</p></td>
<td style="text-align: left;"><p>?h.inflated.H</p></td>
</tr>
<tr>
<td><span id="line-271" class="anchor"></span>
<p>?h.inflated.K</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-272"
class="anchor"></span>
<p>-curvstats</p></td>
<td style="text-align: left;"><p>?h.smoothwm</p></td>
<td rowspan="3" style="text-align: left;"><p>mris_curvature_stats -m
--writeCurvatureFiles -G -o ../stats/?h.curv.stats -F smoothwm
&lt;subjid&gt; ?h curv sulc</p></td>
<td rowspan="3"
style="text-align: left;"><p>stats/?h.curv.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-273" class="anchor"></span>
<p>?h.curv</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-274" class="anchor"></span>
<p>?h.sulc</p></td>
</tr>
</tbody>
</table>

</div>

<span id="line-275" class="anchor"></span><span id="line-276"
class="anchor"></span><span id="line-277" class="anchor"></span>

<div>

<table style="text-align:left;                     ; text-align:left">
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>recon-all step</strong></p></td>
<td><p><strong>Individual Flag</strong></p></td>
<td><p><strong>Input</strong></p></td>
<td><p><strong>Command Line</strong></p></td>
<td><p><strong>Output</strong></p></td>
</tr>
<tr>
<td rowspan="84" style="text-align: left;"><span id="line-278"
class="anchor"></span>
<p><strong><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="https">recon-all</a> -autorecon3 -subjid
&lt;subjid&gt;</strong></p></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-279"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/sphere"
class="https">sphere</a></p></td>
<td><p>?h.inflated</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_sphere"
class="https">mris_sphere</a> ?h.inflated ?h.sphere</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.sphere</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-280" class="anchor"></span>
<p>?h.smoothwm</p></td>
</tr>
<tr>
<td><span id="line-281" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/surfreg"
class="https">surfreg</a></p></td>
<td><p>?h.sphere</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_register"
class="https">mris_register</a> -curv ?h.sphere
$FREESURFER_HOME/average/?h.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif
?h.sphere.reg</p></td>
<td><p>?h.sphere.reg</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-282"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/jacobian_white"
class="https">jacobian_white</a></p></td>
<td><p>?h.white.preaparc</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_jacobian"
class="https">mris_jacobian</a> ?h.white.preaparc ?h.sphere.reg
?h.jacobian_white</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.jacobian_white</p></td>
</tr>
<tr>
<td><span id="line-283" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td><span id="line-284" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/avgcurv"
class="https">avgcurv</a></p></td>
<td><p>?h.sphere.reg</p></td>
<td><p><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/mrisp_paint"
class="https">mrisp_paint</a> -a 5
$FREESURFER_HOME/average/?h.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif#6
?h.sphere.reg ?h.avg_curv</p></td>
<td><p>?h.avg_curv</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-285"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortparc"
class="https">cortparc</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_ca_label"
class="https">mris_ca_label</a> -l ../label/?h.cortex.label -aseg
mri/aseg.presurf.mgz &lt;subjid&gt; ?h ?h.sphere.reg
$FREESURFER_HOME/average/?h.curvature.buckner40.filled.desikan_killiany.2007-06-20.gcs
?h.aparc.annot</p></td>
<td rowspan="3"
style="text-align: left;"><p>label/?h.aparc.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-286" class="anchor"></span>
<p>?h.cortex.label</p></td>
</tr>
<tr>
<td><span id="line-287" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td rowspan="8" style="text-align: left;"><span id="line-288"
class="anchor"></span>
<p>-pial</p></td>
<td style="text-align: left;"><p>aseg.presurf.mgz</p></td>
<td rowspan="8" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_make_surfaces"
class="https">mris_make_surfaces</a> -orig_white white.preaparc
-orig_pial white.preaparc -aseg ../mri/aseg.presurf -mgz -T1
brain.finalsurfs &lt;subjid&gt; ?h</p></td>
<td rowspan="4" style="text-align: left;"><p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-289" class="anchor"></span>
<p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td><span id="line-290" class="anchor"></span>
<p>wm.mgz</p></td>
</tr>
<tr>
<td><span id="line-291" class="anchor"></span>
<p>filled.mgz</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-292"
class="anchor"></span>
<p>?h.orig</p></td>
<td></td>
</tr>
<tr>
<td><span id="line-293" class="anchor"></span>
<p>?h.curv.pial</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-294" class="anchor"></span>
<p>?h.area.pial</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-295" class="anchor"></span>
<p>label/?h.aparc.annot</p></td>
<td><p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="17" style="text-align: left;"><span id="line-296"
class="anchor"></span>
<p>-T2pial <em>or</em><br />
-FLAIRpial <em>optional</em></p></td>
<td><p>orig/T2raw.mgz</p></td>
<td><p>bbregister --s &lt;subjid&gt; --mov mri/orig/T2raw.mgz --lta
mri/transforms/T2raw.lta --init-fsl --T2</p></td>
<td><p>transforms/T2raw.lta</p></td>
</tr>
<tr>
<td><span id="line-297" class="anchor"></span>
<p>orig/T2raw.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>mri_convert -odt float -at
mri/transforms/T2raw.lta -rt cubic -ns 1 -rl mri/orig.mgz
mri/orig/T2raw.mgz mri/T2.prenorm.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>T2.prenorm.mgz</p></td>
</tr>
<tr>
<td><span id="line-298" class="anchor"></span>
<p>transforms/T2raw.lta</p></td>
</tr>
<tr>
<td><span id="line-299" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>mri_normalize -sigma 0.5
-nonmax_suppress 0 -min_dist 1 -aseg mri/aseg.presurf.mgz -surface
surf/rh.white identity.nofile -surface surf/lh.white identity.nofile
mri/T2.prenorm.mgz mri/T2.norm.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>T2.norm.mgz</p></td>
</tr>
<tr>
<td><span id="line-300" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-301" class="anchor"></span>
<p>T2.prenorm.mgz</p></td>
</tr>
<tr>
<td><span id="line-302" class="anchor"></span>
<p>T2.norm.mgz</p></td>
<td rowspan="2" style="text-align: center;"><p>mri_mask mri/T2.norm.mgz
mri/brainmask.mgz mri/T2.mgz</p></td>
<td rowspan="2" style="text-align: center;"><p>T2.mgz</p></td>
</tr>
<tr>
<td><span id="line-303" class="anchor"></span>
<p>brainmask.mgz</p></td>
</tr>
<tr>
<td><span id="line-304" class="anchor"></span>
<p>?h.pial</p></td>
<td><p>cp -v surf/?h.pial surf/?h.woT2.pial</p></td>
<td><p>?h.woT2.pial</p></td>
</tr>
<tr>
<td><span id="line-305" class="anchor"></span>
<p>aseg.presurf.mgz</p></td>
<td rowspan="9" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_make_surfaces">mris_make_surfaces</a>
-orig_white white -orig_pial woT2.pial -aseg ../mri/aseg.presurf
-nowhite -mgz -T1 brain.finalsurfs -T2 ../mri/T2 -nsigma_above 2
-nsigma_below 5 &lt;subjid&gt; ?h</p></td>
<td rowspan="3" style="text-align: left;"><p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-306" class="anchor"></span>
<p>brain.finalsurfs.mgz</p></td>
</tr>
<tr>
<td><span id="line-307" class="anchor"></span>
<p>wm.mgz</p></td>
</tr>
<tr>
<td><span id="line-308" class="anchor"></span>
<p>filled.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.curv.pial</p></td>
</tr>
<tr>
<td><span id="line-309" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-310" class="anchor"></span>
<p>label/?h.aparc.annot</p></td>
<td style="text-align: left;"><p>?h.area.pial</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-311" class="anchor"></span>
<p>T2.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p>?h.thickness</p></td>
</tr>
<tr>
<td><span id="line-312" class="anchor"></span>
<p>?h.woT2.pial</p></td>
</tr>
<tr>
<td><span id="line-313" class="anchor"></span></td>
<td></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-314"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortribbon"
class="https">cortribbon</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_volmask"
class="https">mris_volmask</a> --aseg_name aseg.presurf
--label_left_white 2 --label_left_ribbon 3 --label_right_white 41
--label_right_ribbon 42 --save_ribbon &lt;subjid&gt;</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-315" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-316" class="anchor"></span>
<p>?h.pial</p></td>
<td style="text-align: left;"><p>ribbon.mgz</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-317"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/parcstats"
class="https">parcstats</a></p></td>
<td style="text-align: left;"><p>label/?h.aparc.annot</p></td>
<td rowspan="5" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_anatomical_stats"
class="https">mris_anatomical_stats</a> -th3 -mgz -cortex
../label/?h.cortex.label -f stats/?h.aparc.stats -b -a
label/?h.aparc.annot -c label/aparc.annot.ctab &lt;subjid&gt; ?h
&lt;white or pial&gt;</p></td>
<td><p>stats/?h.aparc.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-318" class="anchor"></span>
<p>wm.mgz, ribbon.mgz</p></td>
<td rowspan="4"
style="text-align: left;"><p>label/aparc.annot.ctab</p></td>
</tr>
<tr>
<td><span id="line-319" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-320" class="anchor"></span>
<p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-321" class="anchor"></span>
<p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-322"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortparc"
class="https">cortparc2</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_ca_label"
class="https">mris_ca_label</a> -l ../label/?h.cortex.label -aseg
aseg.presurf.mgz &lt;subjid&gt; ?h ?h.sphere.reg
$FREESURFER_HOME/average/?h.destrieux.simple.2009-07-29.gcs
label/?h.aparc.a2009s.annot</p></td>
<td rowspan="3"
style="text-align: left;"><p>label/?h.aparc.a2009s.annot</p></td>
</tr>
<tr>
<td><span id="line-323" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td><span id="line-324" class="anchor"></span>
<p>label/?h.cortex.label</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-325"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/parcstats"
class="https">parcstats2</a></p></td>
<td style="text-align: left;"><p>label/?h.aparc.a2009s.annot</p></td>
<td rowspan="5" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_anatomical_stats"
class="https">mris_anatomical_stats</a> -th3 -mgz -cortex
../label/?h.cortex.label -f stats/?h.aparc.a2009s.stats -b -a
label/?h.aparc.a2009s.annot -c label/aparc.annot.a2009s.ctab
&lt;subjid&gt; ?h</p></td>
<td><p>stats/?h.aparc.a2009s.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-326" class="anchor"></span>
<p>wm.mgz, ribbon.mgz</p></td>
<td rowspan="4"
style="text-align: left;"><p>label/aparc.annot.a2009s.ctab</p></td>
</tr>
<tr>
<td><span id="line-327" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-328" class="anchor"></span>
<p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-329" class="anchor"></span>
<p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="3" style="text-align: left;"><span id="line-330"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/cortparc"
class="https">cortparc3</a></p></td>
<td><p>aseg.presurf.mgz</p></td>
<td rowspan="3" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_ca_label"
class="https">mris_ca_label</a> -l ../label/?h.cortex.label -aseg
aseg.presurf.mgz &lt;subjid&gt; ?h ?h.sphere.reg
$FREESURFER_HOME/average/?h.DKTatlas.2016-03-20.gcs
../label/?h.aparc.DKTatlas.annot</p></td>
<td rowspan="3"
style="text-align: left;"><p>label/?h.aparc.DKTatlas.annot</p></td>
</tr>
<tr>
<td><span id="line-331" class="anchor"></span>
<p>?h.sphere.reg</p></td>
</tr>
<tr>
<td><span id="line-332" class="anchor"></span>
<p>label/?h.cortex.label</p></td>
</tr>
<tr>
<td rowspan="5" style="text-align: left;"><span id="line-333"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/parcstats"
class="https">parcstats3</a></p></td>
<td style="text-align: left;"><p>label/?h.aparc.DKTatlas.annot</p></td>
<td rowspan="5" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mris_anatomical_stats"
class="https">mris_anatomical_stats</a> -th3 -mgz -cortex
../label/?h.cortex.label -f stats/?h.aparc.DKTatlas.stats -b -a
label/?h.aparc.DKTatlas.annot -c label/aparc.annot.DKTatlas.ctab
&lt;subjid&gt; ?h</p></td>
<td><p>stats/?h.aparc.DKTatlas.stats</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-334" class="anchor"></span>
<p>wm.mgz, ribbon.mgz</p></td>
<td rowspan="4"
style="text-align: left;"><p>label/aparc.annot.DKTatlas.ctab</p></td>
</tr>
<tr>
<td><span id="line-335" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td><span id="line-336" class="anchor"></span>
<p>?h.pial</p></td>
</tr>
<tr>
<td><span id="line-337" class="anchor"></span>
<p>?h.thickness</p></td>
</tr>
<tr>
<td rowspan="4" style="text-align: left;"><span id="line-338"
class="anchor"></span>
<p>-pctsurfcon</p></td>
<td><p>rawavg.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p>pctsurfcon --s
&lt;subjid&gt; --?h-only</p></td>
<td rowspan="2" style="text-align: left;"><p>?h.w-g.pct.mgh</p></td>
</tr>
<tr>
<td><span id="line-339" class="anchor"></span>
<p>orig.mgz</p></td>
</tr>
<tr>
<td><span id="line-340" class="anchor"></span>
<p>?h.cortex.label</p></td>
<td rowspan="2"
style="text-align: left;"><p>stats/?h.w-g.pct.stats</p></td>
</tr>
<tr>
<td><span id="line-341" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-342"
class="anchor"></span>
<p>-hyporelabel</p></td>
<td style="text-align: left;"><p>aseg.presurf.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p>mri_relabel_hypointensities
aseg.presurf.mgz ../surf aseg.presurf.hypos.mgz</p></td>
<td rowspan="2"
style="text-align: left;"><p>aseg.presurf.hypos.mgz</p></td>
</tr>
<tr>
<td><span id="line-343" class="anchor"></span>
<p>?h.white</p></td>
</tr>
<tr>
<td rowspan="12" style="text-align: left;"><span id="line-344"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/aparc2aseg"
class="https">aparc2aseg</a></p></td>
<td><p>aseg.presurf.hypos.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --volmask --aseg
aseg.presurf.hypos --relabel mri/norm.mgz mri/transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
mri/aseg.auto_noCCseg.label_intensities.txt</p></td>
<td rowspan="4" style="text-align: left;"><p>aparc+aseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-345" class="anchor"></span>
<p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-346" class="anchor"></span>
<p>label/?h.aparc.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-347" class="anchor"></span>
<p>ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-348" class="anchor"></span>
<p>aseg.presurf.hypos.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --volmask --annot
aparc.a2009s --aseg aseg.presurf.hypos --relabel mri/norm.mgz
mri/transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
mri/aseg.auto_noCCseg.label_intensities.txt</p></td>
<td rowspan="4"
style="text-align: left;"><p>aparc.a2009s+aseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-349" class="anchor"></span>
<p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-350" class="anchor"></span>
<p>label/?h.aparc.a2009s.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-351" class="anchor"></span>
<p>ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-352" class="anchor"></span>
<p>aseg.presurf.hypos.mgz</p></td>
<td rowspan="4" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --volmask --annot
aparc.DKTatlas --aseg aseg.presurf.hypos --relabel mri/norm.mgz
mri/transforms/talairach.m3z
$FREESURFER_HOME/average/RB_all_2016-05-10.vc700.gca
mri/aseg.auto_noCCseg.label_intensities.txt</p></td>
<td rowspan="4"
style="text-align: left;"><p>aparc.DKTatlas+aseg.mgz</p></td>
</tr>
<tr>
<td><span id="line-353" class="anchor"></span>
<p>?h.ribbon.mgz</p></td>
</tr>
<tr>
<td><span id="line-354" class="anchor"></span>
<p>label/?h.aparc.DKTatlas.annot</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-355" class="anchor"></span>
<p>ribbon.mgz</p></td>
</tr>
<tr>
<td style="text-align: left;"><span id="line-356" class="anchor"></span>
<p>-apas2aseg</p></td>
<td><p>aparc+aseg.mgz</p></td>
<td style="text-align: left;"><p>apas2aseg --i aparc+aseg.mgz --o
aseg.mgz</p></td>
<td style="text-align: left;"><p>aseg.mgz</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-357"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/segstats"
class="https">segstats</a></p></td>
<td><p>brainmask.mgz, norm.mgz, aseg.mgz, aseg.presurf.mgz,
ribbon.mgz</p></td>
<td rowspan="2" style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_segstats"
class="https">mri_segstats</a> --seg mri/aseg.mgz --sum stats/aseg.stats
--pv mri/norm.mgz --empty --brainmask mri/brainmask.mgz
--brain-vol-from-seg --excludeid 0 --excl-ctxgmwm --supratent
--subcortgray --in mri/norm.mgz --in-intensity-name norm
--in-intensity-units MR --etiv --surf-wm-vol --surf-ctx-vol --totalgray
--euler --ctab $FREESURFER_HOME/ASegStatsLUT.txt --subject
&lt;subjid&gt;</p></td>
<td rowspan="2" style="text-align: left;"><p>stats/aseg.stats</p></td>
</tr>
<tr>
<td><span id="line-358" class="anchor"></span>
<p>?h.orig.nofix, ?h.white, ?h.pial</p></td>
</tr>
<tr>
<td rowspan="2" style="text-align: left;"><span id="line-359"
class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/wmparc"
class="https">wmparc</a></p></td>
<td><p>aparc+aseg.mgz</p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_aparc2aseg"
class="https">mri_aparc2aseg</a> --s &lt;subjid&gt; --labelwm
--hypo-as-wm --rip-unknown --volmask --o mri/wmparc.mgz --ctxseg
aparc+aseg.mgz</p></td>
<td style="text-align: left;"><p>wmparc.mgz</p></td>
</tr>
<tr>
<td><span id="line-360" class="anchor"></span>
<p>talairach.xfm, brainmask.mgz, norm.mgz, ribbon.mgz, wmparc.mgz,
aseg.presurf.mgz, ?h.white, ?h.pial</p></td>
<td style="text-align: left;"><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_segstats"
class="https">mri_segstats</a> --seg mri/wmparc.mgz --sum
stats/wmparc.stats --pv mri/norm.mgz --excludeid 0 --brainmask
mri/brainmask.mgz --in mri/norm.mgz --in-intensity-name norm
--in-intensity-units MR --etiv --subject &lt;subjid&gt; --surf-wm-vol
--ctab $FREESURFER_HOME/WMParcStatsLUT.txt</p></td>
<td style="text-align: left;"><p>stats/wmparc.stats</p></td>
</tr>
<tr>
<td><span id="line-361" class="anchor"></span>
<p>-<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/BrodmannAreaMaps"
class="https">balabels</a></p></td>
<td><p>?h.sphere.reg</p></td>
<td><p><a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/mri_label2label"
class="https">mri_label2label</a> --srcsubject fsaverage --srclabel
fsaverage/label/?h.BA*.label --trgsubject &lt;subjid&gt; --trglabel
?h.BA*.label --hemi ?h --regmethod surface</p></td>
<td><p>label/?h.BA*_exvivo.label label/?h.perirhinal_exvivo.label
label/?h.entorhinal_exvivo.label</p></td>
</tr>
</tbody>
</table>

</div>

<span id="line-362" class="anchor"></span><span id="bottom"
class="anchor"></span>

</div>

ReconAllTableStableV6.0 (last edited 2020-12-14 18:33:16 by
<span title="DevaniCordero @ 10.251.199.69[10.251.199.69]"><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/DevaniCordero"
class="nonexistent"
title="DevaniCordero @ 10.251.199.69[10.251.199.69]">DevaniCordero</a></span>)

<div id="pagebottom">

</div>

</div>

<div id="footer">

- <span class="disabled">Immutable Page</span>

- <a href="ReconAllTableStableV6.0.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV6.0?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV6.0?action=AttachFile"
  class="nbattachments" rel="nofollow">Attachments</a>

- <div>

  More Actions: Raw Text Print View Render as Docbook Delete Cache
  ------------------------ Check Spelling Like Pages Local Site Map
  ------------------------ Rename Page Delete Page
  ------------------------ Subscribe User ------------------------
  Remove Spam Revert to this revision Package Pages Sync Pages
  ------------------------ Load Save SlideShow

  </div>

<!-- -->

- [MoinMoin
  Powered](http://moinmo.in/ "This site uses the MoinMoin Wiki software.")
- [Python
  Powered](http://moinmo.in/Python "MoinMoin is written in Python.")
- [GPL licensed](http://moinmo.in/GPL "MoinMoin is GPL licensed.")
- [Valid HTML
  4.01](http://validator.w3.org/check?uri=referer "Click here to validate this page.")

</div>

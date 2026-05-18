<div id="header">

<div id="logo">

[![FreeSurfer](https://surfer.nmr.mgh.harvard.edu/wiki/fswiki_htdocs/common/fslogosmall.png)](FreeSurferWiki.html)

</div>

<div>

Search:

</div>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferCommandsRegistration?action=login"
  id="login" rel="nofollow">Login</a>

<div id="locationline">

- [FreeSurferCommandsRegistration](FreeSurferCommandsRegistration.html)

</div>

- [FreeSurferWiki](FreeSurferWiki.html)
- [RecentChanges](https://surfer.nmr.mgh.harvard.edu/fswiki/RecentChanges)
- [FindPage](https://surfer.nmr.mgh.harvard.edu/fswiki/FindPage)
- [HelpContents](https://surfer.nmr.mgh.harvard.edu/fswiki/HelpContents)
- [FreeSurferC...egistration](FreeSurferCommandsRegistration.html)

<div id="pageline">

------------------------------------------------------------------------

</div>

- <span class="disabled">Immutable Page</span>

- <a href="FreeSurferCommandsRegistration.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferCommandsRegistration?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferCommandsRegistration?action=AttachFile"
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

Freesurfer comes with a variety of different registration tools designed
for specific purposes. This page is supposed to highlight a few of them
and describe the context in which they should be used: <span id="line-2"
class="anchor"></span><span id="line-3" class="anchor"></span>

### mri_robust_register

<span id="line-4" class="anchor"></span>

[mri_robust_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_robust_register):
2 inputs, rigid/affine, same or cross-modality, unbiased
<span id="line-5" class="anchor"></span><span id="line-6"
class="anchor"></span>

A tool for pairwise image registration. Originally designed for highly
accurate same modality and same subject registration (across time). It
can compute rigid or affine transforms. It is robust with respect to
outlier/anatomy change (removing their influence in the registration)
and is inverse consistent (symmetric). <span id="line-7"
class="anchor"></span>More recent versions (dev) are capable of
registering across modality in a symmetric fashion. <span id="line-8"
class="anchor"></span>robust_register is also used to register histology
scans (part to whole hemisphere), etc. <span id="line-9"
class="anchor"></span><span id="line-10" class="anchor"></span>

### mri_robust_template

<span id="line-11" class="anchor"></span>

[mri_robust_template](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_robust_template):
n inputs, rigid/affine, same-modality, unbiased <span id="line-12"
class="anchor"></span><span id="line-13" class="anchor"></span>

A tool to register several inputs (same modality) to an unbiased average
template, that it creates at the same time. Registration can be rigid or
affine. Inputs are usually of the same subject, e.g. at different times.
robust_template is based on robust_register and inherits the robustness
to outlier. It is used in recon-all in the motion correction step (to
co-register several within session scans to create one higher SNR input)
and for longitudinal processing to create the unbiased average template.
<span id="line-14" class="anchor"></span><span id="line-15"
class="anchor"></span>

### bbregister

<span id="line-16" class="anchor"></span>

[bbregister](https://surfer.nmr.mgh.harvard.edu/fswiki/bbregister): 2
inputs, rigid, cross-modality, needs surfaces <span id="line-17"
class="anchor"></span><span id="line-18" class="anchor"></span>

This program performs within-subject, cross-modal registration using a
<span id="line-19" class="anchor"></span>boundary-based cost function.
The registration is can be 6, 9, or 12 DOF <span id="line-20"
class="anchor"></span>DOF (rigid-to-affine). It is required that you
have an anatomical scan of the <span id="line-21"
class="anchor"></span>subject that has been processed in Freesurfer.
<span id="line-22" class="anchor"></span><span id="line-23"
class="anchor"></span>

### mri_cvs_register

<span id="line-24" class="anchor"></span>

[mri_cvs_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_cvs_register):
2 inputs, non-linear, same-modality, needs surfaces <span id="line-25"
class="anchor"></span><span id="line-26" class="anchor"></span>

This program performs subject-to-subject or subject-to-atlas non-linear
volume <span id="line-27" class="anchor"></span>registration using a
combined volumetric and surface-based (CVS) <span id="line-28"
class="anchor"></span>registration algorithm. It is required that you
have an anatomical scan of the <span id="line-29"
class="anchor"></span>subject that has been processed in Freesurfer!
<span id="line-30" class="anchor"></span><span id="line-31"
class="anchor"></span>

### mri_em_register

<span id="line-32" class="anchor"></span>

[mri_em_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_em_register):
2 inputs, linear, atlas registration <span id="line-33"
class="anchor"></span><span id="line-34" class="anchor"></span>

This generates a linear talairach transform (lta file) from T1
anatomical to gca file (probabilistic atals). It is used in recon-all to
create transforms/talairach.lta . <span id="line-35"
class="anchor"></span><span id="line-36"
class="anchor"></span><span id="line-37" class="anchor"></span>

### mri_ca_register

<span id="line-38" class="anchor"></span>

[mri_ca_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_ca_register):
2 inputs, non-linear, atlas registration <span id="line-39"
class="anchor"></span><span id="line-40" class="anchor"></span>

This generates a multi-dimensional talairach transform from T1
anatomical to a gca file (probabilistic atals) using a linear talairach
(registration) file as initialization. It is used in recon-all to create
transforms/talairach.m3z . <span id="line-41"
class="anchor"></span><span id="line-42" class="anchor"></span>

### other registration tools

<span id="line-43" class="anchor"></span><span id="line-44"
class="anchor"></span>

- <a href="https://surfer.nmr.mgh.harvard.edu/fswiki/tkregister"
  class="nonexistent">tkregister</a> - graphical tool to manually
  register two images <span id="line-45" class="anchor"></span>

- [FreeView](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeviewGuide) -
  graphical viewer that can also do simple rotations, cropping
  <span id="line-46" class="anchor"></span>

- [regdat2xfm](https://surfer.nmr.mgh.harvard.edu/fswiki/regdat2xfm)
  <span id="line-47" class="anchor"></span><span id="line-48"
  class="anchor"></span>

### deprecated

<span id="line-49" class="anchor"></span><span id="line-50"
class="anchor"></span>

- [mri_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_register)
  <span id="line-51" class="anchor"></span>

- [mri_rigid_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_rigid_register)
  <span id="line-52" class="anchor"></span>

- [mri_linear_register](https://surfer.nmr.mgh.harvard.edu/fswiki/mri_linear_register)
  <span id="line-53" class="anchor"></span>

- [orient_mri](https://surfer.nmr.mgh.harvard.edu/fswiki/orient_mri) -
  graphically and interactively re-orient an MRI volume and save the new
  transform <span id="line-54" class="anchor"></span>

<span id="bottom" class="anchor"></span>

</div>

FreeSurferCommandsRegistration (last edited 2011-09-19 15:16:54 by
<span title="MartinReuter @ riemann.nmr.mgh.harvard.edu[132.183.139.80]">[MartinReuter](https://surfer.nmr.mgh.harvard.edu/fswiki/MartinReuter "MartinReuter @ riemann.nmr.mgh.harvard.edu[132.183.139.80]")</span>)

<div id="pagebottom">

</div>

</div>

<div id="footer">

- <span class="disabled">Immutable Page</span>

- <a href="FreeSurferCommandsRegistration.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferCommandsRegistration?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferCommandsRegistration?action=AttachFile"
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

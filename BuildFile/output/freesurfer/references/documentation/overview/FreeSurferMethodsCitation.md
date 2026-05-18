<div id="header">

<div id="logo">

[![FreeSurfer](https://surfer.nmr.mgh.harvard.edu/wiki/fswiki_htdocs/common/fslogosmall.png)](FreeSurferWiki.html)

</div>

<div>

Search:

</div>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferMethodsCitation?action=login"
  id="login" rel="nofollow">Login</a>

<div id="locationline">

- [FreeSurferMethodsCitation](FreeSurferMethodsCitation.html)

</div>

- [FreeSurferWiki](FreeSurferWiki.html)
- [RecentChanges](https://surfer.nmr.mgh.harvard.edu/fswiki/RecentChanges)
- [FindPage](https://surfer.nmr.mgh.harvard.edu/fswiki/FindPage)
- [HelpContents](https://surfer.nmr.mgh.harvard.edu/fswiki/HelpContents)
- [FreeSurferMethodsCitation](FreeSurferMethodsCitation.html)

<div id="pageline">

------------------------------------------------------------------------

</div>

- <span class="disabled">Immutable Page</span>

- <a href="FreeSurferMethodsCitation.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferMethodsCitation?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferMethodsCitation?action=AttachFile"
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
class="anchor"></span><span id="line-2"
class="anchor"></span><span id="line-3"
class="anchor"></span><span id="line-4" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-5" class="anchor"></span><span id="line-6"
class="anchor"></span><span id="line-7" class="anchor"></span>

Cortical reconstruction and volumetric segmentation was performed with
the Freesurfer image analysis suite, which is documented and freely
available for download online
(<a href="http://surfer.nmr.mgh.harvard.edu/"
class="http">http://surfer.nmr.mgh.harvard.edu/</a>). The technical
details of these procedures are described in prior publications (Dale et
al., 1999; Dale and Sereno, 1993; Fischl and Dale, 2000; Fischl et al.,
2001; Fischl et al., 2002; Fischl et al., 2004a; Fischl et al., 1999a;
Fischl et al., 1999b; Fischl et al., 2004b; Han et al., 2006; Jovicich
et al., 2006; Segonne et al., 2004, Reuter et al. 2010, Reuter et al.
2012). Briefly, this processing includes motion correction and averaging
(Reuter et al. 2010) of multiple volumetric T1 weighted images (when
more than one is available), removal of non-brain tissue using a hybrid
watershed/surface deformation procedure (Segonne et al., 2004),
automated Talairach transformation, segmentation of the subcortical
white matter and deep gray matter volumetric structures (including
hippocampus, amygdala, caudate, putamen, ventricles) (Fischl et al.,
2002; Fischl et al., 2004a) intensity normalization (Sled et al., 1998),
tessellation of the gray matter white matter boundary, automated
topology correction (Fischl et al., 2001; Segonne et al., 2007), and
surface deformation following intensity gradients to optimally place the
gray/white and gray/cerebrospinal fluid borders at the location where
the greatest shift in intensity defines the transition to the other
tissue class (Dale et al., 1999; Dale and Sereno, 1993; Fischl and Dale,
2000). Once the cortical models are complete, a number of deformable
procedures can be performed for further data processing and analysis
including surface inflation (Fischl et al., 1999a), registration to a
spherical atlas which is based on individual cortical folding patterns
to match cortical geometry across subjects (Fischl et al., 1999b),
parcellation of the cerebral cortex into units with respect to gyral and
sulcal structure (Desikan et al., 2006; Fischl et al., 2004b), and
creation of a variety of surface based data including maps of curvature
and sulcal depth. This method uses both intensity and continuity
information from the entire three dimensional MR volume in segmentation
and deformation procedures to produce representations of cortical
thickness, calculated as the closest distance from the gray/white
boundary to the gray/CSF boundary at each vertex on the tessellated
surface (Fischl and Dale, 2000). The maps are created using spatial
intensity gradients across tissue classes and are therefore not simply
reliant on absolute signal intensity. The maps produced are not
restricted to the voxel resolution of the original data thus are capable
of detecting submillimeter differences between groups. Procedures for
the measurement of cortical thickness have been validated against
histological analysis (Rosas et al., 2002) and manual measurements
(Kuperberg et al., 2003; Salat et al., 2004). Freesurfer morphometric
procedures have been demonstrated to show good test-retest reliability
across scanner manufacturers and across field strengths (Han et al.,
2006; Reuter et al., 2012). <span id="line-8"
class="anchor"></span><span id="line-9" class="anchor"></span>

**Aseg Atlas Information**\
<span id="line-10" class="anchor"></span>The aseg atlas is built from 40
subjects acquired using the same mp-rage sequence (by people at Wash U
ages ago in collaboration with Randy Buckner). The subjects that make up
the atlas are distributed in 4 groups of 10 subjects each: (1) young,
(2) middle aged, (3) healthy older adults, (4) older adults with AD.
<span id="line-11" class="anchor"></span><span id="line-12"
class="anchor"></span>

**Longitudinal Processing**\
<span id="line-13" class="anchor"></span>To extract reliable volume and
thickness estimates, images where automatically processed with the
longitudinal stream (Reuter et al., 2012) in FreeSurfer. Specifically an
unbiased within-subject template space and image is created using
robust, inverse consistent registration (Reuter et al., 2010). Several
processing steps, such as skull stripping, Talairach transforms, atlas
registration as well as spherical surface maps and parcellations are
then initialized with common information from the within-subject
template, significantly increasing reliability and statistical power
(Reuter et al., 2012).\
<span id="line-14" class="anchor"></span>**Please cite at least (Reuter
et al., 2012) if the longitudinal stream was used!** <span id="line-15"
class="anchor"></span><span id="line-16" class="anchor"></span>

**REFERENCES** <span id="line-17"
class="anchor"></span><span id="line-18" class="anchor"></span>

Dale, A.M., Fischl, B., Sereno, M.I., 1999. Cortical surface-based
analysis. I. Segmentation and surface reconstruction. Neuroimage 9,
179-194. <span id="line-19" class="anchor"></span><span id="line-20"
class="anchor"></span>

Dale, A.M., Sereno, M.I., 1993. Improved localization of cortical
activity by combining EEG and MEG with MRI cortical surface
reconstruction: a linear approach. J Cogn Neurosci 5, 162-176.
<span id="line-21" class="anchor"></span><span id="line-22"
class="anchor"></span>

Desikan, R.S., Segonne, F., Fischl, B., Quinn, B.T., Dickerson, B.C.,
Blacker, D., Buckner, R.L., Dale, A.M., Maguire, R.P., Hyman, B.T.,
Albert, M.S., Killiany, R.J., 2006. An automated labeling system for
subdividing the human cerebral cortex on MRI scans into gyral based
regions of interest. Neuroimage 31, 968-980. <span id="line-23"
class="anchor"></span><span id="line-24" class="anchor"></span>

Fischl, B., Dale, A.M., 2000. Measuring the thickness of the human
cerebral cortex from magnetic resonance images. Proc Natl Acad Sci U S A
97, 11050-11055. <span id="line-25"
class="anchor"></span><span id="line-26" class="anchor"></span>

Fischl, B., Liu, A., Dale, A.M., 2001. Automated manifold surgery:
constructing geometrically accurate and topologically correct models of
the human cerebral cortex. IEEE Trans Med Imaging 20, 70-80.
<span id="line-27" class="anchor"></span><span id="line-28"
class="anchor"></span>

Fischl, B., Salat, D.H., Busa, E., Albert, M., Dieterich, M.,
Haselgrove, C., van der Kouwe, A., Killiany, R., Kennedy, D., Klaveness,
S., Montillo, A., Makris, N., Rosen, B., Dale, A.M., 2002. Whole brain
segmentation: automated labeling of neuroanatomical structures in the
human brain. Neuron 33, 341-355. <span id="line-29"
class="anchor"></span><span id="line-30" class="anchor"></span>

Fischl, B., Salat, D.H., van der Kouwe, A.J., Makris, N., Segonne, F.,
Quinn, B.T., Dale, A.M., 2004a. Sequence-independent segmentation of
magnetic resonance images. Neuroimage 23 Suppl 1, S69-84.
<span id="line-31" class="anchor"></span><span id="line-32"
class="anchor"></span>

Fischl, B., Sereno, M.I., Dale, A.M., 1999a. Cortical surface-based
analysis. II: Inflation, flattening, and a surface-based coordinate
system. Neuroimage 9, 195-207. <span id="line-33"
class="anchor"></span><span id="line-34" class="anchor"></span>

Fischl, B., Sereno, M.I., Tootell, R.B., Dale, A.M., 1999b.
High-resolution intersubject averaging and a coordinate system for the
cortical surface. Hum Brain Mapp 8, 272-284. <span id="line-35"
class="anchor"></span><span id="line-36" class="anchor"></span>

Fischl, B., van der Kouwe, A., Destrieux, C., Halgren, E., Segonne, F.,
Salat, D.H., Busa, E., Seidman, L.J., Goldstein, J., Kennedy, D.,
Caviness, V., Makris, N., Rosen, B., Dale, A.M., 2004b. Automatically
parcellating the human cerebral cortex. Cereb Cortex 14, 11-22.
<span id="line-37" class="anchor"></span><span id="line-38"
class="anchor"></span>

Han, X., Jovicich, J., Salat, D., van der Kouwe, A., Quinn, B., Czanner,
S., Busa, E., Pacheco, J., Albert, M., Killiany, R., Maguire, P., Rosas,
D., Makris, N., Dale, A., Dickerson, B., Fischl, B., 2006. Reliability
of MRI-derived measurements of human cerebral cortical thickness: the
effects of field strength, scanner upgrade and manufacturer. Neuroimage
32, 180-194. <span id="line-39" class="anchor"></span><span id="line-40"
class="anchor"></span>

Jovicich, J., Czanner, S., Greve, D., Haley, E., van der Kouwe, A.,
Gollub, R., Kennedy, D., Schmitt, F., Brown, G., Macfall, J., Fischl,
B., Dale, A., 2006. Reliability in multi-site structural MRI studies:
effects of gradient non-linearity correction on phantom and human data.
Neuroimage 30, 436-443. <span id="line-41"
class="anchor"></span><span id="line-42" class="anchor"></span>

Kuperberg, G.R., Broome, M.R.,
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/McGuire"
class="nonexistent">McGuire</a>, P.K., David, A.S., Eddy, M., Ozawa, F.,
Goff, D., West, W.C., Williams, S.C., van der Kouwe, A.J., Salat, D.H.,
Dale, A.M., Fischl, B., 2003. Regionally localized thinning of the
cerebral cortex in schizophrenia. Arch Gen Psychiatry 60, 878-888.
<span id="line-43" class="anchor"></span><span id="line-44"
class="anchor"></span>

Reuter, M., Schmansky, N.J., Rosas, H.D., Fischl, B. 2012.
Within-Subject Template Estimation for Unbiased Longitudinal Image
Analysis. Neuroimage 61 (4), 1402-1418. <span id="line-45"
class="anchor"></span><a href="http://reuter.mit.edu/papers/reuter-long12.pdf"
class="http">http://reuter.mit.edu/papers/reuter-long12.pdf</a>
<span id="line-46" class="anchor"></span><span id="line-47"
class="anchor"></span>

Reuter, M., Fischl, B., 2011. Avoiding asymmetry-induced bias in
longitudinal image processing. Neuroimage 57 (1), 19-21.
<span id="line-48"
class="anchor"></span><a href="http://reuter.mit.edu/papers/reuter-bias11.pdf"
class="http">http://reuter.mit.edu/papers/reuter-bias11.pdf</a>
<span id="line-49" class="anchor"></span><span id="line-50"
class="anchor"></span>

Reuter, M., Rosas, H.D., Fischl, B., 2010. Highly Accurate Inverse
Consistent Registration: A Robust Approach. Neuroimage 53 (4),
1181–1196. <span id="line-51"
class="anchor"></span><a href="http://reuter.mit.edu/papers/reuter-robreg10.pdf"
class="http">http://reuter.mit.edu/papers/reuter-robreg10.pdf</a>
<span id="line-52" class="anchor"></span><span id="line-53"
class="anchor"></span>

Rosas, H.D., Liu, A.K., Hersch, S., Glessner, M., Ferrante, R.J., Salat,
D.H., van der Kouwe, A., Jenkins, B.G., Dale, A.M., Fischl, B., 2002.
Regional and progressive thinning of the cortical ribbon in Huntington's
disease. Neurology 58, 695-701. <span id="line-54"
class="anchor"></span><span id="line-55" class="anchor"></span>

Salat, D.H., Buckner, R.L., Snyder, A.Z., Greve, D.N., Desikan, R.S.,
Busa, E., Morris, J.C., Dale, A.M., Fischl, B., 2004. Thinning of the
cerebral cortex in aging. Cereb Cortex 14, 721-730. <span id="line-56"
class="anchor"></span><span id="line-57" class="anchor"></span>

Segonne, F., Dale, A.M., Busa, E., Glessner, M., Salat, D., Hahn, H.K.,
Fischl, B., 2004. A hybrid approach to the skull stripping problem in
MRI. Neuroimage 22, 1060-1075. <span id="line-58"
class="anchor"></span><span id="line-59" class="anchor"></span>

Segonne, F., Pacheco, J., Fischl, B., 2007. Geometrically accurate
topology-correction of cortical surfaces using nonseparating loops. IEEE
Trans Med Imaging 26, 518-529. <span id="line-60"
class="anchor"></span><span id="line-61" class="anchor"></span>

Sled, J.G., Zijdenbos, A.P., Evans, A.C., 1998. A nonparametric method
for automatic correction of intensity nonuniformity in MRI data. IEEE
Trans Med Imaging 17, 87-97. <span id="line-62"
class="anchor"></span><span id="line-63"
class="anchor"></span><span id="line-64" class="anchor"></span>

**BibTeX** <span id="line-65" class="anchor"></span><span id="line-66"
class="anchor"></span>

This list of citations is available in the attached BibTeX file <a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferMethodsCitation?action=AttachFile&amp;do=view&amp;target=neuro.bib"
class="attachment" title="neuro.bib">neuro.bib</a> <span id="line-67"
class="anchor"></span><span id="line-68" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-69" class="anchor"></span><span id="bottom"
class="anchor"></span>

</div>

FreeSurferMethodsCitation (last edited 2021-01-19 18:49:50 by
<span title="DevaniCordero @ 152.79.98.1[152.79.98.1]"><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/DevaniCordero"
class="nonexistent"
title="DevaniCordero @ 152.79.98.1[152.79.98.1]">DevaniCordero</a></span>)

<div id="pagebottom">

</div>

</div>

<div id="footer">

- <span class="disabled">Immutable Page</span>

- <a href="FreeSurferMethodsCitation.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferMethodsCitation?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferMethodsCitation?action=AttachFile"
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

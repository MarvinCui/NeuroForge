<div id="header">

<div id="logo">

[![FreeSurfer](https://surfer.nmr.mgh.harvard.edu/wiki/fswiki_htdocs/common/fslogosmall.png)](FreeSurferWiki.html)

</div>

<div>

Search:

</div>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=login"
  id="login" rel="nofollow">Login</a>

<div id="locationline">

- [CoordinateSystems](CoordinateSystems.html)

</div>

- [FreeSurferWiki](FreeSurferWiki.html)
- [RecentChanges](https://surfer.nmr.mgh.harvard.edu/fswiki/RecentChanges)
- [FindPage](https://surfer.nmr.mgh.harvard.edu/fswiki/FindPage)
- [HelpContents](https://surfer.nmr.mgh.harvard.edu/fswiki/HelpContents)
- [CoordinateSystems](CoordinateSystems.html)

<div id="pageline">

------------------------------------------------------------------------

</div>

- <span class="disabled">Immutable Page</span>

- <a href="CoordinateSystems.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=AttachFile"
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

[top](FreeSurferWiki.html) <span id="line-2"
class="anchor"></span><span id="line-3" class="anchor"></span>

# FreeSurfer Coordinate Systems

<span id="line-4" class="anchor"></span><span id="line-5"
class="anchor"></span>

The "official"
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer)
Coordinate definitions can be found in the following power-points slides
(**SEE THESE FIRST**): <span id="line-6"
class="anchor"></span><span id="line-7" class="anchor"></span>

- **<a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=AttachFile&amp;do=get&amp;target=fscoordinates.ppt"
  class="attachment" title="FS Coordinates (PowerPoint)">FS Coordinates
  (PowerPoint)</a>** <span id="line-8"
  class="anchor"></span><span id="line-9" class="anchor"></span>

or PDF: <span id="line-10" class="anchor"></span><span id="line-11"
class="anchor"></span>

- **<a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=AttachFile&amp;do=get&amp;target=fscoordinates.pdf"
  class="attachment" title="FS Coordinates (PDF)">FS Coordinates (PDF)</a>**
  <span id="line-12" class="anchor"></span><span id="line-13"
  class="anchor"></span>

This also includes a little intro to Affine Transformations.
<span id="line-14" class="anchor"></span><span id="line-15"
class="anchor"></span>

See also: **<a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=AttachFile&amp;do=get&amp;target=vox2ras.pdf"
class="attachment" title="VOX2RAS(PDF)">VOX2RAS(PDF)</a>**
<span id="line-16" class="anchor"></span><span id="line-17"
class="anchor"></span>

## Transformations between Freesurfer Surfaces and TrackVis

<span id="line-18" class="anchor"></span>

- [FreeSurferTrackVisTransforms](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferTrackVisTransforms)
  <span id="line-19" class="anchor"></span>

**Also see:** <a
href="http://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferTrackVisTransforms"
class="http">TrackVis Transforms</a> **\<--- !!!** <span id="line-20"
class="anchor"></span><span id="line-21" class="anchor"></span>

## Matlab

<span id="line-22" class="anchor"></span>

You can load an MRI volume into matlab with <span id="line-23"
class="anchor"></span><span id="line-24" class="anchor"></span>

mri = MRIread('file.mgz'); % Can also read mgh, nii, nii.gz, img
<span id="line-25" class="anchor"></span><span id="line-26"
class="anchor"></span>

The mri structure will have several elements, including a 'vol' where
<span id="line-27" class="anchor"></span>the pixel data will be. The
voxel indices of the resulting volume <span id="line-28"
class="anchor"></span>will relate to the
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) voxel
indices in freeview/tkmedit like: <span id="line-29"
class="anchor"></span><span id="line-30" class="anchor"></span>

mri.vol(FSrow+1, FScol+1, FSslice+1) = mri(FScol,FSrow,FSslice)
<span id="line-31" class="anchor"></span><span id="line-32"
class="anchor"></span>

The mri.vox2ras matrix uses FS indices, ie, <span id="line-33"
class="anchor"></span>RAS = mri.vox2ras\*\[FScol FSrow FSslice 1\]'
<span id="line-34" class="anchor"></span><span id="line-35"
class="anchor"></span><span id="line-36" class="anchor"></span>

## Use Cases

<span id="line-37" class="anchor"></span><span id="line-38"
class="anchor"></span>

Below are several cases in which someone has a coordinate in one
coordinate system and wants to transform it to some other coordinate
system (eg, a point on the surface to MNI305 space). Each computation
shows the matrices needed and how to get them as well as a check using
tkmedit/tksurfer. The equations are based on those in **<a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=AttachFile&amp;do=get&amp;target=fscoordinates.ppt"
class="attachment" title="FS Coordinates (PowerPoint)">FS Coordinates
(PowerPoint)</a>**. CRS is column-row-slice. RAS is
right-anterior-superior. <span id="line-39"
class="anchor"></span><span id="line-40" class="anchor"></span>

The checks assume you have run tkmedit and tksurfer in the following
way: <span id="line-41" class="anchor"></span><span id="line-42"
class="anchor"></span>

tkmedit subject orig.mgz -reg register.dat -ov mov.nii -surfs
<span id="line-43" class="anchor"></span><span id="line-44"
class="anchor"></span>

tksurfer subject lh inflated -reg register.dat -ov mov.nii
<span id="line-45" class="anchor"></span><span id="line-46"
class="anchor"></span>

Note on Talairach:
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) does
not report true "Talairach" coordinates. The coordinates listed unter
"Talairach" are actually based on Matthew Brett's 10/8/98 non-linear
transform from MNI305 space (see
<a href="http://www.mrc-cbu.cam.ac.uk/Imaging/mnispace.html"
class="http">http://www.mrc-cbu.cam.ac.uk/Imaging/mnispace.html</a>).
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) also
reports "Talairach MNI" coordinates. These are MNI305 space.
<span id="line-47" class="anchor"></span><span id="line-48"
class="anchor"></span><span id="line-49" class="anchor"></span>

## Transforms within a subject's anatomical space

<span id="line-50" class="anchor"></span><span id="line-51"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-52" class="anchor"></span>1. I have a point on the
surface and want to compute the CRS for <span id="line-53"
class="anchor"></span>voxel in the orig.mgz that corresponds to this
point: <span id="line-54" class="anchor"></span><span id="line-55"
class="anchor"></span>

VoxCRS = inv(Torig)\*\[tkrR tkrA tkrS 1\]' <span id="line-56"
class="anchor"></span><span id="line-57" class="anchor"></span>

where \[tkrR tkrA tkrS\] is the "Vertex RAS" as seen in the tksurfer
<span id="line-58" class="anchor"></span>Tools window (also output of
mris_convert). Torig is the Vox2tkrRAS <span id="line-59"
class="anchor"></span>matrix obtained from "mri_info --vox2ras-tkr
orig.mgz" (note: this is <span id="line-60" class="anchor"></span>the
same for all orig volumes). <span id="line-61"
class="anchor"></span><span id="line-62" class="anchor"></span>

Test: click on a point in tksurfer. Use "Vertex RAS" to compute
<span id="line-63" class="anchor"></span>Vox2CRS. Round Vox2CRS to the
nearest integer. Hit Save Point in <span id="line-64"
class="anchor"></span>tksurfer. In tkmedit, Goto Saved Point. Compare
VoxCRS to "Volume <span id="line-65" class="anchor"></span>Index". Note:
you may need to use the "Volume RAS" from tkmedit in the
<span id="line-66" class="anchor"></span>computation above to get an
exact match. <span id="line-67" class="anchor"></span><span id="line-68"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-69" class="anchor"></span>2. I have an RAS point on the
surface (tkrR tkrA tkrS) ("Vertex RAS" from <span id="line-70"
class="anchor"></span>tksurfer) and want to compute the MNI305 RAS that
corresponds to this <span id="line-71" class="anchor"></span>point:
<span id="line-72" class="anchor"></span><span id="line-73"
class="anchor"></span>

MNI305RAS = TalXFM\*Norig\*inv(Torig)\*\[tkrR tkrA tkrS 1\]'
<span id="line-74" class="anchor"></span>

- TalXFM: subject/orig/transforms/talairach.xfm <span id="line-75"
  class="anchor"></span>Norig: mri_info --vox2ras orig.mgz
  <span id="line-76" class="anchor"></span>Torig: mri_info --vox2ras-tkr
  orig.mgz <span id="line-77" class="anchor"></span><span id="line-78"
  class="anchor"></span>

Test: click on a point in tksurfer. Use "Vertex RAS" to compute
<span id="line-79" class="anchor"></span>MNI305RAS. Compare MNI305RAS to
"Vertex MNI Talairach". Also, hit Save <span id="line-80"
class="anchor"></span>Point in tksurfer. In tkmedit, Goto Saved Point,
compare MNI305RAS to <span id="line-81" class="anchor"></span>"MNI
Coordinates". Note: you may need to use the "Volume RAS" from
<span id="line-82" class="anchor"></span>tkmedit in the computation
above to get an exact match. <span id="line-83"
class="anchor"></span><span id="line-84" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-85" class="anchor"></span>3. I have a point on the
surface ("Vertex RAS" in tksurfer) and want to <span id="line-86"
class="anchor"></span>compute the Scanner RAS in orig.mgz that
corresponds to this point: <span id="line-87"
class="anchor"></span><span id="line-88" class="anchor"></span>

ScannerRAS = Norig\*inv(Torig)\*\[tkrR tkrA tkrS 1\]' <span id="line-89"
class="anchor"></span>

- Norig: mri_info --vox2ras orig.mgz <span id="line-90"
  class="anchor"></span>Torig: mri_info --vox2ras-tkr orig.mgz
  <span id="line-91" class="anchor"></span><span id="line-92"
  class="anchor"></span>

Test: click on a point in tksurfer. Use "Vertex RAS" to compute
<span id="line-93" class="anchor"></span>ScannerRAS. Save Point. In
tkmedit, Goto Saved Point, compare <span id="line-94"
class="anchor"></span>ScannerRAS to "Volume Scanner Coordinates".
<span id="line-95" class="anchor"></span><span id="line-96"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-97" class="anchor"></span>4. I have a CRS from a voxel in
the orig.mgz volume and want to <span id="line-98"
class="anchor"></span>compute the RAS in surface space (tkrRAS) for this
point: <span id="line-99" class="anchor"></span><span id="line-100"
class="anchor"></span>

tkrRAS = Torig\*\[C R S 1\]' <span id="line-101" class="anchor"></span>

- Torig: mri_info --vox2ras-tkr orig.mgz <span id="line-102"
  class="anchor"></span><span id="line-103" class="anchor"></span>

Test: click on a point in tkmedit very close to the left hemi white
<span id="line-104" class="anchor"></span>surface. Use the "Volume
index" to compute tkrRAS. Hit "Save Point" in <span id="line-105"
class="anchor"></span>tkmedit. In tksurfer, Goto Saved Point. Compare
tkrRAS to "Vertex <span id="line-106" class="anchor"></span>RAS". It
might not be exactly the same because you might not have
<span id="line-107" class="anchor"></span>clicked exactly on a vertex in
tkmedit. <span id="line-108" class="anchor"></span><span id="line-109"
class="anchor"></span>

## Transforms within subject across imaging modalities

<span id="line-110" class="anchor"></span><span id="line-111"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-112" class="anchor"></span>5. I have a point on the
surface ("Vertex RAS") and want to compute the CRS for the
<span id="line-113" class="anchor"></span>corresponding voxel in my
functional/diffusion/ASL/rawavg/etc "mov" <span id="line-114"
class="anchor"></span>volume: <span id="line-115"
class="anchor"></span><span id="line-116" class="anchor"></span>

movCRS = inv(Tmov)\*Reg\*\[tkrR tkrA tkrS 1\]' <span id="line-117"
class="anchor"></span>

- Tmov: mri_info --vox2ras-tkr mov.nii <span id="line-118"
  class="anchor"></span>Reg: register.dat <span id="line-119"
  class="anchor"></span>
  - tkregister2 --mov mov.nii --reg register.dat <span id="line-120"
    class="anchor"></span><span id="line-121" class="anchor"></span>

Test: click on a point in tksurfer and hit Save Point. Compute movCRS
<span id="line-122" class="anchor"></span>using the "Vertex RAS". Round
movCRS to the nearest integer. In <span id="line-123"
class="anchor"></span>tkmedit, Goto Saved Point. Compare movCRS to
"Functional Overlay <span id="line-124" class="anchor"></span>Index
Coordinates". <span id="line-125"
class="anchor"></span><span id="line-126" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-127" class="anchor"></span>6. I have a CRS from a voxel
in my functional/diffusion/ASL/rawavg/etc <span id="line-128"
class="anchor"></span>"mov" volume and want to compute the CRS for the
corresponding point in <span id="line-129" class="anchor"></span>the
orig.mgz: <span id="line-130" class="anchor"></span><span id="line-131"
class="anchor"></span>

origCRS = inv(Torig) \* Reg \* Tmov \* \[movC movR movS 1\]'
<span id="line-132" class="anchor"></span>

- Torig: mri_info --vox2ras-tkr orig.mgz <span id="line-133"
  class="anchor"></span>Tmov: mri_info --vox2ras-tkr mov.nii
  <span id="line-134" class="anchor"></span>Reg: register.dat
  <span id="line-135" class="anchor"></span>
  - tkregister2 --mov mov.nii --reg register.dat <span id="line-136"
    class="anchor"></span><span id="line-137" class="anchor"></span>

Test: click on a point in tkmedit very close to the left hemi white
<span id="line-138" class="anchor"></span>surface. Use the "Functional
Overlay Index Coordinates" to compute <span id="line-139"
class="anchor"></span>origCRS (round to the nearest integer). Compare
origCRS to the "Volume <span id="line-140" class="anchor"></span>index".
Note: you may need to use the "Volume RAS" from tkmedit in
<span id="line-141" class="anchor"></span>the computation above to get
an exact match. <span id="line-142"
class="anchor"></span><span id="line-143" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-144" class="anchor"></span>7. I have a CRS from a voxel
in my functional/diffusion/ASL/rawavg/etc <span id="line-145"
class="anchor"></span>"mov" volume and want to compute the tkrRAS for
the corresponding <span id="line-146" class="anchor"></span>point on the
surface: <span id="line-147" class="anchor"></span><span id="line-148"
class="anchor"></span>

tkrRAS = inv(Reg) \* Tmov \* \[movC movR movS 1\]' <span id="line-149"
class="anchor"></span>

- Tmov: mri_info --vox2ras-tkr mov.nii <span id="line-150"
  class="anchor"></span>Reg: register.dat <span id="line-151"
  class="anchor"></span>
  - tkregister2 --mov mov.nii --reg register.dat <span id="line-152"
    class="anchor"></span><span id="line-153" class="anchor"></span>

Test: click on a point in tkmedit very close to the left hemi white
<span id="line-154" class="anchor"></span>surface. Use the "Functional
Overlay Index Coordinates" to compute <span id="line-155"
class="anchor"></span>tkrRAS. Hit "Save Point" in tkmedit. In tksurfer,
hit "Goto Saveed <span id="line-156" class="anchor"></span>Point".
Compare tkrRAS to "Vertex RAS". It might not be exactly the
<span id="line-157" class="anchor"></span>same because you might not
have clicked exactly on a vertex in <span id="line-158"
class="anchor"></span>tkmedit. <span id="line-159"
class="anchor"></span><span id="line-160" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-161" class="anchor"></span>8. I have an RAS from a voxel
in MNI305 space (fsaverage space) which <span id="line-162"
class="anchor"></span>I want to convert to MNI152 space. Create a vector
of the MNI305 space <span id="line-163" class="anchor"></span>point like
v = \[R A S 1\]'. Multiply this vector by the matrix below
<span id="line-164" class="anchor"></span>(ie, M\*v) <span id="line-165"
class="anchor"></span><span id="line-166"
class="anchor"></span><span id="line-167"
class="anchor"></span><span id="line-168"
class="anchor"></span><span id="line-169" class="anchor"></span>

        0.9975   -0.0073    0.0176   -0.0429
        0.0146    1.0009   -0.0024    1.5496
       -0.0130   -0.0093    0.9971    1.1840

<span id="line-170" class="anchor"></span>

Eg, if the RAS point is (10 -20 35), then v = \[10 -20 35 1\]', and M\*v
<span id="line-171" class="anchor"></span>= \[10.695 -18.409 36.137 1\],
so the RAS in MNI152 space would be <span id="line-172"
class="anchor"></span>10.695 -18.409 36.137. <span id="line-173"
class="anchor"></span><span id="line-174" class="anchor"></span>

The above matrix is V152\*inv(T152)\*R\*T305\*inv(V305), where V152 and
<span id="line-175" class="anchor"></span>V305 are the vox2ras matrices
from the 152 and 305 spaces, T152 and <span id="line-176"
class="anchor"></span>T305 are the tkregister-vox2ras matrices from the
152 and 305 spaces, <span id="line-177" class="anchor"></span>and R is
from \$FREESURFER_HOME/average/mni152.register.dat <span id="line-178"
class="anchor"></span><span id="line-179" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-180" class="anchor"></span>8b. I have an RAS from a voxel
in MNI152 space which <span id="line-181" class="anchor"></span>I want
to convert to MNI305 space (fsaverage space). Create a vector of the
MNI152 space <span id="line-182" class="anchor"></span>point like v =
\[R A S 1\]'. Multiply this vector by the matrix below
<span id="line-183" class="anchor"></span>(ie, M\*v) <span id="line-184"
class="anchor"></span><span id="line-185"
class="anchor"></span><span id="line-186"
class="anchor"></span><span id="line-187"
class="anchor"></span><span id="line-188" class="anchor"></span>

        1.0022    0.0071   -0.0177    0.0528
       -0.0146    0.9990    0.0027   -1.5519
        0.0129    0.0094    1.0027   -1.2012

<span id="line-189" class="anchor"></span>

Eg, if the RAS point is (10 -20 35), then v = \[10 -20 35 1\]', and M\*v
<span id="line-190" class="anchor"></span>= \[9.3131 -21.5849 33.8345
1\], so the RAS in MNI305 space would be <span id="line-191"
class="anchor"></span>9.3131 -21.5849 33.8345. <span id="line-192"
class="anchor"></span><span id="line-193" class="anchor"></span>

The above matrix is inv(V152\*inv(T152)\*R\*T305\*inv(V305)), where V152
and <span id="line-194" class="anchor"></span>V305 are the vox2ras
matrices from the 152 and 305 spaces, T152 and <span id="line-195"
class="anchor"></span>T305 are the tkregister-vox2ras matrices from the
152 and 305 spaces, <span id="line-196" class="anchor"></span>and R is
from \$FREESURFER_HOME/average/mni152.register.dat <span id="line-197"
class="anchor"></span><span id="line-198" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-199" class="anchor"></span>9. To convert a volume from
fsaverage to mni152 space, you can use something like
<span id="line-200" class="anchor"></span><span id="line-201"
class="anchor"></span><span id="line-202" class="anchor"></span>

    mri_vol2vol --reg $FREESURFER_HOME/average/mni152.register.dat --mov MNI152.nii.gz --targ orig.mgz --inv --o fsaverage.orig.mni152.mgz

<span id="line-203" class="anchor"></span>

where MNI152.nii.gz is the template volume, either 1mm or 2mm. eg,
\$FSLDIR/data/standard/MNI152_T1_2mm.nii.gz <span id="line-204"
class="anchor"></span><span id="line-205" class="anchor"></span>

To convert a segmentation to mni152, use something like
<span id="line-206" class="anchor"></span><span id="line-207"
class="anchor"></span><span id="line-208" class="anchor"></span>

    mri_label2vol --reg $FREESURFER_HOME/average/mni152.register.dat --seg aparc+aseg.mgz --temp MNI152.nii.gz --o aparc+aseg.mni152.mgz

<span id="line-209" class="anchor"></span><span id="bottom"
class="anchor"></span>

</div>

CoordinateSystems (last edited 2019-07-29 17:18:06 by
<span title="??? @ 172.20.143.167[172.20.143.167]">172</span>)

<div id="pagebottom">

</div>

</div>

<div id="footer">

- <span class="disabled">Immutable Page</span>

- <a href="CoordinateSystems.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems?action=AttachFile"
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

<div id="header">

<div id="logo">

[![FreeSurfer](https://surfer.nmr.mgh.harvard.edu/wiki/fswiki_htdocs/common/fslogosmall.png)](FreeSurferWiki.html)

</div>

<div>

Search:

</div>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall?action=login"
  id="login" rel="nofollow">Login</a>

<div id="locationline">

- [DownloadAndInstall](DownloadAndInstall.html)

</div>

- [FreeSurferWiki](FreeSurferWiki.html)
- [RecentChanges](https://surfer.nmr.mgh.harvard.edu/fswiki/RecentChanges)
- [FindPage](https://surfer.nmr.mgh.harvard.edu/fswiki/FindPage)
- [HelpContents](https://surfer.nmr.mgh.harvard.edu/fswiki/HelpContents)
- [DownloadAndInstall](DownloadAndInstall.html)

<div id="pageline">

------------------------------------------------------------------------

</div>

- <span class="disabled">Immutable Page</span>

- <a href="DownloadAndInstall.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall?action=AttachFile"
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
class="anchor"></span><span id="line-3" class="anchor"></span>

# FreeSurfer Download and Install

<span id="line-4" class="anchor"></span><span id="line-5"
class="anchor"></span>

### Latest Version 7 Release is 7.4.1 (June 2023)

<span id="line-6" class="anchor"></span><span id="line-7"
class="anchor"></span>

Public links to the Freesurfer v7 release downloads and installation
instructions are on the release 7 downloads page
[7.X_releases](https://surfer.nmr.mgh.harvard.edu/fswiki/rel7downloads).
Please note that Linux RPM/DEB and MacOS installer packages are
available. <span id="line-8" class="anchor"></span><span id="line-9"
class="anchor"></span>

If you have not yet upgraded to Freesurfer version 7, you can read about
and compare versions 7 and 6 in the
[ReleaseNotes](https://surfer.nmr.mgh.harvard.edu/fswiki/ReleaseNotes).
<span id="line-10" class="anchor"></span><span id="line-11"
class="anchor"></span>

Martinos users should visit
[InternalFreeSurferDistributions](https://surfer.nmr.mgh.harvard.edu/fswiki/InternalFreeSurferDistributions)
for instructions on how to use pre-installed FreeSurfer distributions.
<span id="line-12" class="anchor"></span><span id="line-13"
class="anchor"></span>

Instructions are available <a
href="https://drive.google.com/file/d/1uNwv29fCeuMHrmTyXw94ZSuroNsPOxu-/view?usp=sharing"
class="https">here</a> about how to setup the 7.4.1 release in a virtual
machine (VM) guest OS (Ubuntu 22) hosted by the open source application
<a href="https://www.virtualbox.org/" class="https">Virtual Box</a> from
Oracle systems. The Virtual Box application runs on most any Windows,
Mac and Linux machine equipped with an Intel processor. As of this
writing, Virtual box does not work on arn64 based machines such as the
silicon macs with M1, M2, M3 processors. For a Windows only VM setup,
see the instructions
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/FS7_wsl_ubuntu"
class="https">here</a> about how to install and run Freesurfer on the
Windows Subsystem for Linux. Please note WSL2 requires an additional
install of a 3rd party X-server on the Windows host in order to view
images in applications such as Freeview (not necessary when running
Virtual Box).\
<span id="line-14" class="anchor"></span><span id="line-15"
class="anchor"></span>

### Previous Version 6 Release (Jan 2017)

<span id="line-16" class="anchor"></span><span id="line-17"
class="anchor"></span>

Freesurfer v6 release downloads and installation instructions are
[here](https://surfer.nmr.mgh.harvard.edu/fswiki/rel6downloads).
<span id="line-18" class="anchor"></span><span id="line-19"
class="anchor"></span>

***Important Note:** When processing a group of subjects for your study,
it is essential to process all your subjects with the same version of
FreeSurfer, on the same OS platform and vendor, and for safety, even the
same version of the OS. While we continue to work to ensure that results
match across platforms, there are none-the-less system-level libraries
that are OS dependent. An exception to this rule is that you may view
and edit files across any platform or version, and run some
post-processing tools (outside the recon-all stream) if you check with
us first (for instance you may run the longitudinal processing with
newer versions).* <span id="line-20"
class="anchor"></span><span id="line-21" class="anchor"></span>

### Other Versions

<span id="line-22" class="anchor"></span><span id="line-23"
class="anchor"></span>

**Development Version:** Daily builds of the FreeSurfer development
branch can be downloaded from
<a href="https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/dev"
class="https">here</a>. <span id="line-24"
class="anchor"></span><span id="line-25" class="anchor"></span>

**Older Releases:** Previous releases of FreeSurfer can be downloaded
from <a href="https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer"
class="https">here</a>. <span id="line-26"
class="anchor"></span><span id="line-27" class="anchor"></span>

**Freeview:** For instructions on how to update Freeview, FreeSurfer's
visualization app, visit the following page: [Updating
Freeview](https://surfer.nmr.mgh.harvard.edu/fswiki/UpdateFreeview).
<span id="line-28" class="anchor"></span><span id="line-29"
class="anchor"></span>

## License

<span id="line-30" class="anchor"></span>

A license key must be obtained to make the FreeSurfer tools operational.
Obtaining a license is free and comes in the form of a license.txt file.
Once you obtain the license.txt key file, copy it to your FreeSurfer
installation directory. This is also the location defined by the
**`FREESURFER_HOME`** environment variable. <span id="line-31"
class="anchor"></span><span id="line-32" class="anchor"></span>

<a href="https://surfer.nmr.mgh.harvard.edu/registration.html"
class="https">Follow this link to obtain a license key.</a>
<span id="line-33" class="anchor"></span><span id="line-34"
class="anchor"></span>

## Additional Resources

<span id="line-35" class="anchor"></span><span id="line-36"
class="anchor"></span>

<a href="Tutorials.html" class="https">Try our tutorials</a>
<span id="line-37" class="anchor"></span><span id="line-38"
class="anchor"></span>

<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/CourseDescription"
class="https">Sign up for a FreeSurfer course</a> <span id="line-39"
class="anchor"></span><span id="line-40" class="anchor"></span>

<a href="FreeSurferSupport.html" class="https">Join the FreeSurfer
mailing list, ask a question, or view the archives</a>
<span id="line-41" class="anchor"></span><span id="line-42"
class="anchor"></span>

<img
src="https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall?action=AttachFile&amp;do=get&amp;target=openneuro_badge.svg"
title="openneuro_badge.svg" class="attachment"
alt="openneuro_badge.svg" /> A free and open platform that can be used
to run FreeSurfer. For more information,
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/OpenNeuro"
class="https">click here</a>. <span id="line-43"
class="anchor"></span><span id="bottom" class="anchor"></span>

</div>

DownloadAndInstall (last edited 2025-08-21 10:57:32 by
<span title="JacksonNolan @ 10.20.34.251[10.20.34.251]"><a href="https://surfer.nmr.mgh.harvard.edu/fswiki/JacksonNolan"
class="nonexistent"
title="JacksonNolan @ 10.20.34.251[10.20.34.251]">JacksonNolan</a></span>)

<div id="pagebottom">

</div>

</div>

<div id="footer">

- <span class="disabled">Immutable Page</span>

- <a href="DownloadAndInstall.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall?action=AttachFile"
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

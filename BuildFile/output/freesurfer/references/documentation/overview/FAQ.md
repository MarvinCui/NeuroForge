<div id="header">

<div id="logo">

[![FreeSurfer](https://surfer.nmr.mgh.harvard.edu/wiki/fswiki_htdocs/common/fslogosmall.png)](../FreeSurferWiki.html)

</div>

<div>

Search:

</div>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions/FAQ?action=login"
  id="login" rel="nofollow">Login</a>

<div id="locationline">

- [UserContributions](https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions)
- [FAQ](FAQ.html)

</div>

- [FreeSurferWiki](../FreeSurferWiki.html)
- [RecentChanges](https://surfer.nmr.mgh.harvard.edu/fswiki/RecentChanges)
- [FindPage](https://surfer.nmr.mgh.harvard.edu/fswiki/FindPage)
- [HelpContents](https://surfer.nmr.mgh.harvard.edu/fswiki/HelpContents)
- [UserContributions/FAQ](FAQ.html)

<div id="pageline">

------------------------------------------------------------------------

</div>

- <span class="disabled">Immutable Page</span>

- <a href="FAQ.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions/FAQ?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions/FAQ?action=AttachFile"
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

[top](https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions)
<span id="line-2" class="anchor"></span><span id="line-3"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-4" class="anchor"></span>

- **FAQ** <span id="line-5" class="anchor"></span><span id="line-6"
  class="anchor"></span>

------------------------------------------------------------------------

<span id="line-7" class="anchor"></span>

- The purpose of this FAQ is to provide a Wiki space where users can add
  the most frequent questions to avoid asking already answered questions
  in the support list. <span id="line-8"
  class="anchor"></span><span id="line-9" class="anchor"></span>

<div class="table-of-contents">

Contents

1.  [General](FAQ.html#General)
    1.  [Q. How can I help this
        FAQ?](FAQ.html#Q._How_can_I_help_this_FAQ.3F)
    2.  [Q. What are the advantages of FreeSurfer over
        VBM?](FAQ.html#Q._What_are_the_advantages_of_FreeSurfer_over_VBM.3F)
    3.  [Q. How do I know the version of FreeSurfer I'm
        running?](FAQ.html#Q._How_do_I_know_the_version_of_FreeSurfer_I.27m_running.3F)
    4.  [Q. Is the FreeSurfer source code
        available?](FAQ.html#Q._Is_the_FreeSurfer_source_code_available.3F)
2.  [Computing](FAQ.html#Computing)
    1.  [Q. How long does it take to finish a
        reconstruction?](FAQ.html#Q._How_long_does_it_take_to_finish_a_reconstruction.3F)
    2.  [Q. How can I reduce the time of recon-all in a group of
        patients?](FAQ.html#Q._How_can_I_reduce_the_time_of_recon-all_in_a_group_of_patients.3F)
    3.  [Q. I want to use freesurfer to quantify cortical thickness, and
        I want to use the software under Linux. What equipment for
        computer do you
        recommend?](FAQ.html#Q._I_want_to_use_freesurfer_to_quantify_cortical_thickness.2C_and_I_want_to_use_the_software_under_Linux._What_equipment_for_computer_do_you_recommend.3F)
    4.  [Q. Is it possible to run FreeSurfer in Ubuntu
        Linux?](FAQ.html#Q._Is_it_possible_to_run_FreeSurfer_in_Ubuntu_Linux.3F)
    5.  [Q. Could I run multiple instances of Freesurfer (on my virtual
        box)?](FAQ.html#Q._Could_I_run_multiple_instances_of_Freesurfer_.28on_my_virtual_box.29.3F)
3.  [Acquisition](FAQ.html#Acquisition)
    1.  [Q. Is it recommended that people use memprage? How are they
        analyzed? Just sqrt sum sqr of the echoes? Or is there something
        more
        elaborate?](FAQ.html#Q._Is_it_recommended_that_people_use_memprage.3F_How_are_they_analyzed.3F_Just_sqrt_sum_sqr_of_the_echoes.3F_Or_is_there_something_more_elaborate.3F)
    2.  [Q. Are there suggested scan sequences which you recommend I use
        with
        Freesurfer?](FAQ.html#Q._Are_there_suggested_scan_sequences_which_you_recommend_I_use_with_Freesurfer.3F)
    3.  [Q. Is it possible to analyze clincial structural MRI exams with
        help of
        Freesurfer?](FAQ.html#Q._Is_it_possible_to_analyze_clincial_structural_MRI_exams_with_help_of_Freesurfer.3F)
4.  [Processing/Re-processing Data in
    FreeSurfer](FAQ.html#Processing.2FRe-processing_Data_in_FreeSurfer)
    1.  [Q. Can I run some cases in my dataset using one version of
        FreeSurfer and others using a different version of
        FreeSurfer?](FAQ.html#Q._Can_I_run_some_cases_in_my_dataset_using_one_version_of_FreeSurfer_and_others_using_a_different_version_of_FreeSurfer.3F)
    2.  [Q. How to run recon-all in a ssh
        terminal](FAQ.html#Q._How_to_run_recon-all_in_a_ssh_terminal)
    3.  [Q. I had a \[Power Outage\|Computer Failure\|Spilled coffee on
        computer\|etc\], how can I resume the
        recon-all?](FAQ.html#Q._I_had_a_.5BPower_Outage.7CComputer_Failure.7CSpilled_coffee_on_computer.7Cetc.5D.2C_how_can_I_resume_the_recon-all.3F)
    4.  [Q. I have a subject which has been running for a really long
        time in recon-all, how can I tell if there is something
        wrong?](FAQ.html#Q._I_have_a_subject_which_has_been_running_for_a_really_long_time_in_recon-all.2C_how_can_I_tell_if_there_is_something_wrong.3F)
    5.  [Q. I have already skull-stripped data. Can I submit it to
        recon-all?](FAQ.html#Q._I_have_already_skull-stripped_data._Can_I_submit_it_to_recon-all.3F)
    6.  [Q. I made white matter and pial edits to my volume. Do I need
        to run -autorecon2-wm and when that is finished run
        -autorecon2-pial?](FAQ.html#Q._I_made_white_matter_and_pial_edits_to_my_volume._Do_I_need_to_run_-autorecon2-wm_and_when_that_is_finished_run_-autorecon2-pial.3F)
    7.  [Q. One of my cases doesn't have the cerebellum so I adjusted
        the watershed threshold to fix it. However, at one threshold,
        the cerebellum is still not included, and at the next the entire
        skull is there. What should I
        do?](FAQ.html#Q._One_of_my_cases_doesn.27t_have_the_cerebellum_so_I_adjusted_the_watershed_threshold_to_fix_it._However.2C_at_one_threshold.2C_the_cerebellum_is_still_not_included.2C_and_at_the_next_the_entire_skull_is_there._What_should_I_do.3F)
    8.  [Q. One or more of the files in a subject's directory was
        accidentally deleted or has become corrupted. How do I recreate
        the missing
        file(s)?](FAQ.html#Q._One_or_more_of_the_files_in_a_subject.27s_directory_was_accidentally_deleted_or_has_become_corrupted.__How_do_I_recreate_the_missing_file.28s.29.3F)
5.  [Common Error messages](FAQ.html#Common_Error_messages)
    1.  [Q. Help! I got this error message: "mri_watershed error: GLOBAL
        region of the brain empty!" - what should I
        do?](FAQ.html#Q._Help.21_I_got_this_error_message:_.22mri_watershed_error:__GLOBAL_region_of_the_brain_empty.21.22_-_what_should_I_do.3F)
    2.  [Q. I get an error message from the Talairach Failure Detection.
        What does this
        mean?](FAQ.html#Q._I_get_an_error_message_from_the_Talairach_Failure_Detection._What_does_this_mean.3F)
    3.  [Q. I get an error during the mri_ca_label step while running
        recon-all. The last thing it says is: "saving intensity scales
        to aseg.auto_noCCseg.label_intensities.txt". What's
        wrong?](FAQ.html#Q._I_get_an_error_during_the_mri_ca_label_step_while_running_recon-all._The_last_thing_it_says_is:_.22saving_intensity_scales_to_aseg.auto_noCCseg.label_intensities.txt.22._What.27s_wrong.3F)
    4.  [Q. I get an error during the Talairach transform step when
        running recon-all on ANALYZE images. Why is this
        happening?](FAQ.html#Q._I_get_an_error_during_the_Talairach_transform_step_when_running_recon-all_on_ANALYZE_images.__Why_is_this_happening.3F)
6.  [FreeSurfer Output Questions](FAQ.html#FreeSurfer_Output_Questions)
    1.  [Q. The surfaces near the medial wall, hippocampus, and amygdala
        aren't accurately following the structures there. How can I fix
        this?](FAQ.html#Q._The_surfaces_near_the_medial_wall.2C_hippocampus.2C_and_amygdala_aren.27t_accurately_following_the_structures_there._How_can_I_fix_this.3F)
    2.  [Q: It seems that there is a 5mm thickness upper limit in my
        volumes. Is it normal? How can I change
        this?](FAQ.html#Q:_It_seems_that_there_is_a_5mm_thickness_upper_limit_in_my_volumes._Is_it_normal.3F_How_can_I_change_this.3F)
    3.  [Q. Why in many subjects the insular cortical surface seems so
        thick? Is the convoluted nature of the Insula that causes
        that?](FAQ.html#Q._Why_in_many_subjects_the_insular_cortical_surface_seems_so_thick.3F_Is_the_convoluted_nature_of_the_Insula_that_causes_that.3F)
    4.  [Q. Why would the orientation of my scans look wrong after
        processing my Siemens DICOM files with
        'mri_convert'?](FAQ.html#Q._Why_would_the_orientation_of_my_scans_look_wrong_after_processing_my_Siemens_DICOM_files_with_.27mri_convert.27.3F)
    5.  [Q. What are the sulc and curv overlays (in QDEC) showing
        us?](FAQ.html#Q._What_are_the_sulc_and_curv_overlays_.28in_QDEC.29_showing_us.3F)
    6.  [Q. How would I put a FreeSurfer output volume and/or
        segmentation back into the same space as my original anatomical
        input (native
        space)?](FAQ.html#Q._How_would_I_put_a_FreeSurfer_output_volume_and.2For_segmentation_back_into_the_same_space_as_my_original_anatomical_input_.28native_space.29.3F)
    7.  [Q. How do I transform coordinates in one space to those in
        another space (eg, a point on the surface to MNI305 space or to
        the col, row, slice of a functional
        volume)?](FAQ.html#Q._How_do_I_transform_coordinates_in_one_space_to_those_in_another_space_.28eg.2C_a_point_on_the_surface_to_MNI305_space_or_to_the_col.2C_row.2C_slice_of_a_functional_volume.29.3F)
    8.  [Q. How can I measure the distance along the cortical surface
        between two points located on the cortical
        surface?](FAQ.html#Q._How_can_I_measure_the_distance_along_the_cortical_surface_between_two_points_located_on_the_cortical_surface.3F)
    9.  [Q. The pial surface includes some cerebellum. How can I fix
        this?](FAQ.html#Q._The_pial_surface_includes_some_cerebellum._How_can_I_fix_this.3F)
    10. [Q. How do I get the cortical thickness maps for several
        subjects into the same template space
        (fsaverage)?](FAQ.html#Q._How_do_I_get_the_cortical_thickness_maps_for_several_subjects_into_the_same_template_space_.28fsaverage.29.3F)
    11. [Q. How can I get a high resolution atlas of the cortex in
        Freesurfer?](FAQ.html#Q._How_can_I_get_a_high_resolution_atlas_of_the_cortex_in_Freesurfer.3F)
    12. [Q. Where can I find V1
        labels?](FAQ.html#Q._Where_can_I_find_V1_labels.3F)
7.  [Analysis of FreeSurfer Data](FAQ.html#Analysis_of_FreeSurfer_Data)
    1.  [Q. I am trying to measure the cortical thickness of a specific
        ROI. How can I do
        this?](FAQ.html#Q._I_am_trying_to_measure_the_cortical_thickness_of_a_specific_ROI._How_can_I_do_this.3F)
    2.  [Q. I am using QDEC to examine the anatomical differences
        between two groups of subjects. The surface-based measures I can
        select are thickness, area, area.pial, sulc, curv, and
        jacobian_white. Could anybody tell me what anatomical features
        the later three (sulc, curv, and jacobian_white) actually
        measure?](FAQ.html#Q._I_am_using_QDEC_to_examine_the_anatomical_differences_between_two_groups_of_subjects._The_surface-based_measures_I_can_select_are_thickness.2C_area.2C_area.pial.2C_sulc.2C_curv.2C_and_jacobian_white._Could_anybody_tell_me_what_anatomical_features_the_later_three_.28sulc.2C_curv.2C_and_jacobian_white.29_actually_measure.3F)
    3.  [Q. I am trying to measure the global mean cortical thickness
        (i.e combined across hemispheres). How would I do
        this?](FAQ.html#Q._I_am_trying_to_measure_the_global_mean_cortical_thickness_.28i.e_combined_across_hemispheres.29._How_would_I_do_this.3F)
    4.  [Q: How can I get measurements of the lobes (parietal, temporal,
        frontal, &
        occipital)?](FAQ.html#Q:_How_can_I_get_measurements_of_the_lobes_.28parietal.2C_temporal.2C_frontal.2C_.26_occipital.29.3F)
    5.  [Q. How would I calculate the total CSF
        volume?](FAQ.html#Q._How_would_I_calculate_the_total_CSF_volume.3F)
    6.  [Q. What is the unit measure of mean curvature and Gaussian
        curvature?](FAQ.html#Q._What_is_the_unit_measure_of_mean_curvature_and_Gaussian_curvature.3F)
    7.  [Q. I want to run make_average_subject in order to prepare my
        data for GLM analysis, which file should I specify for the
        -xform flag, and what are the differences between my
        options?](FAQ.html#Q._I_want_to_run_make_average_subject_in_order_to_prepare_my_data_for_GLM_analysis.2C_which_file_should_I_specify_for_the_-xform_flag.2C_and_what_are_the_differences_between_my_options.3F)
    8.  [Q. What goes into the calculation of subcortical volume? We
        have tried adding volumes of individual subcortical areas but
        the total does not equal the subcortical volume provided by
        aseg. Is the subcortical volume calculation
        accurate?](FAQ.html#Q._What_goes_into_the_calculation_of_subcortical_volume.3F__We_have_tried_adding_volumes_of_individual_subcortical_areas_but_the_total_does_not_equal_the_subcortical_volume_provided_by_aseg.__Is_the_subcortical_volume_calculation_accurate.3F)
    9.  [Q. How would you perform a power analysis for a whole brain
        group comparison QDEC
        analysis?](FAQ.html#Q._How_would_you_perform_a_power_analysis_for_a_whole_brain_group_comparison_QDEC_analysis.3F)
    10. [Q. How can I get the volume of the different lobes of the brain
        (occipital, parietal, temporal, etc) ? White matter and gray
        matter? Labels
        ?](FAQ.html#Q._How_can_I_get_the_volume_of_the_different_lobes_of_the_brain_.28occipital.2C_parietal.2C_temporal.2C_etc.29_.3F_White_matter_and_gray_matter.3F_Labels_.3F)
    11. [Q. Why do I get different results when scanning the same person
        twice?](FAQ.html#Q._Why_do_I_get_different_results_when_scanning_the_same_person_twice.3F)
8.  [FreeSurfer & Matlab](FAQ.html#FreeSurfer_.26_Matlab)
    1.  [Q. How can I use the Freesurfer Matlab commands if I have a
        copy of Matlab installed on a Windows
        machine?](FAQ.html#Q._How_can_I_use_the_Freesurfer_Matlab_commands_if_I_have_a_copy_of_Matlab_installed_on_a_Windows_machine.3F)
    2.  [Q. Can I load FreeSurfer output in
        Matlab?](FAQ.html#Q._Can_I_load_FreeSurfer_output_in_Matlab.3F)
    3.  [Q. How can I make a histogram of cortical
        thickness?](FAQ.html#Q._How_can_I_make_a_histogram_of_cortical_thickness.3F)
    4.  [Q. How can I obtain the thickness of each vertex, and how can
        you identify which structure each vertex belongs
        to?](FAQ.html#Q._How_can_I_obtain_the_thickness_of_each_vertex.2C_and_how_can_you_identify_which_structure_each_vertex_belongs_to.3F)
9.  [FreeSurfer GUI](FAQ.html#FreeSurfer_GUI)
    1.  [Q. How can I troubleshoot rendering problems when using
        TKsurfer?](FAQ.html#Q._How_can_I_troubleshoot_rendering_problems_when_using_TKsurfer.3F)

</div>

<span id="line-10" class="anchor"></span><span id="line-11"
class="anchor"></span>

## General

<span id="line-12" class="anchor"></span>

### Q. How can I help this FAQ?

<span id="line-13" class="anchor"></span>

A: If you are able to edit pages, go ahead! If you don't have permission
to write on the Wiki, send an e-mail to ppj at netfilter dot com dot br
<span id="line-14" class="anchor"></span><span id="line-15"
class="anchor"></span>

### Q. What are the advantages of FreeSurfer over VBM?

<span id="line-16" class="anchor"></span>

A: <span id="line-17" class="anchor"></span><span id="line-18"
class="anchor"></span>

1.  FS uses geometry to do inter-subject registration, which experience
    has shown results in a much better matching of homologous cortical
    regions than volumetric techniques. <span id="line-19"
    class="anchor"></span><span id="line-20" class="anchor"></span>
2.  FS allows you to look at the two components of volume separately
    (thickness and surface area). It has been found that these two do
    not necessarily track one another, and in the worst case where one
    is increasing and the other decreasing the volume change can be 0.
    <span id="line-21" class="anchor"></span><span id="line-22"
    class="anchor"></span>
3.  The target that FS uses for registration (the white matter surface
    geometry) is completely invariant to gm atrophy, so gm changes won't
    result in a different registration. <span id="line-23"
    class="anchor"></span><span id="line-24" class="anchor"></span>

### Q. How do I know the version of FreeSurfer I'm running?

<span id="line-25" class="anchor"></span>

A: Run: <span id="line-26" class="anchor"></span><span id="line-27"
class="anchor"></span>

- recon-all -version <span id="line-28"
  class="anchor"></span><span id="line-29" class="anchor"></span>

### Q. Is the FreeSurfer source code available?

<span id="line-30" class="anchor"></span>

A: Yes, the source code is accessible via
[GitHub](https://surfer.nmr.mgh.harvard.edu/fswiki/GitHub).
<span id="line-31" class="anchor"></span><span id="line-32"
class="anchor"></span>

It is also recommended that you subscribe to the freesurfer mailing
<a href="http://mail.nmr.mgh.harvard.edu/mailman/listinfo/freesurfer"
class="http">list</a> to post questions and monitor solutions from other
users. <span id="line-33" class="anchor"></span><span id="line-34"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-35" class="anchor"></span>

## Computing

<span id="line-36" class="anchor"></span>

### Q. How long does it take to finish a reconstruction?

<span id="line-37" class="anchor"></span>

A: It depends on your processor speed and machine performance (notice
that dual/quad/hex core or hyperthead won't speed up one analysis
significantly), give a look at the link below in the section "Step-wise
directives":
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/recon-all"
class="http">http://surfer.nmr.mgh.harvard.edu/fswiki/recon-all</a>
<span id="line-38" class="anchor"></span><span id="line-39"
class="anchor"></span>

Also you can contribute to our running time statistics:
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllRunTimes"
class="https">https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllRunTimes</a>
<span id="line-40" class="anchor"></span><span id="line-41"
class="anchor"></span>

### Q. How can I reduce the time of recon-all in a group of patients?

<span id="line-42" class="anchor"></span>

A: [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer)
run its process in a non-parallel environment, so you won't have benefit
from a dual/quad/hex core machine for a single case analysis. However if
you have many cases you can start two
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer)
recon-all process in the same machine and theoretically you can reduce
by half the time to analyze your group of cases. A similar procedure can
also be used in quad/hex-core environment. Note that to take benefit of
a multi-core environment you need to use a SMP kernel in your OS.
<span id="line-43" class="anchor"></span><span id="line-44"
class="anchor"></span>

### Q. I want to use freesurfer to quantify cortical thickness, and I want to use the software under Linux. What equipment for computer do you recommend?

<span id="line-45" class="anchor"></span>

This answer requires constant updates: <span id="line-46"
class="anchor"></span><span id="line-47" class="anchor"></span>

**For Best Performances:** <span id="line-48"
class="anchor"></span><span id="line-49" class="anchor"></span>

Use a multi-Core processor Intel (a **i7-900 or newer** series processor
or **Xeon 6500/7500** Series) <span id="line-50"
class="anchor"></span><span id="line-51" class="anchor"></span>

Install at Least 8GB of Memory <span id="line-52"
class="anchor"></span><span id="line-53" class="anchor"></span>

If you prefer **AMD** you can use: <span id="line-54"
class="anchor"></span><span id="line-55" class="anchor"></span>

**AMD Opteron** 12-Core or **Phenon II X6** <span id="line-56"
class="anchor"></span><span id="line-57" class="anchor"></span>

Other alternative much more expensive is:
<a href="http://www.apple.com/macpro/" class="http">Mac Pro</a> with 12
cores and 16GB RAM. <span id="line-58"
class="anchor"></span><span id="line-59" class="anchor"></span>

The number of cores is roughly the number of studies you can process
simultaneously. Notice that each process will take 20-24 hrs.
<span id="line-60" class="anchor"></span><span id="line-61"
class="anchor"></span>

Keep in mind that you need to use the fastest memory in order to achieve
maximum benefit from multi-core architecture. <span id="line-62"
class="anchor"></span><span id="line-63" class="anchor"></span>

### Q. Is it possible to run FreeSurfer in Ubuntu Linux?

<span id="line-64" class="anchor"></span>

A: Yes. Ubuntu Linux is basically a Debian distro, so you should use
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) RH9
version. Depending on your video card you should disable the DRI using
the option NoDRI in the Device section of your X configuration file.
Notice that in older Ubuntu version there's a bug that prevents NoDRI
from working. <span id="line-65"
class="anchor"></span><span id="line-66" class="anchor"></span>

### Q. Could I run multiple instances of Freesurfer (on my virtual box)?

<span id="line-67" class="anchor"></span>

A: Yes, it is certainly possible (even advisable) to run more than one
copy of Freesurfer on a machine. It depends on how many processor cores
you have. You'll need at least 2Gb per process if not 3Gb, one core per
process. It may be possible to run one process using 1Gb if you use the
'no-gcut' flag. Open one terminal window for each instance of
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer),
using serperate commands in each terminal window. When running four
individual recon-all jobs on four cores, we have found that they will
all complete in about 110% of the time of a single run.
<span id="line-68" class="anchor"></span><span id="line-69"
class="anchor"></span>

When using a virtual box, assign N-1 cores to your virtual box, where N
is the total number of processor cores you have, along with at least
(N-1) x 2Gb of RAM. <span id="line-70"
class="anchor"></span><span id="line-71" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-72" class="anchor"></span>

## Acquisition

<span id="line-73" class="anchor"></span>

### Q. Is it recommended that people use memprage? How are they analyzed? Just sqrt sum sqr of the echoes? Or is there something more elaborate?

<span id="line-74" class="anchor"></span>

A: Yes, particularly for longitudinal. The increased bandwidth makes a
huge difference in being able to register across time. And at the moment
we do use the rms. An optimal combo would maybe be a tiny bit better,
but probably not much difference. <span id="line-75"
class="anchor"></span><span id="line-76" class="anchor"></span>

### Q. Are there suggested scan sequences which you recommend I use with Freesurfer?

<span id="line-77" class="anchor"></span>

A: Yes, Custom multiecho sequences for Siemens scanners are <a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurferWiki?action=AttachFile&amp;do=get&amp;target=FreeSurfer_Suggested_Morphometry_Protocols.pdf"
class="https">available</a> from the Martinos Center. The multiecho
FLASH is available as a standard sequence on the Siemens platform and we
distribute a slightly modified version that makes it more convenient to
set up the echo timing and allows a little more flexibility w.r.t.
geometry and spoiling but this isn't critical. We also distribute a
multiecho version of the MPRAGE sequence that isn't a product sequence
yet. <span id="line-78" class="anchor"></span><span id="line-79"
class="anchor"></span>

We are happy to send you binaries but MGH and Siemens requires that you
sign a "C2P" agreement, which is an indemnification document, before we
can provide you with the sequences and protocols for free.
<span id="line-80" class="anchor"></span><span id="line-81"
class="anchor"></span>

### Q. Is it possible to analyze clincial structural MRI exams with help of Freesurfer?

<span id="line-82" class="anchor"></span>

A: Yes, if the resolution is around 1mm, it should be possible. If the
resolution is greater than 1.3mm, then surfaces will probably not be
valid, but subcortical structures might be valid. <span id="line-83"
class="anchor"></span><span id="line-84" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-85" class="anchor"></span>

## Processing/Re-processing Data in FreeSurfer

<span id="line-86" class="anchor"></span>

### Q. Can I run some cases in my dataset using one version of FreeSurfer and others using a different version of FreeSurfer?

<span id="line-87" class="anchor"></span>

A: No, mixing versions is never a good idea as results are expected to
differ, if only slightly. The same version of
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer)
should be used to process all cases within a dataset. Another
consideration is that someone editing data run with an older version of
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) will
probably have more edits to do than if the same case was run with the
most recent version. <span id="line-88"
class="anchor"></span><span id="line-89" class="anchor"></span>

If you are sourcing the stable or dev version of
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) from
within the NMR center, you are strongly encouraged to created a frozen
copy of
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) for
your study. To do that, just download the public distribution from our
site and install it in your SUBJECTS_DIR or some other
project-appropriate place. <span id="line-90"
class="anchor"></span><span id="line-91" class="anchor"></span>

### Q. How to run recon-all in a ssh terminal

<span id="line-92" class="anchor"></span>

A: This is tricky, because recon-all spawns many process and redirect
I/O to the terminal that opened it. Run <span id="line-93"
class="anchor"></span><span id="line-94" class="anchor"></span>

- **recon-all -s subjid -all \> /dev/null 2\>&1 \</dev/null & disown
  -a** <span id="line-95" class="anchor"></span><span id="line-96"
  class="anchor"></span>

### Q. I had a \[Power Outage\|Computer Failure\|Spilled coffee on computer\|etc\], how can I resume the recon-all?

<span id="line-97" class="anchor"></span>

A: You can try <span id="line-98"
class="anchor"></span><span id="line-99" class="anchor"></span>

recon-all -make all -s subject <span id="line-100"
class="anchor"></span><span id="line-101" class="anchor"></span>

Also, depending on your version, there might be a file in the scripts
directory called
"<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/IsRunning"
class="nonexistent">IsRunning</a>". You should delete this if it is
there. <span id="line-102" class="anchor"></span><span id="line-103"
class="anchor"></span>

### Q. I have a subject which has been running for a really long time in recon-all, how can I tell if there is something wrong?

<span id="line-104" class="anchor"></span>

A: Assuming you have processed other subjects in considerably less time,
this probably means that there is a giant defect that will not be
corrected properly (eg. cerebellum or skull attached). You should check
the ?h.inflated.nofix or ?h.orig.nofix surfaces for any large defects.
If you load the filled.mgz you should be able to see whether the
cerebellum is still attached, and if so you would want to edit the
wm.mgz. Also, verify that the pons and corpus collosum were properly
detected. <span id="line-105" class="anchor"></span><span id="line-106"
class="anchor"></span>

### Q. I have already skull-stripped data. Can I submit it to recon-all?

<span id="line-107" class="anchor"></span>

A: If your skull-stripped volume does not have the cerebellum, then no.
If it does, then yes, however you will have to run the data a bit
differently. <span id="line-108"
class="anchor"></span><span id="line-109" class="anchor"></span>

First you must run only -autorecon1 like this:\
**recon-all -autorecon1 -noskullstrip -s \<subjid\>**
<span id="line-110" class="anchor"></span><span id="line-111"
class="anchor"></span>

Then you will have to make a symbolic link or copy T1.mgz to
brainmask.auto.mgz and a link from brainmask.auto.mgz to brainmask.mgz.
Finally, open this brainmask.mgz file and check that it looks okay
(there is no skull, cerebellum is intact; use the sample subject
**bert** that comes with your FreeSurfer installation to make sure it
looks comparable). From there you can run the final stages of
recon-all:\
**recon-all -autrecon2 -autorecon3 -s \<subjid\>** <span id="line-112"
class="anchor"></span><span id="line-113" class="anchor"></span>

### Q. I made white matter and pial edits to my volume. Do I need to run -autorecon2-wm and when that is finished run -autorecon2-pial?

<span id="line-114" class="anchor"></span>

A: No. If you made both white matter and pial edits, you only need to
run -autorecon2-wm which is higher up in the processing stream (before
the steps of -autorecon2-pial). By running -autorecon2-wm, it will
perform the steps necessary to fix a white matter edit and then all the
remaining steps in -autorecon2 including those steps that
-autorecon2-pial would run. The
[OtherUsefulFlags](https://surfer.nmr.mgh.harvard.edu/fswiki/OtherUsefulFlags)
wiki shows the hierarchy of the -autorecon2 flag shortcuts
(-autorecon2-cp starts before -autorecon2-wm which starts before
-autorecon2-pial). In general, you should start the processing stream at
the earliest step where you made an manual intervention and the rest
will be taken care of. Don't forget to run -autorecon3!
<span id="line-115" class="anchor"></span><span id="line-116"
class="anchor"></span>

### Q. One of my cases doesn't have the cerebellum so I adjusted the watershed threshold to fix it. However, at one threshold, the cerebellum is still not included, and at the next the entire skull is there. What should I do?

<span id="line-117" class="anchor"></span>

A: Removal of cerebellum is always bad and must be fixed (cerebellum is
included in the subcortical segmentation portion and is needed for a
proper atlas alignment). Including skull is not good, but leaving skull
is acceptable. The problem being sometimes the wm seg catches skull. So
make adjustments till you get cerebellum, then just see what happens
with the surfaces given remaining skull, and edit out skull in
brainmask.mgz if it hurts it. <span id="line-118"
class="anchor"></span><span id="line-119" class="anchor"></span>

For the command line below, try it with and without the -no-wgcaatlas
flag. Generally the -wsthresh only needs to be varied.
<span id="line-120" class="anchor"></span><span id="line-121"
class="anchor"></span>

- **recon-all -skullstrip -wsthresh 35 -clean-bm -no-wsgcaatlas -subjid
  subjid** <span id="line-122" class="anchor"></span><span id="line-123"
  class="anchor"></span>

If that still doesn't work, try using the multistrip command with the
watershed method. This will give an output of 4 sets of different
thresholds each for the orig, nu, and T1 volume. You can choose the best
one from the set and copy it to brainmask.auto.mgz and run the last step
of -skullstrip. More info can be found here: <a
href="http://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/SkullStripFix"
class="http">http://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/SkullStripFix</a>
<span id="line-124" class="anchor"></span><span id="line-125"
class="anchor"></span>

### Q. One or more of the files in a subject's directory was accidentally deleted or has become corrupted. How do I recreate the missing file(s)?

<span id="line-126" class="anchor"></span>

A: You will need to rerun the recon-all step in which that file is first
created. For example, to recreate the norm.mgz volume you would need to
run recon-all -canorm -s \<subjid\>. Click
[here](https://surfer.nmr.mgh.harvard.edu/fswiki/ReconAllTableStableV5.1)
to find out in which step a certain file is created in the version 5.3
recon-all process flow. <span id="line-127"
class="anchor"></span><span id="line-128" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-129" class="anchor"></span>

## Common Error messages

<span id="line-130" class="anchor"></span>

### Q. Help! I got this error message: "mri_watershed error: GLOBAL region of the brain empty!" - what should I do?

<span id="line-131" class="anchor"></span>

A: Run this:\
**recon-all -skullstrip -no-wsgcaatlas -s \<subjid\>**
<span id="line-132" class="anchor"></span><span id="line-133"
class="anchor"></span>

If that goes through without error, you can finish processing your data
by running:\
**recon-all -autorecon2 -autorecon3 -s \<subjid\>** <span id="line-134"
class="anchor"></span><span id="line-135" class="anchor"></span>

### Q. I get an error message from the Talairach Failure Detection. What does this mean?

<span id="line-136" class="anchor"></span>

A: In certain versions of FreeSurfer, the talairach failure detection is
too conservative so this may not be a problem. First, you will want to
check the talairach transform to make sure it looks okay. Directions on
how to do that are here:
<a href="https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/Talairach"
class="https">https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/Talairach</a>
<span id="line-137" class="anchor"></span><span id="line-138"
class="anchor"></span>

Essentially, you want to use the command: <span id="line-139"
class="anchor"></span><span id="line-140" class="anchor"></span>

<span id="line-141" class="anchor"></span><span id="line-142"
class="anchor"></span>

    tkregister2 --mgz --s <subjid> --fstal

<span id="line-143" class="anchor"></span>

and see if the green lines line up with the anatomy of the blurry brain
image. If so, then you can run this subject as you did before, just add
-notal-check to your command. For example, **recon-all -all -s subjid
-notal-check**. If the green lines do not line up well with the anatomy,
you will want to follow directions on the wiki page mentioned above to
fix it. If the images you passed to recon-all are in Analyze format,
verify that the orientation is correct. <span id="line-144"
class="anchor"></span><span id="line-145" class="anchor"></span>

### Q. I get an error during the mri_ca_label step while running recon-all. The last thing it says is: "saving intensity scales to aseg.auto_noCCseg.label_intensities.txt". What's wrong?

<span id="line-146" class="anchor"></span>

A: This is a bug in v.4.5. A fixed mri_ca_label can be downloaded from
here:\
<a
href="ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/misc/linux-centos4_x86_64/"
class="ftp">ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/misc/linux-centos4_x86_64/</a>
<span id="line-147" class="anchor"></span><span id="line-148"
class="anchor"></span>

copy it your \$FREESURFER_HOME/bin <span id="line-149"
class="anchor"></span><span id="line-150" class="anchor"></span>

We would advise rerunning all subjects with this fixed version.
<span id="line-151" class="anchor"></span><span id="line-152"
class="anchor"></span>

### Q. I get an error during the Talairach transform step when running recon-all on ANALYZE images. Why is this happening?

<span id="line-153" class="anchor"></span>

A: Images in the ANALYZE format do not retain orientation information
(left/right). You can bypass the Talairach check by including the
'-notal-check' flag in your recon-all command. Alternatively, you can
specify the orientation (neurological or radiological) using
mri_convert. Run 'mri_convert --help' to get info on specifying volume
orientation in the description section. Lastly, you can manually
register your brain volume in Talairach space by following this
[tutorial](https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial/Talairach).
<span id="line-154" class="anchor"></span><span id="line-155"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-156" class="anchor"></span><span id="line-157"
class="anchor"></span>

## FreeSurfer Output Questions

<span id="line-158" class="anchor"></span>

### Q. The surfaces near the medial wall, hippocampus, and amygdala aren't accurately following the structures there. How can I fix this?

<span id="line-159" class="anchor"></span>

A: The good news is you don't have to! These areas are generally
unreliable for a thickness study so you would want to exclude them from
your analysis. If you use glmfit, it calls the ?h.cortex.label file in
order to determine thickness. This file automatically has set these
areas to zero so they will not be included in your analysis. To see what
area ?h.cortex.label excludes you can load it in tksurfer on top of the
inflated surface. If you have tkmedit open at the same time for the same
subject, you can use the Go To Saved Point function to make sure areas
of concern are in this excluded section. \*Note: If you are using a
FreeSurfer version older than 4.3.0, the excluded region includes the
insula. If you are using an analysis program other than glmfit, just be
sure to use the ?h.cortex.label file to get your thickness measurements.
<span id="line-160" class="anchor"></span><span id="line-161"
class="anchor"></span>

Several reasons make it difficult to generate pial/wm surfaces in the
medial temporal lobe area. This region tends to be furthest away from
the coils receiving the MR signal, potentially late to myelinate in
individuals under 20 years old, very thin white matter in general, and
is in close proximity to regions of susceptibility. <span id="line-162"
class="anchor"></span><span id="line-163" class="anchor"></span>

The picture below shows the ?h.cortex.label (outlined in yellow) over
the ?h.aparc.annot. Notice how the ?h.cortex.label includes some of the
?h.unknown.label:\
<img
src="https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions/FAQ?action=AttachFile&amp;do=get&amp;target=cortex_label_over_aparc.jpeg"
title="cortex_label_over_aparc.jpeg" class="attachment"
alt="cortex_label_over_aparc.jpeg" /> <span id="line-164"
class="anchor"></span><span id="line-165" class="anchor"></span>

As always, use the example subject **bert** that comes with the
FreeSurfer installation to see what we define as acceptable surfaces.
<span id="line-166" class="anchor"></span><span id="line-167"
class="anchor"></span>

### Q: It seems that there is a 5mm thickness upper limit in my volumes. Is it normal? How can I change this?

<span id="line-168" class="anchor"></span>

A: We did this to prevent noncortical regions such as the basal ganglia
from corrupting the thickness measure through averaging. With the
?h.cortex.label it is probably no longer needed, however you can use
mris_thickness -max \<max thick\> to generate a thickness with a
different max. Take a look in the example below:\
\
**mris_thickness -max 10 bert lh newlh.thickness**\
\
The file **newlh.thickness** will be created inside the surf directory
of your subject. But we don't think the true thickness is ever that much
except in pathological cases like dysplasia and other disorders of
cortical development. <span id="line-169"
class="anchor"></span><span id="line-170" class="anchor"></span>

### Q. Why in many subjects the insular cortical surface seems so thick? Is the convoluted nature of the Insula that causes that?

<span id="line-171" class="anchor"></span>

A: It's not the convoluted nature of the Insula. It's the fact that
extreme capsule is so thin that it frequently isn't very apparent on MR,
and so there appears to be continuous gray matter from the basal ganglia
into the cortex. We think version 4.0 fixes this. <span id="line-172"
class="anchor"></span><span id="line-173" class="anchor"></span>

### Q. Why would the orientation of my scans look wrong after processing my Siemens DICOM files with 'mri_convert'?

<span id="line-174" class="anchor"></span>

A: It can be misleading to check orientation using FSLVIEW because it
orients volumes based on the way they are on disk so you often get
things looking pretty strange (e.g., upside-down). FSLVIEW does dispaly
little letters to indicate what it thinks the orientation is, so if you
stick to those, then you can properly judge whether the orientation is
correct. <span id="line-175" class="anchor"></span><span id="line-176"
class="anchor"></span>

### Q. What are the sulc and curv overlays (in QDEC) showing us?

<span id="line-177" class="anchor"></span>

A: The 'sulc' conveys information on how far removed a particular vertex
point on a surface is from a hypothetical "mid-surface" that exists
between the gyri and sulci. This surface is chosen so that the "mean" of
all these displacements is zero. The 'sulc' gives a indication then of
linear distance and displacements: how "deep" and how "high" are brain
folds <span id="line-178" class="anchor"></span><span id="line-179"
class="anchor"></span>

In [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer),
gyri have negative 'sulc' values, are colored green, and indicate how
far "down" a point has to travel to reach this "mid-surface". Sulci have
positive 'sulc' values, are colored red, and indicate how far "up" a
point needs to travel to reach the mid-surface. <span id="line-180"
class="anchor"></span><span id="line-181" class="anchor"></span>

The 'curv' conveys information on the curvature (not distance) at a
specific vertex point. The color conveys the sign, and is just an
arbitrary choice. The sharper the curve, the higher the value (positive
or negative). Areas with positive curvature, are colored red, and
correspond to curvatures in sulci, i.e. curving "up". Areas with
negative curvature are colored green, and correspond to curves pointing
"down", i.e. gyri. <span id="line-182"
class="anchor"></span><span id="line-183" class="anchor"></span>

So, in a nutshell, the difference is that the 'curv' files contain
information about curvatures, and the 'sulc' files contain information
about displacement. <span id="line-184"
class="anchor"></span><span id="line-185" class="anchor"></span>

### Q. How would I put a FreeSurfer output volume and/or segmentation back into the same space as my original anatomical input (native space)?

<span id="line-186" class="anchor"></span>

A: Please see directions on how to do this
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/FsAnat-to-NativeAnat"
class="http">here</a>, and also on this page
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems"
class="http">http://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems</a>
<span id="line-187" class="anchor"></span><span id="line-188"
class="anchor"></span>

### Q. How do I transform coordinates in one space to those in another space (eg, a point on the surface to MNI305 space or to the col, row, slice of a functional volume)?

<span id="line-189" class="anchor"></span>

A: Directions on how to do this are on this page:
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems"
class="http">http://surfer.nmr.mgh.harvard.edu/fswiki/CoordinateSystems</a>
<span id="line-190" class="anchor"></span><span id="line-191"
class="anchor"></span>

### Q. How can I measure the distance along the cortical surface between two points located on the cortical surface?

<span id="line-192" class="anchor"></span>

A: There is a tool which allows you to do this called 'mris_pmake'.
Please read the associated help file for details on how to use it
('mris_pmake --help'). <span id="line-193"
class="anchor"></span><span id="line-194" class="anchor"></span>

### Q. The pial surface includes some cerebellum. How can I fix this?

<span id="line-195" class="anchor"></span>

A: This fix only works for v4.3 and up. If you are using an earlier
version, please contact us for help. <span id="line-196"
class="anchor"></span><span id="line-197" class="anchor"></span>

In order to fix this problem, you will have to edit the
brain.finalsurfs.mgz (and **not** the brainmask.mgz). Remove the parts
of the cerebellum that are affecting the surfaces. Save your changes and
then run:\
recon-all -make all -s subjid <span id="line-198"
class="anchor"></span><span id="line-199" class="anchor"></span>

### Q. How do I get the cortical thickness maps for several subjects into the same template space (fsaverage)?

<span id="line-200" class="anchor"></span>

A: Include the '-qcache -measure thickness' flags in your recon-all
command for each subject. This will create files in the /surf directory
which sample the thickness data at different smoothing levels onto the
fsaverage subject space. If the '-measure' flag is not included, all
cortical measurements will be sampled onto fsaverage and smoothed
(thickness, sulc, area, curv, etc.). <span id="line-201"
class="anchor"></span><span id="line-202" class="anchor"></span>

### Q. How can I get a high resolution atlas of the cortex in Freesurfer?

<span id="line-203" class="anchor"></span>

A: This can be accomplished using 'mris_divide_parcellation'. You can
pass your preferred max area of a parcellation and it will keep
subdividing along the primary eigen-axis until no units are above that
surface area. <span id="line-204"
class="anchor"></span><span id="line-205" class="anchor"></span>

### Q. Where can I find V1 labels?

<span id="line-206" class="anchor"></span>

A: V1 labeling is produced by default in recon-all as part of the
Brodmann area set (located in ../fsaverage/label/?h.V1.label). Those
labels are described
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/BrodmannAreaMaps"
class="http">here</a>. The Hind's V1 labeling method must be run
seperately by adding the '-label-v1' flag to your recon-all command:
<span id="line-207" class="anchor"></span><span id="line-208"
class="anchor"></span>

<span id="line-209" class="anchor"></span><span id="line-210"
class="anchor"></span>

    recon-all -all -s bert -label-v1

<span id="line-211" class="anchor"></span>

The accuracy of the Hinds and Fischl V1 labeling method compared to
retinotopy depends under what conditions the retinotopy is carried out
(field strength, \# of coils elements, voxel size, etc.). In our
comparision, the folding patterns predict the border location to about
2.5mm, which is probably better than you can get with retinotopy. (click
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/RetinotopyStimuli"
class="http">here</a> for tips on creating retinotopy stimuli)
<span id="line-212" class="anchor"></span><span id="line-213"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-214" class="anchor"></span>

## Analysis of FreeSurfer Data

<span id="line-215" class="anchor"></span>

### Q. I am trying to measure the cortical thickness of a specific ROI. How can I do this?

<span id="line-216" class="anchor"></span>

A: You can save the ROI to a label file and then use:\
\
<span id="line-217" class="anchor"></span><span id="line-218"
class="anchor"></span>

- **mris_anatomical_stats -l \<label file\>** <span id="line-219"
  class="anchor"></span><span id="line-220" class="anchor"></span>

### Q. I am using QDEC to examine the anatomical differences between two groups of subjects. The surface-based measures I can select are thickness, area, area.pial, sulc, curv, and jacobian_white. Could anybody tell me what anatomical features the later three (sulc, curv, and jacobian_white) actually measure?

<span id="line-221" class="anchor"></span>

\
**sulc** = "average convexity" from our 1999 reconII paper(<a
href="https://surfer.nmr.mgh.harvard.edu/ftp/articles/fischl99b-recon2.pdf"
class="https">https://surfer.nmr.mgh.harvard.edu/ftp/articles/fischl99b-recon2.pdf</a>).\
Essentially measures the depth/height of each point above the average
surface.\
**curv** = smoothed mean curvature.\
**jacobian_white** = the jacobian of the spherical transform. Measures
the amount of distortion needed to warp a subject into register with the
atlas.\
You might want to look at the slides downloadable from the top of this
page:\
\
<a href="http://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial"
class="http">http://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial</a>\
which contain pictures showing the meaning of 'curv' and 'sulc'.\
<span id="line-222" class="anchor"></span><span id="line-223"
class="anchor"></span>

### Q. I am trying to measure the global mean cortical thickness (i.e combined across hemispheres). How would I do this?

<span id="line-224" class="anchor"></span>

A: One suggestion is to use the surface area of each hemisphere as the
weighting factor. In which case the global mean thickness including both
hemispheres would be given by: <span id="line-225"
class="anchor"></span><span id="line-226" class="anchor"></span>

bh.thickness = ( (lh.thickness \* lh.surfarea) + (rh.thickness \*
rh.surfarea) ) / (lh.surfarea + rh.surfarea) <span id="line-227"
class="anchor"></span><span id="line-228" class="anchor"></span>

If you use the values in the ?h.aparc.stats, it already factors out the
'unknown' region, so you don't have to do it yourself.
<span id="line-229" class="anchor"></span><span id="line-230"
class="anchor"></span>

### Q: How can I get measurements of the lobes (parietal, temporal, frontal, & occipital)?

<span id="line-231" class="anchor"></span>

A: You can either use the PALS_B12 atlas (mapped to fsaverage in v5.0)
or create your own following the directions on the
[CorticalParcellation](https://surfer.nmr.mgh.harvard.edu/fswiki/CorticalParcellation)
wiki. <span id="line-232" class="anchor"></span><span id="line-233"
class="anchor"></span>

### Q. How would I calculate the total CSF volume?

<span id="line-234" class="anchor"></span>

A: You can add up the various ventricular structures to get total
ventricular volume, but we don't segment sulcal CSF, since it's not
distinguishible from bone on a T1-weighted MRI. <span id="line-235"
class="anchor"></span><span id="line-236" class="anchor"></span>

### Q. What is the unit measure of mean curvature and Gaussian curvature?

<span id="line-237" class="anchor"></span>

A: See these wiki pages for more info: [Mean
curvature](https://surfer.nmr.mgh.harvard.edu/fswiki/MeanCurvature),
[Gaussian
curvature](https://surfer.nmr.mgh.harvard.edu/fswiki/GaussianCurvature)
<span id="line-238" class="anchor"></span><span id="line-239"
class="anchor"></span>

### Q. I want to run make_average_subject in order to prepare my data for GLM analysis, which file should I specify for the -xform flag, and what are the differences between my options?

<span id="line-240" class="anchor"></span>

A: Your typical options are talairach.lta, talairach.xfm, and
talairach.m3z. The .lta and .xfm are linear transforms to a Talairach
coordinate system. The .m3z is a non-linear morph and will give you a
much higer anatomical resolution. <span id="line-241"
class="anchor"></span><span id="line-242" class="anchor"></span>

### Q. What goes into the calculation of subcortical volume? We have tried adding volumes of individual subcortical areas but the total does not equal the subcortical volume provided by aseg. Is the subcortical volume calculation accurate?

<span id="line-243" class="anchor"></span>

A: The aseg.stats file takes into account partial voluming which is not
taken into account when you simply sum up the subcortical structures
because some of those structures will be partially volumed with white
matter. <span id="line-244" class="anchor"></span><span id="line-245"
class="anchor"></span>

### Q. How would you perform a power analysis for a whole brain group comparison QDEC analysis?

<span id="line-246" class="anchor"></span>

A: For the power analysis, you need four things: <span id="line-247"
class="anchor"></span><span id="line-248" class="anchor"></span>

1.  Effect Size <span id="line-249"
    class="anchor"></span><span id="line-250" class="anchor"></span>
2.  Number of Subjects <span id="line-251"
    class="anchor"></span><span id="line-252" class="anchor"></span>
3.  Target False Positive Rate (alpha) <span id="line-253"
    class="anchor"></span><span id="line-254" class="anchor"></span>
4.  Target False Negative Rate (beta) <span id="line-255"
    class="anchor"></span><span id="line-256" class="anchor"></span>

Given any 3, you can compute the 4th. You can get the Effect Size from
the output of the QDEC analysis. Each analysis creates a GLM directory,
and there is a directory for each contrast in the GLM dir. In the
contrast dir, you will find several files, but the important ones for
this are the gamma.mgh and the gammavar.mgh. The gammavar is the square
of the error bar (ie, t=gamma/sqrt(gammavar)). The gamma will not change
as you add subjects (at least in expectation). The gammavar will drop
linearly with the number of subjects (again in expectation). The effect
size will then be gamma/sqrt(gammavar\*Npilot), where Npilot is the
number subjects in the pilot study. In a new study with Nnew subjects,
the expected t will be tnew = gamma/sqrt(gammavar\*Npilot/Nnew).
<span id="line-257" class="anchor"></span><span id="line-258"
class="anchor"></span>

### Q. How can I get the volume of the different lobes of the brain (occipital, parietal, temporal, etc) ? White matter and gray matter? Labels ?

<span id="line-259" class="anchor"></span>

A: For V5.0 and later, you can run mri_annotation2label with
--lobesStrict to get a lobe annotation. If that definition of "lobes" is
good for you, then you can run mris_anatomical_stats to get the volume
for each lobe. For versions prior to 5.0, you can use
mri_annotation2label to break the labels apart, then use mri_mergelabels
to combine the individual labels into lobe labels, then use
mris_label2annot to create a lobe annotation, then use
mris_anatomical_stats. <span id="line-260"
class="anchor"></span><span id="line-261" class="anchor"></span>

### Q. Why do I get different results when scanning the same person twice?

<span id="line-262" class="anchor"></span>

A: There are a variety of sources of variance. First there are some
reasons that affect the images. Different looking images will of course
affect the structural estimates. The second set of reasons is related to
random noise and processing bias. <span id="line-263"
class="anchor"></span><span id="line-264" class="anchor"></span>

**a) Acquisition** <span id="line-265"
class="anchor"></span><span id="line-266" class="anchor"></span>

a\) 1. *Head Motion* during acquisition changes the image and results in
smaller GM estimates (even for images that pass QC)\
<a href="http://reuter.mit.edu/publications/pid/reuter-motion14"
class="http">http://reuter.mit.edu/publications/pid/reuter-motion14</a>\
<a href="http://reuter.mit.edu/publications/pid/tisdall15"
class="http">http://reuter.mit.edu/publications/pid/tisdall15</a>
<span id="line-267" class="anchor"></span><span id="line-268"
class="anchor"></span>

a\) 2. *Hydration levels* affect the image and e.g. GM estimates\
<a href="http://reuter.mit.edu/publications/pid/biller15"
class="http">http://reuter.mit.edu/publications/pid/biller15</a>
<span id="line-269" class="anchor"></span><span id="line-270"
class="anchor"></span>

a\) 3. *Different head positions* can cause large differences if images
are not gradient unwarped (depending on your hardware these effects can
be small or large). Also there is of course noise in the images which
can lead to different results. <span id="line-271"
class="anchor"></span><span id="line-272" class="anchor"></span>

a\) 4. *Different person*: sometimes errors in the de-identification
(annonymization) pipeline can causes images with the same subject id to
come from different subjects. Also people sometimes send a sibling or
friend to a follow-up visit (in order to complete the study and get
paid, if they cannot come themselves). <span id="line-273"
class="anchor"></span><span id="line-274" class="anchor"></span>

**b) Processing** <span id="line-275"
class="anchor"></span><span id="line-276" class="anchor"></span>

b\) 1. Different *noise* or small changes in the image can trigger
processing to do different things (e.g. small skull strip failure,
different surface placement, e.g. one time including dura the other time
not). Small changes can accumulate. This can produce arbitrary large
changes in a single subject. It can be reduced/fixed via manual edits.
<span id="line-277" class="anchor"></span><span id="line-278"
class="anchor"></span>

b\) 2. *Processing bias*, for example, mapping the follow-up to baseline
(which some people do as a pre-processing step), is problematic as
follow-ups get interpolated (which looks like smoothing) and so you
introduce a change to some of your images (the follow-up only), biasing
your measurements of change. See\
<a href="http://reuter.mit.edu/publications/pid/reuter-long12"
class="http">http://reuter.mit.edu/publications/pid/reuter-long12</a>\
<a href="http://reuter.mit.edu/publications/pid/reuter-bias11"
class="http">http://reuter.mit.edu/publications/pid/reuter-bias11</a>\
This problem (and some of b.1) can be improved by using the longitudinal
pipeline in
[FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeSurfer) to
analyze your data:\
<a
href="https://surfer.nmr.mgh.harvard.edu/fswiki/LongitudinalProcessing"
class="https">https://surfer.nmr.mgh.harvard.edu/fswiki/LongitudinalProcessing</a>
<span id="line-279" class="anchor"></span><span id="line-280"
class="anchor"></span>

Finally note, that you cannot trust individual cortical thickness
values. People usually run studies comparing 10 or 15 subjects per
group. There can always be individual outliers. Manual checking and
editing can fix some of that, but not all. Especially effects from
motion or hydration cannot be removed. <span id="line-281"
class="anchor"></span><span id="line-282" class="anchor"></span>

------------------------------------------------------------------------

<span id="line-283" class="anchor"></span>

## FreeSurfer & Matlab

<span id="line-284" class="anchor"></span>

(In the directory '\$FREESURFER_HOME/matlab' you will find several
Matlab-based scripts for reading and writing surface- and volume-based
data generated in freesurfer.) <span id="line-285"
class="anchor"></span><span id="line-286" class="anchor"></span>

### Q. How can I use the Freesurfer Matlab commands if I have a copy of Matlab installed on a Windows machine?

<span id="line-287" class="anchor"></span>

A: You can try to transport files from Linux to Windows which will be
tedious and things may not work properly. Alternatively, you could
install Matlab for Linux or you can try using Octave (a kind of GNU
Matlab for Linux). <span id="line-288"
class="anchor"></span><span id="line-289" class="anchor"></span>

### Q. Can I load FreeSurfer output in Matlab?

<span id="line-290" class="anchor"></span>

A: If you write it as .mgz format then load_mgh (or MRIread) will read
it <span id="line-291" class="anchor"></span><span id="line-292"
class="anchor"></span>

### Q. How can I make a histogram of cortical thickness?

<span id="line-293" class="anchor"></span>

A: In Matlab you can use the read_curv() function, as in the example
below.\
\
<span id="line-294" class="anchor"></span><span id="line-295"
class="anchor"></span>

- **thick = read_curv
  ('/usr/local/freesurfer/subjects/bert/surfer/lh.thickness');\
  hist (thick,100);**\
  \
  Notice that there are many zero values that refer to areas where
  there's no cortical surface. The best procedure is to create a new
  array without the zero values and then make the histogram.
  <span id="line-296" class="anchor"></span><span id="line-297"
  class="anchor"></span>

### Q. How can I obtain the thickness of each vertex, and how can you identify which structure each vertex belongs to?

<span id="line-298" class="anchor"></span>

A: You will need to use the read_curv() function to get the thickness
estimates, and use the read_annotation() function to assign each index
in the surface vector to a specific structure. You can then match up
corresponding indices in the the thickness vector and the structure
vector to determine the thickness and structure label for each vertex.
<span id="line-299" class="anchor"></span><span id="line-300"
class="anchor"></span>

------------------------------------------------------------------------

<span id="line-301" class="anchor"></span>

## FreeSurfer GUI

<span id="line-302" class="anchor"></span>

### Q. How can I troubleshoot rendering problems when using TKsurfer?

<span id="line-303" class="anchor"></span>

A: Please refer to
[TksurferDisplayProblems](https://surfer.nmr.mgh.harvard.edu/fswiki/TksurferDisplayProblems)
<span id="line-304" class="anchor"></span><span id="bottom"
class="anchor"></span>

</div>

UserContributions/FAQ (last edited 2019-12-14 14:15:45 by
<span title="DougGreve @ 66.31.42.139[66.31.42.139]">[DougGreve](https://surfer.nmr.mgh.harvard.edu/fswiki/DougGreve "DougGreve @ 66.31.42.139[66.31.42.139]")</span>)

<div id="pagebottom">

</div>

</div>

<div id="footer">

- <span class="disabled">Immutable Page</span>

- <a href="FAQ.html#" class="nbcomment"
  onclick="toggleComments();return false;">Comments</a>

- <span class="disabled">Discussion</span>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions/FAQ?action=info"
  class="nbinfo" rel="nofollow">Info</a>

- <a
  href="https://surfer.nmr.mgh.harvard.edu/fswiki/UserContributions/FAQ?action=AttachFile"
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

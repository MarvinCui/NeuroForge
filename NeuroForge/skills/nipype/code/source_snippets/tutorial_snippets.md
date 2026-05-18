# nipype Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Save Load Resultfile

- Kind: `tutorial`
- Source: `references/tutorials/save-load-resultfile/save-load-resultfile.md`
- Note: Workflow: Test minimally the save/load functions for result files.

```python
# Setup
# Fixtures: tmpdir, use_relative

# Workflow
'Test minimally the save/load functions for result files.'
from shutil import copytree, rmtree
tmpdir.chdir()
old_use_relative = config.getboolean('execution', 'use_relative_paths')
config.set('execution', 'use_relative_paths', use_relative)
spc = pe.Node(StrPathConfuser(in_str='2'), name='spc')
spc.base_dir = tmpdir.mkdir('node').strpath
result = spc.run()
loaded_result = load_resultfile(tmpdir.join('node').join('spc').join('result_spc.pklz').strpath)
assert result.runtime.dictcopy() == loaded_result.runtime.dictcopy()
assert result.inputs == loaded_result.inputs
assert result.outputs.get() == loaded_result.outputs.get()
copytree(tmpdir.join('node').strpath, tmpdir.join('node2').strpath)
rmtree(tmpdir.join('node').strpath)
if use_relative:
    loaded_result2 = load_resultfile(tmpdir.join('node2').join('spc').join('result_spc.pklz').strpath)
    assert result.runtime.dictcopy() == loaded_result2.runtime.dictcopy()
    assert result.inputs == loaded_result2.inputs
    assert loaded_result2.outputs.get() != result.outputs.get()
    newpath = result.outputs.out_path.replace('/node/', '/node2/')
    assert loaded_result2.outputs.out_path == newpath
    assert loaded_result2.outputs.out_tuple[0] == newpath
    assert loaded_result2.outputs.out_dict_path['2'] == newpath
else:
    with pytest.raises(nib.TraitError):
        load_resultfile(tmpdir.join('node2').join('spc').join('result_spc.pklz').strpath)
config.set('execution', 'use_relative_paths', old_use_relative)
```

## 2. How To: Convert To Traits Type

- Kind: `tutorial`
- Source: `references/tutorials/convert-to-traits-type/convert-to-traits-type.md`
- Note: Workflow: test convert to traits type

```python
# Workflow
Params = namedtuple('Params', 'traits_type is_file')
Res = namedtuple('Res', 'traits_type subtype is_mandatory')
l_entries = [Params('variable string', False), Params('variable int', False), Params('variable float', False), Params('variable bool', False), Params('variable complex', False), Params('variable int, optional', False), Params('variable string, optional', False), Params('variable float, optional', False), Params('variable bool, optional', False), Params('variable complex, optional', False), Params('string', False), Params('int', False), Params('string', True), Params('float', False), Params('bool', False), Params('complex', False), Params('string, optional', False), Params('int, optional', False), Params('string, optional', True), Params('float, optional', False), Params('bool, optional', False), Params('complex, optional', False)]
l_expected = [Res(traits.List, traits.Str, True), Res(traits.List, traits.Int, True), Res(traits.List, traits.Float, True), Res(traits.List, traits.Bool, True), Res(traits.List, traits.Complex, True), Res(traits.List, traits.Int, False), Res(traits.List, traits.Str, False), Res(traits.List, traits.Float, False), Res(traits.List, traits.Bool, False), Res(traits.List, traits.Complex, False), Res(traits.Str, None, True), Res(traits.Int, None, True), Res(File, None, True), Res(traits.Float, None, True), Res(traits.Bool, None, True), Res(traits.Complex, None, True), Res(traits.Str, None, False), Res(traits.Int, None, False), Res(File, None, False), Res(traits.Float, None, False), Res(traits.Bool, None, False), Res(traits.Complex, None, False)]
for entry, res in zip(l_entries, l_expected):
    traits_type, is_mandatory = convert_to_traits_type(entry.traits_type, entry.is_file)
    trait_instance = traits_type()
    assert isinstance(trait_instance, res.traits_type)
    if res.subtype:
        assert isinstance(trait_instance.inner_traits()[0].trait_type, res.subtype)
    assert is_mandatory == res.is_mandatory
with pytest.raises(IOError):
    convert_to_traits_type('file, optional')
```

## 3. How To: Randomise Parallel

- Kind: `tutorial`
- Source: `references/tutorials/randomise-parallel/randomise-parallel.md`
- Note: Workflow: test Randomise parallel

```python
# Workflow
rand = fsl.Randomise_parallel()
assert rand.cmd == 'randomise_parallel'
with pytest.raises(ValueError):
    rand.run()
rand.inputs.input_4D = 'infile.nii'
rand.inputs.output_rootname = 'outfile'
rand.inputs.design_matrix = 'design.mat'
rand.inputs.t_contrast = 'infile.con'
actualCmdline = sorted(rand.cmdline.split())
cmd = 'randomise_parallel -i infile.nii -o outfile -d design.mat -t infile.con'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
rand2 = fsl.Randomise_parallel(input_4D='infile2', output_rootname='outfile2', f_contrast='infile.f', one_sample_gmean=True, int_seed=4)
actualCmdline = sorted(rand2.cmdline.split())
cmd = 'randomise_parallel -i infile2 -o outfile2 -1 -f infile.f --seed=4'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
rand3 = fsl.Randomise_parallel()
results = rand3.run(input_4D='infile3', output_rootname='outfile3')
assert results.runtime.cmdline == 'randomise_parallel -i infile3 -o outfile3'
opt_map = {'demean_data': ('-D', True), 'one_sample_gmean': ('-1', True), 'mask_image': ('-m inp_mask', 'inp_mask'), 'design_matrix': ('-d design.mat', 'design.mat'), 't_contrast': ('-t input.con', 'input.con'), 'f_contrast': ('-f input.fts', 'input.fts'), 'xchange_block_labels': ('-e design.grp', 'design.grp'), 'print_unique_perm': ('-q', True), 'print_info_parallelMode': ('-Q', True), 'num_permutations': ('-n 10', 10), 'vox_pvalus': ('-x', True), 'fstats_only': ('--fonly', True), 'thresh_free_cluster': ('-T', True), 'thresh_free_cluster_2Dopt': ('--T2', True), 'cluster_thresholding': ('-c 0.20', 0.2), 'cluster_mass_thresholding': ('-C 0.40', 0.4), 'fcluster_thresholding': ('-F 0.10', 0.1), 'fcluster_mass_thresholding': ('-S 0.30', 0.3), 'variance_smoothing': ('-v 0.20', 0.2), 'diagnostics_off': ('--quiet', True), 'output_raw': ('-R', True), 'output_perm_vect': ('-P', True), 'int_seed': ('--seed=20', 20), 'TFCE_height_param': ('--tfce_H=0.11', 0.11), 'TFCE_extent_param': ('--tfce_E=0.50', 0.5), 'TFCE_connectivity': ('--tfce_C=0.30', 0.3), 'list_num_voxel_EVs_pos': ('--vxl=' + repr([1, 2, 3, 4]), repr([1, 2, 3, 4])), 'list_img_voxel_EVs': ('--vxf=' + repr([6, 7, 8, 9, 3]), repr([6, 7, 8, 9, 3]))}
for name, settings in list(opt_map.items()):
    rand4 = fsl.Randomise_parallel(input_4D='infile', output_rootname='root', **{name: settings[1]})
    assert rand4.cmdline == rand4.cmd + ' -i infile -o root ' + settings[0]
```

## 4. How To: Randomise2

- Kind: `tutorial`
- Source: `references/tutorials/randomise2/randomise2.md`
- Note: Workflow: test randomise2

```python
# Workflow
rand = fsl.Randomise()
assert rand.cmd == 'randomise'
with pytest.raises(ValueError):
    rand.run()
rand.inputs.input_4D = 'infile.nii'
rand.inputs.output_rootname = 'outfile'
rand.inputs.design_matrix = 'design.mat'
rand.inputs.t_contrast = 'infile.con'
actualCmdline = sorted(rand.cmdline.split())
cmd = 'randomise -i infile.nii -o outfile -d design.mat -t infile.con'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
rand2 = fsl.Randomise(input_4D='infile2', output_rootname='outfile2', f_contrast='infile.f', one_sample_gmean=True, int_seed=4)
actualCmdline = sorted(rand2.cmdline.split())
cmd = 'randomise -i infile2 -o outfile2 -1 -f infile.f --seed=4'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
rand3 = fsl.Randomise()
results = rand3.run(input_4D='infile3', output_rootname='outfile3')
assert results.runtime.cmdline == 'randomise -i infile3 -o outfile3'
opt_map = {'demean_data': ('-D', True), 'one_sample_gmean': ('-1', True), 'mask_image': ('-m inp_mask', 'inp_mask'), 'design_matrix': ('-d design.mat', 'design.mat'), 't_contrast': ('-t input.con', 'input.con'), 'f_contrast': ('-f input.fts', 'input.fts'), 'xchange_block_labels': ('-e design.grp', 'design.grp'), 'print_unique_perm': ('-q', True), 'print_info_parallelMode': ('-Q', True), 'num_permutations': ('-n 10', 10), 'vox_pvalus': ('-x', True), 'fstats_only': ('--fonly', True), 'thresh_free_cluster': ('-T', True), 'thresh_free_cluster_2Dopt': ('--T2', True), 'cluster_thresholding': ('-c 0.20', 0.2), 'cluster_mass_thresholding': ('-C 0.40', 0.4), 'fcluster_thresholding': ('-F 0.10', 0.1), 'fcluster_mass_thresholding': ('-S 0.30', 0.3), 'variance_smoothing': ('-v 0.20', 0.2), 'diagnostics_off': ('--quiet', True), 'output_raw': ('-R', True), 'output_perm_vect': ('-P', True), 'int_seed': ('--seed=20', 20), 'TFCE_height_param': ('--tfce_H=0.11', 0.11), 'TFCE_extent_param': ('--tfce_E=0.50', 0.5), 'TFCE_connectivity': ('--tfce_C=0.30', 0.3), 'list_num_voxel_EVs_pos': ('--vxl=1,2,3,4', '1,2,3,4'), 'list_img_voxel_EVs': ('--vxf=6,7,8,9,3', '6,7,8,9,3')}
for name, settings in list(opt_map.items()):
    rand4 = fsl.Randomise(input_4D='infile', output_rootname='root', **{name: settings[1]})
    assert rand4.cmdline == rand4.cmd + ' -i infile -o root ' + settings[0]
```

## 5. How To: Fit Qt1

- Kind: `tutorial`
- Source: `references/tutorials/fit-qt1/fit-qt1.md`
- Note: Workflow: Testing FitQt1 interface.

```python
# Workflow
'Testing FitQt1 interface.'
fit_qt1 = FitQt1()
cmd = get_custom_path('fit_qt1', env_dir='NIFTYFITDIR')
assert fit_qt1.cmd == cmd
with pytest.raises(ValueError):
    fit_qt1.run()
in_file = example_data('TI4D.nii.gz')
fit_qt1.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
assert fit_qt1.cmdline == expected_cmd
fit_qt1_2 = FitQt1(tis=[1, 2, 5], ir_flag=True)
in_file = example_data('TI4D.nii.gz')
fit_qt1_2.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -IR -TIs 1.0 2.0 5.0 -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
assert fit_qt1_2.cmdline == expected_cmd
fit_qt1_3 = FitQt1(flips=[2, 4, 8], spgr=True)
in_file = example_data('TI4D.nii.gz')
fit_qt1_3.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -flips 2.0 4.0 8.0 -m0map {map0} -mcmap {cmap} -res {res} -SPGR -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
assert fit_qt1_3.cmdline == expected_cmd
```

## 6. How To: Vec Reg

- Kind: `tutorial`
- Source: `references/tutorials/vec-reg/vec-reg.md`
- Note: Workflow: test Vec reg

```python
# Workflow
vrg = fsl.VecReg()
assert vrg.cmd == 'vecreg'
with pytest.raises(ValueError):
    vrg.run()
vrg.inputs.infile = 'infile'
vrg.inputs.outfile = 'outfile'
vrg.inputs.refVolName = 'MNI152'
vrg.inputs.affineTmat = 'tmat.mat'
assert vrg.cmdline == 'vecreg -i infile -o outfile -r MNI152 -t tmat.mat'
vrg2 = fsl.VecReg(infile='infile2', outfile='outfile2', refVolName='MNI152', affineTmat='tmat2.mat', brainMask='nodif_brain_mask')
actualCmdline = sorted(vrg2.cmdline.split())
cmd = 'vecreg -i infile2 -o outfile2 -r MNI152 -t tmat2.mat -m nodif_brain_mask'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
vrg3 = fsl.VecReg()
results = vrg3.run(infile='infile3', outfile='outfile3', refVolName='MNI152', affineTmat='tmat3.mat')
assert results.runtime.cmdline == 'vecreg -i infile3 -o outfile3 -r MNI152 -t tmat3.mat'
assert results.runtime.returncode != 0
assert results.interface.inputs.infile == 'infile3'
assert results.interface.inputs.outfile == 'outfile3'
assert results.interface.inputs.refVolName == 'MNI152'
assert results.interface.inputs.affineTmat == 'tmat3.mat'
opt_map = {'verbose': ('-v', True), 'helpDoc': ('-h', True), 'tensor': ('--tensor', True), 'affineTmat': ('-t Tmat', 'Tmat'), 'warpFile': ('-w wrpFile', 'wrpFile'), 'interpolation': ('--interp=sinc', 'sinc'), 'brainMask': ('-m mask', 'mask')}
for name, settings in list(opt_map.items()):
    vrg4 = fsl.VecReg(infile='infile', outfile='outfile', refVolName='MNI152', **{name: settings[1]})
    assert vrg4.cmdline == vrg4.cmd + ' -i infile -o outfile -r MNI152 ' + settings[0]
```

## 7. How To: Reg Jacobian Jac

- Kind: `tutorial`
- Source: `references/tutorials/reg-jacobian-jac/reg-jacobian-jac.md`
- Note: Workflow: Test interface for RegJacobian

```python
# Workflow
'Test interface for RegJacobian'
nr_jacobian = RegJacobian()
assert nr_jacobian.cmd == get_custom_path('reg_jacobian')
with pytest.raises(ValueError):
    nr_jacobian.run()
ref_file = example_data('im1.nii')
trans_file = example_data('warpfield.nii')
nr_jacobian.inputs.ref_file = ref_file
nr_jacobian.inputs.trans_file = trans_file
nr_jacobian.inputs.omp_core_val = 4
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jac {jac}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jac.nii.gz')
assert nr_jacobian.cmdline == expected_cmd
nr_jacobian_2 = RegJacobian(type='jacM', omp_core_val=4)
ref_file = example_data('im1.nii')
trans_file = example_data('warpfield.nii')
nr_jacobian_2.inputs.ref_file = ref_file
nr_jacobian_2.inputs.trans_file = trans_file
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacM {jac}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jacM.nii.gz')
assert nr_jacobian_2.cmdline == expected_cmd
nr_jacobian_3 = RegJacobian(type='jacL', omp_core_val=4)
ref_file = example_data('im1.nii')
trans_file = example_data('warpfield.nii')
nr_jacobian_3.inputs.ref_file = ref_file
nr_jacobian_3.inputs.trans_file = trans_file
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacL {jac}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jacL.nii.gz')
assert nr_jacobian_3.cmdline == expected_cmd
```

## 8. How To: Bbregister Inputs

- Kind: `tutorial`
- Source: `references/tutorials/bbregister-inputs/bbregister-inputs.md`
- Note: Workflow: test BBRegister inputs

```python
# Workflow
input_map_5_3 = dict(args=dict(argstr='%s'), contrast_type=dict(argstr='--%s', mandatory=True), dof=dict(argstr='--%d'), environ=dict(nohash=True, usedefault=True), epi_mask=dict(argstr='--epi-mask'), fsldof=dict(argstr='--fsl-dof %d'), init=dict(argstr='--init-%s', mandatory=True, xor=['init_reg_file']), init_cost_file=dict(argstr='--initcost %s'), init_reg_file=dict(argstr='--init-reg %s', mandatory=True, xor=['init']), intermediate_file=dict(argstr='--int %s'), out_fsl_file=dict(argstr='--fslmat %s'), out_lta_file=dict(argstr='--lta %s', min_ver='5.2.0'), out_reg_file=dict(argstr='--reg %s', genfile=True), reg_frame=dict(argstr='--frame %d', xor=['reg_middle_frame']), reg_middle_frame=dict(argstr='--mid-frame', xor=['reg_frame']), registered_file=dict(argstr='--o %s'), source_file=dict(argstr='--mov %s', copyfile=False, mandatory=True), spm_nifti=dict(argstr='--spm-nii'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
input_map_6_0 = dict(args=dict(argstr='%s'), contrast_type=dict(argstr='--%s', mandatory=True), dof=dict(argstr='--%d'), environ=dict(nohash=True, usedefault=True), epi_mask=dict(argstr='--epi-mask'), fsldof=dict(argstr='--fsl-dof %d'), init=dict(argstr='--init-%s', xor=['init_reg_file']), init_reg_file=dict(argstr='--init-reg %s', xor=['init']), init_cost_file=dict(argstr='--initcost %s'), intermediate_file=dict(argstr='--int %s'), out_fsl_file=dict(argstr='--fslmat %s'), out_lta_file=dict(argstr='--lta %s', min_ver='5.2.0'), out_reg_file=dict(argstr='--reg %s', genfile=True), reg_frame=dict(argstr='--frame %d', xor=['reg_middle_frame']), reg_middle_frame=dict(argstr='--mid-frame', xor=['reg_frame']), registered_file=dict(argstr='--o %s'), source_file=dict(argstr='--mov %s', copyfile=False, mandatory=True), spm_nifti=dict(argstr='--spm-nii'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict())
instance = BBRegister()
if isinstance(instance.inputs, BBRegisterInputSpec6):
    input_map = input_map_6_0
else:
    input_map = input_map_5_3
for key, metadata in list(input_map.items()):
    for metakey, value in list(metadata.items()):
        assert getattr(instance.inputs.traits()[key], metakey) == value
```

## 9. How To: Dtiprocess Inputs

- Kind: `tutorial`
- Source: `references/tutorials/dtiprocess-inputs/dtiprocess-inputs.md`
- Note: Workflow: test dtiprocess inputs

```python
# Workflow
input_map = dict(DTI_double=dict(argstr='--DTI_double '), RD_output=dict(argstr='--RD_output %s', hash_files=False), affineitk_file=dict(argstr='--affineitk_file %s', extensions=None), args=dict(argstr='%s'), color_fa_output=dict(argstr='--color_fa_output %s', hash_files=False), correction=dict(argstr='--correction %s'), deformation_output=dict(argstr='--deformation_output %s', hash_files=False), dof_file=dict(argstr='--dof_file %s', extensions=None), dti_image=dict(argstr='--dti_image %s', extensions=None), environ=dict(nohash=True, usedefault=True), fa_gradient_output=dict(argstr='--fa_gradient_output %s', hash_files=False), fa_gradmag_output=dict(argstr='--fa_gradmag_output %s', hash_files=False), fa_output=dict(argstr='--fa_output %s', hash_files=False), forward=dict(argstr='--forward %s', extensions=None), frobenius_norm_output=dict(argstr='--frobenius_norm_output %s', hash_files=False), hField=dict(argstr='--hField '), interpolation=dict(argstr='--interpolation %s'), lambda1_output=dict(argstr='--lambda1_output %s', hash_files=False), lambda2_output=dict(argstr='--lambda2_output %s', hash_files=False), lambda3_output=dict(argstr='--lambda3_output %s', hash_files=False), mask=dict(argstr='--mask %s', extensions=None), md_output=dict(argstr='--md_output %s', hash_files=False), negative_eigenvector_output=dict(argstr='--negative_eigenvector_output %s', hash_files=False), newdof_file=dict(argstr='--newdof_file %s', extensions=None), outmask=dict(argstr='--outmask %s', hash_files=False), principal_eigenvector_output=dict(argstr='--principal_eigenvector_output %s', hash_files=False), reorientation=dict(argstr='--reorientation %s'), rot_output=dict(argstr='--rot_output %s', hash_files=False), scalar_float=dict(argstr='--scalar_float '), sigma=dict(argstr='--sigma %f'), verbose=dict(argstr='--verbose '))
inputs = dtiprocess.input_spec()
for key, metadata in list(input_map.items()):
    for metakey, value in list(metadata.items()):
        assert getattr(inputs.traits()[key], metakey) == value
```

## 10. How To: Outputs Removal Wf

- Kind: `tutorial`
- Source: `references/tutorials/outputs-removal-wf/outputs-removal-wf.md`
- Note: Workflow: test outputs removal wf

```python
# Setup
# Fixtures: tmpdir, plugin, remove_unnecessary_outputs, keep_inputs

# Workflow
config.set_default_config()
config.set('execution', 'remove_unnecessary_outputs', remove_unnecessary_outputs)
config.set('execution', 'keep_inputs', keep_inputs)
n1 = pe.Node(niu.Function(output_names=['out_file1', 'out_file2', 'dir'], function=_test_function), name='n1', base_dir=tmpdir.strpath)
n1.inputs.arg1 = 1
n2 = pe.Node(niu.Function(output_names=['out_file1', 'out_file2', 'n'], function=_test_function2), name='n2', base_dir=tmpdir.strpath)
n2.inputs.arg = 2
n3 = pe.Node(niu.Function(output_names=['n'], function=_test_function3), name='n3', base_dir=tmpdir.strpath)
wf = pe.Workflow(name='node_rem_test' + plugin, base_dir=tmpdir.strpath)
wf.connect(n1, 'out_file1', n2, 'in_file')
wf.run(plugin=plugin)
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file2.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file2.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'subdir', 'file4.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file3.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file3.txt')) is not remove_unnecessary_outputs
n4 = pe.Node(UtilsTestInterface(), name='n4', base_dir=tmpdir.strpath)
wf.connect(n2, 'out_file1', n4, 'in_file')

def pick_first(l):
    return l[0]
wf.connect(n4, ('output1', pick_first), n3, 'arg')
rmtree(os.path.join(wf.base_dir, wf.name))
wf.run(plugin=plugin)
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file2.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n4.name, 'file1.txt')) is keep_inputs
```

## 11. How To: Callback Gantt

- Kind: `tutorial`
- Source: `references/tutorials/callback-gantt/callback-gantt.md`
- Note: Workflow: test callback gantt

```python
# Setup
# Fixtures: tmp_path, plugin

# Workflow
import logging
from os import path
from nipype.utils.profiler import log_nodes_cb
from nipype.utils.draw_gantt_chart import generate_gantt_chart
log_filename = tmp_path / 'callback.log'
logger = logging.getLogger('callback')
logger.setLevel(logging.DEBUG)
handler = logging.FileHandler(log_filename)
logger.addHandler(handler)
wf = pe.Workflow(name='test', base_dir=str(tmp_path))
f_node = pe.Node(niu.Function(function=func, input_names=[], output_names=[]), name='f_node')
wf.add_nodes([f_node])
wf.config['execution'] = {'crashdump_dir': wf.base_dir, 'poll_sleep_duration': 2}
plugin_args = {'status_callback': log_nodes_cb}
if plugin != 'Linear':
    plugin_args['n_procs'] = 8
wf.run(plugin=plugin, plugin_args=plugin_args)
with open(log_filename, 'r') as _f:
    loglines = _f.readlines()
first_line = json.loads(loglines[0])
if 'duration' in first_line:
    del first_line['duration']
loglines[0] = f'{json.dumps(first_line)}\n'
loglines.append(loglines[-1])
with open(log_filename, 'w') as _f:
    _f.write(''.join(loglines))
with pytest.warns(Warning):
    generate_gantt_chart(str(log_filename), 1 if plugin == 'Linear' else 8)
assert (tmp_path / 'callback.log.html').exists()
```

## 12. How To: Input Version Missing Error

- Kind: `tutorial`
- Source: `references/tutorials/input-version-missing-error/input-version-missing-error.md`
- Note: Workflow: test input version missing error

```python
# Setup
# Fixtures: caplog

# Workflow
from nipype import config

class DerivedInterface(nib.BaseInterface):

    class input_spec(nib.TraitedSpec):
        foo = nib.traits.Int(min_ver='0.9')
        bar = nib.traits.Int(max_ver='0.9')
    _version = 'misparsed-garbage'
obj1 = DerivedInterface(foo=1)
obj2 = DerivedInterface(bar=1)
with caplog.at_level(logging.WARNING, logger='nipype.interface'):
    with mock.patch.object(config, 'getboolean', return_value=True):
        with pytest.raises(ValueError):
            obj1._check_version_requirements(obj1.inputs)
        with pytest.raises(ValueError):
            obj2._check_version_requirements(obj2.inputs)
assert len(caplog.records) == 2
```

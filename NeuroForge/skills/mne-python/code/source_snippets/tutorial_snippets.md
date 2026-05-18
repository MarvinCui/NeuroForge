# mne-python Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Plot Evoked Field Notebook

- Kind: `tutorial`
- Source: `references/tutorials/plot-evoked-field-notebook/plot-evoked-field-notebook.md`
- Note: Workflow: Test plotting the evoked field inside a notebook.

```python
# Setup
# Fixtures: renderer_notebook, nbexec

# Workflow
'Test plotting the evoked field inside a notebook.'
import pytest
from mne import make_field_map, read_evokeds
from mne.datasets import testing
from mne.viz import Brain, EvokedField, Figure3D, set_3d_backend
set_3d_backend('notebook')
with pytest.MonkeyPatch().context() as mp:
    mp.delenv('_MNE_FAKE_HOME_DIR')
    data_path = testing.data_path(download=False)
evoked_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-ave.fif'
trans_fname = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif'
subjects_dir = data_path / 'subjects'
evoked = read_evokeds(evoked_fname, condition='Left Auditory', baseline=(-0.2, 0.0))
evoked.pick(evoked.ch_names[::10])
with pytest.warns(RuntimeWarning, match='projection'):
    maps = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, n_jobs=None, ch_type='meg')
fig = evoked.plot_field(maps, time_viewer=True)
assert isinstance(fig, EvokedField)
fig = evoked.plot_field(maps, time_viewer=False)
assert isinstance(fig, Figure3D)
brain = Brain('fsaverage', 'lh', 'inflated', subjects_dir=subjects_dir)
with pytest.raises(NotImplementedError):
    fig = evoked.plot_field(maps, time=0.1, fig=brain)
```

## 2. How To: Xdawn Decoding Performance

- Kind: `tutorial`
- Source: `references/tutorials/xdawn-decoding-performance/xdawn-decoding-performance.md`
- Note: Workflow: Test decoding performance and extracted pattern on synthetic data.

```python
# Workflow
'Test decoding performance and extracted pattern on synthetic data.'
pytest.importorskip('sklearn')
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
from sklearn.model_selection import KFold
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import MinMaxScaler
from mne.decoding import Vectorizer
n_xdawn_comps = 3
expected_accuracy = 0.98
epochs, mixing_mat = _simulate_erplike_mixed_data(n_epochs=100)
y = epochs.events[:, 2]
xdawn_pipe = make_pipeline(Xdawn(n_components=n_xdawn_comps), Vectorizer(), MinMaxScaler(), LogisticRegression(solver='liblinear'))
xdawn_trans_pipe = make_pipeline(XdawnTransformer(n_components=n_xdawn_comps), Vectorizer(), MinMaxScaler(), LogisticRegression(solver='liblinear'))
cv = KFold(n_splits=3, shuffle=False)
for pipe, X in ((xdawn_pipe, epochs), (xdawn_trans_pipe, epochs.get_data(copy=False))):
    predictions = np.empty_like(y, dtype=float)
    for train, test in cv.split(X, y):
        pipe.fit(X[train], y[train])
        predictions[test] = pipe.predict(X[test])
    cv_accuracy_xdawn = accuracy_score(y, predictions)
    assert_allclose(cv_accuracy_xdawn, expected_accuracy, atol=0.01)
    fitted_xdawn = pipe.steps[0][1]
    if isinstance(fitted_xdawn, Xdawn):
        relev_patterns = np.concatenate([comps[[0]] for comps in fitted_xdawn.patterns_.values()])
    else:
        pick_patterns = fitted_xdawn._subset_multi_components(name='patterns')
        relev_patterns = pick_patterns[::n_xdawn_comps]
    for i in range(len(relev_patterns)):
        r, _ = stats.pearsonr(relev_patterns[i, :], mixing_mat[0, :])
        assert np.abs(r) > 0.99
```

## 3. How To: Morph Stc Sparse

- Kind: `tutorial`
- Source: `references/tutorials/morph-stc-sparse/morph-stc-sparse.md`
- Note: Workflow: Test morphing stc with sparse=True.

```python
# Workflow
'Test morphing stc with sparse=True.'
subject_from = 'sample'
subject_to = 'fsaverage'
stc_from = read_source_estimate(fname_smorph, subject='sample')
stc_from.vertices[0] = stc_from.vertices[0][[100, 500]]
stc_from.vertices[1] = stc_from.vertices[1][[200]]
stc_from._data = stc_from._data[:3]
stc_to_sparse = compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=None, sparse=True, subjects_dir=subjects_dir).apply(stc_from)
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
assert len(stc_from.lh_vertno) == len(stc_to_sparse.lh_vertno)
assert stc_to_sparse.subject == subject_to
assert stc_from.tmin == stc_from.tmin
assert stc_from.tstep == stc_from.tstep
stc_from.vertices[0] = np.array([], dtype=np.int64)
stc_from._data = stc_from._data[:1]
stc_to_sparse = compute_source_morph(stc_from, subject_from, subject_to, spacing=None, sparse=True, subjects_dir=subjects_dir).apply(stc_from)
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
assert len(stc_from.lh_vertno) == len(stc_to_sparse.lh_vertno)
assert stc_to_sparse.subject == subject_to
assert stc_from.tmin == stc_from.tmin
assert stc_from.tstep == stc_from.tstep
with pytest.raises(ValueError, match='spacing must be set to None'):
    compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=5, sparse=True, subjects_dir=subjects_dir)
with pytest.raises(ValueError, match='xhemi=True can only be used with'):
    compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=None, sparse=True, xhemi=True, subjects_dir=subjects_dir)
```

## 4. How To: Add Channels

- Kind: `tutorial`
- Source: `references/tutorials/add-channels/add-channels.md`
- Note: Workflow: Test tfr splitting / re-appending channel types.

```python
# Workflow
'Test tfr splitting / re-appending channel types.'
data = np.zeros((6, 2, 3))
times = np.array([0.1, 0.2, 0.3])
freqs = np.array([0.1, 0.2])
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003', 'EEG 001', 'EEG 002', 'STIM 001'], 1000.0, ['mag', 'mag', 'mag', 'eeg', 'eeg', 'stim'])
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
tfr_eeg = tfr.copy().pick(picks='eeg')
tfr_meg = tfr.copy().pick(picks='meg')
tfr_stim = tfr.copy().pick(picks='stim')
tfr_eeg_meg = tfr.copy().pick(picks=['meg', 'eeg'])
tfr_new = tfr_meg.copy().add_channels([tfr_eeg, tfr_stim])
assert all((ch in tfr_new.ch_names for ch in tfr_stim.ch_names + tfr_meg.ch_names))
tfr_new = tfr_meg.copy().add_channels([tfr_eeg])
have_all = all((ch in tfr_new.ch_names for ch in tfr.ch_names if ch != 'STIM 001'))
assert have_all
assert_array_equal(tfr_new.data, tfr_eeg_meg.data)
assert all((ch not in tfr_new.ch_names for ch in tfr_stim.ch_names))
tfr_badsf = tfr_eeg.copy()
with tfr_badsf.info._unlock():
    tfr_badsf.info['sfreq'] = 3.1415927
tfr_eeg = tfr_eeg.crop(0.1, 0.1)
pytest.raises(RuntimeError, tfr_meg.add_channels, [tfr_badsf])
pytest.raises(ValueError, tfr_meg.add_channels, [tfr_eeg])
pytest.raises(ValueError, tfr_meg.add_channels, [tfr_meg])
pytest.raises(TypeError, tfr_meg.add_channels, tfr_badsf)
tfr1 = EpochsTFRArray(info=mne.create_info(['EEG 001'], 1000, 'eeg'), data=np.zeros((5, 1, 2, 3)), times=[0.1, 0.2, 0.3], freqs=[0.1, 0.2])
tfr2 = EpochsTFRArray(info=mne.create_info(['EEG 002', 'EEG 003'], 1000, 'eeg'), data=np.zeros((5, 2, 2, 3)), times=[0.1, 0.2, 0.3], freqs=[0.1, 0.2])
tfr1.add_channels([tfr2])
assert tfr1.ch_names == ['EEG 001', 'EEG 002', 'EEG 003']
assert tfr1.data.shape == (5, 3, 2, 3)
```

## 5. How To: Source Psd Epochs

- Kind: `tutorial`
- Source: `references/tutorials/source-psd-epochs/source-psd-epochs.md`
- Note: Workflow: Test multi-taper source PSD computation in label from epochs.

```python
# Setup
# Fixtures: method

# Workflow
'Test multi-taper source PSD computation in label from epochs.'
raw = read_raw_fif(fname_data)
inverse_operator = read_inverse_operator(fname_inv)
label = read_label(fname_label)
label2 = read_label(fname_label2)
event_id, tmin, tmax = (1, -0.2, 0.5)
lambda2 = 1.0 / 9.0
bandwidth = 8.0
fmin, fmax = (0, 100)
picks = pick_types(raw.info, meg=True, eeg=False, stim=True, ecg=True, eog=True, include=['STI 014'], exclude='bads')
reject = dict(grad=4e-10, mag=4e-12, eog=0.00015)
events = find_events(raw, stim_channel='STI 014')
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), reject=reject)
epochs.drop_bad()
one_epochs = epochs[:1]
inv = prepare_inverse_operator(inverse_operator, nave=1, lambda2=1.0 / 9.0, method='dSPM')
stc_psd = compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=bandwidth, fmin=fmin, fmax=fmax, prepared=True)[0]
stcs = compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=bandwidth, fmin=fmin, fmax=fmax, return_generator=True, prepared=True)
for stc in stcs:
    stc_psd_gen = stc
assert_allclose(stc_psd.data, stc_psd_gen.data, atol=1e-07)
stc = apply_inverse_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, prepared=True)[0]
sfreq = epochs.info['sfreq']
psd, freqs = psd_array_multitaper(stc.data, sfreq=sfreq, bandwidth=bandwidth, fmin=fmin, fmax=fmax)
assert_allclose(psd, stc_psd.data, atol=1e-07)
assert_allclose(freqs, stc_psd.times)
with pytest.raises(ValueError, match='use a value of at least'):
    compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=0.01, low_bias=True, fmin=fmin, fmax=fmax, return_generator=False, prepared=True)
with pytest.raises(TypeError, match='Label or BiHemi'):
    compute_source_psd_epochs(one_epochs, inv, label=[label, label2])
```

## 6. How To: Make Forward Solution Sphere

- Kind: `tutorial`
- Source: `references/tutorials/make-forward-solution-sphere/make-forward-solution-sphere.md`
- Note: Workflow: Test making a forward solution with a sphere model.

```python
# Setup
# Fixtures: tmp_path, fname_src_small

# Workflow
'Test making a forward solution with a sphere model.'
out_name = tmp_path / 'tmp-fwd.fif'
run_subprocess(['mne_forward_solution', '--meg', '--eeg', '--meas', fname_raw, '--src', fname_src_small, '--mri', fname_trans, '--fwd', out_name])
fwd = read_forward_solution(out_name)
sphere = make_sphere_model(head_radius=0.1, relative_radii=(0.95, 0.97, 0.98, 1), verbose=True)
src = read_source_spaces(fname_src_small)
fwd_py = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=True, verbose=True)
_compare_forwards(fwd, fwd_py, 366, 108, meg_rtol=0.5, meg_atol=1e-06, eeg_rtol=0.5, eeg_atol=0.5)
for meg, eeg in zip([True, False], [False, True]):
    fwd_ = pick_types_forward(fwd, meg=meg, eeg=eeg)
    fwd_py_ = pick_types_forward(fwd, meg=meg, eeg=eeg)
    assert_allclose(np.corrcoef(fwd_['sol']['data'].ravel(), fwd_py_['sol']['data'].ravel())[0, 1], 1.0, rtol=0.001)
assert len(sphere['layers']) == 4
fwd = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
sphere_1 = make_sphere_model(head_radius=None)
assert len(sphere_1['layers']) == 0
assert_array_equal(sphere['r0'], sphere_1['r0'])
fwd_1 = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
_compare_forwards(fwd, fwd_1, 306, 108, meg_rtol=1e-12, meg_atol=1e-12)
sphere = make_sphere_model(head_radius=None)
with pytest.raises(RuntimeError, match='zero shells.*EEG'):
    make_forward_solution(fname_raw, fname_trans, src, sphere)
custom_trans = Transform('head', 'mri')
custom_trans['trans'][0, 3] = 0.05
sphere = make_sphere_model()
fwd = make_forward_solution(fname_raw, custom_trans, src, sphere)
assert fwd['mri_head_t']['trans'][0, 3] == -0.05
```

## 7. How To: Esss

- Kind: `tutorial`
- Source: `references/tutorials/esss/esss.md`
- Note: Workflow: Test extended-basis SSS.

```python
# Setup
# Fixtures: regularize, bads

# Workflow
'Test extended-basis SSS.'
raw_erm = read_crop(erm_fname).load_data().pick('meg')
raw_erm.info['bads'] = bads
proj_sss = mne.compute_proj_raw(raw_erm, meg='combined', verbose='error', n_mag=15, n_grad=15)
good_info = pick_info(raw_erm.info, pick_types(raw_erm.info, meg=True))
S_tot = _trans_sss_basis(dict(int_order=0, ext_order=3, origin=(0.0, 0.0, 0.0)), all_coils=_prep_mf_coils(good_info), coil_scale=1.0, trans=None)
assert S_tot.shape[-1] == len(proj_sss)
for a, b in zip(proj_sss, S_tot.T):
    a['data']['data'][:] = b
with catch_logging() as log:
    raw_sss = maxwell_filter(raw_erm, coord_frame='meg', regularize=regularize, verbose=True)
log = log.getvalue()
assert 'xtend' not in log
with catch_logging() as log:
    raw_sss_2 = maxwell_filter(raw_erm, coord_frame='meg', regularize=regularize, ext_order=0, extended_proj=proj_sss, verbose=True)
log = log.getvalue()
assert 'Extending external SSS basis using 15 projection' in log
assert_allclose(raw_sss_2._data, raw_sss._data, atol=1e-20)
raw_erm.info['bads'] = raw_erm.info['bads'] + ['MEG0112']
maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
proj_sss = proj_sss[:2]
proj_sss[0]['data']['col_names'] = proj_sss[0]['data']['col_names'][:-1]
with pytest.raises(ValueError, match='were missing'):
    maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
proj_sss[0] = 1.0
with pytest.raises(TypeError, match='extended_proj\\[0\\] must be an inst'):
    maxwell_filter(raw_erm, coord_frame='meg', extended_proj=proj_sss)
with pytest.raises(TypeError, match='extended_proj must be an inst'):
    maxwell_filter(raw_erm, coord_frame='meg', extended_proj=1.0)
```

## 8. How To: Simulate Sparse Stc

- Kind: `tutorial`
- Source: `references/tutorials/simulate-sparse-stc/simulate-sparse-stc.md`
- Note: Workflow: Test generation of sparse source estimate.

```python
# Setup
# Fixtures: _get_fwd_labels

# Workflow
'Test generation of sparse source estimate.'
pytest.importorskip('nibabel')
fwd, labels = _get_fwd_labels
n_times = 10
tmin = 0
tstep = 0.001
times = np.arange(n_times, dtype=np.float64) * tstep + tmin
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(labels), times, labels=labels, location='center', subject='sample', subjects_dir=subjects_dir)
mylabels = []
for label in labels:
    this_label = label.copy()
    this_label.values.fill(1.0)
    mylabels.append(this_label)
for location in ('random', 'center'):
    random_state = 0 if location == 'random' else None
    stc_1 = simulate_sparse_stc(fwd['src'], len(mylabels), times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
    assert_equal(stc_1.subject, 'sample')
    assert stc_1.data.shape[0] == len(mylabels)
    assert stc_1.data.shape[1] == n_times
    stc_2 = simulate_sparse_stc(fwd['src'], len(mylabels), times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
    assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
    assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='center', subject='foo', subjects_dir=subjects_dir)
del fwd['src'][0]['subject_his_id']
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='center', subjects_dir=subjects_dir)
fwd['src'][0]['subject_his_id'] = 'sample'
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='foo')
err_str = 'Number of labels'
with pytest.raises(ValueError, match=err_str):
    simulate_sparse_stc(fwd['src'], len(mylabels) + 1, times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
```

## 9. How To: Check Sphere

- Kind: `tutorial`
- Source: `references/tutorials/check-sphere/check-sphere.md`
- Note: Workflow: Test the _check_sphere function.

```python
# Workflow
'Test the _check_sphere function.'
info = mne.io.read_info(fname_raw)
info_eeglab = create_info(ch_names=['Fpz', 'Oz', 'T7', 'T8'], sfreq=100, ch_types='eeg')
info_eeglab.set_montage('biosemi64')
assert_equal(_check_sphere(None), [0, 0, 0, 0.095])
assert not np.any(_check_sphere(None, info) == 0)
assert_equal(_check_sphere([1, 2, 3, 4], info), [1, 2, 3, 4])
assert_equal(_check_sphere([1, 2, 3, 4], info=None), [1, 2, 3, 4])
with pytest.raises(ValueError, match='1D array of shape \\(4,\\)'):
    _check_sphere([1, 2, 3], info)
sphere_auto = _check_sphere('auto', info)
sphere_eeglab = _check_sphere('eeglab', info_eeglab)
sphere_extra = _check_sphere('extra', info)
sphere_eeg = _check_sphere('eeg', info)
with _record_warnings(), pytest.warns(RuntimeWarning, match='may be inaccurate'):
    sphere_hpi = _check_sphere('hpi', info)
sphere_all = _check_sphere(['extra', 'eeg', 'cardinal', 'hpi'], info)
assert_allclose(sphere_auto, sphere_extra)
assert not np.allclose(sphere_auto, sphere_eeglab, rtol=0.0001, atol=0.0001)
assert not np.allclose(sphere_auto, sphere_eeg, rtol=0.0001, atol=0.0001)
assert not np.allclose(sphere_auto, sphere_hpi, rtol=0.0001, atol=0.0001)
assert not np.allclose(sphere_auto, sphere_all, rtol=0.0001, atol=0.0001)
with pytest.raises(TypeError, match='Item must be an instance of Info'):
    _check_sphere('auto', info=None)
info_trunc = info.copy()
with info_trunc._unlock():
    info_trunc['dig'] = info_trunc['dig'][:20]
with _record_warnings(), pytest.warns(RuntimeWarning, match='may be inaccurate'):
    _check_sphere('auto', info_trunc)
with mne.use_log_level('error'):
    _check_sphere('auto', info_trunc)
```

## 10. How To: Plot Ctf

- Kind: `tutorial`
- Source: `references/tutorials/plot-ctf/plot-ctf.md`
- Note: Workflow: Test plotting of CTF evoked.

```python
# Workflow
'Test plotting of CTF evoked.'
raw = mne.io.read_raw_ctf(ctf_fname, preload=True)
events = np.array([[200, 0, 1]])
event_id = 1
tmin, tmax = (-0.1, 0.5)
picks = mne.pick_types(raw.info, meg=True, stim=True, eog=True, ref_meg=True, exclude='bads')[::20]
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, proj=True, picks=picks, preload=True, decim=10, verbose='error')
evoked = epochs.average()
evoked.plot_joint(times=[0.1])
with pytest.raises(TypeError, match='ylim must be an instance of dict or None'):
    evoked.plot_joint(times=[0.1], ts_args=dict(ylim=(-10, 10)))
mne.viz.plot_compare_evokeds([evoked, evoked])
times = [0.1, 0.2, 0.3]
fig = plt.figure()
gs = gridspec.GridSpec(3, 7, hspace=0.5, top=0.8, figure=fig)
topo_axes = [fig.add_subplot(gs[0, idx * 2:(idx + 1) * 2]) for idx in range(len(times))]
topo_axes.append(fig.add_subplot(gs[0, -1]))
ts_axis = fig.add_subplot(gs[1:, 1:-1])

def get_axes_midpoints(axes):
    midpoints = list()
    for ax in axes[:-1]:
        pos = ax.get_position()
        midpoints.append([pos.x0 + pos.width * 0.5, pos.y0 + pos.height * 0.5])
    return np.array(midpoints)
midpoints_before = get_axes_midpoints(topo_axes)
evoked.plot_joint(times=times, ts_args={'axes': ts_axis}, topomap_args={'axes': topo_axes}, title=None)
midpoints_after = get_axes_midpoints(topo_axes)
assert (np.linalg.norm(midpoints_before - midpoints_after) < 0.1).all()
```

## 11. How To: Plot Volume Source Estimates Morph

- Kind: `tutorial`
- Source: `references/tutorials/plot-volume-source-estimates-morph/plot-volume-source-estimates-morph.md`
- Note: Workflow: Test interactive plotting of volume source estimates with morph.

```python
# Workflow
'Test interactive plotting of volume source estimates with morph.'
pytest.importorskip('nibabel')
pytest.importorskip('dipy')
pytest.importorskip('nilearn')
forward = read_forward_solution(fwd_fname)
sample_src = forward['src']
vertices = [s['vertno'] for s in sample_src]
n_verts = sum((len(v) for v in vertices))
n_time = 2
data = np.random.RandomState(0).rand(n_verts, n_time)
stc = VolSourceEstimate(data, vertices, 1, 1)
sample_src[0]['subject_his_id'] = 'sample'
morph = compute_source_morph(sample_src, 'sample', 'fsaverage', zooms=5, subjects_dir=subjects_dir)
initial_pos = (-0.05, -0.01, -0.006)
with _record_warnings():
    with catch_logging() as log:
        stc.plot(morph, subjects_dir=subjects_dir, mode='glass_brain', initial_pos=initial_pos, verbose=True)
log = log.getvalue()
assert 't = 1.000 s' in log
assert '(-52.0, -8.0, -7.0) mm' in log
with pytest.raises(ValueError, match='Allowed values are'):
    stc.plot(sample_src, 'sample', subjects_dir, mode='abcd')
vertices.append([])
surface_stc = SourceEstimate(data, vertices, 1, 1)
with pytest.raises(TypeError, match='an instance of VolSourceEstimate'):
    plot_volume_source_estimates(surface_stc, sample_src, 'sample', subjects_dir)
with pytest.raises(ValueError, match='Negative colormap limits'):
    stc.plot(sample_src, 'sample', subjects_dir, clim=dict(lims=[-1, 2, 3], kind='value'))
```

## 12. How To: Cuda Fir

- Kind: `tutorial`
- Source: `references/tutorials/cuda-fir/cuda-fir.md`
- Note: Workflow: Test CUDA-based filtering.

```python
# Workflow
'Test CUDA-based filtering.'
rng = np.random.RandomState(0)
sfreq = 500
sig_len_secs = 20
a = rng.randn(sig_len_secs * sfreq)
kwargs = dict(fir_design='firwin')
with catch_logging() as log_file:
    for fl in ['auto', '10s', 2048]:
        args = [a, sfreq, 4, 8, None, fl, 1.0, 1.0]
        bp = filter_data(*args, **kwargs)
        bp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(bp, bp_c, 12)
        args = [a, sfreq, 8 + 1.0, 4 - 1.0, None, fl, 1.0, 1.0]
        bs = filter_data(*args, **kwargs)
        bs_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(bs, bs_c, 12)
        args = [a, sfreq, None, 8, None, fl, 1.0]
        lp = filter_data(*args, **kwargs)
        lp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(lp, lp_c, 12)
        args = [lp, sfreq, 4, None, None, fl, 1.0]
        hp = filter_data(*args, **kwargs)
        hp_c = filter_data(*args, n_jobs='cuda', verbose='info', **kwargs)
        assert_array_almost_equal(hp, hp_c, 12)
out = log_file.getvalue().split('\n')[:-1]
from mne.cuda import _cuda_capable
tot = 12 if _cuda_capable else 0
assert sum(['Using CUDA for FFT FIR filtering' in o for o in out]) == tot
if not _cuda_capable:
    pytest.skip('CUDA not enabled')
```

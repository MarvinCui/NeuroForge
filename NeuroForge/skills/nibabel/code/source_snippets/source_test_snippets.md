# nibabel Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_rst_table

- Kind: `test-workflow`
- Source: `nibabel/nibabel/tests/test_rstutils.py:9`
- Note: Workflow: test rst table

```python
R, C = (3, 4)
cell_values = np.arange(R * C).reshape((R, C))
assert rst_table(cell_values) == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
assert rst_table(cell_values, ['a', 'b', 'c']) == '+---+--------+--------+--------+--------+\n|   | col[0] | col[1] | col[2] | col[3] |\n+===+========+========+========+========+\n| a |  0.00  |  1.00  |  2.00  |  3.00  |\n| b |  4.00  |  5.00  |  6.00  |  7.00  |\n| c |  8.00  |  9.00  | 10.00  | 11.00  |\n+---+--------+--------+--------+--------+'
with pytest.raises(ValueError):
    rst_table(cell_values, ['a', 'b'])
with pytest.raises(ValueError):
    rst_table(cell_values, ['a', 'b', 'c', 'd'])
assert rst_table(cell_values, None, ['1', '2', '3', '4']) == '+--------+-------+-------+-------+-------+\n|        |   1   |   2   |   3   |   4   |\n+========+=======+=======+=======+=======+\n| row[0] |  0.00 |  1.00 |  2.00 |  3.00 |\n| row[1] |  4.00 |  5.00 |  6.00 |  7.00 |\n| row[2] |  8.00 |  9.00 | 10.00 | 11.00 |\n+--------+-------+-------+-------+-------+'
with pytest.raises(ValueError):
    rst_table(cell_values, None, ['1', '2', '3'])
with pytest.raises(ValueError):
    rst_table(cell_values, None, list('12345'))
assert rst_table(cell_values, title='A title') == '*******\nA title\n*******\n\n+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
assert rst_table(cell_values, val_fmt='{0}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0      | 1      | 2      | 3      |\n| row[1] | 4      | 5      | 6      | 7      |\n| row[2] | 8      | 9      | 10     | 11     |\n+--------+--------+--------+--------+--------+'
cell_values_back = np.arange(R * C)[::-1].reshape((R, C))
cell_3d = np.dstack((cell_values, cell_values_back))
assert rst_table(cell_3d, val_fmt='{0[0]}-{0[1]}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0-11   | 1-10   | 2-9    | 3-8    |\n| row[1] | 4-7    | 5-6    | 6-5    | 7-4    |\n| row[2] | 8-3    | 9-2    | 10-1   | 11-0   |\n+--------+--------+--------+--------+--------+'
formats = dict(down='!', along='_', thick_long='~', cross='%', title_heading='#')
assert rst_table(cell_values, title='A title', format_chars=formats) == '#######\nA title\n#######\n\n%________%________%________%________%________%\n!        ! col[0] ! col[1] ! col[2] ! col[3] !\n%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%\n! row[0] !  0.00  !  1.00  !  2.00  !  3.00  !\n! row[1] !  4.00  !  5.00  !  6.00  !  7.00  !\n! row[2] !  8.00  !  9.00  ! 10.00  ! 11.00  !\n%________%________%________%________%________%'
formats['funny_value'] = '!'
with pytest.raises(ValueError):
    rst_table(cell_values, title='A title', format_chars=formats)
```

## 2. test_extend

- Kind: `test-workflow`
- Source: `nibabel/nibabel/streamlines/tests/test_tractogram.py:271`
- Note: Workflow: test extend

```python
sdict = PerArrayDict(len(DATA['tractogram']), DATA['data_per_streamline'])
new_data = {'mean_curvature': 2 * np.array(DATA['mean_curvature']), 'mean_torsion': 3 * np.array(DATA['mean_torsion']), 'mean_colors': 4 * np.array(DATA['mean_colors']), 'clusters_labels': 5 * np.array(DATA['clusters_labels'], dtype=object)}
sdict2 = PerArrayDict(len(DATA['tractogram']), new_data)
sdict.extend(sdict2)
assert len(sdict) == len(sdict2)
for k in DATA['tractogram'].data_per_streamline:
    assert_arrays_equal(sdict[k][:len(DATA['tractogram'])], DATA['tractogram'].data_per_streamline[k])
    assert_arrays_equal(sdict[k][len(DATA['tractogram']):], new_data[k])
sdict_orig = copy.deepcopy(sdict)
sdict.extend(PerArrayDict())
for k in sdict_orig.keys():
    assert_arrays_equal(sdict[k], sdict_orig[k])
new_data = {'mean_curvature': 2 * np.array(DATA['mean_curvature']), 'mean_torsion': 3 * np.array(DATA['mean_torsion']), 'mean_colors': 4 * np.array(DATA['mean_colors']), 'clusters_labels': 5 * np.array(DATA['clusters_labels'], dtype=object), 'other': 6 * np.array(DATA['mean_colors'])}
sdict2 = PerArrayDict(len(DATA['tractogram']), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
new_data = {'mean_curvature': 2 * np.array(DATA['mean_curvature']), 'mean_torsion': 3 * np.array(DATA['mean_torsion']), 'other': 4 * np.array(DATA['mean_colors'])}
sdict2 = PerArrayDict(len(DATA['tractogram']), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
new_data = {'mean_curvature': 2 * np.array(DATA['mean_curvature']), 'mean_torsion': 3 * np.array(DATA['mean_torsion']), 'mean_colors': 4 * np.array(DATA['mean_torsion']), 'clusters_labels': 5 * np.array(DATA['clusters_labels'], dtype=object)}
sdict2 = PerArrayDict(len(DATA['tractogram']), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
```

## 3. test_extend

- Kind: `test-workflow`
- Source: `nibabel/nibabel/streamlines/tests/test_tractogram.py:381`
- Note: Workflow: test extend

```python
total_nb_rows = DATA['tractogram'].streamlines.total_nb_rows
sdict = PerArraySequenceDict(total_nb_rows, DATA['data_per_point'])
list_nb_points = [2, 7, 4]
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:]}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
sdict.extend(sdict2)
assert len(sdict) == len(sdict2)
for k in DATA['tractogram'].data_per_point:
    assert_arrays_equal(sdict[k][:len(DATA['tractogram'])], DATA['tractogram'].data_per_point[k])
    assert_arrays_equal(sdict[k][len(DATA['tractogram']):], new_data[k])
sdict_orig = copy.deepcopy(sdict)
sdict.extend(PerArraySequenceDict())
for k in sdict_orig.keys():
    assert_arrays_equal(sdict[k], sdict_orig[k])
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:], 'other': (7,)}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'other': DATA['fa'][0].shape[1:]}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:] + (3,)}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
```

## 4. test_read_geometry

- Kind: `test-workflow`
- Source: `nibabel/nibabel/cifti2/tests/test_cifti2io_header.py:203`
- Note: Workflow: test read geometry

```python
img = ci.Cifti2Image.from_filename(DATA_FILE6)
geometry_mapping = img.header.matrix.get_index_map(1)
expected_geometry = [('CIFTI_STRUCTURE_CORTEX_LEFT', 29696, 0, 32491), ('CIFTI_STRUCTURE_CORTEX_RIGHT', 29716, 0, 32491), ('CIFTI_STRUCTURE_ACCUMBENS_LEFT', 135, [49, 66, 28], [48, 72, 35]), ('CIFTI_STRUCTURE_ACCUMBENS_RIGHT', 140, [40, 66, 29], [43, 66, 36]), ('CIFTI_STRUCTURE_AMYGDALA_LEFT', 315, [55, 61, 21], [56, 58, 31]), ('CIFTI_STRUCTURE_AMYGDALA_RIGHT', 332, [34, 62, 20], [36, 61, 31]), ('CIFTI_STRUCTURE_BRAIN_STEM', 3472, [42, 41, 0], [46, 50, 36]), ('CIFTI_STRUCTURE_CAUDATE_LEFT', 728, [50, 72, 32], [53, 60, 49]), ('CIFTI_STRUCTURE_CAUDATE_RIGHT', 755, [40, 68, 33], [37, 62, 49]), ('CIFTI_STRUCTURE_CEREBELLUM_LEFT', 8709, [49, 35, 4], [46, 37, 37]), ('CIFTI_STRUCTURE_CEREBELLUM_RIGHT', 9144, [38, 35, 4], [44, 38, 36]), ('CIFTI_STRUCTURE_DIENCEPHALON_VENTRAL_LEFT', 706, [52, 53, 26], [56, 49, 35]), ('CIFTI_STRUCTURE_DIENCEPHALON_VENTRAL_RIGHT', 712, [39, 54, 26], [35, 49, 36]), ('CIFTI_STRUCTURE_HIPPOCAMPUS_LEFT', 764, [55, 60, 21], [54, 44, 39]), ('CIFTI_STRUCTURE_HIPPOCAMPUS_RIGHT', 795, [33, 60, 21], [38, 45, 39]), ('CIFTI_STRUCTURE_PALLIDUM_LEFT', 297, [56, 59, 32], [55, 61, 39]), ('CIFTI_STRUCTURE_PALLIDUM_RIGHT', 260, [36, 62, 32], [35, 62, 39]), ('CIFTI_STRUCTURE_PUTAMEN_LEFT', 1060, [51, 66, 28], [58, 64, 43]), ('CIFTI_STRUCTURE_PUTAMEN_RIGHT', 1010, [34, 66, 29], [31, 62, 43]), ('CIFTI_STRUCTURE_THALAMUS_LEFT', 1288, [55, 47, 33], [52, 53, 46]), ('CIFTI_STRUCTURE_THALAMUS_RIGHT', 1248, [32, 47, 34], [38, 55, 46])]
current_index = 0
for from_file, expected in zip(geometry_mapping.brain_models, expected_geometry):
    assert from_file.model_type in ('CIFTI_MODEL_TYPE_SURFACE', 'CIFTI_MODEL_TYPE_VOXELS')
    assert from_file.brain_structure == expected[0]
    assert from_file.index_offset == current_index
    assert from_file.index_count == expected[1]
    current_index += from_file.index_count
    if from_file.model_type == 'CIFTI_MODEL_TYPE_SURFACE':
        assert from_file.voxel_indices_ijk is None
        assert len(from_file.vertex_indices) == expected[1]
        assert from_file.vertex_indices[0] == expected[2]
        assert from_file.vertex_indices[-1] == expected[3]
        assert from_file.surface_number_of_vertices == 32492
    else:
        assert from_file.vertex_indices is None
        assert from_file.surface_number_of_vertices is None
        assert len(from_file.voxel_indices_ijk) == expected[1]
        assert from_file.voxel_indices_ijk[0] == expected[2]
        assert from_file.voxel_indices_ijk[-1] == expected[3]
assert current_index == img.shape[1]
expected_affine = [[-2, 0, 0, 90], [0, 2, 0, -126], [0, 0, 2, -72], [0, 0, 0, 1]]
expected_dimensions = (91, 109, 91)
assert np.array_equal(geometry_mapping.volume.transformation_matrix_voxel_indices_ijk_to_xyz.matrix, expected_affine)
assert geometry_mapping.volume.volume_dimensions == expected_dimensions
```

## 5. test_slope_inter

- Kind: `test-workflow`
- Source: `nibabel/nibabel/tests/test_nifti1.py:142`
- Note: Workflow: test slope inter

```python
hdr = self.header_class()
nan, inf, minf = (np.nan, np.inf, -np.inf)
HDE = HeaderDataError
assert hdr.get_slope_inter() == (1.0, 0.0)
for in_tup, exp_err, out_tup, raw_values in (((None, None), None, (None, None), (nan, nan)), ((nan, None), None, (None, None), (nan, nan)), ((None, nan), None, (None, None), (nan, nan)), ((nan, nan), None, (None, None), (nan, nan)), ((None, 0), HDE, (None, None), (nan, 0)), ((nan, 0), HDE, (None, None), (nan, 0)), ((1, None), HDE, (None, None), (1, nan)), ((1, nan), HDE, (None, None), (1, nan)), ((0, 0), HDE, (None, None), (0, 0)), ((0, None), HDE, (None, None), (0, nan)), ((0, nan), HDE, (None, None), (0, nan)), ((0, inf), HDE, (None, None), (0, inf)), ((0, minf), HDE, (None, None), (0, minf)), ((inf, 0), HDE, (None, None), (inf, 0)), ((inf, None), HDE, (None, None), (inf, nan)), ((inf, nan), HDE, (None, None), (inf, nan)), ((inf, inf), HDE, (None, None), (inf, inf)), ((inf, minf), HDE, (None, None), (inf, minf)), ((minf, 0), HDE, (None, None), (minf, 0)), ((minf, None), HDE, (None, None), (minf, nan)), ((minf, nan), HDE, (None, None), (minf, nan)), ((minf, inf), HDE, (None, None), (minf, inf)), ((minf, minf), HDE, (None, None), (minf, minf)), ((2, None), HDE, HDE, (2, nan)), ((2, nan), HDE, HDE, (2, nan)), ((2, inf), HDE, HDE, (2, inf)), ((2, minf), HDE, HDE, (2, minf)), ((2, 0), None, (2, 0), (2, 0)), ((2, 1), None, (2, 1), (2, 1))):
    hdr = self.header_class()
    if not exp_err is None:
        with pytest.raises(exp_err):
            hdr.set_slope_inter(*in_tup)
        in_list = [v if not v is None else np.nan for v in in_tup]
        hdr['scl_slope'], hdr['scl_inter'] = in_list
    else:
        hdr.set_slope_inter(*in_tup)
        if isinstance(out_tup, Exception):
            with pytest.raises(out_tup):
                hdr.get_slope_inter()
        else:
            assert hdr.get_slope_inter() == out_tup
            hdr = self.header_class.from_header(hdr, check=True)
            assert hdr.get_slope_inter() == out_tup
    assert_array_equal([hdr['scl_slope'], hdr['scl_inter']], raw_values)
```

## 6. test_tractogram_creation

- Kind: `test-workflow`
- Source: `nibabel/nibabel/streamlines/tests/test_tractogram.py:492`
- Note: Workflow: test tractogram creation

```python
tractogram = Tractogram()
check_tractogram(tractogram)
assert tractogram.affine_to_rasmm is None
tractogram = Tractogram(streamlines=DATA['streamlines'])
check_tractogram(tractogram, DATA['streamlines'])
affine = np.diag([1, 2, 3, 1])
tractogram = Tractogram(affine_to_rasmm=affine)
assert_array_equal(tractogram.affine_to_rasmm, affine)
tractogram = Tractogram(DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
check_tractogram(tractogram, DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
assert is_data_dict(tractogram.data_per_streamline)
assert is_data_dict(tractogram.data_per_point)
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
assert_tractogram_equal(tractogram2, tractogram)
tractogram = LazyTractogram(DATA['streamlines_func'], DATA['data_per_streamline_func'], DATA['data_per_point_func'])
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
wrong_data = [[(1, 0, 0)] * 1, [(0, 1, 0), (0, 1)], [(0, 0, 1)] * 5]
data_per_point = {'wrong_data': wrong_data}
with pytest.raises(ValueError):
    Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
wrong_data = [[(1, 0, 0)] * 1, [(0, 1)] * 2, [(0, 0, 1)] * 5]
data_per_point = {'wrong_data': wrong_data}
with pytest.raises(ValueError):
    Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
```

## 7. test_sorting_multiecho_ASL

- Kind: `test-workflow`
- Source: `nibabel/nibabel/tests/test_parrec.py:389`
- Note: Workflow: test sorting multiecho ASL

```python
asl_par = pjoin(DATA_PATH, 'ASL_3D_Multiecho.PAR')
with open(asl_par) as fobj:
    asl_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
np.random.shuffle(asl_hdr.image_defs)
sorted_indices = asl_hdr.get_sorted_slice_indices()
sorted_slices = asl_hdr.image_defs['slice number'][sorted_indices]
sorted_echos = asl_hdr.image_defs['echo number'][sorted_indices]
sorted_dynamics = asl_hdr.image_defs['dynamic scan number'][sorted_indices]
sorted_labels = asl_hdr.image_defs['label type'][sorted_indices]
ntotal = len(asl_hdr.image_defs)
nslices = sorted_slices.max()
nechos = sorted_echos.max()
nlabels = sorted_labels.max()
ndynamics = sorted_dynamics.max()
assert nslices == 8
assert nechos == 3
assert nlabels == 2
assert ndynamics == 2
assert_array_equal(np.all(sorted_dynamics[:ntotal // ndynamics] == 1), True)
assert_array_equal(np.all(sorted_dynamics[ntotal // ndynamics:ntotal] == 2), True)
assert_array_equal(np.all(sorted_labels[:nslices * nechos] == 1), True)
assert_array_equal(np.all(sorted_labels[nslices * nechos:2 * nslices * nechos] == 2), True)
assert_array_equal(np.all(sorted_echos[:nslices] == 1), True)
assert_array_equal(np.all(sorted_echos[nslices:2 * nslices] == 2), True)
assert_array_equal(np.all(sorted_echos[2 * nslices:3 * nslices] == 3), True)
assert_array_equal(sorted_slices[:nslices], np.arange(1, nslices + 1))
vol_labels = asl_hdr.get_volume_labels()
assert list(vol_labels.keys()) == ['echo number', 'label type', 'dynamic scan number']
assert_array_equal(vol_labels['dynamic scan number'], [1] * 6 + [2] * 6)
assert_array_equal(vol_labels['label type'], [1] * 3 + [2] * 3 + [1] * 3 + [2] * 3)
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

## 8. test_gifti_round_trip

- Kind: `test-workflow`
- Source: `nibabel/nibabel/gifti/tests/test_gifti.py:438`
- Note: Workflow: test gifti round trip

```python
test_data = b'<?xml version="1.0" encoding="UTF-8"?>\n<!DOCTYPE GIFTI SYSTEM "http://www.nitrc.org/frs/download.php/1594/gifti.dtd">\n<GIFTI\nxmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"\nxsi:noNamespaceSchemaLocation="http://www.nitrc.org/frs/download.php/1303/GIFTI_Caret.xsd"\nVersion="1.0"\nNumberOfDataArrays="2">\n<MetaData>\n<MD>\n<Name><![CDATA[date]]></Name>\n<Value><![CDATA[Thu Nov 15 09:05:22 2007]]></Value>\n</MD>\n</MetaData>\n<LabelTable/>\n<DataArray Intent="NIFTI_INTENT_POINTSET"\nDataType="NIFTI_TYPE_FLOAT32"\nArrayIndexingOrder="RowMajorOrder"\nDimensionality="2"\nDim0="4"\nDim1="3"\nEncoding="ASCII"\nEndian="LittleEndian"\nExternalFileName=""\nExternalFileOffset="">\n<CoordinateSystemTransformMatrix>\n<DataSpace><![CDATA[NIFTI_XFORM_TALAIRACH]]></DataSpace>\n<TransformedSpace><![CDATA[NIFTI_XFORM_TALAIRACH]]></TransformedSpace>\n<MatrixData>\n1.000000 0.000000 0.000000 0.000000\n0.000000 1.000000 0.000000 0.000000\n0.000000 0.000000 1.000000 0.000000\n0.000000 0.000000 0.000000 1.000000\n</MatrixData>\n</CoordinateSystemTransformMatrix>\n<Data>\n10.5 0 0\n0 20.5 0\n0 0 30.5\n0 0 0\n</Data>\n</DataArray>\n<DataArray Intent="NIFTI_INTENT_TRIANGLE"\nDataType="NIFTI_TYPE_INT32"\nArrayIndexingOrder="RowMajorOrder"\nDimensionality="2"\nDim0="4"\nDim1="3"\nEncoding="ASCII"\nEndian="LittleEndian"\nExternalFileName="" ExternalFileOffset="">\n<Data>\n0 1 2\n1 2 3\n0 1 3\n0 2 3\n</Data>\n</DataArray>\n</GIFTI>'
exp_verts = np.zeros((4, 3))
exp_verts[0, 0] = 10.5
exp_verts[1, 1] = 20.5
exp_verts[2, 2] = 30.5
exp_faces = np.asarray([[0, 1, 2], [1, 2, 3], [0, 1, 3], [0, 2, 3]], dtype=np.int32)

def _check_gifti(gio):
    vertices = gio.get_arrays_from_intent('NIFTI_INTENT_POINTSET')[0].data
    faces = gio.get_arrays_from_intent('NIFTI_INTENT_TRIANGLE')[0].data
    assert_array_equal(vertices, exp_verts)
    assert_array_equal(faces, exp_faces)
bio = BytesIO()
fmap = dict(image=FileHolder(fileobj=bio))
bio.write(test_data)
bio.seek(0)
gio = GiftiImage.from_file_map(fmap)
_check_gifti(gio)
bio.seek(0)
gio.to_file_map(fmap)
bio.seek(0)
gio2 = GiftiImage.from_file_map(fmap)
_check_gifti(gio2)
```

## 9. test_wrapper_from_data

- Kind: `test-workflow`
- Source: `nibabel/nibabel/nicom/tests/test_dicomwrappers.py:145`
- Note: Workflow: test wrapper from data

```python
for dw in (didw.wrapper_from_data(DATA), didw.wrapper_from_file(DATA_FILE)):
    assert dw.get('InstanceNumber') == 2
    assert dw.get('AcquisitionNumber') == 2
    with pytest.raises(KeyError):
        dw['not an item']
    assert dw.is_mosaic
    assert_array_almost_equal(np.dot(didr.DPCS_TO_TAL, dw.affine), EXPECTED_AFFINE)
for dw in (didw.wrapper_from_data(DATA_PHILIPS), didw.wrapper_from_file(DATA_FILE_PHILIPS)):
    assert dw.get('InstanceNumber') == 1
    assert dw.get('AcquisitionNumber') == 3
    with pytest.raises(KeyError):
        dw['not an item']
    assert dw.is_multiframe
dw = didw.wrapper_from_file(DATA_FILE_SLC_NORM)
assert dw.is_mosaic
fake_data = dict()
fake_data['SOPClassUID'] = '1.2.840.10008.5.1.4.1.1.4.2'
dw = didw.wrapper_from_data(fake_data)
assert not dw.is_multiframe
fake_data['SOPClassUID'] = '1.2.840.10008.5.1.4.1.1.4.1'
with pytest.raises(didw.WrapperError):
    didw.wrapper_from_data(fake_data)
fake_data['PerFrameFunctionalGroupsSequence'] = [pydicom.Dataset()]
with pytest.raises(didw.WrapperError):
    didw.wrapper_from_data(fake_data)
fake_data['SharedFunctionalGroupsSequence'] = [pydicom.Dataset()]
dw = didw.wrapper_from_data(fake_data)
assert dw.is_multiframe
```

## 10. test_load_file_with_wrong_information

- Kind: `test-workflow`
- Source: `nibabel/nibabel/streamlines/tests/test_tck.py:116`
- Note: Workflow: test load file with wrong information

```python
tck_file = open(DATA['simple_tck_fname'], 'rb').read()
new_tck_file = tck_file.replace(b'Float32LE', b'Float32BE')
with pytest.raises(DataError):
    TckFile.load(BytesIO(new_tck_file))
new_tck_file = tck_file.replace(b'Float32LE', b'int32')
with pytest.raises(HeaderError):
    TckFile.load(BytesIO(new_tck_file))
new_tck_file = tck_file.replace(b'datatype: Float32LE\n', b'')
new_tck_file = new_tck_file.replace(b'file: . 67\n', b'file: . 47\n')
with pytest.warns(HeaderWarning, match="Missing 'datatype'"):
    tck = TckFile.load(BytesIO(new_tck_file))
assert_array_equal(tck.header['datatype'], 'Float32LE')
new_tck_file = tck_file.replace(b'\nfile: . 67', b'')
with pytest.warns(HeaderWarning, match="Missing 'file'"):
    tck = TckFile.load(BytesIO(new_tck_file))
assert_array_equal(tck.header['file'], '. 56')
new_tck_file = tck_file.replace(b'file: . 67\n', b'file: dummy.mat 75\n')
with pytest.raises(HeaderError):
    TckFile.load(BytesIO(new_tck_file))
eos = TckFile.FIBER_DELIMITER.tobytes()
eof = TckFile.EOF_DELIMITER.tobytes()
new_tck_file = tck_file[:-(len(eos) + len(eof))] + tck_file[-len(eof):]
buffer_size = 1.0 / 1024 ** 2
hdr = TckFile._read_header(BytesIO(new_tck_file))
tck_reader = TckFile._read(BytesIO(new_tck_file), hdr, buffer_size)
with pytest.raises(DataError):
    list(tck_reader)
new_tck_file = tck_file[:-len(eof)]
with pytest.raises(DataError):
    TckFile.load(BytesIO(new_tck_file))
```

## 11. test_load_file_with_wrong_information

- Kind: `test-workflow`
- Source: `nibabel/nibabel/streamlines/tests/test_tck.py:116`
- Note: Workflow: test load file with wrong information

```python
tck_file = open(DATA['simple_tck_fname'], 'rb').read()
new_tck_file = tck_file.replace(b'Float32LE', b'Float32BE')
with pytest.raises(DataError):
    TckFile.load(BytesIO(new_tck_file))
new_tck_file = tck_file.replace(b'Float32LE', b'int32')
with pytest.raises(HeaderError):
    TckFile.load(BytesIO(new_tck_file))
new_tck_file = tck_file.replace(b'datatype: Float32LE\n', b'')
new_tck_file = new_tck_file.replace(b'file: . 67\n', b'file: . 47\n')
with pytest.warns(HeaderWarning, match="Missing 'datatype'"):
    tck = TckFile.load(BytesIO(new_tck_file))
assert_array_equal(tck.header['datatype'], 'Float32LE')
new_tck_file = tck_file.replace(b'\nfile: . 67', b'')
with pytest.warns(HeaderWarning, match="Missing 'file'"):
    tck = TckFile.load(BytesIO(new_tck_file))
assert_array_equal(tck.header['file'], '. 56')
new_tck_file = tck_file.replace(b'file: . 67\n', b'file: dummy.mat 75\n')
with pytest.raises(HeaderError):
    TckFile.load(BytesIO(new_tck_file))
eos = TckFile.FIBER_DELIMITER.tobytes()
eof = TckFile.EOF_DELIMITER.tobytes()
new_tck_file = tck_file[:-(len(eos) + len(eof))] + tck_file[-len(eof):]
buffer_size = 1.0 / 1024 ** 2
hdr = TckFile._read_header(BytesIO(new_tck_file))
tck_reader = TckFile._read(BytesIO(new_tck_file), hdr, buffer_size)
with pytest.raises(DataError):
    list(tck_reader)
new_tck_file = tck_file[:-len(eof)]
with pytest.raises(DataError):
    TckFile.load(BytesIO(new_tck_file))
```

## 12. test_slope_inter_castable

- Kind: `test-workflow`
- Source: `nibabel/nibabel/tests/test_arraywriters.py:272`
- Note: Workflow: test slope inter castable

```python
for in_dtt in FLOAT_TYPES + IUINT_TYPES:
    for out_dtt in NUMERIC_TYPES:
        for klass in (ArrayWriter, SlopeArrayWriter, SlopeInterArrayWriter):
            arr = np.zeros((5,), dtype=in_dtt)
            klass(arr, out_dtt)
arr = np.array([np.inf, np.nan, -np.inf])
for in_dtt in FLOAT_TYPES:
    for out_dtt in IUINT_TYPES:
        in_arr = arr.astype(in_dtt)
        with pytest.raises(WriterError):
            ArrayWriter(in_arr, out_dtt)
        SlopeArrayWriter(arr.astype(in_dtt), out_dtt)
        SlopeInterArrayWriter(arr.astype(in_dtt), out_dtt)
for in_dtt, out_dtt, arr, slope_only, slope_inter, neither in ((np.float32, np.float32, 1, True, True, True), (np.float64, np.float32, 1, True, True, True), (np.float32, np.complex128, 1, True, True, True), (np.uint32, np.complex128, 1, True, True, True), (np.int64, np.float32, 1, True, True, True), (np.float32, np.int16, 1, True, True, False), (np.complex128, np.float32, 1, False, False, False), (np.complex128, np.int16, 1, False, False, False), (np.uint8, np.int16, 1, True, True, True), (np.uint16, np.int16, 1, True, True, True), (np.uint16, np.int16, 2 ** 16 - 1, True, True, False), (np.uint16, np.int16, (0, 2 ** 16 - 1), True, True, False), (np.uint16, np.uint8, 1, True, True, True), (np.int16, np.uint16, 1, True, True, True), (np.int16, np.uint16, -1, True, True, False), (np.int16, np.uint16, (-1, 1), False, True, False), (np.int8, np.uint16, 1, True, True, True), (np.int8, np.uint16, -1, True, True, False), (np.int8, np.uint16, (-1, 1), False, True, False)):
    data = np.array(arr, dtype=in_dtt)
    if slope_only:
        SlopeArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            SlopeArrayWriter(data, out_dtt)
    if slope_inter:
        SlopeInterArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            SlopeInterArrayWriter(data, out_dtt)
    if neither:
        ArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            ArrayWriter(data, out_dtt)
```

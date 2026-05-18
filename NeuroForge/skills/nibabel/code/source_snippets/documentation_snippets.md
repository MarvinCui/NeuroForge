# nibabel Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Ioimplementation

- Kind: `documentation`
- Source: `references/documentation/other/ioimplementation.rst`
- Note: Documentation code block extracted for implementation use.

```text
Creating array image, saving

>>> import tempfile
>>> from nibabel.images import Image
>>> from nibabel import load, save
>>> fp, fname = tempfile.mkstemp('.nii')
>>> data = np.arange(24).reshape((2,3,4))
>>> img = Image(data)
>>> img.filename is None
True
>>> img.save()
Traceback (most recent call last):
   ...
ImageError: no filespec to save to
>>> save(img)
Traceback (most recent call last):
   ...
ImageError: no filespec to save to
>>> img2 = save(img, 'some_image.nii') # type guessed from filename
>>> img2.filename == fname
True
>>> img.filename is None # still
True
>>> img.filename = 'some_filename.nii' # read only property
Traceback (most recent call last):
   ...
AttributeError: can't set attribute

Load, futz, save

>>> img3 = load(fname, mode='r')
>>> img3.filename == fname
True
>>> np.all(img3.data == data)
True
>>> img3.data[0,0] = 99
>>> img3.save()
Traceback (most recent call last):
   ...
ImageError: trying to write to read only image
>>> img3.mode = 'rw'
>>> img3.save()
>>> load(img4)
>>> img4.mode # 'r' is the default
'r'
>>> mod_data = data.copy()
>>> mod_data[0,0] = 99
>>> np.all(img4.data = mod_data)
True

Prepare image for later writing

>>> img5 = Image(np.zeros(2,3,4))
>>> fp, fname2 = tempfile.mkstemp('.nii')
>>> img5.set_filespec(fname2)
>>> # then do some things to the image
>>> img5.save()

This is an example where you do need the io API

>>> from nibabel.ioimps import guessed_imp
>>> fp, fname3 = tempfile.mkstemp('.nii')
>>> ioimp = guessed_imp(fname3)
>>> ioimp.set_data_dtype(np.float64)
>>> ioimp.set_data_shape((2,3,4)) # set_data_shape method
>>> slice_def = (slice(None), slice(None), 0)
>>> ioimp.write_slice(data[slice_def], slice_def) # write_slice method
>>> slice_def = (2, 3, 1)
>>> ioimp.write_slice(data[slice_def], slice_def) # write_slice method
Traceback (most recent call last):
   ...
ImageIOError: data write is not contiguous
```

## 2. Biap 0005 #2

- Kind: `documentation`
- Source: `references/documentation/other/biap_0005.rst`
- Note: Documentation code block extracted for implementation use.

```text
>>> import nibabel as nib
>>> points = [np.arange(1*3).reshape((1,3)),
              np.arange(2*3).reshape((2,3)),
              np.arange(5*3).reshape((5,3))]
>>> streamlines = nib.streamlines.Streamlines(points)
>>> nib.streamlines.save(streamlines, 'data1.trk')  # Default TRK header is used but updated with streamlines information.

>>> FA = nib.load('FA.nii')
>>> streamlines.header = nib.streamlines.header.from_nifti(FA)  # Uses information of the FA to create an header.
>>> nib.streamlines.save(streamlines, 'data2.trk')  # Streamlines' header is used but also updated with streamlines information.

>>> from nib.streamlines.header import VOXEL_ORDER, VOXEL_SIZES
>>> hdr = nib.streamlines.TrkFile.get_empty_header()  # Default TRK header
>>> hdr[VOXEL_ORDER] = "LAS"
>>> hdr[VOXEL_SIZES] = (2, 2, 2)
>>> streamlines.header = hdr
>>> nib.streamlines.save(streamlines, 'data3.trk')  # Uses hdr to create a TRK header.
```

## 3. Neuro Radio Conventions #2

- Kind: `documentation`
- Source: `references/documentation/other/neuro_radio_conventions.rst`
- Note: Documentation code block extracted for implementation use.

```text
:context:

>>> import nibabel as nib
>>> import matplotlib.pyplot as plt
>>> img = nib.load('downloads/someones_anatomy.nii.gz')
>>> # The 3x3 part of the affine is diagonal with all +ve values
>>> img.affine
array([[  2.75,   0.  ,   0.  , -78.  ],
       [  0.  ,   2.75,   0.  , -91.  ],
       [  0.  ,   0.  ,   2.75, -91.  ],
       [  0.  ,   0.  ,   0.  ,   1.  ]])
>>> img_data = img.get_fdata()
>>> a_slice = img_data[:, :, 28]
>>> # Need transpose to put first axis left-right, second bottom-top
>>> plt.imshow(a_slice.T, cmap="gray", origin="lower")  # doctest: +SKIP
```

## 4. Dicom Niftiheader #2

- Kind: `documentation`
- Source: `references/documentation/other/dicom_niftiheader.rst`
- Note: Documentation code block extracted for implementation use.

```text
>> nim = nib.load('pet.nii')
>> nim.header.extensions
[]
>> from dicom.dataset import Dataset
>> ds = Dataset()
>> ds.add_new((0x0054,0x1001),'CS','Bq/ml')
>> ds.add_new((0x0055,0x0010),'LO','PMOD_1')
>> ds.add_new((0x0055,0x1001),'FD',[0.,30.,60.,13720.,14320.])
>> ds.add_new((0x0055,0x1004),'FD',[30000.,30000.,30000.,600000.,600000.])
>> dcmext = nib.nifti1.Nifti1DicomExtension(2,ds)  # Use DICOM ecode 2
>> nim.header.extensions.append(dcmext)
>> nib.save(nim,'pet_withdcm.nii')
```

## 5. Biap 0005 #1

- Kind: `documentation`
- Source: `references/documentation/other/biap_0005.rst`
- Note: Documentation code block extracted for implementation use.

```text
>>> import nibabel as nib
>>> f = nib.streamlines.load('my_trk.trk', lazy_load=False)
>>> type(f)
nibabel.streamlines.base_format.Streamlines
>>> f.points
[array([ [1, 1, 1],
         [2, 2, 2],
         [3, 3, 3] ]),
 array([ [4, 4, 4],
         [5, 5, 5] ])]
>>> nib.streamlines.convert('my_trk.trk', 'my_tck.tck')
>>> f2 = nib.streamlines.load('my_trk.tck', lazy_load=False)
>>> type(f2)
nibabel.streamlines.base_format.Streamlines
>>> f2.points
[array([ [1, 1, 1],
         [2, 2, 2],
         [3, 3, 3] ]),
 array([ [4, 4, 4],
         [5, 5, 5] ])]
```

## 6. Dicom Niftiheader #1

- Kind: `documentation`
- Source: `references/documentation/other/dicom_niftiheader.rst`
- Note: Documentation code block extracted for implementation use.

```python
>> import nibabel as nib
>> nim = nib.load('pmod_pet.nii')
>> dcmext = nim.header.extensions[0]
>> dcmext
Nifti1Extension('dicom', '(0054, 1001) Units                               CS: 'Bq/ml'
(0055, 0010) Private Creator                     LO: 'PMOD_1'
(0055, 1001) [Frame Start Times Vector]          FD: [0.0, 30.0, 60.0, ..., 13720.0, 14320.0]
(0055, 1004) [Frame Durations (ms) Vector]       FD: [30000.0, 30000.0, 30000.0,600000.0, 600000.0]'))
```

## 7. Biap 0003 #2

- Kind: `documentation`
- Source: `references/documentation/other/biap_0003.rst`
- Note: Documentation code block extracted for implementation use.

```text
>>> import numpy as np
>>> element = dict(applies_to=['time'],
...                q_vector = dict(
...                   spatial_axes = ['frequency', 'phase', 'slice'],
...                   array = [[0, 0, 0],
...                            [1000, 0, 0],
...                            [0, 1000, 0],
...                            [0, 0, 1000],
...                            [0, 0, 0],
...                            [1000, 0, 0],
...                            [0, 1000, 0],
...                            [0, 0, 1000],
...                            [0, 0, 0],
...                            [1000, 0, 0]
...                           ]))
>>> np.array(element['q_vector']['array']).shape
(10, 3)
```

## 8. Neuro Radio Conventions #1

- Kind: `documentation`
- Source: `references/documentation/other/neuro_radio_conventions.rst`
- Note: Documentation code block extracted for implementation use.

```text
:context:
:nofigs:

>>> import numpy as np
>>> from nibabel.affines import apply_affine
>>> diag_affine = np.array([[3., 0,  0,  0],
...                         [0,  3., 0,  0],
...                         [0,  0, 4.5, 0],
...                         [0,  0,  0,  1]])
>>> ijk = [1, 0, 0] # moving one unit on the first voxel axis
>>> apply_affine(diag_affine, ijk)
array([3., 0., 0.])
```

## 9. Biap 0009

- Kind: `documentation`
- Source: `references/documentation/other/biap_0009.rst`
- Note: Documentation code block extracted for implementation use.

```bash
bold = CoordinateImage.from_filename("/data/func/hemi-L_bold.func.gii")
dm = make_first_level_design_matrix(...)
betas = CoordinateImage(results["betas"], bold.coordaxis, bold.header)
graphs = get_graphs(bold.coordaxis)
distances = distance_matrix(graphs['lh']) # n_coords x n_coords matrix
weights = normalize(gaussian(distances, sigma))
smoothed = CoordinateImage(weights @ bold.get_fdata(), bold.coordaxis, bold.header)
data = img.get_fdata()
tstats = CoordinateImage.from_filename("/data/stats/hemi-L_contrast-taskVsBase_tstat.mgz")
fs_subject = FreeSurferSubject.from_spec("/data/subjects/fsaverage5")
img = nb.load("sub-01_task-rest_bold.dtseries.nii") # Assume CIFTI CoordinateImage
parcel = nb.load("sub-fsLR_hemi-L_label-DLPFC_mask.label.gii") # GiftiImage
```

## 10. Coordinate Systems #2

- Kind: `documentation`
- Source: `references/documentation/other/coordinate_systems.rst`
- Note: Documentation code block extracted for implementation use.

```text
:context:

>>> import matplotlib.pyplot as plt
>>> def show_slices(slices):
...    """ Function to display row of image slices """
...    fig, axes = plt.subplots(1, len(slices))
...    for i, slice in enumerate(slices):
...        axes[i].imshow(slice.T, cmap="gray", origin="lower")
>>>
>>> slice_0 = epi_img_data[26, :, :]
>>> slice_1 = epi_img_data[:, 30, :]
>>> slice_2 = epi_img_data[:, :, 16]
>>> show_slices([slice_0, slice_1, slice_2])
>>> plt.suptitle("Center slices for EPI image")  # doctest: +SKIP
```

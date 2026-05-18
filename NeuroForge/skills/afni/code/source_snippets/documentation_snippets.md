# afni Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Demonstration Examples #1

- Kind: `documentation`
- Source: `references/documentation/other/Demonstrations.md`
- Note: Documentation code block extracted for implementation use.

```bash
git clone https://github.com/NIFTI-Imaging/nifti_clib.git
  mkdir -p build-nifti_clib
  cd build-nifti_clib
  cmake ../nifti_clib
  make -j 2
  ctest
  mkdir ../build-stand-alone
  cd ../build-stand-alone
  export STAND_ALONE_SOURCE_DIR=../nifti_clib/real_easy/stand_alone_app
  cmake -DNIFTI_DIR:PATH=../build-nifti_clib ${STAND_ALONE_SOURCE_DIR}
  make
```

## 2. Demonstration Examples #2

- Kind: `documentation`
- Source: `references/documentation/other/Demonstrations.md`
- Note: Documentation code block extracted for implementation use.

```bash
git clone https://github.com/NIFTI-Imaging/nifti_clib.git
  mkdir -p build-test-integrated-demo
  cd build-test-integrated-demo
  cmake ../nifti_clib/real_easy/parent_project_demo
  make
```

## 3. Readme

- Kind: `documentation`
- Source: `references/documentation/other/README.rst`
- Note: Documentation code block extracted for implementation use.

```bash
git clone https://github.com/afni/afni.git
python interpreter. From the base directory of AFNI source code:
```

## 4. Demonstration Examples #3

- Kind: `documentation`
- Source: `references/documentation/other/Demonstrations.md`
- Note: Documentation code block extracted for implementation use.

```bash
git clone https://github.com/NIFTI-Imaging/nifti_clib.git
```

# nipype Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Git Resources

- Kind: `documentation`
- Source: `references/documentation/other/git_resources.rst`
- Note: Documentation code block extracted for implementation use.

```bash
git help push
git push --help
`git ready`_ |emdash| a nice series of tutorials
`git casts`_ |emdash| video snippets giving git how-tos.
`git magic`_ |emdash| extended introduction with intermediate detail
`git svn crash course`_: git_ for those of us used to subversion_
`git add`_
`git branch`_
`git checkout`_
`git clone`_
`git commit`_
`git config`_
```

## 2. Configure Git

- Kind: `documentation`
- Source: `references/documentation/other/configure_git.rst`
- Note: Documentation code block extracted for implementation use.

```bash
git config --global
git checkout
git wdiff
git config --global user.name "Your Name"
git config --global user.email you@yourdomain.example.com
git config --global alias.ci "commit -a"
git config --global alias.co checkout
git config --global alias.st "status -a"
git config --global alias.stat "status -a"
git config --global alias.br branch
git config --global alias.wdiff "diff --color-words"
git config --global core.editor vim
```

## 3. Python Interface Devel #1

- Kind: `documentation`
- Source: `references/documentation/other/python_interface_devel.rst`
- Note: Documentation code block extracted for implementation use.

```text
volume = File(exists=True, desc='volume to be thresholded', mandatory=True)
threshold = traits.Float(desc='everything below this value will be set to zero',
thresholded_volume = File(exists=True, desc="thresholded volume")
img = nb.load(fname)
data = np.array(img.get_data())
thresholded_map = np.zeros(data.shape)
new_img = nb.Nifti1Image(thresholded_map, img.affine, img.header)
outputs = self._outputs().get()
```

## 4. Python Interface Devel #2

- Kind: `documentation`
- Source: `references/documentation/other/python_interface_devel.rst`
- Note: Documentation code block extracted for implementation use.

```bash
volume = File(exists=True, desc='volume to be thresholded', mandatory=True)
threshold = traits.Float(desc='everything below this value will be set to zero',
thresholded_volume = File(exists=True, desc="thresholded volume")
img = nb.load(fname)
data = np.array(img.get_data())
thresholded_map = np.zeros(data.shape)
new_img = nb.Nifti1Image(thresholded_map, img.affine, img.header)
outputs = self._outputs().get()
```

## 5. Install #1

- Kind: `documentation`
- Source: `references/documentation/other/install.rst`
- Note: Documentation code block extracted for implementation use.

```text
python -c "import nipype; print(nipype.__version__)"
python -c "import nipype; nipype.test()"
```

## 6. Install #2

- Kind: `documentation`
- Source: `references/documentation/other/install.rst`
- Note: Documentation code block extracted for implementation use.

```bash
python -c "import nipype; print(nipype.__version__)"
python -c "import nipype; nipype.test()"
```

## 7. Set Up Fork

- Kind: `documentation`
- Source: `references/documentation/other/set_up_fork.rst`
- Note: Documentation code block extracted for implementation use.

```bash
git branch -a
git remote -v
git remote -v show
git clone git@github.com:your-user-name/nipype.git
git remote add upstream git://github.com/nipy/nipype.git
``git branch -a`` to show you all branches. You'll get something
```

## 8. Cmd Interface Devel #1

- Kind: `documentation`
- Source: `references/documentation/other/cmd_interface_devel.rst`
- Note: Documentation code block extracted for implementation use.

```text
input_volume = File(desc = "Input volume", exists = True,
parameter = traits.Int(desc = "some parameter")
output_volume = File(desc = "Output volume", exists = True)
```

## 9. Interface Specs #3

- Kind: `documentation`
- Source: `references/documentation/other/interface_specs.rst`
- Note: Documentation code block extracted for implementation use.

```text
jobtype = traits.Enum('estwrite', 'estimate', 'write',
jobtype = traits.Enum('estwrite', 'estimate', 'write',
job_type = traits.Enum('estwrite', 'estimate', 'write',
```

## 10. Cmd Interface Devel #2

- Kind: `documentation`
- Source: `references/documentation/other/cmd_interface_devel.rst`
- Note: Documentation code block extracted for implementation use.

```text
input_volume = File(desc = "Input volume", exists = True,
parameter = traits.Int(desc = "some parameter", argstr = "--param %d")
```

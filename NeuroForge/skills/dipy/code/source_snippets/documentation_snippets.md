# dipy Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Api Changes #1

- Kind: `documentation`
- Source: `references/documentation/other/api_changes.rst`
- Note: Documentation code block extracted for implementation use.

```text
# old
  LocalTracking(pam, stopping_criterion, seeds, affine, step_size)

  # new
  from dipy.tracking.tracker import eudx_tracking
  eudx_tracking(seeds, stopping_criterion, affine, pam=pam, step_size=step_size)
```

## 2. Contributing to DIPY #2

- Kind: `documentation`
- Source: `references/documentation/other/CONTRIBUTING.md`
- Note: Documentation code block extracted for implementation use.

```bash
# Step 1: Create the branch from master and push to upstream.
git fetch upstream
git checkout master && git merge --ff-only upstream/master
git branch maint/1.14.x master
git push upstream maint/1.14.x

# Step 2: Create the GitHub label — this is the ONLY required change.
gh label create "backport-maint/1.14.x" \
  --repo dipy/dipy \
  --color "e4a400" \
  --description "Backport this PR to maint/1.14.x"
```

## 3. Git Resources

- Kind: `documentation`
- Source: `references/documentation/other/git_resources.rst`
- Note: Documentation code block extracted for implementation use.

```bash
git help push
git push --help
git resources
`git ready`_ |emdash| a nice series of tutorials
`git casts`_ |emdash| video snippets giving git how-tos.
`git magic`_ |emdash| extended introduction with intermediate detail
`git foundation`_ expands on the `git parable`_.
`git svn crash course`_: git for those of us used to subversion_
`git add`_
`git branch`_
`git checkout`_
`git clone`_
```

## 4. Data #2

- Kind: `documentation`
- Source: `references/documentation/guides/data.rst`
- Note: Documentation code block extracted for implementation use.

```text
from dipy.data import fetch_bundle_fa_hcp

files, folder = fetch_bundle_fa_hcp()
```

## 5. Configure Git #2

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

## 6. Maintainer Workflow #2

- Kind: `documentation`
- Source: `references/documentation/other/maintainer_workflow.rst`
- Note: Documentation code block extracted for implementation use.

```text
git remote add someone git://github.com/someone/dipy.git
git fetch someone
git branch cool-feature --track someone/cool-feature
git checkout cool-feature
```

## 7. Contributing to DIPY #1

- Kind: `documentation`
- Source: `references/documentation/other/CONTRIBUTING.md`
- Note: Documentation code block extracted for implementation use.

```bash
# Fetch the draft branch created by the automation.
git fetch upstream
git checkout backport-<PR_NUMBER>-to-maint/1.13.x

# Resolve conflicts in your editor, then stage and continue.
git add <resolved-files>
git cherry-pick --continue

# Push and mark the draft PR as ready for review.
git push upstream backport-<PR_NUMBER>-to-maint/1.13.x
gh pr ready <BACKPORT_PR_NUMBER> --repo dipy/dipy
```

## 8. Getting Started #1

- Kind: `documentation`
- Source: `references/documentation/guides/getting_started.rst`
- Note: Documentation code block extracted for implementation use.

```text
gtab = gradient_table(bvals, bvecs=bvecs)
tenmodel = TensorModel(gtab)
tenfit = tenmodel.fit(data)
```

## 9. Getting Started #2

- Kind: `documentation`
- Source: `references/documentation/guides/getting_started.rst`
- Note: Documentation code block extracted for implementation use.

```bash
gtab = gradient_table(bvals, bvecs=bvecs)
tenmodel = TensorModel(gtab)
tenfit = tenmodel.fit(data)
```

## 10. Development Workflow #3

- Kind: `documentation`
- Source: `references/documentation/other/development_workflow.rst`
- Note: Documentation code block extracted for implementation use.

```text
git commit -am 'ENH - much better code'
 git push origin master # pushes directly into your repo
```

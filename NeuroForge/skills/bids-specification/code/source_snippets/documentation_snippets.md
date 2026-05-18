# bids-specification Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Common principles

- Kind: `documentation`
- Source: `references/documentation/other/common-principles.md`
- Note: Documentation code block extracted for implementation use.

```text
## The Inheritance Principle

In some circumstances, there can be multiple data files for which
all or a subset of the relevant metadata is precisely equivalent.
Where this occurs,
it may be preferable to define those metadata *only once*,
and be placed on the filesystem in such a way that those files
are deemed to be *applicable* to each relevant data file individually,
but *not* be erroneously associated with other data files
to which the metadata contained within are not applicable.
The Inheritance Principle defines a systematized set of rules
to determine which metadata files to associate with which data files.
Further, because multiple metadata files may apply to an individual data file,
the Principle defines the *order of precedence* of such metadata content;
this is necessary for resolution of conflicts if the same metadata field
contains different values in different metadata files
(though it is RECOMMENDED to avoid such overloading).

### Rules

1.  Any metadata file (such as `.json`, `.bvec` or `.tsv`) MAY be defined at any directory level.

1.  For a given data file, any metadata file is applicable to that data file if:
    1.  It is stored at the same directory level or higher;
    1.  The metadata and the data filenames possess the same suffix;
    1.  The metadata filename does not include any entity absent from the data filename.

1.  A metadata file MUST NOT have a filename that would be otherwise applicable
    to some data file based on rules 2.b and 2.c but is made inapplicable based on its
    location in the directory structure as per rule 2.a.

1.  There MUST NOT be multiple metadata files applicable to a data file at one level
    of the directory hierarchy.

1.  If multiple metadata files satisfy criteria 2.a-c above:

    1.  For [tabular files](#tabular-files) and other simple metadata files
        (for instance,
        [`bvec` / `bval` files for diffusion MRI](modality-specific-files/magnetic-resonance-imaging-data.md#required-gradient-orientation-information)),
        accessing metadata associated with a data file MUST consider only the
        applicable file that is lowest in the filesystem hierarchy.

    1.  For [JSON files](#key-value-files-dictionaries), key-values are loaded
        from files from the top of the directory hierarchy downwards, such that
        key-values from the top level are inherited by all data files at lower
        levels to which it is applicable unless overridden by a value for the
        same key present in another metadata file at a lower level
        (though it is RECOMMENDED to minimize the extent of such overrides).

### Corollaries

1.  As per rule 3, metadata files applicable only to a specific participant / session
    MUST be defined in or below the directory corresponding to that participant / session;
    similarly, a metadata file that is applicable to multiple participants / sessions
    MUST NOT be placed within a directory corresponding to only one such participant / session.

1.  It is permissible for a single metadata file to be applicable to multiple data
    files at that level of the hierarchy or below. Where such metadata content is consistent
    across multiple data files, it is RECOMMENDED to store metadata in this
    way, rather than duplicating that metadata content across multiple metadata files.

1.  Where multiple applicable JSON files are loaded as per rule 5.b, key-values can
    only be overwritten by files lower in the filesystem hierarchy; the absence of
    a key-value in a later file does not imply the "unsetting" of that field
    (indeed removal of existing fields is not possible).

### Examples

Example 1: Demonstration of inheritance principle

<!-- This block generates a file tree.
A guide for using macros can be found at
 https://github.com/bids-standard/bids-specification/blob/master/macros_doc.md
-->
{{ MACROS___make_filetree_example(
    {
    "sub-01": {
        "func": {
            "sub-01_task-rest_acq-default_bold.nii.gz": "",
            "sub-01_task-rest_acq-longtr_bold.nii.gz": "",
            "sub-01_task-rest_acq-longtr_bold.json": "",
            },
        "sub-01_scans.tsv": "",
        },
    "task-rest_bold.json": "",
    "scans.json": ""
    }
) }}

Contents of file `task-rest_bold.json`:
```

## 2. BIDS Schema Tools Quick Start

- Kind: `documentation`
- Source: `references/documentation/other/quickstart.md`
- Note: Documentation code block extracted for implementation use.

```bash
schema = bst.schema.load_schema()
spec = UPath(os.getenv('BIDS_SPEC_REPO', UPath(os.getcwd()).parent.parent.parent))
schema_from_directory = bst.schema.load_schema(spec / 'src' / 'schema')
schema_path = UPath('https://bids-specification.readthedocs.io/en/latest/schema.json')
schema_from_json = bst.schema.load_schema(schema_path)
```

## 3. Release Procedure #2

- Kind: `documentation`
- Source: `references/documentation/overview/Release_Protocol.md`
- Note: Documentation code block extracted for implementation use.

```shell
cd bids-specification
git remote add upstream git@github.com:bids-standard/bids-specification.git
```

## 4. Release Procedure #1

- Kind: `documentation`
- Source: `references/documentation/overview/Release_Protocol.md`
- Note: Documentation code block extracted for implementation use.

```shell
git remote get-url upstream
git@github.com:bids-standard/bids-specification.git
```

## 5. Release Procedure #3

- Kind: `documentation`
- Source: `references/documentation/overview/Release_Protocol.md`
- Note: Documentation code block extracted for implementation use.

```shell
git fetch upstream
git checkout -b rel/1.2.0 upstream/master
```

# snakemake Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Modularization

- Kind: `documentation`
- Source: `references/documentation/other/modularization.rst`
- Note: Documentation code block extracted for implementation use.

```text
A rule cannot be overwritten under the same name, unless it was previously imported via `use rule * from ...` statement.
This is the **only allowed scenario** where an existing rule name may be overwritten, and is provided for convenience when selectively customizing some rules without introducing new names.
In such cases, the second statement uses the same final name as produced by the previous import (via the `as` clause).
Importantly, once a rule has been modified in this way, it cannot be redefined or modified again under the same name, but you should import under different names to customize the same rule multiple times:

.. code-block:: python

    use rule * from other_workflow as other_*

    use rule some_task from other_workflow as other_some_task with:
        output:
            "results/some-result.txt"

    use rule some_task from other_workflow as else_some_task with:
        output:
            "custom_output.txt"

Once a rule has been modified this way under a given name, it **cannot** be redefined or modified again under the same name:

.. code-block:: python

    use rule some_task from other_workflow as other_some_task with:
        output:
            "results/some-result.txt"

    use rule some_task from other_workflow as other_some_task with:
        threads: 1
    # Not allowed: "other_some_task" was already defined above.

Similarly, if a `use rule * from ...` statement would result in a rule name that collides with a previously defined rule (regardless of its source), Snakemake will raise an error, and you should resolve the conflict by changing the import order or using a different `as` modifier:

.. code-block:: python

    use rule some_task from other_workflow as else_some_task with:
        output:
            "custom_output.txt"

    use rule * from other_workflow as else_*
    # Will fail: "else_some_task" is already defined.
```

## 2. Rules #2

- Kind: `documentation`
- Source: `references/documentation/other/rules.rst`
- Note: Documentation code block extracted for implementation use.

```text
Note that benchmarking is only possible in a reliable fashion for subprocesses (thus for tasks run through the ``shell``, ``script``, and ``wrapper`` directive).
In the ``run`` block, the variable ``bench_record`` is available that you can pass to ``shell()`` as ``bench_record=bench_record``.
When using ``shell(..., bench_record=bench_record)``, the maximum of all measurements of all ``shell()`` calls will be used but the running time of the rule execution including any Python code.
```

## 3. Additional Features #1

- Kind: `documentation`
- Source: `references/documentation/guides/additional_features.rst`
- Note: Documentation code block extracted for implementation use.

```python
rule bwa_map:
    input:
        "data/genome.fa",
        lambda wildcards: config["samples"][wildcards.sample]
    output:
        temp("mapped_reads/{sample}.bam")
    params:
        rg=r"@RG\tID:{sample}\tSM:{sample}"
    log:
        "logs/bwa_mem/{sample}.log"
    benchmark:
        "benchmarks/{sample}.bwa.benchmark.txt"
    threads: 8
    shell:
        "(bwa mem -R '{params.rg}' -t {threads} {input} | "
        "samtools view -Sb - > {output}) 2> {log}"
```

## 4. Rules #3

- Kind: `documentation`
- Source: `references/documentation/other/rules.rst`
- Note: Documentation code block extracted for implementation use.

```text
A rule cannot be redefined without renaming it using the ``as`` clause.
Otherwise, you will have two versions of the same rule, which might be unintended (a common symptom of such unintended repeated uses would be ambiguous rule exceptions thrown by Snakemake).
However, it is allowed to create **multiple modified versions** of the same rule, as long as each has a **unique name**.
The only exception is when a rule was previously imported via a general ``use rule * from`` statement, such rules may be **further modified once** under the same final name for convenience (see :ref:`snakefiles-modules`).
```

## 5. Cli

- Kind: `documentation`
- Source: `references/documentation/other/cli.rst`
- Note: Documentation code block extracted for implementation use.

```bash
snakemake --help
snakemake --workflow-profile my_profile
snakemake --workflow-profile relative_path/to/my_profile
snakemake --workflow-profile extra_profiles_dir/workflow_profile.yaml
snakemake --workflow-profile workfklow_on_xyz --default-resources mem_mb 1000 --cores 2
snakemake -h
$ snakemake --cores 1
$ snakemake -n
$ snakemake --cores 4
$ snakemake --cores 4 --set-threads myrule=2
$ snakemake --cores 4 --set-resources myrule:partition="foo"
$ snakemake --cores 4 --batch myrule=1/3
```

## 6. Advanced #1

- Kind: `documentation`
- Source: `references/documentation/guides/advanced.rst`
- Note: Documentation code block extracted for implementation use.

```python
rule bwa_map:
    input:
        "data/genome.fa",
        "data/samples/{sample}.fastq"
    output:
        "mapped_reads/{sample}.bam"
    threads: 8
    shell:
        "bwa mem -t {threads} {input} | samtools view -Sb - > {output}"
```

## 7. Basics #1

- Kind: `documentation`
- Source: `references/documentation/guides/basics.rst`
- Note: Documentation code block extracted for implementation use.

```python
rule bwa_map:
    input:
        "data/genome.fa",
        "data/samples/A.fastq"
    output:
        "mapped_reads/A.bam"
    shell:
        "bwa mem {input} | samtools view -Sb - > {output}"
```

## 8. Deployment #2

- Kind: `documentation`
- Source: `references/documentation/other/deployment.rst`
- Note: Documentation code block extracted for implementation use.

```bash
snakemake --sdm conda --conda-create-envs-only
snakemake --use-envmodules
snakemake --software-deployment-method conda
snakemake --software-deployment-method apptainer
snakemake --sdm apptainer
snakemake --containerize > Dockerfile
snakemake --containerize apptainer > myworkflow.def
snakemake --software-deployment-method conda apptainer
snakemake --sdm conda apptainer
snakemake --archive my-workflow.tar.gz
snakemake -n
```

## 9. Storage #3

- Kind: `documentation`
- Source: `references/documentation/other/storage.rst`
- Note: Documentation code block extracted for implementation use.

```text
rule example:
    input:
        local("resources/example-input.txt")
    output:
        "example-output.txt"
    shell:
        "..."
```

## 10. Rules #1

- Kind: `documentation`
- Source: `references/documentation/other/rules.rst`
- Note: Documentation code block extracted for implementation use.

```text
On a cluster node, Snakemake uses as many cores as available on that node.
Hence, the number of threads used by a rule never exceeds the number of physically available cores on the node.
Note: This behavior is not affected by ``--local-cores``, which only applies to jobs running on the main node.
```

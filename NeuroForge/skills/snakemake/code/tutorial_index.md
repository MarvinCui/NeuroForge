# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: Case Sensitivity | references/tutorials/case-sensitivity/case-sensitivity.md | Workflow: Test case sensitivity of matching | unittest.mock, pytest, snakemake.output_index |
| How To: Code Block Manifest Spacing Around Language | references/tutorials/code-block-manifest-spacing-around-language/code-block-manifest-spacing-around-language.md | Workflow: test code block manifest spacing around language | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Code Block Manifest With Shebang | references/tutorials/code-block-manifest-with-shebang/code-block-manifest-with-shebang.md | Workflow: test code block manifest with shebang | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Code Block Manifest Without Shebang | references/tutorials/code-block-manifest-without-shebang/code-block-manifest-without-shebang.md | Workflow: test code block manifest without shebang | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Expand | references/tutorials/expand/expand.md | Configuration example: test expand | pathlib, snakemake.io, snakemake.exceptions |
| How To: Issue4063 | references/tutorials/issue4063/issue4063.md | Workflow: test issue4063 | os, shutil, sys, subprocess, logging |
| How To: Log Events | references/tutorials/log-events/log-events.md | Workflow: Test LogEvent counts of records captured during workflow run. | os, shutil, sys, subprocess, logging |
| How To: Logfile | references/tutorials/logfile/logfile.md | Workflow: test logfile | os, shutil, sys, subprocess, logging |
| How To: Logger In Workflow | references/tutorials/logger-in-workflow/logger-in-workflow.md | Workflow: Test adding a handler to the ``logger`` global in the Snakefile. relevant issue: https://github.com/snakemake/snakemake/issues/3558 | os, shutil, sys, subprocess, logging |
| How To: Logging Config | references/tutorials/logging-config/logging-config.md | Workflow: Test configuring logging using ``logging.config.dictConfig()`` in the Snakefile. Relevant issue: https://github.com/snakemake/snakemake/issues/3044 | os, shutil, sys, subprocess, logging |
| How To: Plugin | references/tutorials/plugin/plugin.md | Workflow: Test using a logger plugin. Adds the logging/plugins/ directory to PYTHONPATH so the plugin registry can detect the "snakemake_logger_plugin_test" package. The plugin outputs each record in JSON format on a sin | os, shutil, sys, subprocess, logging |
| How To: Profile Parse | references/tutorials/profile-parse/profile-parse.md | Workflow: test profile parse | snakemake.cli, io, snakemake.profiles, textwrap, pytest |
| How To: Single Line Manifest Formatting Not Touched Even If Wrong | references/tutorials/single-line-manifest-formatting-not-touched-even-if-wrong/single-line-manifest-formatting-not-touched-even-if-wrong.md | Workflow: The dependency delimiter is wrong, but we let rust-script deal with it | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Single Line Manifest Is Case Insensitive | references/tutorials/single-line-manifest-is-case-insensitive/single-line-manifest-is-case-insensitive.md | Workflow: test single line manifest is case insensitive | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Single Line Manifest Not At Start With Shebang | references/tutorials/single-line-manifest-not-at-start-with-shebang/single-line-manifest-not-at-start-with-shebang.md | Workflow: test single line manifest not at start with shebang | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Single Line Manifest Not At Start Without Shebang | references/tutorials/single-line-manifest-not-at-start-without-shebang/single-line-manifest-not-at-start-without-shebang.md | Workflow: test single line manifest not at start without shebang | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Single Line Manifest Spacing Has No Impact | references/tutorials/single-line-manifest-spacing-has-no-impact/single-line-manifest-spacing-has-no-impact.md | Workflow: test single line manifest spacing has no impact | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Single Line Manifest With Empty Line Without Shebang | references/tutorials/single-line-manifest-with-empty-line-without-shebang/single-line-manifest-with-empty-line-without-shebang.md | Workflow: test single line manifest with empty line without shebang | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Single Line Manifest With Shebang And Second Manifest | references/tutorials/single-line-manifest-with-shebang-and-second-manifest/single-line-manifest-with-shebang-and-second-manifest.md | Workflow: test single line manifest with shebang and second manifest | textwrap, snakemake.iocontainers, snakemake.script |
| How To: Special Characters | references/tutorials/special-characters/special-characters.md | Instantiate PrefixLookup: test special characters | snakemake.common.prefix_lookup |

## Snippets Extracted

- `references/tutorials/plugin/plugin.md`: How To: Plugin
- `references/tutorials/logger-in-workflow/logger-in-workflow.md`: How To: Logger In Workflow
- `references/tutorials/log-events/log-events.md`: How To: Log Events
- `references/tutorials/single-line-manifest-formatting-not-touched-even-if-wrong/single-line-manifest-formatting-not-touched-even-if-wrong.md`: How To: Single Line Manifest Formatting Not Touched Even If Wrong
- `references/tutorials/logfile/logfile.md`: How To: Logfile
- `references/tutorials/single-line-manifest-not-at-start-with-shebang/single-line-manifest-not-at-start-with-shebang.md`: How To: Single Line Manifest Not At Start With Shebang
- `references/tutorials/single-line-manifest-not-at-start-without-shebang/single-line-manifest-not-at-start-without-shebang.md`: How To: Single Line Manifest Not At Start Without Shebang
- `references/tutorials/single-line-manifest-with-shebang-and-second-manifest/single-line-manifest-with-shebang-and-second-manifest.md`: How To: Single Line Manifest With Shebang And Second Manifest
- `references/tutorials/single-line-manifest-spacing-has-no-impact/single-line-manifest-spacing-has-no-impact.md`: How To: Single Line Manifest Spacing Has No Impact
- `references/tutorials/single-line-manifest-is-case-insensitive/single-line-manifest-is-case-insensitive.md`: How To: Single Line Manifest Is Case Insensitive
- `references/tutorials/single-line-manifest-with-empty-line-without-shebang/single-line-manifest-with-empty-line-without-shebang.md`: How To: Single Line Manifest With Empty Line Without Shebang
- `references/tutorials/issue4063/issue4063.md`: How To: Issue4063

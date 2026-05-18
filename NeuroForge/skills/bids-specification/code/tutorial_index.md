# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: Get Bids Version Fallback | references/tutorials/-get-bids-version-fallback/-get-bids-version-fallback.md | Workflow: test get bids version fallback | json, os, subprocess, collections.abc, pytest |
| How To: Accept Non Bids Dir | references/tutorials/accept-non-bids-dir/accept-non-bids-dir.md | Workflow: test accept non bids dir | os, shutil, pytest, bidsschematools.conftest, bidsschematools.validator |
| How To: Assignability | references/tutorials/assignability/assignability.md | Workflow: Verify that dataclass values can be assigned to variables annotated with protocols. For pytest, this just checks instantiability. Running mypy with bst installed should check assignability, for example, with:: | bidsschematools.types, bidsschematools.types |
| How To: Broken Json Dataset | references/tutorials/broken-json-dataset/broken-json-dataset.md | Workflow: Perhaps this can be integrated into https://github.com/bids-standard/bids-error-examples . | os, shutil, pytest, bidsschematools.conftest, bidsschematools.validator |
| How To: Check Format Email Scenarios | references/tutorials/check-format-email-scenarios/check-format-email-scenarios.md | Workflow: Parametrized test for check_format usage on valid/invalid email addresses under Draft202012Validator. | contextlib, typing, pytest, jsonschema.exceptions, jsonschema.protocols |
| How To: Dereferencing | references/tutorials/dereferencing/dereferencing.md | Workflow: test dereferencing | json, os, subprocess, collections.abc, pytest |
| How To: Entity Order | references/tutorials/entity-order/entity-order.md | Workflow: Check the order of the entities of the suffix group of each datatype and lists those that are out of order. | warnings, collections.abc, pytest |
| How To: Entity Rule | references/tutorials/entity-rule/entity-rule.md | Workflow: test entity rule | re, bidsschematools, types |
| How To: Exclude Files | references/tutorials/exclude-files/exclude-files.md | Workflow: test exclude files | os, shutil, pytest, bidsschematools.conftest, bidsschematools.validator |
| How To: Formats | references/tutorials/formats/formats.md | Workflow: Test valid string patterns allowed by the specification. | json, os, subprocess, collections.abc, pytest |
| How To: Invalid Schema Raises Schema Error | references/tutorials/invalid-schema-raises-schema-error/invalid-schema-raises-schema-error.md | Configuration example: Provide an invalid schema, ensuring that 'SchemaError' is raised. | contextlib, typing, pytest, jsonschema.exceptions, jsonschema.protocols |
| How To: Make Columns Table | references/tutorials/make-columns-table/make-columns-table.md | Workflow: Test whether expected columns are present and the requirement level is applied correctly. This should be robust with respect to schema format. | bidsschematools.render, bidsschematools.render.utils |
| How To: Make Glossary | references/tutorials/make-glossary/make-glossary.md | Workflow: Test whether files under the schema objects subdirectory correspond to entries, and that rules are not misloaded as objects. This may need to be updated for schema hierarchy changes. | os, pytest, bidsschematools.render |
| How To: Make Sidecar Table | references/tutorials/make-sidecar-table/make-sidecar-table.md | Workflow: Test whether expected metadata fields are present and the requirement level is applied correctly. This should be robust with respect to schema format. | bidsschematools.render, bidsschematools.render.utils |
| How To: Remove Admonitions | references/tutorials/remove-admonitions/remove-admonitions.md | Workflow: test remove admonitions | pathlib, remove_admonitions |
| How To: Resolve Metadata Type | references/tutorials/resolve-metadata-type/resolve-metadata-type.md | Workflow: A unit test for utils.resolve_metadata_type. | bidsschematools.render |
| How To: Valid Sidecar Field | references/tutorials/valid-sidecar-field/valid-sidecar-field.md | Workflow: Check sidecar fields actually exist in the metadata listed in the schema. Test failures are usually due to typos. | __future__, collections.abc, functools, pytest, pyparsing.exceptions |
| How To: Validate Bids | references/tutorials/validate-bids/validate-bids.md | Workflow: test validate bids | os, shutil, pytest, bidsschematools.conftest, bidsschematools.validator |
| How To: Write Report | references/tutorials/write-report/write-report.md | Workflow: test write report | os, shutil, pytest, bidsschematools.conftest, bidsschematools.validator |

## Snippets Extracted

- `references/tutorials/assignability/assignability.md`: How To: Assignability
- `references/tutorials/entity-rule/entity-rule.md`: How To: Entity Rule
- `references/tutorials/formats/formats.md`: How To: Formats
- `references/tutorials/dereferencing/dereferencing.md`: How To: Dereferencing
- `references/tutorials/write-report/write-report.md`: How To: Write Report
- `references/tutorials/accept-non-bids-dir/accept-non-bids-dir.md`: How To: Accept Non Bids Dir
- `references/tutorials/make-sidecar-table/make-sidecar-table.md`: How To: Make Sidecar Table
- `references/tutorials/make-columns-table/make-columns-table.md`: How To: Make Columns Table
- `references/tutorials/exclude-files/exclude-files.md`: How To: Exclude Files
- `references/tutorials/valid-sidecar-field/valid-sidecar-field.md`: How To: Valid Sidecar Field
- `references/tutorials/make-glossary/make-glossary.md`: How To: Make Glossary
- `references/tutorials/validate-bids/validate-bids.md`: How To: Validate Bids

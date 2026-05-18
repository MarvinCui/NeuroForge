# Tutorial And Workflow Index

Implementation-oriented tutorials recovered from the original generated output. The snippet files contain compact extracted examples rather than full copied tutorial trees.

| Title | Package source | Implementation focus | Imports |
| --- | --- | --- | --- |
| How To: Add Args And Kwargs | references/tutorials/add-args-and-kwargs/add-args-and-kwargs.md | Workflow: test add args and kwargs | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Add Invalid Modifiers | references/tutorials/add-invalid-modifiers/add-invalid-modifiers.md | Workflow: test add invalid modifiers | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Add Kwargs | references/tutorials/add-kwargs/add-kwargs.md | Workflow: test add kwargs | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Adddata With Mutable Values | references/tutorials/adddata-with-mutable-values/adddata-with-mutable-values.md | Workflow: test addData with mutable values | psychopy, numpy, os, glob, shutil |
| How To: Aliasdict | references/tutorials/aliasdict/aliasdict.md | Workflow: Test that the AliasDict class works as expected. | psychopy.tools, pytest, numpy |
| How To: Alignment | references/tutorials/alignment/alignment.md | Workflow: test alignment | pathlib, numpy, psychopy, psychopy.alerts, psychopy.alerts._errorHandler |
| How To: All Code Component Tabs | references/tutorials/all-code-component-tabs/all-code-component-tabs.md | Workflow: test all code component tabs | pathlib, tempfile, psychopy, psychopy.experiment.loops, psychopy.experiment.routines |
| How To: All Have Depth | references/tutorials/all-have-depth/all-have-depth.md | Workflow: test all have depth | psychopy.experiment.exports, psychopy, inspect |
| How To: Anchor Flip | references/tutorials/anchor-flip/anchor-flip.md | Workflow: Check that flipping the image doesn't flip the direction of the anchor | pathlib, psychopy, test_basevisual, psychopy.tests.test_experiment.test_component_compile_python, psychopy.tests |
| How To: Applyinitialrule False | references/tutorials/applyinitialrule-false/applyinitialrule-false.md | Workflow: test applyInitialRule False | numpy, shutil, json_tricks, tempfile, operator |
| How To: Aspect Ratio | references/tutorials/aspect-ratio/aspect-ratio.md | Workflow: Test that images set with one or both dimensions as None maintain their aspect ratio | pathlib, psychopy, test_basevisual, psychopy.tests.test_experiment.test_component_compile_python, psychopy.tests |
| How To: Audioclip Attrib | references/tutorials/audioclip-attrib/audioclip-attrib.md | Workflow: Test `AudioClip` attribute setters and getters. Tests attributes `samples`, `sampleRateHz`, `duration`, and `gain()`. | os, tempfile, pytest, numpy, psychopy |
| How To: Audioclip Create | references/tutorials/audioclip-create/audioclip-create.md | Workflow: Create an audio clip object and see if the properties are correct. Basic stress test to check if we get the value we expect. | os, tempfile, pytest, numpy, psychopy |
| How To: Audioclip File | references/tutorials/audioclip-file/audioclip-file.md | Workflow: Test saving and loading audio samples from files. Checks the integrity of loaded data to ensure things are similar to the original. | os, tempfile, pytest, numpy, psychopy |
| How To: Audioclip Rms | references/tutorials/audioclip-rms/audioclip-rms.md | Workflow: Test the RMS method of `AudioClip`. Just check if the function give back values that are correctly formatted given the input data. | os, tempfile, pytest, numpy, psychopy |
| How To: Audioclip Synth | references/tutorials/audioclip-synth/audioclip-synth.md | Workflow: Test `AudioClip` static methods for sound generation. Just check if the sounds created give back data structured as expected. Not testing if the contents are correctly generated (yet). | os, tempfile, pytest, numpy, psychopy |
| How To: Background Image Fit | references/tutorials/background-image-fit/background-image-fit.md | Workflow: test background image fit | importlib, copy, pathlib, psychopy, psychopy.tests |
| How To: Blank Timing | references/tutorials/blank-timing/blank-timing.md | Workflow: Check that this Component can handle blank start/stop values. | ast, esprima, re, pathlib, esprima.error_handler |
| How To: Border Contains | references/tutorials/border-contains/border-contains.md | Workflow: test border contains | pathlib, psychopy, psychopy.tests, psychopy.visual, numpy |
| How To: Capturemovieframes | references/tutorials/capturemovieframes/capturemovieframes.md | Workflow: test captureMovieFrames | sys, os, copy, pathlib, psychopy |
| How To: Caret Position | references/tutorials/caret-position/caret-position.md | Workflow: test caret position | pathlib, numpy, psychopy, psychopy.alerts, psychopy.alerts._errorHandler |
| How To: Circle | references/tutorials/circle/circle.md | Workflow: test circle | sys, os, copy, pathlib, psychopy |
| How To: Code Muting | references/tutorials/code-muting/code-muting.md | Workflow: Test that routines are only written when enabled and targets match. | pathlib, pytest, psychopy, psychopy.hardware |
| How To: Colors | references/tutorials/colors/colors.md | Workflow: test colors | pathlib, numpy, psychopy, psychopy.alerts, psychopy.alerts._errorHandler |
| How To: Combinations | references/tutorials/combinations/combinations.md | Workflow: Test that question options interact well | os, pathlib, pytest, pandas, psychopy.tests.test_visual.test_basevisual |
| How To: Contains | references/tutorials/contains/contains.md | Workflow: test contains | pathlib, psychopy, psychopy.tests, psychopy.visual, numpy |
| How To: Contrast | references/tutorials/contrast/contrast.md | Workflow: test contrast | psychopy.alerts, psychopy.alerts._errorHandler, psychopy.tests, psychopy, numpy |
| How To: Default | references/tutorials/default/default.md | Workflow: test default | psychopy, numpy, os, glob, shutil |
| How To: Delitem | references/tutorials/delitem/delitem.md | Workflow: test delitem | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Delitem String | references/tutorials/delitem-string/delitem-string.md | Workflow: test delitem string | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Device Json | references/tutorials/device-json/device-json.md | Configuration example: test device JSON | threading, psychopy, psychopy.hardware, psychopy.tests, pathlib |
| How To: Disabled Code Muting | references/tutorials/disabled-code-muting/disabled-code-muting.md | Workflow: Test that components are only written when enabled and targets match. | ast, esprima, re, pathlib, esprima.error_handler |
| How To: Dist | references/tutorials/dist/dist.md | Workflow: Test the distance function in mathtools. This also test the `normalize` function to ensure all vectors have a length of 1. | psychopy.tools.mathtools, psychopy.tools.viewtools, numpy, pytest |
| How To: Dkl2Rgb | references/tutorials/dkl2rgb/dkl2rgb.md | Workflow: Test the conversion (forward) for DKL to RGB (signed). | psychopy.tools.colorspacetools, numpy, pytest |
| How To: Dot | references/tutorials/dot/dot.md | Workflow: Test the dot-product function `dot()`. Tests cases Nx2, Nx3, and Nx4 including one-to-many cases. The test for the `cross()` function validates if the values computed by `dot()` are meaningful. | psychopy.tools.mathtools, psychopy.tools.viewtools, numpy, pytest |
| How To: Editable | references/tutorials/editable/editable.md | Workflow: test editable | pathlib, numpy, psychopy, psychopy.alerts, psychopy.alerts._errorHandler |
| How To: Element Array Colors | references/tutorials/element-array-colors/element-array-colors.md | Instantiate ElementArrayStim: test element array colors | psychopy.alerts, psychopy.alerts._errorHandler, psychopy.tests, psychopy, numpy |
| How To: Event Processing | references/tutorials/event-processing/event-processing.md | Workflow: test event processing | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Exp Loadcompilepsyexp | references/tutorials/exp-loadcompilepsyexp/exp-loadcompilepsyexp.md | Workflow: test Exp LoadCompilePsyexp | pathlib, psychopy.experiment, psychopy.experiment.components.text, psychopy.experiment._experiment, psychopy.tests.utils |
| How To: Formatting | references/tutorials/formatting/formatting.md | Workflow: test formatting | pathlib, numpy, psychopy, psychopy.alerts, psychopy.alerts._errorHandler |
| How To: Fps | references/tutorials/fps/fps.md | Workflow: Check that images can be updated sufficiently fast to create frame animations | pathlib, psychopy, test_basevisual, psychopy.tests.test_experiment.test_component_compile_python, psychopy.tests |
| How To: Frustumtoprojectionmatrix | references/tutorials/frustumtoprojectionmatrix/frustumtoprojectionmatrix.md | Workflow: Ensure the `computeFrustum` + `perspectiveProjectionMatrix` and `generalizedPerspectiveProjection` give similar results, therefore testing them both at the same time. | psychopy.tools.mathtools, psychopy.tools.viewtools, numpy, pytest |
| How To: Future Trials | references/tutorials/future-trials/future-trials.md | Workflow: test future trials | threading, psychopy, psychopy.hardware, psychopy.tests, pathlib |
| How To: Gammasetgetmatch | references/tutorials/gammasetgetmatch/gammasetgetmatch.md | Workflow: test that repeatedly getting and setting the gamma table has no cumulative effect. | psychopy, numpy, psychopy.tests |
| How To: Genfilenamefromdelimiter | references/tutorials/genfilenamefromdelimiter/genfilenamefromdelimiter.md | Workflow: test genFilenameFromDelimiter | shutil, os, sys, json, pickle |
| How To: Get Data | references/tutorials/get-data/get-data.md | Workflow: test get data | os, pathlib, pytest, pandas, psychopy.tests.test_visual.test_basevisual |
| How To: Get Info | references/tutorials/get-info/get-info.md | Workflow: test get info | pathlib, test_base_components, psychopy, utils |
| How To: Getdatestr | references/tutorials/getdatestr/getdatestr.md | Workflow: test getDateStr | os, pathlib, pytest, numpy, psychopy |
| How To: Getfuturetrials | references/tutorials/getfuturetrials/getfuturetrials.md | Workflow: Check that TrialHandler2 can return future trials correctly. | os, glob, os.path, shutil, tempfile |
| How To: Getitem Modifiers List | references/tutorials/getitem-modifiers-list/getitem-modifiers-list.md | Workflow: test getitem modifiers list | pytest, psychopy, psychopy.preferences, psychopy.visual, pyglet.window.key |
| How To: Getprocesses | references/tutorials/getprocesses/getprocesses.md | Workflow: test getProcesses | psychopy.tests, psychopy.tests.test_iohub.testutil, psychopy.iohub, psychopy.core |
| How To: Getrating | references/tutorials/getrating/getrating.md | Workflow: test getRating | pathlib, psychopy.tests, psychopy.tests.test_visual.test_basevisual, psychopy.tests.test_experiment.test_component_compile_python, psychopy.visual.window |
| How To: Gettime | references/tutorials/gettime/gettime.md | Workflow: test getTime | psychopy.tests, psychopy.tests.test_iohub.testutil, psychopy.iohub, psychopy.core |
| How To: Glyph Rendering | references/tutorials/glyph-rendering/glyph-rendering.md | Workflow: test glyph rendering | pathlib, numpy, psychopy, psychopy.alerts, psychopy.alerts._errorHandler |
| How To: Gratingimageandgauss | references/tutorials/gratingimageandgauss/gratingimageandgauss.md | Workflow: test gratingImageAndGauss | sys, os, copy, pathlib, psychopy |
| How To: Greyscaleimage | references/tutorials/greyscaleimage/greyscaleimage.md | Workflow: test greyscaleImage | sys, os, copy, pathlib, psychopy |
| How To: Hammingsmallblock | references/tutorials/hammingsmallblock/hammingsmallblock.md | Workflow: test HammingSmallBlock | psychopy.sound._base, psychopy.constants, psychopy.exceptions, numpy, pytest |
| How To: Handlefilecollision Rename File Exists | references/tutorials/handlefilecollision-rename-file-exists/handlefilecollision-rename-file-exists.md | Workflow: test handleFileCollision rename file exists | pytest, os, shutil, tempfile, psychopy.tools.fileerrortools |
| How To: Handlefilecollision Rename Multiple Files Exists | references/tutorials/handlefilecollision-rename-multiple-files-exists/handlefilecollision-rename-multiple-files-exists.md | Workflow: test handleFileCollision rename multiple files exists | pytest, os, shutil, tempfile, psychopy.tools.fileerrortools |
| How To: Horiz | references/tutorials/horiz/horiz.md | Workflow: test horiz | pathlib, psychopy.tests, psychopy.tests.test_visual.test_basevisual, psychopy.tests.test_experiment.test_component_compile_python, psychopy.visual.window |

## Snippets Extracted

- `references/tutorials/all-code-component-tabs/all-code-component-tabs.md`: How To: All Code Component Tabs
- `references/tutorials/loaded-namespace/loaded-namespace.md`: How To: Loaded Namespace
- `references/tutorials/param-str/param-str.md`: How To: Param Str
- `references/tutorials/writing/writing.md`: How To: Writing
- `references/tutorials/aspect-ratio/aspect-ratio.md`: How To: Aspect Ratio
- `references/tutorials/combinations/combinations.md`: How To: Combinations
- `references/tutorials/colors/colors.md`: How To: Colors
- `references/tutorials/typing/typing.md`: How To: Typing
- `references/tutorials/formatting/formatting.md`: How To: Formatting
- `references/tutorials/indentation-consistency/indentation-consistency.md`: How To: Indentation Consistency
- `references/tutorials/glyph-rendering/glyph-rendering.md`: How To: Glyph Rendering
- `references/tutorials/soundheard/soundheard.md`: How To: Soundheard

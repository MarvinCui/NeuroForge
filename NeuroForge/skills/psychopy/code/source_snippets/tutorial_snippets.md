# psychopy Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: All Code Component Tabs

- Kind: `tutorial`
- Source: `references/tutorials/all-code-component-tabs/all-code-component-tabs.md`
- Note: Workflow: test all code component tabs

```python
# Workflow
comp, rt, exp = self.make_minimal_experiment()
tabs = {'Before Experiment': '___before_experiment___', 'Begin Experiment': '___begin_experiment___', 'Begin Routine': '___begin_routine___', 'Each Frame': '___each_frame___', 'End Routine': '___end_routine___', 'End Experiment': '___end_experiment___'}
for paramName, marker in tabs.items():
    jsParamName = paramName.replace(' ', ' JS ')
    comp.params[paramName].val = comp.params[jsParamName].val = ' = '.join([self.comp.__name__, comp.name, marker])
pyScript = exp.writeScript(target='PsychoPy')
jsScript = exp.writeScript(target='PsychoJS')
for lang, script in {'Python': pyScript, 'JS': jsScript}.items():
    for paramName, marker in tabs.items():
        try:
            assert marker in script, f'Could not find {marker} in {lang} script.'
        except AssertionError as err:
            ext = '.py' if lang == 'Python' else '.js'
            with open(Path(TESTS_DATA_PATH) / ('test_all_code_component_tabs_local' + ext), 'w') as f:
                f.write(script)
            raise err
    if lang == 'Python':
        assert script.find('___before_experiment___') < script.find('___begin_experiment___') < script.find('___begin_routine___') < script.find('___each_frame___') < script.find('___end_routine___') < script.find('___end_experiment___')
        assert script.find('___before_experiment___') < script.find('visual.Window') < script.find('___begin_experiment___') < script.find('continueRoutine = True')
        assert script.find('continueRoutine = True') < script.find('___begin_routine___') < script.find('while continueRoutine:') < script.find('___each_frame___')
        assert script.find('thisComponent.setAutoDraw(False)') < script.find('___end_routine___') < script.find('routineTimer.reset()') < script.find('___end_experiment___')
```

## 2. How To: Loaded Namespace

- Kind: `tutorial`
- Source: `references/tutorials/loaded-namespace/loaded-namespace.md`
- Note: Workflow: test loaded namespace

```python
# Workflow
exp = experiment.Experiment()
allRoutines = experiment.getAllStandaloneRoutines(fetchIcons=False)
"\n        Case structure\n        ==============\n        file : str\n            Experiment file to load\n        expectedSet : Set[str]\n            The expected names in the user namespace after routines are loaded and added\n        names : List[str]\n            Name of each routine to be added after experiment is loaded, paired with tags\n        tags : List[str]\n            Type of each routine to be added after experiment is loaded, paired with names\n            Can be 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine'\n        "
cases = [{'file': 'test_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance', 'counterbalance_2', 'counterbalance_3', 'counterbalance_4', 'counterbalance_5', 'calibration', 'calibration_2'}, 'names': ['counterbalance', 'counterbalance', 'calibration', 'calibration'], 'tags': ['CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance', 'counterbalance_2', 'counterbalance_3', 'calibration', 'counterbalance_4', 'calibration_2'}, 'names': ['calibration', 'counterbalance', 'calibration'], 'tags': ['EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_custom_missing.psyexp', 'expectedSet': {'trial', 'custom_2', 'counterbalance_2', 'counterbalance', 'counterbalance_3', 'calibration', 'calibration_2'}, 'names': ['counterbalance', 'counterbalance', 'calibration', 'calibration'], 'tags': ['CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_missing_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance_2', 'counterbalance', 'counterbalance_3'}, 'names': ['counterbalance', 'counterbalance'], 'tags': ['CounterbalanceRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_mix_exp.psyexp', 'expectedSet': {'trial', 'counterbalance', 'calibration', 'counterbalance_2', 'validation', 'counterbalance_3', 'calibration_2', 'validation_2'}, 'names': ['counterbalance', 'calibration', 'validation'], 'tags': ['CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine']}, {'file': 'test_mix_missing.psyexp', 'expectedSet': {'trial', 'calibration_2', 'counterbalance_2', 'calibration', 'counterbalance', 'calibration_3', 'counterbalance_3'}, 'names': ['calibration_2', 'counterbalance_2', 'calibration', 'counterbalance'], 'tags': ['EyetrackerCalibrationRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'CounterbalanceRoutine']}, {'file': 'test_mix_name_calibration.psyexp', 'expectedSet': {'trial', 'calibration_2', 'custom_2', 'counterbalance_2', 'calibration', 'calibration_3', 'custom_3', 'custom'}, 'names': ['calibration', 'calibration', 'custom_2', 'custom'], 'tags': ['EyetrackerCalibrationRoutine', 'CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine']}]
for case in cases:
    exp.loadFromXML(Path(TESTS_DATA_PATH) / 'test_loaded_namespace' / case['file'])
    namespace = exp.namespace
    for name, tag in zip(case['names'], case['tags']):
        routine = allRoutines[tag](exp=exp, name=name)
        rtGoodName = routine.params['name'].val = namespace.makeValid(routine.params['name'].val)
        namespace.add(rtGoodName)
        exp.addStandaloneRoutine(routineName=rtGoodName, routine=routine)
    actualSet = set(namespace.user)
    expectedSet = case['expectedSet']
    print()
    print(case['file'])
    print(actualSet)
    print(expectedSet)
    print()
    assert len(actualSet) == len(expectedSet)
    assert len(actualSet) == len(actualSet.intersection(expectedSet))
```

## 3. How To: Param Str

- Kind: `tutorial`
- Source: `references/tutorials/param-str/param-str.md`
- Note: Workflow: Test that params convert to str as expected in both Python and JS

```python
# Workflow
'\n    Test that params convert to str as expected in both Python and JS\n    '
sl = '\\'
cases = [{'obj': Param('Hello there', 'str'), 'py': f'{_q}Hello there{_q}', 'js': f'{_q}Hello there{_q}'}, {'obj': Param('\\, | or /', 'str', canBePath=False), 'py': f'{_q}{_sl}, \\| or /{_q}', 'js': f'{_q}{_sl}, \\| or /{_q}'}, {'obj': Param('$win.color', 'str'), 'py': f'win.color', 'js': f'psychoJS.window.color'}, {'obj': Param('1', 'int'), 'py': f'1', 'js': f'1'}, {'obj': Param('1', 'num'), 'py': f'1.0', 'js': f'1.0'}, {'obj': Param('C:/Downloads/file.ext', 'file'), 'py': f'{_q}C:/Downloads/file.ext{_q}', 'js': f'{_q}C:/Downloads/file.ext{_q}'}, {'obj': Param('C:/Downloads/file.csv', 'table'), 'py': f'{_q}C:/Downloads/file.csv{_q}', 'js': f'{_q}C:/Downloads/file.csv{_q}'}, {'obj': Param('red', 'color'), 'py': f'{_q}red{_q}', 'js': f'{_q}red{_q}'}, {'obj': Param('0.7, 0.7, 0.7', 'color'), 'py': f'{_lb}0.7, 0.7, 0.7{_rb}', 'js': f'{_lb}0.7, 0.7, 0.7{_rb}'}, {'obj': Param('win.color', 'code'), 'py': f'win.color', 'js': f'psychoJS.window.color'}, {'obj': Param('for x in y:\n\tprint(y)', 'extendedCode'), 'py': f'for x in y:\n\tprint{_lb}y{_rb}', 'js': f'for x in y:\n\tprint{_lb}y{_rb}'}, {'obj': Param('1, 2, 3', 'list'), 'py': f'{_lb}1, 2, 3{_rb}', 'js': f'{_lb}1, 2, 3{_rb}'}, {'obj': Param(__file__, 'str'), 'py': f"{_q}{__file__.replace(sl, '/')}{_q}", 'js': f"{_q}{__file__.replace(sl, '/')}{_q}"}, {'obj': Param('C:\\\\Downloads\\file.csv', 'str'), 'py': f'{_q}C:/Downloads/file.csv{_q}', 'js': f'{_q}C:/Downloads/file.csv{_q}'}, {'obj': Param('C:\\\\Downloads\\_file.csv', 'str'), 'py': f'{_q}C:/Downloads/_file.csv{_q}', 'js': f'{_q}C:/Downloads/_file.csv{_q}'}, {'obj': Param('This costs \\$4.20', 'str'), 'py': f'{_q}This costs {_d}4.20{_q}', 'js': f'{_q}This costs {_d}4.20{_q}'}, {'obj': Param('This \\ that', 'str'), 'py': f'{_q}This {_sl} that{_q}', 'js': f'{_q}This {_sl} that{_q}'}, {'obj': Param('variableName', 'code'), 'py': f'variableName', 'js': f'variableName'}, {'obj': Param('$letterColor', 'color'), 'py': f'letterColor', 'js': f'letterColor'}, {'obj': Param('"left", "down", "right"', 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("'left', 'down', 'right'", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("('left', 'down', 'right')", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("['left', 'down', 'right']", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param('"left"', 'list'), 'py': f'{_lb}{_q}left{_q}{_rb}'}, {'obj': Param('["left"]', 'list'), 'py': f'{_lb}{_q}left{_q}{_rb}'}, {'obj': Param('$left', 'list'), 'py': 'left', 'js': 'left'}, {'obj': Param('path\\to\\resource', 'str', canBePath=True), 'py': "'path/to/resource'", 'js': "'path/to/resource'"}, {'obj': Param("$Math.E+'$'", 'str'), 'py': "Math\\.E\\+'\\$'", 'js': '\\(Math.E \\+ \\"\\$\\"\\)'}]
initTarget = exputils.scriptTarget
for case in cases:
    if 'py' in case:
        exputils.scriptTarget = 'PsychoPy'
        assert re.fullmatch(case['py'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['py']}`, but it was `{case['obj']}`"
    if 'js' in case:
        exputils.scriptTarget = 'PsychoJS'
        assert re.fullmatch(case['js'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['js']}`, but it was `{case['obj']}`"
exputils.scriptTarget = initTarget
```

## 4. How To: Writing

- Kind: `tutorial`
- Source: `references/tutorials/writing/writing.md`
- Note: Workflow: test writing

```python
# Workflow
if pyVersion > Version('3.6'):
    return
exp = experiment.Experiment()
rt = experiment.routines.Routine(name='testRoutine', exp=exp)
exp.addRoutine('testRoutine', rt)
exp.flow.addRoutine(rt, 0)
comp = polygon.PolygonComponent(exp=exp, parentName='testRoutine')
rt.addComponent(comp)
exp.settings.params['Use version'].val = '2021.1.4'
exp.saveToXML(str(self.temp / 'versionText.psyexp'))
scriptFile = str(self.temp / 'versionText.py')
generateScript(outfile=scriptFile, exp=exp, target='PsychoPy')
with open(scriptFile, 'r') as f:
    script = f.read()
args = script.split(f'{comp.name} = visual.ShapeStim(')[1]
args = args.split(')')[0]
assert 'anchor' not in args, "When compiling Py with useversion 2021.1.4, found 'anchor' argument in ShapeStim; this was not implemented in requested version."
scriptFile = str(self.temp / 'versionText.js')
generateScript(outfile=scriptFile, exp=exp, target='PsychoJS')
with open(scriptFile, 'r') as f:
    script = f.read()
assert "import { PsychoJS } from './lib/core-2021.1.4.js'" in script, 'When compiling JS with useversion 2021.1.4, could not find version-specific import statement.'
```

## 5. How To: Aspect Ratio

- Kind: `tutorial`
- Source: `references/tutorials/aspect-ratio/aspect-ratio.md`
- Note: Workflow: Test that images set with one or both dimensions as None maintain their aspect ratio

```python
# Workflow
'\n        Test that images set with one or both dimensions as None maintain their aspect ratio\n        '
cases = [{'img': 'default.png', 'aspect': (1, 1), 'size': (None, 2), 'units': 'norm', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (2, None), 'units': 'norm', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'norm', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'norm', 'tag': 'default_None'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, 1), 'units': 'height', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (1 / self.win.size[1] * self.win.size[0], None), 'units': 'height', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'height', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'height', 'tag': 'default_None'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, self.win.size[1]), 'units': 'pix', 'tag': 'default_xNone_yFull'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (self.win.size[0], None), 'units': 'pix', 'tag': 'default_xFull_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': (None, None), 'units': 'pix', 'tag': 'default_xNone_yNone'}, {'img': 'default.png', 'aspect': (1, 1), 'size': None, 'units': 'pix', 'tag': 'default_None'}]
for case in cases:
    self.obj.image = case['img']
    self.obj.units = case['units']
    self.obj.size = case['size']
    assert self.obj.aspectRatio == case['aspect']
    self.obj.draw()
    filename = f"test_image_aspect_{case['tag']}.png"
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=7)
    self.win.flip()
```

## 6. How To: Combinations

- Kind: `tutorial`
- Source: `references/tutorials/combinations/combinations.md`
- Note: Workflow: Test that question options interact well

```python
# Workflow
'\n        Test that question options interact well\n        '
exemplars = {'bigResp': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.3, 'responseColor': 'darkred', 'responseWidth': 0.7, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.3, 'responseColor': 'darkslateblue', 'responseWidth': 0.7, 'font': 'Noto Sans'}], 'bigItem': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.7, 'responseColor': 'darkred', 'responseWidth': 0.3, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.7, 'responseColor': 'darkslateblue', 'responseWidth': 0.3, 'font': 'Noto Sans'}]}
tykes = {'bigRespOverflow': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.4, 'responseColor': 'darkred', 'responseWidth': 0.8, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.4, 'responseColor': 'darkslateblue', 'responseWidth': 0.8, 'font': 'Noto Sans'}], 'bigItemOverflow': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.8, 'responseColor': 'darkred', 'responseWidth': 0.4, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.8, 'responseColor': 'darkslateblue', 'responseWidth': 0.4, 'font': 'Noto Sans'}]}
cases = exemplars.copy()
cases.update(tykes)
self.win.flip()
for name, case in cases.items():
    for thisType in self.respTypes:
        for i, q in enumerate(case):
            case[i]['type'] = thisType
        survey = Form(self.win, units='height', size=(1, 1), fillColor='white', items=case)
        survey.draw()
        filename = f'test_form_combinations_{thisType}_{name}.png'
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
        self.win.flip()
```

## 7. How To: Colors

- Kind: `tutorial`
- Source: `references/tutorials/colors/colors.md`
- Note: Workflow: test colors

```python
# Workflow
_TestColorMixin.test_colors(self)
self.textbox.text = 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.'
exemplars = [{'color': (1, 1, 1), 'fillColor': (-1, -1, -1), 'borderColor': (-1, -1, -1), 'space': 'rgb', 'screenshot': 'colors_WOB.png'}, {'color': 'white', 'fillColor': 'black', 'borderColor': 'black', 'space': 'rgb', 'screenshot': 'colors_WOB.png'}, {'color': '#ffffff', 'fillColor': '#000000', 'borderColor': '#000000', 'space': 'hex', 'screenshot': 'colors_WOB.png'}, {'color': 'red', 'fillColor': 'yellow', 'borderColor': 'blue', 'space': 'rgb', 'screenshot': 'colors_exemplar1.png'}, {'color': 'yellow', 'fillColor': 'blue', 'borderColor': 'red', 'space': 'rgb', 'screenshot': 'colors_exemplar2.png'}, {'color': 'blue', 'fillColor': 'red', 'borderColor': 'yellow', 'space': 'rgb', 'screenshot': 'colors_exemplar3.png'}]
tykes = [{'color': 'white', 'fillColor': None, 'borderColor': None, 'space': 'rgb', 'screenshot': 'colors_tyke1.png'}, {'color': None, 'fillColor': 'white', 'borderColor': None, 'space': 'rgb', 'screenshot': 'colors_tyke2.png'}, {'color': None, 'fillColor': None, 'borderColor': 'white', 'space': 'rgb', 'screenshot': 'colors_tyke3.png'}]
for case in exemplars + tykes:
    if not all((key in case for key in ['color', 'fillColor', 'borderColor', 'space', 'screenshot'])):
        raise KeyError(f'Case spec for test_colors in class {self.__class__.__name__} ({__file__}) invalid, test cannot be run.')
    self.textbox.colorSpace = case['space']
    self.textbox.color = case['color']
    self.textbox.fillColor = case['fillColor']
    self.textbox.borderColor = case['borderColor']
    for lineBreaking in ('default', 'uax14'):
        self.win.flip()
        self.textbox.draw()
    if case['screenshot']:
        filename = 'textbox_{}_{}'.format(self.textbox._lineBreaking, case['screenshot'])
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

## 8. How To: Typing

- Kind: `tutorial`
- Source: `references/tutorials/typing/typing.md`
- Note: Workflow: Check that continuous typing doesn't break anything

```python
# Workflow
"Check that continuous typing doesn't break anything"
self.textbox.color = 'white'
self.textbox.fillColor = None
self.textbox.borderColor = None
wasEditable = self.textbox.editable
self.textbox.editable = True
exemplars = [{'text': '', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_blank.png'}, {'text': 'test←←←←', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_blank.png'}, {'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_pangram.png'}, {'text': 'ther◀◀◀◀Hello ▶▶▶▶e', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_navLR.png'}, {'text': 'Hello←o there←e◀◀◀→e', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_navDel.png'}, {'text': 'Hello\nthere', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_newline.png'}]
tykes = [{'text': 'i need a word which will go off the page, antidisestablishmentarianism is a very long word', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_longWord.png'}]
for case in exemplars + tykes:
    self.textbox.font = case['font']
    self.textbox.text = ''
    for letter in case['text']:
        if letter == '◀':
            self.textbox._onCursorKeys('MOTION_LEFT')
        elif letter == '▶':
            self.textbox._onCursorKeys('MOTION_RIGHT')
        elif letter == '←':
            self.textbox._onCursorKeys('MOTION_BACKSPACE')
        elif letter == '→':
            self.textbox._onCursorKeys('MOTION_DELETE')
        else:
            self.textbox._onText(letter)
        self.textbox.draw()
        self.win.flip()
    if case['screenshot']:
        self.win.flip()
        self.textbox.draw()
        self.textbox.caret.draw(override=True)
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / case['screenshot'], self.win, crit=20)
self.textbox.editable = wasEditable
```

## 9. How To: Formatting

- Kind: `tutorial`
- Source: `references/tutorials/formatting/formatting.md`
- Note: Workflow: test formatting

```python
# Workflow
cases = [{'text': 'This contains ***bold italic*** text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'bolditalic'}, {'text': 'This contains **bold** text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'bold'}, {'text': 'This contains *italic* text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'italic'}, {'text': 'This contains \\*escaped\\* text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'escaped'}, {'text': 'This contains [color=red]colorful[/color] text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'color'}, {'text': 'This text contains ***bold italic***, **bold**, *italic*, \\*escaped\\*, and [color=red]colorful[/color] text.', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'all'}, {'text': 'This text contains no formatting, but looks like it contains ***bold italic***, **bold**, *italic*, \\*escaped\\*, and [color=red]colorful[/color] text.', 'syntax': 'raw', 'languageStyle': 'LTR', 'screenshot': 'md'}, {'text': 'השועל [color=brown]החום[/color] המהיר קופץ **מעל** הכלב ה*עצלן*.', 'syntax': 'md', 'languageStyle': 'RTL', 'screenshot': 'all'}, {'text': 'This text contains <b><i>bold italic</i></b>, <i><b>italic bold</b></i>, <b>bold</b>, <i>italic</i>, <div>div wrapped</div> and <span style="color: red">colorful</span> text.', 'syntax': 'html', 'languageStyle': 'LTR', 'screenshot': 'all'}, {'text': 'This text contains no formatting, but looks like it contains <b><i>bold italic</i></b>, <i><b>italic bold</b></i>, <b>bold</b>, <i>italic</i>, <div>div wrapped</div> and <span style="color: red">colorful</span> text.', 'syntax': 'raw', 'languageStyle': 'LTR', 'screenshot': 'html'}, {'text': 'השועל <span style="color: brown">החום</span> המהיר קופץ <b>מעל</b> הכלב ה<i>עצלן</i>.', 'syntax': 'html', 'languageStyle': 'RTL', 'screenshot': 'all'}]
self.textbox.fontMGR.addGoogleFont('Noto Sans Hebrew')
self.textbox.fontMGR.addGoogleFont('Noto Sans')
for case in cases:
    if case['languageStyle'] == 'RTL':
        self.textbox.font = 'Noto Sans Hebrew'
    else:
        self.textbox.font = 'Noto Sans'
    self.textbox.languageStyle = case['languageStyle']
    self.textbox.formattingSyntax = case['syntax']
    self.textbox.text = case['text']
    self.win.flip()
    self.textbox.draw()
    filename = f'{type(self).__name__}_textbox_formatting_%(screenshot)s_%(syntax)s_%(languageStyle)s.png' % case
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

## 10. How To: Indentation Consistency

- Kind: `tutorial`
- Source: `references/tutorials/indentation-consistency/indentation-consistency.md`
- Note: Workflow: No component should exit any of its write methods at a different indent level as it entered, as this would break subsequent components / routines.

```python
# Workflow
'\n        No component should exit any of its write methods at a different indent level as it entered, as this would break subsequent components / routines.\n        '
comp, rt, exp = self.make_minimal_experiment()
if 'startVal' not in comp.params or 'stopVal' not in comp.params:
    pytest.skip()
buff = IndentingBuffer(target='PsychoPy')
errMsgTemplate = 'Writing {} code for {} changes indent level by {} when start is `{}` and stop is `{}`.'
exp.flow.writeStartCode(buff)
cases = [{'startVal': '0', 'stopVal': '1'}, {'startVal': '', 'stopVal': '1'}, {'startVal': '0', 'stopVal': ''}, {'startVal': '', 'stopVal': ''}]
for case in cases:
    errMsg = errMsgTemplate.format('{}', type(comp).__name__, '{}', case['startVal'], case['stopVal'])
    comp.params['startType'].val = 'time (s)'
    comp.params['stopType'].val = 'time (s)'
    for param, val in case.items():
        comp.params[param].val = val
    comp.writeInitCode(buff)
    assert buff.indentLevel == 0, errMsg.format('init', buff.indentLevel)
    comp.writeRoutineStartCode(buff)
    assert buff.indentLevel == 0, errMsg.format('routine start', buff.indentLevel)
    comp.writeFrameCode(buff)
    assert buff.indentLevel == 0, errMsg.format('each frame', buff.indentLevel)
    comp.writeRoutineEndCode(buff)
    assert buff.indentLevel == 0, errMsg.format('routine end', buff.indentLevel)
    comp.writeExperimentEndCode(buff)
    assert buff.indentLevel == 0, errMsg.format('experiment end', buff.indentLevel)
```

## 11. How To: Glyph Rendering

- Kind: `tutorial`
- Source: `references/tutorials/glyph-rendering/glyph-rendering.md`
- Note: Workflow: test glyph rendering

```python
# Workflow
self.textbox.colorSpace = 'rgb'
self.textbox.color = 'white'
self.textbox.fillColor = (0, 0, 0)
self.textbox.borderColor = None
self.textbox.opacity = 1
for font in ['Noto Sans', 'Noto Sans HK', 'Noto Sans JP', 'Noto Sans KR', 'Noto Sans SC', 'Noto Sans TC', 'Niramit', 'Indie Flower']:
    self.textbox.fontMGR.addGoogleFont(font)
exemplars = [{'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'exemplar_1.png'}, {'text': 'ə saɪkəʊpaɪ zɛlət nəʊz ə smidge ɒv wx, bʌt ˈʤɑːvəskrɪpt ɪz ðə ˈkwɛsʧən', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'exemplar_2.png'}, {'text': '아 프시초피 제알롣 크노W스 아 s믿게 오f wx, 붇 자v앗c립t 잇 테 q왯디온', 'font': 'Noto Sans KR', 'size': 16, 'screenshot': 'exemplar_3.png'}, {'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Indie Flower', 'size': 16, 'screenshot': 'exemplar_4.png'}]
tykes = [{'text': 'कोशिकायें', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'tyke_1.png'}, {'text': 'ขาว แดง เขียว เหลือง ชมพู ม่วง เทา', 'font': 'Niramit', 'size': 16, 'screenshot': 'tyke_2.png'}, {'text': 'โฬิปื้ด็ลู', 'font': 'Niramit', 'size': 36, 'screenshot': 'cutoff_top.png'}]
for case in exemplars + tykes:
    self.textbox.reset()
    self.textbox.fontMGR.addGoogleFont(case['font'])
    self.textbox.letterHeight = layout.Size(case['size'], 'pix', self.win)
    self.textbox.font = case['font']
    self.textbox.text = case['text']
    self.win.flip()
    self.textbox.draw()
    if case['screenshot']:
        filename = 'textbox_{}_{}'.format(self.textbox._lineBreaking, case['screenshot'])
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

## 12. How To: Soundheard

- Kind: `tutorial`
- Source: `references/tutorials/soundheard/soundheard.md`
- Note: Workflow: Check that the sound sensor validator detects a sound played from an audible speaker.

```python
# Workflow
'\n        Check that the sound sensor validator detects a sound played from an audible speaker.\n        '
clock = core.Clock()
self.validator.resetTimer(clock)
t = 0
snd = sound.Sound('A', speaker=self.speaker)
snd.tStart = snd.tStop = None
snd.status = self.validator.status = constants.NOT_STARTED
while t < 3:
    t = clock.getTime()
    if self.validator.status == constants.STARTED and snd.status == constants.STARTED:
        self.validator.tStart, self.validator.valid = self.validator.validate(state=True, t=snd.tStart, adjustment=0.12)
        if self.validator.tStart:
            self.validator.status = constants.FINISHED
            assert self.validator.valid
    if self.validator.status == constants.STARTED and snd.status == constants.FINISHED:
        self.validator.tStop, self.validator.valid = self.validator.validate(state=False, t=snd.tStop, adjustment=0)
        if self.validator.tStop:
            self.validator.status = constants.FINISHED
            assert self.validator.valid
    if snd.status == constants.NOT_STARTED and t > 1:
        snd.play()
        snd.tStart = t
        snd.status = constants.STARTED
        self.validator.status = constants.STARTED
    if snd.status == constants.STARTED and t > 2:
        snd.stop()
        snd.tStop = t
        snd.status = constants.FINISHED
        self.validator.status = constants.STARTED
assert self.validator.tStart is not None
assert self.validator.tStop is not None
```

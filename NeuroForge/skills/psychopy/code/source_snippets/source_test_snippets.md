# psychopy Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_importConditions

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_data/test_utils.py:18`
- Note: Workflow: test importConditions

```python
standard_files = []
standard_files.append(join(fixturesPath, 'trialTypes.xlsx'))
standard_files.append(join(fixturesPath, 'trialTypes.csv'))
standard_files.append(join(fixturesPath, 'trialTypes_eu.csv'))
standard_files.append(join(fixturesPath, 'trialTypes.tsv'))
fileName_pkl = join(fixturesPath, 'trialTypes.pkl')
fileName_docx = join(fixturesPath, 'trialTypes.docx')
expected_cond = utils.OrderedDict([('text', 'red'), ('congruent', 1), ('corrAns', 1), ('letterColor', 'red'), ('n', 2), ('float', 1.1)])
for filename in standard_files:
    conds = utils.importConditions(filename)
    assert conds[0] == expected_cond, "Did not correctly import for '{}': expected({}) != imported({})".format(filename, expected_cond, conds[0])
assert utils.importConditions(fileName=None) == []
assert utils.importConditions(fileName=None, returnFieldNames=True) == ([], [])
with pytest.raises(exceptions.ConditionsImportError) as errMsg:
    utils.importConditions(fileName='raiseErrorfileName')
assert 'Conditions file not found:' in str(errMsg.value)
assert 'raiseErrorfileName' in str(errMsg.value)
conds = utils.importConditions(fileName_pkl)
assert conds[0] == expected_cond
with pytest.raises(exceptions.ConditionsImportError) as errMsg:
    utils.importConditions(fileName_docx)
assert 'Your conditions file should be an xlsx, csv, dlm, tsv or pkl file' == str(errMsg.value)
with pytest.raises(exceptions.ConditionsImportError) as err:
    utils.importConditions(str(Path(fixturesPath) / 'duplicateHeaders.csv'))
assert "'dupe'" in str(err.value)
all_conditions = utils.importConditions(standard_files[0])
assert len(all_conditions) == 6
num_selected_conditions = 1001
selected_conditions = utils.importConditions(standard_files[0], selection=np.concatenate(([0.9], np.random.random(num_selected_conditions - 1) * len(all_conditions))))
assert selected_conditions[0] == expected_cond
assert len(selected_conditions) == num_selected_conditions
```

## 2. test_writing

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_tools/test_versionchooser.py:42`
- Note: Workflow: test writing

```python
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

## 3. test_all_code_component_tabs

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_experiment/test_components/test_CodeComponent.py:26`
- Note: Workflow: test all code component tabs

```python
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

## 4. test_all_code_component_tabs

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_experiment/test_components/test_CodeComponent.py:26`
- Note: Workflow: test all code component tabs

```python
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

## 5. test_param_str

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_experiment/test_params.py:167`
- Note: Workflow: Test that params convert to str as expected in both Python and JS

```python
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

## 6. test_typing

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_visual/test_textbox.py:399`
- Note: Workflow: Check that continuous typing doesn't break anything

```python
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

## 7. test_loaded_namespace

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_experiment/test_experiment.py:104`
- Note: Workflow: test loaded namespace

```python
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

## 8. test_soundHeard

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_validators/test_voicekeyValidator.py:45`
- Note: Workflow: Check that the sound sensor validator detects a sound played from an audible speaker.

```python
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

## 9. test_combinations

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_visual/test_form.py:115`
- Note: Workflow: Test that question options interact well

```python
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

## 10. test_combinations

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_visual/test_form.py:115`
- Note: Workflow: Test that question options interact well

```python
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

## 11. test_glyph_rendering

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_visual/test_textbox.py:45`
- Note: Workflow: test glyph rendering

```python
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

## 12. test_glyph_rendering

- Kind: `test-workflow`
- Source: `psychopy/psychopy/tests/test_visual/test_textbox.py:45`
- Note: Workflow: test glyph rendering

```python
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

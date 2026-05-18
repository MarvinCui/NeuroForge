---
name: psychopy
description: Local codebase analysis for psychopy
doc_version: 
---

# psychopy Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `psychopy`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

### 🎨 Design Patterns Detected

*From C3.1 codebase analysis (confidence > 0.7)*

- **Builder**: 1 instances
- **Strategy**: 1 instances

*Total: 2 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: test movement** (complexity: 1.00)

```python
self.win.color = 'black'
self.win.flip()
obj = visual.DotStim(self.win, nDots=1, fieldPos=(0, 0), fieldSize=(1, 1), units='height', dotSize=(32, 32), dotLife=0, noiseDots='direction', dir=0, speed=0.25, coherence=1)
obj.draw()
screen1 = np.array(self.win._getFrame(buffer='back'))
self.win.flip()
obj.draw()
screen2 = np.array(self.win._getFrame(buffer='back'))
self.win.flip()
compound = np.clip(screen1 + screen2, 0, 255)
assert compound.mean() > screen1.mean() and compound.mean() > screen2.mean(), 'Dot stimulus does not appear to have moved across two frames.'
```

**Workflow: test addData with mutable values** (complexity: 1.00)

```python
exp = data.ExperimentHandler(name='testExp', savePickle=False, saveWideText=True, dataFileName=self.tmpDir + 'mutables')
mutant = [1]
exp.addData('mutable', mutant)
exp.nextEntry()
mutant[0] = 9999
exp.addData('mutable', mutant)
exp.nextEntry()
exp.saveAsWideText(exp.dataFileName + '.csv', delim=',')
with io.open(exp.dataFileName + '.csv', 'r', encoding='utf-8-sig') as f:
    contents = f.read()
assert contents == 'thisRow.t,notes,mutable,\n,,[1],\n,,[9999],\n'
```

**Workflow: Check that the sound sensor validator detects a sound played from an audible speaker.** (complexity: 1.00)

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

**Workflow: Test the conversion (forward and inverse) for HSV to RGB (signed). This
does not test for "correctness", but rather if the functions provided for
the conversion are the inverse of each other.** (complexity: 1.00)

```python
'Test the conversion (forward and inverse) for HSV to RGB (signed). This\n    does not test for "correctness", but rather if the functions provided for\n    the conversion are the inverse of each other.\n\n    '
N = 1024
np.random.seed(123456)
hsvColors = np.zeros((N, 3))
hsvColors[:, 0] = np.random.randint(0, 360, (N,))
hsvColors[:, 1:] = np.random.uniform(0, 1, (N, 2))
hsvOut = rgb2hsv(hsv2rgb(hsvColors))
assert np.allclose(hsvOut, hsvColors)
hsvColors = np.zeros((N, N, 3))
hsvColors[:, :, 0] = np.random.randint(0, 360, (N, N))
hsvColors[:, :, 1:] = np.random.uniform(0, 1, (N, N, 2))
hsvOut = rgb2hsv(hsv2rgb(hsvColors))
assert np.allclose(hsvOut, hsvColors)
```

**Workflow: Test the conversion (forward) for DKL to RGB (signed).

    ** (complexity: 1.00)

```python
'Test the conversion (forward) for DKL to RGB (signed).\n\n    '
N = 1024
np.random.seed(123456)
dklColors = np.zeros((N, 3))
dklColors[:, 0] = np.random.uniform(0, 90, (N,))
dklColors[:, 1] = np.random.uniform(0, 360, (N,))
dklColors[:, 2] = np.random.uniform(0, 1, (N,))
_ = dkl2rgb(dklColors)
dklWhite = [90, 0, 1]
assert np.allclose(np.asarray((1, 1, 1)), dkl2rgb(dklWhite))
```

**Instantiate ElementArrayStim: test element array colors** (complexity: 1.00)

```python
obj = visual.ElementArrayStim(self.win, units='pix', fieldPos=(0, 0), fieldSize=(128, 128), fieldShape='square', nElements=2, sizes=[[64, 128], [64, 128]], xys=[[-32, 0], [32, 0]], elementMask=None, elementTex=None)
```

**Workflow: test StaticPeriod** (complexity: 1.00)

```python
if RUNNING_IN_VM:
    pytest.skip()
static = StaticPeriod()
static.start(0.1)
wait(0.05)
assert static.complete() == 1
static.start(0.1)
wait(0.11)
assert static.complete() == 0
win = Window(autoLog=False)
static = StaticPeriod(screenHz=60, win=win)
static.start(0.002)
assert win.recordFrameIntervals is False
static.complete()
assert static._winWasRecordingIntervals == win.recordFrameIntervals
win.close()
refresh_rate = 100.0
period_duration = 0.1
timer = CountdownTimer()
win = Window(autoLog=False)
static = StaticPeriod(screenHz=refresh_rate, win=win)
static.start(period_duration)
timer.reset(period_duration)
static.complete()
if systemtools.isVM_CI():
    tolerance = 0.01
else:
    tolerance = 0.001
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
win.close()
```

**Workflow: test writing** (complexity: 1.00)

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

**Workflow: test importConditions** (complexity: 1.00)

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

**Workflow: Test if screenHz parameter is respected, i.e., if after completion of the
StaticPeriod, 1/screenHz seconds are still remaining, so the period will
complete after the next flip.** (complexity: 1.00)

```python
'Test if screenHz parameter is respected, i.e., if after completion of the\n    StaticPeriod, 1/screenHz seconds are still remaining, so the period will\n    complete after the next flip.\n    '
refresh_rate = 100.0
period_duration = 0.1
timer = CountdownTimer()
win = Window(autoLog=False)
static = StaticPeriod(screenHz=refresh_rate, win=win)
static.start(period_duration)
timer.reset(period_duration)
static.complete()
if systemtools.isVM_CI():
    tolerance = 0.01
else:
    tolerance = 0.001
assert np.allclose(timer.getTime(), 1.0 / refresh_rate, atol=tolerance)
win.close()
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 135
**Total Settings:** 1798
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 135 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 48
**Categories:** 7

### Overview

- **README.md** (`README.md`)

### Architecture

- **README.md** (`psychopy/demos/builder/Design Templates/branchedExperiment/README.md`)
- **readme.md** (`psychopy/demos/builder/Design Templates/dualWindow/readme.md`)
- **README.md** (`psychopy/demos/builder/Design Templates/psychophysicsStaircase/README.md`)
- **README.md** (`psychopy/demos/builder/Design Templates/psychophysicsStairsInterleaved/README.md`)
- **README.md** (`psychopy/demos/builder/Design Templates/randomisedBlocks/README.md`)
- *...and 1 more*

### Features

- **readme.md** (`psychopy/demos/builder/Feature Demos/buttonBox/readme.md`)
- **readme.md** (`psychopy/demos/builder/Feature Demos/gratings/readme.md`)
- **readme.md** (`psychopy/demos/builder/Feature Demos/movies/readme.md`)
- **readme.md** (`psychopy/demos/builder/Feature Demos/noise/readme.md`)
- **readme.md** (`psychopy/demos/builder/Feature Demos/pilotMode/readme.md`)
- *...and 3 more*

### Authors

- **AUTHORS.md** (`AUTHORS.md`)

### Community

- **code-of-conduct.md** (`code-of-conduct.md`)

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis

# jspsych Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Building Surveys in jsPsych #3

- Kind: `documentation`
- Source: `references/documentation/other/building-surveys.md`
- Note: Documentation code block extracted for implementation use.

```javascript
// Create an array of color choices
const color_choices = ['red', 'green', 'blue', 'yellow', 'pink', 'orange', 'purple'];

// Create an html-button-response trial where the participant can choose a color
const select_color_trial = {
  type: jsPsychHtmlButtonResponse,
  stimulus: '<p>Which of these is your favorite color?</p>',
  choices: color_choices,
  button_html: (choice) => `<button class="jspsych-btn" style="color:${choice};">%choice%</button>`,
  data: {trial_id: 'color_trial'}
};

// Create the survey JSON 
const color_survey_json = {
  elements: [{
    type: "boolean",
    renderAs: "radio",
    name: "color_confirmation",
    title: "" // This value will be set in the survey function
  }]
};

// Create a survey function to access the participant's response 
// from an earlier trial and modify the survey accordingly
const color_survey_function = (survey) => {
  // Get the earlier color selection response (button index) from the jsPsych data
  const color_choice_index = jsPsych.data.get().filter({trial_id: 'color_trial'}).values()[0].response;
  const color_choice = color_choices[color_choice_index];
  // Get the question that we want to modify
  const color_confirmation_question = survey.getQuestionByName('color_confirmation');
  // Change the question title to include the name of the color that was selected
  color_confirmation_question.title = `
    Earlier you chose ${color_choice.toUpperCase()}. Do you still like that color?
  `;
}

// Create the jsPsych survey trial using both the survey JSON and survey function
const color_survey_trial = {
  type: jsPsychSurvey,
  survey_json: color_survey_json,
  survey_function: color_survey_function
};

jsPsych.run([select_color_trial, color_survey_trial]);
```

## 2. mouse-tracking #3

- Kind: `documentation`
- Source: `references/documentation/other/mouse-tracking.md`
- Note: Documentation code block extracted for implementation use.

```javascript
var trial = {
          type: jsPsychHtmlButtonResponse,
          stimulus: '<div id="target" style="width:250px; height: 250px; background-color: #333; margin: auto;"></div>',
          choices: ['Done'],
          prompt: "<p>Move your mouse around inside the square.</p>",
          extensions: [
            {type: jsPsychExtensionMouseTracking, params: {targets: ['#target']}}
          ],
          data: {
            task: 'draw'
          }
        };

        var replay = {
          type: jsPsychHtmlButtonResponse,
          stimulus: '<div id="target" style="width:250px; height: 250px; background-color: #333; margin: auto; position: relative;"></div>',
          choices: ['Done'],
          prompt: "<p>Here's the recording of your mouse movements</p>",
          on_load: function(){
            var mouseMovements = jsPsych.data.get().last(1).values()[0].mouse_tracking_data;
            var targetRect = jsPsych.data.get().last(1).values()[0].mouse_tracking_targets['#target'];
            
            var startTime = performance.now();

            function draw_frame() {
              var timeElapsed = performance.now() - startTime;
              var points = mouseMovements.filter((x) => x.t <= timeElapsed);
              var html = ``;
              for(var p of points){
                html += `<div style="width: 3px; height: 3px; background-color: blue; position: absolute; top: ${p.y - 1 - targetRect.top}px; left: ${p.x - 1 - targetRect.left}px;"></div>`
              }
              document.querySelector('#target').innerHTML = html;
              if(points.length < mouseMovements.length) {
                requestAnimationFrame(draw_frame);
              }
            }

            requestAnimationFrame(draw_frame);

          },
          data: {
            task: 'replay'
          }
        }
```

## 3. html-button-response #3

- Kind: `documentation`
- Source: `references/documentation/other/html-button-response.md`
- Note: Documentation code block extracted for implementation use.

```javascript
const trial = {
            type: jsPsychHtmlButtonResponse,
            stimulus: `<div style="width: 600px">
                <div style="width: 50px; height: 50px; background-color: red; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: red; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: green; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: blue; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: red; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: red; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: green; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: blue; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: red; display: inline-block"></div>
                <div style="width: 50px; height: 50px; background-color: gray; display: inline-block"></div>
            </div>`,
            choices: ['red', 'green', 'blue'],
            prompt: "<p>What color should the gray block be?</p>",
            button_html: (choice) => `<div style="width: 80px; height: 80px; margin: 20px; background-color: ${choice}; cursor: pointer;"></div>`
        };
```

## 4. Media Preloading #2

- Kind: `documentation`
- Source: `references/documentation/other/media-preloading.md`
- Note: Documentation code block extracted for implementation use.

```javascript
// this image file cannot be automatically preloaded because it is embedded in 
// an HTML string
var image_trial = {
	type: jsPsychHtmlKeyboardResponse,
	stimulus: '<img src="img/file1.png"></img>',
}

// this audio file cannot be automatically preloaded because it is returned 
// from a function
var sound_trial = {
	type: jsPsychAudioKeyboardResponse,
	stimulus: function() { return 'audio/sound1.mp3' }
}

// these video files cannot be automatically preloaded because they are passed 
// into a trial using the jsPsych.timelineVariable function
var video_trials = {
	timeline: [
		{
			type: jsPsychVideoKeyboardResponse,
			stimulus: jsPsych.timelineVariable('video')
		}
	],
	timeline_variables: [
		{video: ['video/1.mp4']},
		{video: ['video/2.mp4']}
	]
}

// to manually preload media files, create an array of file paths for each 
// media type
var images = ['img/file1.png'];
var audio = ['audio/sound1.mp3'];
var video = ['video/1.mp4', 'video/2.mp4'];

// these array can be passed into the preload plugin using the images, audio 
// and video parameters
var preload = {
	type: jsPsychPreload,
	images: images,
	audio: audio,
	video: video
}

jsPsych.run([preload, image_trial, sound_trial, video_trials]);
```

## 5. Dynamic parameters #1

- Kind: `documentation`
- Source: `references/documentation/other/dynamic-parameters.md`
- Note: Documentation code block extracted for implementation use.

```javascript
var timeline = [];

var trial = {
  type: jsPsychHtmlKeyboardResponse,
  stimulus: '<<<<<',
  choices: ['f','j'],
  data: {
    stimulus_type: 'congruent',
    target_direction: 'left'
  },
  on_finish: function(data){
    // Score the keyboard response as correct or incorrect.
    if(jsPsych.pluginAPI.compareKeys(data.response, "f")){
      data.correct = true;
    } else {
      data.correct = false; 
    }
  }
}

var feedback = {
  type: jsPsychHtmlKeyboardResponse,
  trial_duration: 1000,
  stimulus: function(){
    // The feedback stimulus is a dynamic parameter because we can't know in advance whether
    // the stimulus should be 'correct' or 'incorrect'.
    // Instead, this function will check the accuracy of the last response and use that information to set
    // the stimulus value on each trial.
    var last_trial_correct = jsPsych.data.get().last(1).values()[0].correct;
    if(last_trial_correct){
      return "<p>Correct!</p>"; // the parameter value has to be returned from the function
    } else {
      return "<p>Wrong.</p>"; // the parameter value has to be returned from the function
    }
  }
}

timeline.push(trial, feedback);
```

## 6. reconstruction #2

- Kind: `documentation`
- Source: `references/documentation/other/reconstruction.md`
- Note: Documentation code block extracted for implementation use.

```javascript
var sample_function = function(param){
            var size = 50 + Math.floor(param*250);
            var html = '<div style="display: block; margin: auto; height: 300px; width: 300px; position: relative;">'+
            '<div style="display: block; position: absolute; top: '+(150 - size/2)+'px; left:'+(150 - size/2)+'px; background-color: #000000; '+
            'width: '+size+'px; height: '+size+'px;"></div></div><p>Press "h" to make the square larger. Press "g" to make the square smaller.</p>'+
            '<p>When the square is the same size as the previous one, click Continue.</p>';
            return html;
        }

        var match_item = {
            type: jsPsychHtmlKeyboardResponse,
            stimulus: '<div style="display: block; margin: auto; height: 300px; width: 300px; position: relative;">'+
            '<div style="display: block; position: absolute; top: '+(150 - 210/2)+'px; left:'+(150 - 210/2)+'px; background-color: #000000; '+
            'width: 210px; height: 210px;"></div></div>',
            choices: ['c'],
            post_trial_gap: 1250,
            prompt: '<p>Study the size of this square carefully. On the next screen you will have to recreate it. When you are ready, press "c".</p>'
        }

        var reconstruction = {
            type: jsPsychReconstruction,
            stim_function: sample_function,
            starting_value: 0.5,
        }
```

## 7. serial-reaction-time #3

- Kind: `documentation`
- Source: `references/documentation/other/serial-reaction-time.md`
- Note: Documentation code block extracted for implementation use.

```javascript
var instructions = {
          type: jsPsychHtmlButtonResponse,
          stimulus: '<p>Use the R, I, V, and M keys to respond.</p>',
          choices: ['Continue']
        }

        var grid = [
          [1,1],
          [1,1]
        ]

        var response_map = [
          ['r','i'],
          ['v','m']
        ]

        var trial_1 = {
          type: jsPsychSerialReactionTime,
          grid: grid,
          choices: response_map,
          target: [0,0],
          show_response_feedback: true,
          feedback_duration: 500
        }
        var trial_2 = {
          type: jsPsychSerialReactionTime,
          grid: grid,
          choices: response_map,
          target: [0,1],
          show_response_feedback: true,
          feedback_duration: 500
        }
        var trial_3 = {
          type: jsPsychSerialReactionTime,
          grid: grid,
          choices: response_map,
          target: [1,1],
          show_response_feedback: true,
          feedback_duration: 500
        }
        var trial_4 = {
          type: jsPsychSerialReactionTime,
          grid: grid,
          choices: response_map,
          target: [1,0],
          show_response_feedback: true,
          feedback_duration: 500
        }
```

## 8. record-video #3

- Kind: `documentation`
- Source: `references/documentation/other/record-video.md`
- Note: Documentation code block extracted for implementation use.

```javascript
const init_camera = {
          type: jsPsychInitializeCamera
        };

        const trial = {
          type: jsPsychHtmlButtonResponse,
          stimulus: `<div id="target" style="width:250px; height: 250px; background-color: #333; position: relative; margin: 2em auto;">
              <div class="orbit" style="width:25px; height:25px; border-radius:25px;background-color: #f00; position: absolute; top:calc(50% - 12px); left:calc(50% - 12px);"></div>
            </div>
            <style>
              .orbit {
                transform: translateX(100px);
                animation: orbit 4s infinite;
              }
              @keyframes orbit {
                0% {
                  transform: rotate(0deg) translateX(100px);
                }
                100% {
                  transform: rotate(360deg) translateX(100px);
                }
              }
            </style>`,
          choices: ['Done'],
          prompt: "<p>Video is recording. Click done after a few seconds.</p>",
          extensions: [
            {type: jsPsychExtensionRecordVideo}
          ]
        };
```

## 9. canvas-button-response #2

- Kind: `documentation`
- Source: `references/documentation/other/canvas-button-response.md`
- Note: Documentation code block extracted for implementation use.

```javascript
function filledCirc(canvas, radius, color) {
            var ctx = canvas.getContext("2d");
            ctx.beginPath();
            ctx.arc(150, 150, radius, 0, 2 * Math.PI);
            ctx.fillStyle = color;
            ctx.fill();
        }

        var circle_1 = {
            type: jsPsychCanvasButtonResponse,
            stimulus: function(c) {
                filledCirc(c, 100, 'blue');
            },
            canvas_size: [300, 300],
            choices: ['Red', 'Green', 'Blue'],
            prompt: '<p>What color is the circle?</p>',
            data: {color: 'blue', radius: 100}
        };

        var circle_2 = {
            type: jsPsychCanvasButtonResponse,
            stimulus: function(c) {
                filledCirc(c, 150, 'green');
            },
            canvas_size: [300, 300],
            choices: ['Larger', 'Smaller'],
            stimulus_duration: 1000,
            prompt: '<p>Is this circle larger or smaller than the last one?</p>'+
                '<p>Stimulus will be hidden after 1 second.</p>',
            data: {color: 'green', radius: 150}
        };
```

## 10. Media Preloading #3

- Kind: `documentation`
- Source: `references/documentation/other/media-preloading.md`
- Note: Documentation code block extracted for implementation use.

```javascript
// this file can be preloaded automatically
var image_trial = {
	type: jsPsychImageKeyboardResponse,
	stimulus: 'img/file1.png'
}

// this file can be preloaded automatically
var sound_trial = {
	type: jsPsychAudioKeyboardResponse,
	stimulus: 'audio/hello.mp3'
}

// these files must be preloaded manually
var video_trials = {
	timeline: [
		{
			type: jsPsychVideoKeyboardResponse,
			stimulus: jsPsych.timelineVariable('video')
		}
	],
	timeline_variables: [
		{video: ['video/1.mp4']},
		{video: ['video/2.mp4']}
	]
}

var video = ['video/1.mp4', 'video/2.mp4'];

var preload = {
	type: jsPsychPreload,
	auto_preload: true, // automatically preload the image and audio files
	video: video // manually preload the videos used with timeline variables
}

jsPsych.run([preload, image_trial, sound_trial, video_trials]);
```

# jspsych-single-stim plugin

This plugin displays an image or HTML-formatted content and allows the subject to respond by pressing a key on the keyboard. The stimulus can be displayed until a response is given, or for a pre-determined amount of time. The trial can be ended automatically if the subject has failed to respond within a fixed length of time.

Because this plugin can display any HTML content, it is quite versatile. It can be used for any situation in which the response generated by the subject is a single keystroke.

## Parameters

This table lists the parameters associated with this plugin. Parameters with a default value of *undefined* must be specified. Other parameters can be left unspecified if the default value is acceptable.

Parameter | Type | Default Value | Description
----------|------|---------------|------------
stimulus | string | *undefined* | The stimulus to display. Either HTML-formatted, or the path to an image.
is_html | boolean | false | If `stimulus` is an HTML-formatted string, this parameter needs to be set to `true`.
choices | array | [ ] | This array contains the keys that the subject is allowed to press in order to respond to the stimulus. Keys can be specified as their [numeric key code](http://www.cambiaresearch.com/articles/15/javascript-char-codes-key-codes) or as characters (e.g. `'a'`, `'q'`). The default value of an empty array means that all keys will be accepted as valid responses.
prompt | string | "" | This string can contain HTML markup. Any content here will be displayed below the stimulus. The intention is that it can be used to provide a reminder about the action the subject is supposed to take (e.g. which key to press).
timing_stim | numeric | -1 | How long to show the stimulus for in milliseconds. If the value is -1, then the stimulus will be shown until the subject makes a response.
timing_response | numeric | -1 | How long to wait for the subject to make a response before ending the trial in milliseconds. If the subject fails to make a response before this timer is reached, the the subject's response will be recorded as -1 for the trial and the trial will end. If the value of this parameter is -1, then the trial will wait for a response indefinitely.
response_ends_trial | boolean | true | If true, then the trial will end whenever the subject makes a response (assuming they make their response before the cutoff specified by the `timing_response` parameter). If false, then the trial will continue until the value for `timing_response` is reached. You can use this parameter to force the subject to view a stimulus for a fixed amount of time, even if they respond before the time is complete.

## Data Generated

In addition to the [default data collected by all plugins](overview#datacollectedbyplugins), this plugin collects the following data for each trial.

Name | Type | Value
-----|------|------
stimulus | string | Either the path to the image file or the string containing the HTML formatted content that the subject saw on this trial.
key_press | numeric | Indicates which key the subject pressed. The value is the [numeric key code](http://www.cambiaresearch.com/articles/15/javascript-char-codes-key-codes) corresponding to the subject's response.
rt | numeric | The response time in milliseconds for the subject to make a response. The time is measured from when the stimulus first appears on the screen until the subject's response.

## Examples

#### Displaying image until subject gives a response

```javascript
var trial = {
	type: 'single-stim',
	stimulus: 'img/happy_face.png'
}
```

#### Restricting which keys the subject can use to respond

```javascript
var trial = {
	type: 'single-stim',
	stimulus: 'img/happy_face.png',
	choices: ['h','s']
}
```

#### Displaying HTML content for a fixed length of time

```javascript
var trial = {
	type: 'single-stim',
	stimulus: '<p>Radio</p>',
	is_html: true,
	timing_response: 1500,
	response_ends_trial: false
}
```

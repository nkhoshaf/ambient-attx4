#Ambient
Driver for the ambient-attx4 Tessel ambient (light and sound detecting) module. The hardware documentation can be found [here](https://github.com/tessel/hardware/blob/master/modules-overview.md#ambient).

Use the Ambient module to gather data about the ambient light and sound levels.

The module currently supports 'streams' of light levels and sound levels, as well as trigger levels for light and sound levels. You can use triggers to get notified when, for example, a light turns on or somebody claps.

All the values received and used for triggers are between 0.0 and 1.0.

You'll notice that the light readings seem to be logarithmic - when making the ambient light brighter, the reading will increase slowly and then get faster. That's a property of the photodiode itself.

If you run into any issues you can ask for support on the [Ambient Module Forums](http://forums.tessel.io/category/ambient).

###Installation
```sh
npm install ambient-attx4
```

###Example
```js
// Any copyright is dedicated to the Public Domain.
// http://creativecommons.org/publicdomain/zero/1.0/

/*********************************************
This ambient module example reports sound and
light levels to the console, and console.logs
whenever a specified light or sound level
trigger is met.
*********************************************/

var tessel = require('tessel');
<<<<<<< HEAD
var ambient = require('ambient-attx4').use(tessel.port['A']);
=======
var ambientlib = require('../');// Replace '../' with 'ambient-attx4' in your own code

var ambient = ambientlib.use(tessel.port['A']); 
>>>>>>> polishing the readme and examples

ambient.on('ready', function () {
 // Get a stream of light data
  ambient.on('light', function(data) {
    console.log("Got some  light: ", data);
  });

  // Get a stream of sound level data
  ambient.on('sound', function(data) {
    console.log("Got some  sound: ", data);
  });

  // Set trigger levels
  // The trigger value is a float between zero to 1
  ambient.setLightTrigger(0.15);

  ambient.on('light-trigger', function(data) {
    console.log("Our light trigger was hit:", data);

    // Clear the trigger so it stops firing
    ambient.clearLightTrigger();
    //After 1.5 seconds reset light trigger
    setTimeout(function () { 
<<<<<<< HEAD

        ambient.setLightTrigger(0.15);

=======

        ambient.setLightTrigger(0.15);

>>>>>>> polishing the readme and examples
    },1500);
  });

  // Set a sound level trigger
  // The trigger is a float between 0 and 1
  ambient.setSoundTrigger(0.43);

  ambient.on('sound-trigger', function(data) {

    console.log("Something happened with sound: ", data);

    // Clear it
    ambient.clearSoundTrigger();

    //After 1.5 seconds reset sound trigger
    setTimeout(function () { 
      
        ambient.setSoundTrigger(0.43);

    },1500);

  });
});

ambient.on('error', function (err) {
  console.log(err)
});
```

###Methods

&#x20;<a href="#api-ambient-clearLightTrigger-callback-err-triggerVal-Clears-trigger-listener-for-light-trigger" name="api-ambient-clearLightTrigger-callback-err-triggerVal-Clears-trigger-listener-for-light-trigger">#</a> ambient<b>.clearLightTrigger</b>( callback(err, triggerVal) )  
 Clears trigger listener for light trigger.  

&#x20;<a href="#api-ambient-clearSoundTrigger-callback-err-triggerVal-Clears-trigger-listener-for-sound-trigger" name="api-ambient-clearSoundTrigger-callback-err-triggerVal-Clears-trigger-listener-for-sound-trigger">#</a> ambient<b>.clearSoundTrigger</b>( callback(err, triggerVal) )  
 Clears trigger listener for sound trigger.  

&#x20;<a href="#api-ambient-getLightBuffer-callback-err-data-Gets-the-last-10-light-readings" name="api-ambient-getLightBuffer-callback-err-data-Gets-the-last-10-light-readings">#</a> ambient<b>.getLightBuffer</b>( callback(err, data) )  
 Gets the last 10 light readings.  

&#x20;<a href="#api-ambient-getLightLevel-callback-err-data-Gets-a-single-data-point-of-light-level" name="api-ambient-getLightLevel-callback-err-data-Gets-a-single-data-point-of-light-level">#</a> ambient<b>.getLightLevel</b>( callback(err, data) )  
 Gets a single data point of light level.  

&#x20;<a href="#api-ambient-getSoundBuffer-callback-err-data-Gets-the-last-10-sound-readings" name="api-ambient-getSoundBuffer-callback-err-data-Gets-the-last-10-sound-readings">#</a> ambient<b>.getSoundBuffer</b>( callback(err, data) )  
 Gets the last 10 sound readings.  

&#x20;<a href="#api-ambient-getSoundLevel-callback-err-data-Gets-a-single-data-point-of-sound-level" name="api-ambient-getSoundLevel-callback-err-data-Gets-a-single-data-point-of-sound-level">#</a> ambient<b>.getSoundLevel</b>( callback(err, data) )  
 Gets a single data point of sound level.  

&#x20;<a href="#api-ambient-setLightTrigger-triggerVal-callback-err-triggerVal-Sets-a-trigger-to-emit-a-light-trigger-event-when-triggerVal-is-reached-triggerVal-is-a-float-between-0-and-1-0" name="api-ambient-setLightTrigger-triggerVal-callback-err-triggerVal-Sets-a-trigger-to-emit-a-light-trigger-event-when-triggerVal-is-reached-triggerVal-is-a-float-between-0-and-1-0">#</a> ambient<b>.setLightTrigger</b>( triggerVal, callback(err, triggerVal) )  
 Sets a trigger to emit a 'light-trigger' event when triggerVal is reached. triggerVal is a float between 0 and 1.0.  

&#x20;<a href="#api-ambient-setSoundTrigger-triggerVal-callback-err-triggerVal-Sets-a-trigger-to-emit-a-sound-trigger-event-when-triggerVal-is-reached-triggerVal-is-a-float-between-0-and-1-0" name="api-ambient-setSoundTrigger-triggerVal-callback-err-triggerVal-Sets-a-trigger-to-emit-a-sound-trigger-event-when-triggerVal-is-reached-triggerVal-is-a-float-between-0-and-1-0">#</a> ambient<b>.setSoundTrigger</b>( triggerVal, callback(err, triggerVal) )  
 Sets a trigger to emit a 'sound-trigger' event when triggerVal is reached. triggerVal is a float between 0 and 1.0.  

###Events

&#x20;<a href="#api-ambient-on-error-callback-err-Emitted-upon-error" name="api-ambient-on-error-callback-err-Emitted-upon-error">#</a> ambient<b>.on</b>( 'error', callback(err) )  
 Emitted upon error.  

&#x20;<a href="#api-ambient-on-light-callback-lightData-Get-a-stream-of-light-data" name="api-ambient-on-light-callback-lightData-Get-a-stream-of-light-data">#</a> ambient<b>.on</b>( 'light', callback(lightData) )  
 Get a stream of light data.  

&#x20;<a href="#api-ambient-on-light-trigger-callback-lightTriggerValue-Emitted-upon-crossing-light-trigger-threshold" name="api-ambient-on-light-trigger-callback-lightTriggerValue-Emitted-upon-crossing-light-trigger-threshold">#</a> ambient<b>.on</b>( 'light-trigger', callback(lightTriggerValue) )  
 Emitted upon crossing light trigger threshold.  

&#x20;<a href="#api-ambient-on-ready-callback-Emitted-upon-first-successful-communication-between-the-Tessel-and-the-module" name="api-ambient-on-ready-callback-Emitted-upon-first-successful-communication-between-the-Tessel-and-the-module">#</a> ambient<b>.on</b>( 'ready', callback() )  
 Emitted upon first successful communication between the Tessel and the module.  

&#x20;<a href="#api-ambient-on-sound-callback-soundData-Get-a-stream-of-sound-level-data" name="api-ambient-on-sound-callback-soundData-Get-a-stream-of-sound-level-data">#</a> ambient<b>.on</b>( 'sound', callback(soundData) )  
 Get a stream of sound level data.  

&#x20;<a href="#api-ambient-on-sound-trigger-callback-soundTriggerValue-Emitted-upon-crossing-sound-trigger-threshold" name="api-ambient-on-sound-trigger-callback-soundTriggerValue-Emitted-upon-crossing-sound-trigger-threshold">#</a> ambient<b>.on</b>( 'sound-trigger', callback(soundTriggerValue) )  
 Emitted upon crossing sound trigger threshold.  

###Further Examples  
* [Ambient Stream](https://github.com/tessel/ambient-attx4/blob/master/examples/ambient_stream.js). This example demonstrates the two methods for getting the ambient module's data. 

### License
MIT or Apache 2.0, at your option  

# node-play-mp3

[![Coverage Status](https://coveralls.io/repos/github/CommaSword/node-play-mp3/badge.svg?branch=master)](https://coveralls.io/github/CommaSword/node-play-mp3?branch=master)
[![Build Status](https://travis-ci.org/CommaSword/node-play-mp3.svg?branch=master)](https://travis-ci.org/CommaSword/node-play-mp3)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

Use the browser Audio api to play mp3 files in node.
Browser api brought to you by electron (specifically `electron-spawn`)
The motivation being this should be more cross-platform friendly.
API is still early stages and supposed the basic stuff, we're open to new functionality being requested and/or contributed.


## usage

Require the `createAudio` method and use it to get the `Audio` constructor.
The Audio constructor has more or less the same API as the browser Audio global. See the API section for specific quircks.

Please note that the `createAudio` method instantiates an `electron` child_process in order to access the the browser API.
Calling it multiple times will instantiate multiple `electron` processes. This is probably not what you want.
You probably want to create multiple files using the Audio pseudo constructor. Though if multiple electron instances is your thing, knock your socks off.

```javascript
const { createAudio } = require('node-play-mp3')
const Audio = createAudio()

(async () => {
  const myFile = await Audio(`${__dirname}/mp3/foo.mp3`)
  await play() // set both files at 50% volume
  await Audio.volume(0.5)
  const currentVolume = await Audio.volume() // 0.5
  await Audio.loop()
  await Audio.stop()
})()

```

## API
Should be the same as the browser Audio api, except it returns promises and thus uses traditional functions rather than getters/setters.

### constructor
```javascript
const myFile = await Audio('/path/to/my/file')
```

### play / stop
```javascript
const myFile = await Audio('/path/to/my/file')
await myFile.play() // plays the file
await myFile.stop() // stops the file
```

### volume
```javascript
const myFile = await Audio('/path/to/my/file')
await myFile.volume(0.5) // changes the volume, similar to the browser myFile.volume = 0.5
```

### loop
```javascript
const myFile = await Audio('/path/to/my/file')
await myFile.loop(true) // loops the file similar to the browser myFile.loop = true
await myFile.loop(false) // unloops the file similar to the browser myFile.loop = false
```

## license
MIT
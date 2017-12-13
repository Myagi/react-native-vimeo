# React Native Vimeo Player

It is easy enough to embed Vimeo videos in your React Native app using a standard
React Native Webview, however it is impossible to access the Vimeo player API that way.
This component allows you to easily embed a Vimeo video in your app and have full access to
the Vimeo player JS API (documented at https://developer.vimeo.com/player/js-api).

## Installation

1. Go through the instructions for installing the
`React Native Webview Bridge` component, found here: https://github.com/alinz/react-native-webview-bridge.

2. Run `npm install react-native-vimeo -S` within your project.

3. Compile and build to make sure everything is set up properly.

## Usage

```
  <Vimeo
    ref='video'
    videoId='2619976' // Vimeo video ID
    onReady={ () => console.log('Video is ready') }
    onPlay={ () => console.log('Video is playing') }
    onPlayProgress={ data => console.log('Video progress data:', data) }
    onFinish={ () => console.log('Video is finished') }
    height{300}
  />
```

`this.refs.video.api('getDuration', dur => console.log('Video duration is:', dur))`

NOTE: Any `api` method calls must be made after `onReady` has been called.

## How it works

Internally, a webview loads a HTML page which is hosted via Github Pages. This HTML page loads your
Vimeo video in an iFrame, then uses the Froogaloop JS library provided by Vimeo to pass event
information through the webview bridge to your application. Vimeo API calls are made by sending a
message to the HTML page via the webview bridge.

Ideally, the HTML page content would just be passed as a string into the webview, however if that
were the case then the Vimeo JS API would not function. As stated in the Vimeo JS API
documentation, the Froogaloop library can only interact with the Vimeo iFrame when the page is
served up by a web server, not when it is loaded locally.

If you would like to view the contents of the HTML page used, simply clone this repo
and checkout the `gh-pages` branch (more info here
https://help.github.com/articles/creating-project-pages-manually/). Alternatively, just visit
http://myagi.github.io/react-native-vimeo/ and view the source.

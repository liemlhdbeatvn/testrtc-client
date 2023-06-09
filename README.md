# Daily testRTC client

This repository contains everything you need to test [Daily WebRTC calls](https://daily.co) in various configurations in [testRTC](https://testrtc.com). This consists of a simple Daily client that is able to create rooms and join calls in various configurations and a set of testRTC scripts set up to test Daily performance by using this client.

It is intended to facilitate quick deployment to [Netlify](https://netlify.com) to get up and running.

## Getting started

### Getting a Daily API key

You will need a Daily API key. To get one, sign up for a free [Daily account](https://dashboard.daily.co/signup). You will find your API key in your [Daily dashboard](https://dashboard.daily.co/developers).

### Deployment

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/daily-co/testrtc-client&stack=cms)

### Using our prebuilt testRTC scripts

You can import the JSON files from the `testrtc` directory into your testRTC account. Replace the Service URL with the address of your Netlify deployment. This can be done by two methods:

* Clicking the `Import` button in your testRTC test dashboard and navigating to the relevant test JSON file.
* Using the [`@testrtc/scripts-import-export`](https://www.npmjs.com/package/@testrtc/scripts-import-export) package with your testRTC API key.

Check out [testRTC's testing documentation](https://testrtc.com/article-categories/testingrtc/) for more information on using testRTC.

### Running locally

Currently, local runs are supported on OS X and Linux (including WSL).

1. `mv env.sample .env`
1. Set your Daily API key in `.env`
1. `npm i`
1. `npm run dev`

⚠️ The above process will result in your local `netlify.toml` file being modified with your Daily API key. This should be set back to `"DAILY_API_KEY_PLACEHOLDER"` automatically when you exit the development environment, but **always double check to make sure you do not commit the file with your API key**!

## Writing your own tests

The test client allows callers to specify their own room creation and call configuration options as query prameters. You can use these if you'd like to modify our bundled tests or write your own:

* `callOptions`: JSON string matching Daily's [call object configuration properties](https://docs.daily.co/reference/daily-js/factory-methods/create-call-object)
* `roomParams`: JSON string matching Daily's [room configuration properties](https://docs.daily.co/reference/rest-api/rooms/config)
* `roomURL`: A string containing the full URL to a Daily room for testRTC agents to join.
* `setBandwidth`: A JSON string matching the expected parameter taken by Daily's [`setBandwidth()`](https://docs.daily.co/reference/daily-js/instance-methods/set-bandwidth#main) API method. If provided, the client will call `setBandwidth()` once the call is joined.
* `codec`: Either `"VP8"`, `"VP9"`, or `"H264"`. Which video codec to set as preferred, with the default being VP8.

### Example

a `GET` request to the following URL will result in a room being created which will connect to the Sydney signaling server:

```
https://your-deployment.netlifyapp.com/?roomParams={"geo":"ap-southeast-2"}
```

## Contributing and feedback

Please run `npm run fix` to run eslint and prettier. This will format and auto-fix what it can, outputting any remaining issues you need to handle manually to the console.

Ensure all tests pass with `npm run test`.
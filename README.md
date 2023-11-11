# i-Ready Lesson Environment Vulnerability

This vulnerability in i-Ready's lesson allows for manipulation, tricking the lesson into changing environments.

## How it Works

i-Ready's lesson checks the environment using the following code:
```js
key: "isIntegratedEnvironment",
value: function e() {
  return window !== window.parent
}
```
This code is highly vulnerable as window.parent can be overridden, posing a security risk. A more secure alternative would be using window.top, which cannot be overridden. Interestingly, other parts of the codebase use window.top, but this specific instance uses window.parent. Furthermore, using window.parent here can cause the code to break if used before the lesson is fully loaded due to improper checks elsewhere.

# Usage

## i-Ready enviroment
This manipulates the lesson into thinking it's in an iframe within the actual i-Ready environment.
```js
html5Iframe.contentWindow.parent = { postMessage : console.log }
```
Note: Setting postMessage to console.log is done to prevent errors and observe the behavior of the associated Penpal.

## Local enviroment
This manipulates the lesson into thinking it's not in an iframe, simulating the scenario where the URL is directly opened.
```js
html5Iframe.contentWindow.parent = html5Iframe.contentWindow
```

# lesson-env-vuln
i-Ready lesson vulnerability that tricks lesson into changing enviroments

# How it works
i-Ready's lesson checks enviroment using this. This is extremely vulnerable because window.parent can be overriden. They could easily fix it by using window.top because it can't be overriden.
Interesting that they use window.top in other places but used parent here, in fact it breaks if you use it before lesson is fully loaded because of the other proper checks.
```js
key: "isIntegratedEnvironment",
value: function e() {
  return window !== window.parent
}
```

# Usage

## i-Ready enviroment
tricks lesson into thinking its in an iframe in the real i-Ready enviroment. <br>
sidenote : you can make the parent = `{}` i just made postMessage = console.log to prevent errors and to look at whatever penpal is doing. <br>
```js
html5Iframe.contentWindow.parent = { postMessage : console.log }
```

## Local enviroment
tricks lesson into thinking its not in an iframe and that you just opened the url. <br>
```js
html5Iframe.contentWindow.parent = html5Iframe.contentWindow
```

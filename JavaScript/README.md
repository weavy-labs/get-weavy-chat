# Drop-in UI

The Drop-in UI is a JavaScript library that you add to your existing app or website. The library enables you to quickly add collaboration features such as messaging, document collaboration, and more to your application. It handles Single-Sign-On (SSO) between your app and Weavy, and features an API for initializing and rendering Weavy UI components that are served from the Weavy.Dropin area on the Weavy backend.

## Getting started
Follow the steps below and we'll show you how to install and get started with the Drop-in UI.

###### 1. Add the Drop-in UI
The easiest way to install the library is by adding it with npm install (you can also clone the open-source weavy-dropin-js repo and build it yourself).
```JS
npm install @weavy/dropin-js
```
Another option is to include a <script> tag in the <head> element of your page (in the example below we reference a pre-built version from the [jsDelivr CDN](https://www.jsdelivr.com/))
```HTML
<script src="https://cdn.jsdelivr.net/npm/@weavy/dropin-js/dist/weavy-dropin.js" crossorigin="anonymous"></script>
```

###### 2. Initialize Weavy
The Weavy instance is the main entry point for the Drop-in UI. It sets up an authenticated connection to your Weavy backend and handles realtime communication, event distribution, and more.

The minimum configuration requires the url to your Weavy backend and a tokenFactory function that is reponsible for providing an access_token for your authenticated user. Check out the [authentication documentation](https://www.weavy.com/docs/frontend/drop-in/authentication) for details on how to implement this function.
  
```JavaScript
// import Weavy if you are using npm and a build system such as webpack
import Weavy from "@weavy/dropin-js";

const weavy = new Weavy({
  url: "{WEAVY_BACKEND_URL}",
  tokenFactory: async () => "{ACCESS_TOKEN}"
});
```
  
###### 3. Add apps
After initializing the Weavy instance you can start adding Weavy apps (UI components) to your website. The apps are presented using server rendered HTML and integrated by the frontend using iframe technology. See [Working with apps](https://www.weavy.com/docs/frontend/drop-in/apps) and [Open and closing apps](https://www.weavy.com/docs/frontend/drop-in/open-close) for more information.

In the example below we inititialize a messenger app. As you can see you need to supply a DOM element (container) to place it in, for instance a <div>. The container can be referenced a DOM element or as a [css selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors). The app automatically adapts to the size of the container (if your container does not have a size the app will not be visible).
```HTML
<div id="messenger-container" style="height:600px;"></div>
```
```JavaScript
const messenger = weavy.app({ 
  type: "messenger",
  container: "#messenger-container"
})
```
  
## A complete example
Here is an example of how to bind the messenger app to a toggle button and display the number of unread messages. In this example we're loading the script from a CDN, but you could of course import it from npm instead.
  
```HTML
<head>
  ...
  <!-- Using package from CDN -->
  <script src="https://cdn.jsdelivr.net/npm/@weavy/dropin-js/dist/weavy-dropin.js" crossorigin="anonymous"></script>
  ...
</head>
<body>
  ...
  <!-- Messenger toggle button -->
  <button id="messenger-button">Messenger</button>
  ...
  <!-- A container to place the messenger in (height is used to define a size on the container) -->
  <div id="messenger-container" style="height: 600px"></div>
  ...
</body>
```
```JavaScript
const weavy = new Weavy({
  url: "{WEAVY_BACKEND_URL}",
  tokenFactory: async () => "{ACCESS_TOKEN}"
});

let messengerButton = document.getElementById("messenger-button");
let messengerContainer = document.getElementById("messenger-container");

let messenger = weavy.app({ 
  type: "messenger",
  container: messengerContainer,
  open: false,
  badge: true
});

// Let the button toggle the messenger on click
messengerButton.addEventListener("click", () => messenger.toggle());

// Add/remove classes on the container when the messenger is opened or closed
messenger.on("app-open", () => messengerContainer.classList.add("open"))
messenger.on("app-close", () => messengerContainer.classList.remove("open"));

// Update your UI with badge count from the messenger
messenger.on("badge", (e, badge) => { 
  messengerButton.innerText = "Unread conversations: " + badge.count; 
});
```

## Notes
Check out the full documentation at [this link](https://www.weavy.com/docs/frontend/drop-in).

# get-weavy-chat

Get started with Weavy Chat via GitHub Marketplace / Student Pack - free license!

Welcome to Weavy, a simpler way of adding collaboration to your projects!

## The backend

To get started, you need a backend to host the service. Weavy offers a free to use cloud-based backend, which you can access by heading over to our [sign-up page](https://get.weavy.io/sign-up).<br>
If you would rather host your own backend, check out the relevant [documentation](https://www.weavy.com/docs/backend).

After you have a backend running, follow the steps below to have chat running in a few minutes.

## The frontend

###### Add the Drop-In UI JavaScript library<br>
Start by adding the Drop-In UI to your page by including these lines in the <head> element.
```html
<script src="https://cdn.jsdelivr.net/npm/@weavy/dropin-js@14.0.4/dist/weavy-dropin.js" crossorigin="anonymous"></script>
```

###### Prepare a placeholder<br>
Next, add a DOM element (container) to your application where you want to render the Weavy Drop-in UI (the container must have a size, otherwise the UI will not be visible).
```html
<div id="messenger" style="height:600px;border:1px solid black;"></div>
```

###### Initialize Weavy<br>
Finally, add this code snippet just before </body>. It initializes Weavy and sets up an authenticated connection to your backend environment (the access token in the sample below is only for demo purposes and is valid for 40 days). It also initialize a messenger app and renders it in the #messenger container.
```JS
<script>
    const weavy = new Weavy({
      url: "https://joannatest.weavy.io",
      tokenFactory: async (refresh) => "wyu_pfLc1BLTbVY6C8Mc753fNou5TEhVnw4MQTGb"
    });

    const messenger = weavy.app({
      uid: "messenger-demo",
      type: "messenger",    
      container: "#messenger"
    });
</script>
```

## Notes
We have two examples of frontend implementation ([JavaScript](https://github.com/JoannaWeavy/weavy-get-started/tree/main/JavaScript) and [React](https://github.com/JoannaWeavy/weavy-get-started/tree/main/React), more comming) prepared for you to reference or clone. Navigate to the correct folder to learn more.

For further help, check out the [Weavy docs](https://www.weavy.com/docs), join our [community forum](https://community.weavy.com/) or join our [Discord server](https://discord.gg/NNsAHGcqAr).

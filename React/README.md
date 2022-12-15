# React UI kit

The React UI kit is a library that you can add to your new or existing React application. The UI kit consists of various UI components for the Weavy apps . In contrast to the Drop-in UI which uses iframes to display server rendered HTML, the React UI kit uses the Web API to communicate with the Weavy backend.

## Getting started
This guide explains how to install the React UI kit and add Weavy chat functionality to your React application.

###### 1. Installation
Install the React UI kit from npm (you can also clone the open-source weavy-uikit-react repo and build it yourself).
```JS
npm install @weavy/uikit-react
```

###### 2. Add the <Messenger> component
Next add the <Messenger> component to your React app. The <Messenger> is a component that combines some of the other UI kit components (<Conversation> and <ConversationList>) that is exposed by the @weavy/uikit-react library (note that that Weavy UI kit must be wrapped in a <WeavyProvider> component).

In your app.tsx or wherever you would like to add the Weavy Messenger:
```React
import React from 'react';
import { WeavyClient, WeavyProvider, Messenger } from '@weavy/uikit-react';

const weavyClient = new WeavyClient({ 
   url: "{WEAVY_BACKEND_URL}", 
   tokenFactory: async () => "{ACCESS_TOKEN}"
});

function App() {
   return (
       <div className="App">
           <WeavyProvider client={weavyClient}>
               <Messenger />
           </WeavyProvider>
       </div>
   )
}

export default App;
```

###### 3. Configure url and authentication
In the code snippet above replace {WEAVY_BACKEND_URL} with the url to your Weavy backend and implement the token factory function that provides Weavy with an access_token for acting on behalf of your authenticated user.

###### 4. Run the app
Start your React app. You should see the Weavy Messenger component rendering a Conversation list and a Conversation with the currently selected conversation.

## Notes
Check out the full documentation at [this link](https://www.weavy.com/docs/frontend/uikit-react).

---
title: React Native
date: 2023-08-17 +0000
categories: [js, documentation, webserver, mobile]
tags: [js, documentation, webserver, webdev, framework, application, react, mobile]
---

## Install

The quickest way to set up a new react native project is with the [Expo CLI](https://docs.expo.dev/workflow/expo-cli/).

```bash
npm install -g expo-cli
```

## Setup

```bash
npx create-expo-app my-app
cd my-app
code . # open in vscode
expo start
```

If `expo start` does not work try `expo start --tunnel`.

## App.js

The `App.js` file is the root component of the application. It is the first component that is rendered when the application starts.

```javascript
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
``` 

The second import line is used to import native components from the react native library. <br/>
The `View` component is like a `div` in html. It is used to wrap other components. <br/>
For styling the `StyleSheet` component is used. The atributes are the same as in CSS except they are written in camelCase <br/>

## Components

### Native Components

#### SafeAreaView

The `SafeAreaView` component is used to make sure the content is not hidden by the status bar or the notch on the iPhone.
It is recommended to use this component as the root component of the application.

```javascript
export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <StatusBar style="auto" />
    </SafeAreaView>
  );
}
```

#### Text

The `Text` component is used to display text.

```javascript
export default function App() {
  return (
    <SafeAreaView>
      <Text>Hello World!</Text>
    </SafeAreaView>
  );
}
```

## Event Handling

### Touchable Components

The `TouchableOpacity` component is used to make other components touchable.

```javascript
export default function App() {
  return (
    <SafeAreaView>
      <TouchableOpacity onPress={() => console.log('Image tapped')}>
        <Image source={require('./assets/icon.png')} />
      </TouchableOpacity>
    </SafeAreaView>
  );
}
```

### Buttons

The `Button` component is used to create a button.

```javascript
export default function App() {
  return (
    <SafeAreaView>
      <Button title='Click Me' onPress={() => console.log('Button tapped')} />
    </SafeAreaView>
  );
}
```

## Hooks

### useState

Changes the state of the component.

```javascript
import React, { useState } from 'react';

export default function App() {
  const [text, setText] = useState('Open up App.js to start working on your app!');
  return (
    <SafeAreaView>
      <Text onPress={() => setText('Hello World!')}>{text}</Text>
    </SafeAreaView>
  );
}
```

### useEffect

Runs code when the component is rendered if the [] are empty or when one of the given variables changes.

```javascript
import React, { useEffect } from 'react';

export default function App() {
  useEffect(() => {
    console.log('Hello World');
  }, []);
  return (
    <View>
      <Text>Open up App.js to start working on your app!</Text>
    </View>
  );
}
```

### useRef


# React Context
Context menyediakan cara untuk oper data melalui diagram komponen tanpa harus oper props secara manual di setiap tingkat. Singkat saja, Context itu seperti variable global yang bisa kamu akses dimana saja tanpa kamu harus memparsing props ke setiap komponen.

Ketika akan membuat context, ada beberapa hal yang perlu di ingat, yaitu:
1. State.
2. Reducer.
3. Type.
4. CreateContext().

![contect](https://storage.googleapis.com/kotakode-prod-public/images/cfe2535c-4002-49d7-8f9f-3a8921a0f0a4-Context-API-vs-Props-Drilling.png)

## Membuat Context
Buat suatu file didalam folder src, Jadi saya bisa bikin context di modul yg terpisah, misalnya userContext.js
``` 
import React from 'react';

const userContext = React.createContext({user: {}});

export { userContext };
```

> Context.Provider

Pass user state as value to context.Provider so it can be consumed by context.Consumer (src/App.js):
Terus buat Provider di komponen Parent.
``` 
import React from 'react';

import Main from './Main';

import {userContext} from './userContext';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      user: {}
    };
  }

  componentDidMount() {
    // get and set currently logged in user to state
  }

  render() {
    return (
      <userContext.Provider value={this.state.user}>
        <Main/>
      </userContext.Provider>
    );
  }
}

export default App;
```

> Context.Consumer

userContext.Consumer takes in a function as a child. This function receives the current context value (value that is passed as a prop to userContext.Provider) and returns a React node (src/Main.js).
``` 
import Sidebar from './Sidebar';
import Content from './Content';
import Avatar from './Avatar';

import {userContext} from './userContext';

function Main(props) {
  return (
    <Sidebar/>
    <userContext.Consumer>
      {({value}) => {
        <Avatar value={value}/>
      }}
    </userContext.Consumer>
    <Content/>
  )
}

export default Main;
```

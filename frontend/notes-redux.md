# Redux Learning Notes

## Benefits of Redux

- Centralizes application`s state
- Makes data flow transparent and predictable

### Pros and Cons

#### Pros

- Predictable state changes
- Centralized state
- Easy debugging
- Preserve page state
- Undo/redo

#### Cons

- Complexity
- Verbosity

## Setting up environment

- `npm i`

## Functional programming

### Programing paradigms

- Functional
- Object-oriented
- Procedural
- Event-driven

### Functions as First-class Citizens

- Assign to a variable
- Pass an argurement
- Return an function

```Javascript
function sayHello () {
  return function () {
    return 'Hello World'
  }
}

let fn = sayHello()
let message = f()
```

### Function composition

```JavaScript
import { compose, pipe } from 'lodash'

let input = '   JavaScript   '
let output = '<div>' + input.trim() + '</div>'

const trim = str => str.trim()
const wrapInDiv = str => `<div>${str}</div>`
const toLowerCase = str => str.toLowerCase()

const result = wrapInDiv(toLowerCase(trim(input)))
const transform = compose(wrapInDiv, toLowerCase, trim)
const newTransform = pipe(trim, toLowerCase, wrapInDiv)

// -> To use Lodash

// trim
// wrapInDiv
```

`npm i lodash`

### Curry

```JavaScript
import { compose, pipe } from 'lodash/fp'

let input = '   JavaScript   '
// let output = '<div>' + input.trim() + '</div>'

const trim = str => str.trim()
const wrap = type => str => `<${type}>${str}</${type}>`
const toLowerCase = str => str.toLowerCase()

const transform = pipe(trim, toLowerCase, wrap('div'))
console.log(transform(input))

```

```JavaScript
function add(a) {
    return function(b) {
        return a + b;
    }
}

const add2 = a => b => a + b; // (a, b) => a + b

add(1)(5);

// -> To use Lodash

// trim
// wrapInDiv

```

### Pure functions - Make sure reduce function as pure

- No random values
- No current date/time
- No global state (DOM, files, db, etc)

### Immutability - Once created, cannot be changed!

_WHY IMMUTABILITY?_

- Predictability
- Faster Change Detection
- Concurrency

_CONS_

- Performance
- Memory overhead

#### Updating objects

```JavaScript
const person = { name: 'Jun' }
const updated = Object.assign({}, person, { name: 'Cheryl', age: 35 })
console.log(updated)
```

```JavaScript
const person = {
  name: 'Jun',
  address: {
    country: 'China',
    city: 'Shanghai'
  }
}

// Deep copy
const updated = {
  ...person,
  address: {
    ...person.address,
    city: 'Guangzhou'
  },
  name: 'Tom'
}
console.log(person)

```

#### Updating arrays

```JavaScript
const numbers = [1, 2, 3]

// Adding
const index = numbers.indexOf(2)
const added = [...numbers.slice(0, index), 4, ...numbers.slice(index)]

console.log('added', added)

// Removing
const removed = numbers.filter(n => n !== 2)

console.log('removed', removed)

// Updating

const updated = numbers.map(n => (n === 2 ? 20 : n))
console.log('updated', updated)
```

#### Enforcing Immutability

_LIBRARIES_

- Immutable
- Immer
- Mori

Mutable scripts!

```JavaScript
let book = { title: 'Harry Potter' }

function publish (book) {
  book.isPublished = true
}

publish(book)
console.log(book)

```

##### Immutable

`npm i immutable`

```JavaScript
import { Map } from 'immutable'

let book = Map({ title: 'Harry Potter' })

function publish (book) {
  return book.set('isPublished', true)
}

book = publish(book)
console.log(book.toJS())

```

##### Immer

```JavaScript
import { produce } from 'immer'

let book = { title: 'Harry Potter' }

function publish (book) {
  return produce(book, drafBook => {
    drafBook.isPublished = true
  })
}

const updated = publish(book)
console.log('book', book)
console.log('updated', updated)
```

## Fundamental of Redux

### Steps

`npm i redux@4.0`

#### Design the store

```JSON
{
    bugs: [
    {
        id: 1,
        description: "",
        resovled: false
    },
    {...},
    {...},
    ],
    currentUser: {}
}
```

#### Define the actions

- Add a Bug
- Mark as Resolved
- Delete a Bug

```JSON
{
    type: "bugAdded",
    payload: {
        description: "..."
    }

}

{
    type: "bugRemoved",
    payload: {
        id: 1
    }

}
```

#### Create a reducer

_Create a reducer.js file_

```JavaScript
// reducer.js
let lastId = 0

export default function reducer (state = [], action) {
  switch (action.type) {
    case 'bugAdded':
      return [
        ...state,
        {
          id: ++lastId,
          description: action.payload.description,
          resolved: false
        }
      ]

    case 'bugRemoved':
      return state.filter(bug => bug.id !== action.payload.id)

    default:
      return state
  }
}

```

#### Set up the store

_Create a store.js file_

```JavaScript
// store.js
import { createStore } from 'redux'
import reducer from './reducer'

const store = createStore(reducer)

export default store
```

## Build Redux from scratch

### Fisrt dispatch

```JavaScript
// index.js
import store from './store'

store.dispatch({
  type: 'bugAdded',
  payload: {
    description: 'Bug1'
  }
})

store.dispatch({
  type: 'bugRemoved',
  payload: {
    id: 1
  }
})

console.log(store.getState())
```

### Subscribing to the Store

```JavaScript
// index.js

import store from './store'

const unsubscribe = store.subscribe(() => {
  console.log('Store Change!', store.getState())
})

store.dispatch({
  type: 'bugAdded',
  payload: {
    description: 'Bug1'
  }
})

unsubscribe()

store.dispatch({
  type: 'bugRemoved',
  payload: {
    id: 1
  }
})

console.log(store.getState())

```

### Action Types

_Create a actionTypes.js file_

```JavaScript
// actionTypes.js
export const BUG_ADDED = 'bugAdded'
export const BUG_REMOVED = 'bugRemoved'
```

```JavaScript
import * as actions from './actionTypes'
```

### Action Creators

_Create a actions.js file_

```JavaScript
// action.js
import * as actions from './actionTypes'

export const bugAdded = description => ({
  type: actions.BUG_ADDED,
  payload: {
    description: 'Bug1'
  }
})
```

```JavaScript
// index.js

import store from './store'
import { bugAdded } from './actions'

const unsubscribe = store.subscribe(() => {
  console.log('Store Change!', store.getState())
})

store.dispatch(bugAdded())

console.log(store.getState())
```

### Implement to Resolve a Bug

- Think about the action first rather than reducer

## Build Redux

### Private Properties

_Create a customStore.js file_

```JavaScript
// customStore.js
function createStore () {
  let state

  function getState () {
    return state
  }

  return {
    getState
  }
}

export default createStore()
```

### Dispatching Actions

```JavaScript
// customStore.js

import reducer from './reducer'

function createStore (reducer) {
  let state

  function dispatch (action) {
    // Call the reducer to get the new state
    // Notify the subscribers

    state = reducer(state, action)
  }

  function getState () {
    return state
  }

  return {
    getState,
    dispatch
  }
}

export default createStore(reducer)
```

```JavaScript
// index.js

import store from './customStore'
import * as actions from './actions'

store.dispatch(actions.bugAdded('Bug1'))
console.log(store.getState())
```

### Subscribing to the Stoer

```JavaScript
// customStore.js

import reducer from './reducer'

function createStore (reducer) {
  let state
  let listners = []

  function subscribe (listner) {
    // listner()
    listners.push(listner)
  }

  function dispatch (action) {
    // Call the reducer to get the new state
    // Notify the subscribers

    state = reducer(state, action)

    for (let i = 0; i < listners.length; i++) {
      listners[i]()
    }
  }

  function getState () {
    return state
  }

  return {
    subscribe,
    getState,
    dispatch
  }
}

export default createStore(reducer)
```

## Debugging

`npm install --save redux-devtools-extension`

```JavaScript
import { createStore } from 'redux';
import { devToolsEnhancer } from 'redux-devtools-extension';

const store = createStore(reducer, /* preloadedState, */ devToolsEnhancer(
  // Specify name here, actionsBlacklist, actionsCreators and other options if needed
));
```

## Writing clean code

```JavaScript
// actionTypes
export const BUG_ADDED = "bugAdded";
export const BUG_REMOVED = "bugRemoved";
export const BUG_RESOLVED = "bugResolved";

// actionCreators
export const bugAdded = (description) => ({
  type: BUG_ADDED,
  payload: {
    description,
  },
});

export const bugResolved = (id) => ({
  type: BUG_RESOLVED,
  payload: {
    // id: id
    id,
  },
});

// Reducer
let lastId = 0;

export default function reducer(state = [], action) {
  switch (action.type) {
    case BUG_ADDED:
      return [
        ...state,
        {
          id: ++lastId,
          description: action.payload.description,
          resolved: false,
        },
      ];

    case BUG_REMOVED:
      return state.filter((bug) => bug.id !== action.payload.id);

    case BUG_RESOLVED:
      return state.map((bug) =>
        bug.id !== action.payload.id ? bug : { ...bug, resolved: true }
      );

    default:
      return state;
  }
}
```

### Redux Toolkit

`npm i @reduxjs/toolkit@1.2.5`

### Creating Store

```JavaScript
import { configureStore } from "@reduxjs/toolkit";
import reducer from "./bugs";

export default function () {
  return configureStore({ reducer });
}
```

### Creating Actions

```JavaScript
import { createAction } from "@reduxjs/toolkit";

// actionCreators
export const bugAdded = createAction("bugAdded");
export const bugRemoved = createAction("bugRemoved");
export const bugResolved = createAction("bugResolved");

// Reducer
let lastId = 0;

export default function reducer(state = [], action) {
  switch (action.type) {
    case bugAdded.type:
      return [
        ...state,
        {
          id: ++lastId,
          description: action.payload.description,
          resolved: false,
        },
      ];

    case bugRemoved.type:
      return state.filter((bug) => bug.id !== action.payload.id);

    case bugResolved.type:
      return state.map((bug) =>
        bug.id !== action.payload.id ? bug : { ...bug, resolved: true }
      );

    default:
      return state;
  }
}
```

### Creating Reducers

```JavaScript
import { createAction, createReducer } from "@reduxjs/toolkit";

// actionCreators
export const bugAdded = createAction("bugAdded");
export const bugRemoved = createAction("bugRemoved");
export const bugResolved = createAction("bugResolved");

// Reducer
let lastId = 0;

export default createReducer([], {
  // key: value
  // actions: functions (event => event handler)
  [bugAdded.type]: (bugs, action) => {
    bugs.push({
      id: ++lastId,
      description: action.payload.description,
      resolved: false,
    });
  },

  [bugRemoved.type]: (bugs, action) => {
    bugs.filter((bug) => bug.id !== action.payload.id);
  },

  [bugResolved.type]: (bugs, action) => {
    const index = bugs.findIndex((bug) => bug.id === action.payload.id);
    bugs[index].resolved = true;
  },
});
```

### Creating slices

```JavaScript
import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";

let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: [],
  reducers: {
    // actions => action handlers
    bugAdded: (bugs, action) => {
      bugs.push({
        id: ++lastId,
        description: action.payload.description,
        resolved: false,
      });
    },
    bugResolved: (bugs, action) => {
      const index = bugs.findIndex((bug) => bug.id === action.payload.id);
      bugs[index].resolved = true;
    },
  },
});

export const { bugAdded, bugResolved } = slice.actions;
export default slice.reducer;
```

## Desiging Redux Store

### Redux State vs Local State

#### Benefits of Store-All-State than Store-Global-State

- Unified data access
- Cacheability
- Easier debugging
- More testable code

* The more stoe we put in the store, the more we can get out of Redux.

### Structing the Redux Store

- Fast lookup => use object
- Ordered data => use array
- Or use both

```JSON
{
  byID: {
    1: {...},
    2: {...},
    3: {...},
  },
  allIds: [3, 1, 2]
}

{
  entities: {...},
  auth: {userId: 1, name: "John"},
  ui: {
    bugs: { query:"...", sortBy:"..."}
  }
}
```

### Combining Multiple Reducers

_Create a reducer.js file_

```JavaScript
// reducer.js
import { combineReducers } from "redux";
import bugReducer from "./bugs";
import projectReducer from "./projects";

export default combineReducers({
  bugs: bugReducer,
  projects: projectReducer,
});
```

### Normalization

github: paularmstrong / normalizr

### Selectors

```JavaScript
// In bugs.js
// Selector function
export const getUnresolvedBugs = (state) =>
  state.entities.bugs.filter((bug) => !bug.resolved);
```

### Meorizing Selectors with Reselect

```JavaScript
// Selector function
const x = getUnresolvedBugs(store.getState());
const y = getUnresolvedBugs(store.getState());
console.log(x === y); // false
```

- The `filter` function is quite expensive.
- Every time we call it, we have to wait for 0.5 seconds.
- Memorization is a technique of optimizing expensive functions.
- To build a cache `f(x) => y {input: 1, output: 2}`
- The time we call this `f(x)`:
  - if the `input` is 1, there is no reason to re-compute it.
  - This is memorization.
- If the `bugs` state doesn`t change:
  - To get the unresolved bugs from the cache as a single in the memory.
  - `npm i reselect`

```JavaScript
import { createSelector } from "reselect";
// ......
export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.filter((bug) => !bug.resolved)
);
```

### Exercise

Add the ability to

- assign a bug to a team member
- get the list of bugs assigned to a team member

Solutions:

- Create a slice for users. {id, name}
- Create an action for adding a user.
- Create an action for assigning a bug to a user.
- Create a selector for getting bugs by a user.

## Middleware

### What is Middleware

Middleware is piece of codes executed after action dispatched and before it reaches the reducer.

- Calling APIs
- Error reporting
- Analytics
- Authorizations

Action => Log => Auth => ...

### Creating Middleware

_Create a logger.js file_

```JavaScript
const logger = (store) => (next) => (action) => {
  console.log("store", store);
  console.log("next", next);
  console.log("action", action);
  next(action);
};

export default logger;
```

```JavaScript
// configureStore.js
import { configureStore } from "@reduxjs/toolkit";
import reducer from "./reducer";
import logger from "./middleware/logger";

export default function () {
  return configureStore({
    reducer,
    middleware: [logger],
  });
}
```

### Parameterizing Middleware

```JavaScript
const logger = param => (store) => (next) => (action) => {
  console.log("param", param)
  console.log("store", store);
  console.log("next", next);
  console.log("action", action);
  next(action);
};

export default logger;
```

```JavaScript
// configureStore.js
import { configureStore } from "@reduxjs/toolkit";
import reducer from "./reducer";
import logger from "./middleware/logger";

export default function () {
  return configureStore({
    reducer,
    middleware: [logger("param")],
  });
}
```

### Dispathcing Functions

_Create a func.js file_

```JavaScript
// Thunk / Func

const func = ({ dispatch, getState }) => (next) => (action) => {
  if (typeof action === "function") action(dispatch, getState);
  else next(action);
};

export default func;
```

```JavaScript
// index.js

import configureStore from "./store/configureStore";
// import * as actions from "./store/bugs";
// import { getUnresolvedBugs, getBugsByUser } from "./store/bugs";
// import { projectAdded } from "./store/projects";
// import { userAdded } from "./store/users";

const store = configureStore();

store.dispatch((dispatch, getState) => {
  // Call an API
  // When the promise is resolve => dispatch()
  // If the promise is rejected => dispatch()
  dispatch({ type: "bugReceived", bugs: [1, 2, 3] });
  // Add a middleware function
});
```

`npm i redux-thunk`

```JavaScript
import { configureStore, getDefaultMiddleware } from "@reduxjs/toolkit";
import reducer from "./reducer";
import logger from "./middleware/logger";
// import func from "./middleware/func";

export default function () {
  return configureStore({
    reducer,
    middleware: [
      ...getDefaultMiddleware(),
      logger({
        destination: "console",
      }),
    ],
  });
}
```

## Consuming APIs

### The Approach

```JavaScript
function actionCreator() {
  return function(dispatch) {

  }
}
```

```JavaScript
const actionCreator = () => (dispatch) => {

    // Call api
    // Resolved: dispatch(success)
    // Rejected: dispatch(rejected)
  }
}
```

Actions:

- bugsRequested
- bugsReceived
- bugsRequestFailed

### API Middleware

`npm i axios`
_Create a app.js file_

```JavaScript
import axios from "axios";

// In api.js

// Only for demonstration
// const action = {
//   type: "apiCallBegan", // apiReuqest
//   payload: {
//     url: "/bugs",
//     methord: "get",
//     data: {},
//     onSuccess: "bugReceived",
//     onError: "apiRequestFailed",
//   },
// };

const api = ({ dispatch }) => (next) => async (action) => {
  //   if (action.type !== "apiCallBegan") {
  //     next(action);
  //     return; // We don`t want the rest of functions been executed
  //   }
  if (action.type !== "apiCallBegan") return next(action);
  next(action);
  const { url, method, data, onSuccess, onError } = action.payload;
  try {
    const response = await axios.request({
      baseURL: "http://localhost:9001/api", // Configurable in real projects
      url, //bugs
      method,
      data,
    });
    dispatch({ type: onSuccess, payload: response.data });
  } catch (error) {
    dispatch({ type: onError, payload: error });
  }
};

export default api;
```

```JavaScript
// index.js

import configureStore from "./store/configureStore";

const store = configureStore();

store.dispatch((dispatch, getState) => {
  // Call an API
  // When the promise is resolve => dispatch()
  // If the promise is rejected => dispatch()
  dispatch({
    type: "apiCallBegan", // apiReuqest
    payload: {
      url: "/bugs",
      method: "get",
      data: {},
      onSuccess: "bugReceived",
      onError: "apiRequestFailed",
    },
  });
  // Add a middleware function
});

```

### Create Actions

_Create api.js in store folder_

```JavaScript
import { createAction } from "@reduxjs/toolkit";

export const apiCallBegan = createAction("api/callBegan");
export const apiCallSuccess = createAction("api/callSuccess");
export const apiCallFailed = createAction("api/callFailed");
```

```JavaScript
import axios from "axios";
import * as actions from "../api";

// Only for demonstration
// const action = {
//   type: "apiCallBegan", // apiReuqest
//   payload: {
//     url: "/bugs",
//     methord: "get",
//     data: {},
//     onSuccess: "bugReceived",
//     onError: "apiRequestFailed",
//   },
// };

const api = ({ dispatch }) => (next) => async (action) => {
  //   if (action.type !== "apiCallBegan") {
  //     next(action);
  //     return; // We don`t want the rest of functions been executed
  //   }
  if (action.type !== actions.apiCallBegan.type) return next(action);

  next(action);
  const { url, method, data, onSuccess, onError } = action.payload;
  try {
    const response = await axios.request({
      baseURL: "http://localhost:9001/api", // Configurable in real projects
      url, //bugs
      method,
      data,
    });
    // General
    dispatch(actions.apiCallSuccess(response.data));
    // Specific
    // Make sure onError has been defined
    if (onSuccess) dispatch({ type: onSuccess, payload: response.data });
  } catch (error) {
    // General
    dispatch(actions.apiCallFailed(error));
    // Specific
    if (onError)
      // Make sure onError has been defined
      dispatch({ type: onError, payload: error });
  }
};

export default api;
```

```JavaScript
// index.js

import configureStore from "./store/configureStore";
import * as actions from "./store/api";
// import { getUnresolvedBugs, getBugsByUser } from "./store/bugs";
// import { projectAdded } from "./store/projects";
// import { userAdded } from "./store/users";

const store = configureStore();

store.dispatch(
  actions.apiCallBegan({
    url: "/bugs",
    method: "get",
    data: {},
    onSuccess: "bugReceived",
    onError: actions.apiCallFailed.type, // Made in middle
  })
);
```

### Restructing the Store

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";

let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null, // Last time called the server
  },
  reducers: {
    // actions => action handlers

    bugAssignedToUser: (bugs, action) => {
      const { bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
    },

    bugAdded: (bugs, action) => {
      bugs.list.push({
        id: ++lastId,
        description: action.payload.description,
        resolved: false,
      });
    },
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const { bugAdded, bugResolved, bugAssignedToUser } = slice.actions;
export default slice.reducer;
```

### Getting Data from the Server

To add a reducer in bugs.js

```JavaScript
  reducers: {
    // actions => action handlers

    busReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
    },
```

To change the namespace in index.js

```JavaScript
const store = configureStore();

// UI Layer

store.dispatch(
  actions.apiCallBegan({
    url: "/bugs",
    method: "get",
    data: {},
    onSuccess: "bugs/bugReceived",
    onError: actions.apiCallFailed.type, // Made in middle
  })
);
```

To add the action creator in the bottom of bugs.js

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";
import { apiCallBegan } from "./api";

let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null, // Last time called the server
  },
  reducers: {
    // actions => action handlers

    bugsReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
    },

    bugAssignedToUser: (bugs, action) => {
      const { bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
    },

    bugAdded: (bugs, action) => {
      bugs.list.push({
        id: ++lastId,
        description: action.payload.description,
        resolved: false,
      });
    },
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
} = slice.actions;
export default slice.reducer;

// Action Creators
const url = "/bugs";

export const loadBugs = () =>
  apiCallBegan({
    url: url,
    // method: "get",
    // data: {},
    onSuccess: bugsReceived.type,
    // onError: actions.apiCallFailed.type, // Made in middle
  });
```

```JavaScript
// index.js

import configureStore from "./store/configureStore";
// import * as actions from "./store/api";
import { loadBugs } from "./store/bugs";
// import { projectAdded } from "./store/projects";
// import { userAdded } from "./store/users";

const store = configureStore();

// UI Layer
store.dispatch(loadBugs());

// store.dispatch(
//   actions.apiCallBegan({
//     url: "/bugs",
//     method: "get",
//     data: {},
//     onSuccess: "bugs/bugReceived",
//     onError: actions.apiCallFailed.type, // Made in middle
//   })
// );
```

### Loading Indicators

To define:

- action: bugsRequested
- reducer: loading = true
- middleware: dispatch a new action

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";
import { apiCallBegan } from "./api";

let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null, // Last time called the server
  },
  reducers: {
    // actions => action handlers

    bugsRequested: (bugs, action) => {
      bugs.loading = true;
    },

    bugsRequestFailed: (bugs, action) => {
      bugs.loading = false;
    },

    bugsReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
      bugs.loading = false;
    },

    bugAssignedToUser: (bugs, action) => {
      const { bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
    },

    bugAdded: (bugs, action) => {
      bugs.list.push({
        id: ++lastId,
        description: action.payload.description,
        resolved: false,
      });
    },
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
  bugsRequested,
  bugsRequestFailed,
} = slice.actions;
export default slice.reducer;

// Action Creators
const url = "/bugs";

export const loadBugs = () =>
  apiCallBegan({
    url: url,
    // method: "get",
    // data: {},
    onStart: bugsRequested.type,
    onSuccess: bugsReceived.type,
    onError: bugsRequestFailed.type,
  });
```

```JavaScript
import axios from "axios";
import * as actions from "../api";

// Only for demonstration
// const action = {
//   type: "apiCallBegan", // apiReuqest
//   payload: {
//     url: "/bugs",
//     methord: "get",
//     data: {},
//     onSuccess: "bugReceived",
//     onError: "apiRequestFailed",
//   },
// };

const api = ({ dispatch }) => (next) => async (action) => {
  //   if (action.type !== "apiCallBegan") {
  //     next(action);
  //     return; // We don`t want the rest of functions been executed
  //   }
  if (action.type !== actions.apiCallBegan.type) return next(action);

  const { url, method, data, onStart, onSuccess, onError } = action.payload;
  if (onStart) dispatch({ type: onStart });
  next(action);
  try {
    const response = await axios.request({
      baseURL: "http://localhost:9002/api", // Configurable in real projects
      url, //bugs
      method,
      data,
    });
    // General
    dispatch(actions.apiCallSuccess(response.data));
    // Specific
    // Make sure onError has been defined
    if (onSuccess) dispatch({ type: onSuccess, payload: response.data });
  } catch (error) {
    // General
    dispatch(actions.apiCallFailed(error.message));
    // Specific
    if (onError)
      // Make sure onError has been defined
      dispatch({ type: onError, payload: error.message });
  }
};

export default api;
```

### Caching

Add `lastFetch`

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";
import { apiCallBegan } from "./api";

let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null,
  },
  reducers: {
    // actions => action handlers

    bugsRequested: (bugs, action) => {
      bugs.loading = true;
      bugs.lastFetch = Date.now();
    },

    bugsRequestFailed: (bugs, action) => {
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugsReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugAssignedToUser: (bugs, action) => {
      const { bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
    },

    bugAdded: (bugs, action) => {
      bugs.list.push({
        id: ++lastId,
        description: action.payload.description,
        resolved: false,
      });
    },
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
  bugsRequested,
  bugsRequestFailed,
} = slice.actions;
export default slice.reducer;

// Action Creators
const url = "/bugs";

// () => fn(dispatch, getState), the fn is the function returning
export const loadBugs = () => (dispatch, getState) => {
  const { lastFetch } = getState().entities.bugs;
  console.log(lastFetch);
  dispatch(
    apiCallBegan({
      url: url,
      // method: "get",
      // data: {},
      onStart: bugsRequested.type,
      onSuccess: bugsReceived.type,
      onError: bugsRequestFailed.type,
    })
  );
};

// export const loadBugs = () =>
//   apiCallBegan({
//     url: url,
//     // method: "get",
//     // data: {},
//     onStart: bugsRequested.type,
//     onSuccess: bugsReceived.type,
//     onError: bugsRequestFailed.type,
//   });
```

`npm i moment`

Revised in `loadBugs()`

```JavaScript
export const loadBugs = () => (dispatch, getState) => {
  const { lastFetch } = getState().entities.bugs;
  const diffInMinutes = moment().diff(moment(lastFetch), "minutes");
  if (diffInMinutes < 10) return;
  dispatch(
    apiCallBegan({
      url: url,
      // method: "get",
      // data: {},
      onStart: bugsRequested.type,
      onSuccess: bugsReceived.type,
      onError: bugsRequestFailed.type,
    })
  );
};
```

### Saving Data to the Server

- Mkae an API call
- Promise resolved => dispatch(success)
- Promise rejected => dispatch(error)

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";
import { apiCallBegan } from "./api";
import moment from "moment";

// let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null,
  },
  reducers: {
    // actions => action handlers

    bugsRequested: (bugs, action) => {
      bugs.loading = true;
      bugs.lastFetch = Date.now();
    },

    bugsRequestFailed: (bugs, action) => {
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugsReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugAssignedToUser: (bugs, action) => {
      const { bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
      bugs.lastFetch = Date.now();
    },

    bugAdded: (bugs, action) => {
      bugs.list.push(action.payload);
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
  bugsRequested,
  bugsRequestFailed,
} = slice.actions;
export default slice.reducer;

// Action Creators
const url = "/bugs";

// () => fn(dispatch, getState), the fn is the function returning
// These two new parameters will be called eventually in index.js by store
export const loadBugs = () => (dispatch, getState) => {
  const { lastFetch } = getState().entities.bugs;
  const diffInMinutes = moment().diff(moment(lastFetch), "minutes");
  if (diffInMinutes < 10) return;
  dispatch(
    apiCallBegan({
      url: url,
      // method: "get",
      // data: {},
      onStart: bugsRequested.type,
      onSuccess: bugsReceived.type,
      onError: bugsRequestFailed.type,
    })
  );
};

export const addBug = (bug) =>
  apiCallBegan({
    url,
    method: "post",
    data: bug,
    onStart: bugsRequested.type,
    onSuccess: bugAdded.type,
  });
```

### Exersice User Management

Save the data when:

- Assigning a bug to a user
- Resolving a bug

### Solution - Resolving Bugs

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";
import { apiCallBegan } from "./api";
import moment from "moment";

// let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null,
  },
  reducers: {
    // actions => action handlers

    bugsRequested: (bugs, action) => {
      bugs.loading = true;
      bugs.lastFetch = Date.now();
    },

    bugsRequestFailed: (bugs, action) => {
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugsReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugAssignedToUser: (bugs, action) => {
      const { bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
      bugs.lastFetch = Date.now();
    },

    // command - event
    // addBug - bugAdded
    bugAdded: (bugs, action) => {
      bugs.list.push(action.payload);
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    // resolveBug (command)
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
  bugsRequested,
  bugsRequestFailed,
} = slice.actions;
export default slice.reducer;

// Action Creators
const url = "/bugs";

// () => fn(dispatch, getState), the fn is the function returning
// These two new parameters will be called eventually in index.js by store
export const loadBugs = () => (dispatch, getState) => {
  const { lastFetch } = getState().entities.bugs;
  const diffInMinutes = moment().diff(moment(lastFetch), "minutes");
  if (diffInMinutes < 10) return;
  dispatch(
    apiCallBegan({
      url: url,
      // method: "get",
      // data: {},
      onStart: bugsRequested.type,
      onSuccess: bugsReceived.type,
      onError: bugsRequestFailed.type,
    })
  );
};

export const addBug = (bug) =>
  apiCallBegan({
    url,
    method: "post",
    data: bug,
    onStart: bugsRequested.type,
    onSuccess: bugAdded.type,
  });

export const resolveBug = (id) =>
  apiCallBegan({
    // bugs
    // PATCH /bugs/1
    url: url + "/" + id,
    method: "patch",
    data: { resolved: true },
    onSuccess: bugResolved.type,
  });
```

### Solution - Assigning a Bug

```JavaScript
// store/bugs.js

import { createAction, createReducer, createSlice } from "@reduxjs/toolkit";
import { createSelector } from "reselect";
import { apiCallBegan } from "./api";
import moment from "moment";

// let lastId = 0;

const slice = createSlice({
  name: "bugs",
  initialState: {
    list: [],
    loading: false,
    lastFetch: null,
  },
  reducers: {
    // actions => action handlers

    bugsRequested: (bugs, action) => {
      bugs.loading = true;
      bugs.lastFetch = Date.now();
    },

    bugsRequestFailed: (bugs, action) => {
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugsReceived: (bugs, action) => {
      // bugs/bugsReceived
      bugs.list = action.payload;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    bugAssignedToUser: (bugs, action) => {
      const { id: bugId, userId } = action.payload;
      const index = bugs.list.findIndex((bug) => bug.id == bugId);
      bugs.list[index].userId = userId;
      bugs.lastFetch = Date.now();
    },

    // command - event
    // addBug - bugAdded
    bugAdded: (bugs, action) => {
      bugs.list.push(action.payload);
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },

    // resolveBug (command)
    bugResolved: (bugs, action) => {
      const index = bugs.list.findIndex((bug) => bug.id === action.payload.id);
      bugs.list[index].resolved = true;
      bugs.loading = false;
      bugs.lastFetch = Date.now();
    },
  },
});

// Selector
// export const getUnresolvedBugs = (state) =>
//   state.entities.bugs.filter((bug) => !bug.resolved);

export const getUnresolvedBugs = createSelector(
  (state) => state.entities.bugs,
  (bugs) => bugs.list.filter((bug) => !bug.resolved)
);

export const getBugsByUser = (userId) =>
  createSelector(
    (state) => state.entities.bugs,
    (bugs) => bugs.list.filter((bug) => bug.userId === userId)
  );

export const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
  bugsRequested,
  bugsRequestFailed,
} = slice.actions;
export default slice.reducer;

// Action Creators
const url = "/bugs";

// () => fn(dispatch, getState), the fn is the function returning
// These two new parameters will be called eventually in index.js by store
export const loadBugs = () => (dispatch, getState) => {
  const { lastFetch } = getState().entities.bugs;
  const diffInMinutes = moment().diff(moment(lastFetch), "minutes");
  if (diffInMinutes < 10) return;
  dispatch(
    apiCallBegan({
      url: url,
      // method: "get",
      // data: {},
      onStart: bugsRequested.type,
      onSuccess: bugsReceived.type,
      onError: bugsRequestFailed.type,
    })
  );
};

export const addBug = (bug) =>
  apiCallBegan({
    url,
    method: "post",
    data: bug,
    onStart: bugsRequested.type,
    onSuccess: bugAdded.type,
  });

export const resolveBug = (id) =>
  apiCallBegan({
    // bugs
    // PATCH /bugs/1
    url: url + "/" + id,
    method: "patch",
    data: { resolved: true },
    onSuccess: bugResolved.type,
  });

export const assignBugToUser = (id, userId) =>
  apiCallBegan({
    url: url + "/" + id,
    method: "patch",
    data: { userId },
    onSuccess: bugAssignedToUser.type,
  });
```

### Reducing Coupling

```JavaScript
const {
  bugAdded,
  bugResolved,
  bugAssignedToUser,
  bugsReceived,
  bugsRequested,
  bugsRequestFailed,
} = slice.actions;
export default slice.reducer;
```

### Cohesion

Combine the high correlated codes into one file such as bugs.js

## Testing Redux apps

### What is Automated Testing?

TYPES OF TESTS:

- Unit tests: Test the application without its external dependencies
- Integration tests
- End-to-End test

Unit tests: Test the application without its external dependencies.

App Code -> Mock API -> API

A unit can be a signle or multiple objects.

---> Slower
Unit -> Integration -> E2E

### Seting Up the Testing Environment

`npm i jest @types/jest @babel/core @babel/preset-env babel-jest -D`

Add [babel.config.json] in root folder

```json
{
  "presets": ["@babel/preset-env"]
}
```

Add [math.spec.js] in src folder

```JavaScript
it("first test", () => {});
```

Run `jest` in terminal, if it doesn't work, run `./node_modules/.bin/jest`.

Add the script into package.json

```json
  "scripts": {
    "start": "webpack-dev-server --config ./webpack.config.js",
    "test": "jest"
  }
```

Update the package.json as

```json
  "scripts": {
    "start": "webpack-dev-server --config ./webpack.config.js",
    "test": "jest --watch"
  }
```

### Your First Test

```JavaScript
// math.spec.js

import { isEven } from "./math";

describe("isEven", () => {
  it("Should return true if given an even number", () => {
    // Function under test
    const result = isEven(2);
    expect(result).toEqual(true);
  });

  it("Should return false if given an odd number", () => {
    // Function under test
    const result = isEven(1);
    expect(result).toEqual(false);
  });
});
```

### Unit Test Redux Applications

Test the behavior, not the implementation!

### Solitary Tests

Add a [tests] folder in [store]

```JavaScript
// src.store/tests/bugs.specs.js

import { addBug, bugAdded, bugsRequested } from "../bugs";
import { apiCallBegan } from "../api";

describe("bugsSlice", () => {
  describe("action creators", () => {
    it("addBug", () => {
      const bug = { description: "a" };
      const result = addBug(bug);
      const expected = {
        type: apiCallBegan.type,
        payload: {
          url: "/bugs",
          method: "post",
          data: bug,
          onStart: bugsRequested.type,
          onSuccess: bugAdded.type,
        },
      };
      expect(result).toEqual(expected);
    });
  });
});
```

### Social Testing

`npm i @babel/plugin-transform-runtime -D`
Configue int [babel.config.json]

```json
{
  "presets": ["@babel/preset-env"],
  "plugins": ["@babel/plugin-traonsform-runtime"]
}
```

Then run `jest` again

Add `return` in the codes of middleware

```JavaScript
// src/store/middleware/toast.js

const toast = (store) => (next) => (action) => {
  if (action.type === "error") console.log("Toastify", action.payload.message);
  else return next(action);
};

export default toast;
```

```JavaScript
const logger = (param) => (store) => (next) => (action) => {
  console.log("Logging", param);
  //   console.log("store", store);
  //   console.log("next", next);
  //   console.log("action", action);
  return next(action);
};

export default logger;
```

Test the same behavior

```JavaScript
export const addBug = (bug) => async (dispatch) => {
  const response = await axios.request({
    baseURL: "http://localhost:9001/api",
    url: "/bugs",
    method: "post",
    data: bug,
  });
  dispatch(bugAdded(response.data));
};

// export const addBug = (bug) =>
//   apiCallBegan({
//     url,
//     method: "post",
//     data: bug,
//     onStart: bugsRequested.type,
//     onSuccess: bugAdded.type,
//   });
```

```JavaScript
// src.store/tests/bugs.specs.js
import { addBug } from "../bugs";
import configureStore from "../configureStore";

describe("bugsSlice", () => {
  it("Should handle the addBug action", async () => {
    const store = configureStore();
    const bug = { description: "a" };
    await store.dispatch(addBug(bug));
    // console.log(store.getState());
    expect(store.getState().entities.bugs.list).toHaveLength(1);
  });
});
```

### Mocking HTTP Calls

`npm i axios-mock-adapter -D`

```JavaScript
// src.store/tests/bugs.specs.js
import { addBug } from "../bugs";
import configureStore from "../configureStore";
import MockAdapter from "axios-mock-adapter";
import axios from "axios";

describe("bugsSlice", () => {
  it("Should handle the addBug action", async () => {
    // Arrange
    const bug = { description: "a" };
    const savedBug = { ...bug, id: 1 };
    const fakeAxios = new MockAdapter(axios);
    fakeAxios.onPost("/bugs").reply(200, savedBug);
    const store = configureStore();

    // Act
    await store.dispatch(addBug(bug));

    // Assert
    expect(store.getState().entities.bugs.list).toContainEqual(savedBug);
  });
});
```

### Writing Clean Tests

```JavaScript
// src.store/tests/bugs.specs.js
import { addBug } from "../bugs";
import configureStore from "../configureStore";
import MockAdapter from "axios-mock-adapter";
import axios from "axios";

describe("bugsSlice", () => {
  let fakeAxios;
  let store;

  beforeEach(() => {
    fakeAxios = new MockAdapter(axios);
    store = configureStore();
  });

  const bugsSlice = () => store.getState().entities.bugs;

  it("Should add the bug to the store if it`s saved to the server", async () => {
    const bug = { description: "a" };
    const savedBug = { ...bug, id: 1 };
    fakeAxios.onPost("/bugs").reply(200, savedBug);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toContainEqual(savedBug);
  });

  it("Should not add the bug to the store if it`s not saved to the server", async () => {
    const bug = { description: "a" };
    fakeAxios.onPost("/bugs").reply(500);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toHaveLength(0);
  });
});
```

### Test Coverage

`jest --coverage`

Check the [index.html] in [lcov-report]

### Exersice

- resolving a bug
- loading bugs
- getting unresolved bugs

### Solution - getUnresolvedBugs

```JavaScript
// src.store/tests/bugs.specs.js
import { addBug, getUnresolvedBugs } from "../bugs";
import configureStore from "../configureStore";
import MockAdapter from "axios-mock-adapter";
import axios from "axios";

describe("bugsSlice", () => {
  let fakeAxios;
  let store;

  beforeEach(() => {
    fakeAxios = new MockAdapter(axios);
    store = configureStore();
  });

  const bugsSlice = () => store.getState().entities.bugs;

  const createState = () => ({
    entities: {
      bugs: { list: [] },
    },
  });

  it("Should add the bug to the store if it`s saved to the server", async () => {
    const bug = { description: "a" };
    const savedBug = { ...bug, id: 1 };
    fakeAxios.onPost("/bugs").reply(200, savedBug);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toContainEqual(savedBug);
  });

  it("Should not add the bug to the store if it`s not saved to the server", async () => {
    const bug = { description: "a" };
    fakeAxios.onPost("/bugs").reply(500);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toHaveLength(0);
  });

  describe("selectors", () => {
    it("getUnresolvedBugs", () => {
      const state = createState();
      console.log(state);
      state.entities.bugs.list = [
        { id: 1, resolved: true },
        { id: 2 },
        { id: 3 },
      ];

      const result = getUnresolvedBugs(state);

      expect(result).toHaveLength(2);
    });
  });
});
```

### Solution - resolveBug

```JavaScript
// src.store/tests/bugs.specs.js
import { addBug, getUnresolvedBugs, resolveBug } from "../bugs";
import configureStore from "../configureStore";
import MockAdapter from "axios-mock-adapter";
import axios from "axios";

describe("bugsSlice", () => {
  let fakeAxios;
  let store;

  beforeEach(() => {
    fakeAxios = new MockAdapter(axios);
    store = configureStore();
  });

  const bugsSlice = () => store.getState().entities.bugs;

  const createState = () => ({
    entities: {
      bugs: { list: [] },
    },
  });

  it("should mark the bug as resolved if it`s saved to the server", async () => {
    // AAA
    fakeAxios.onPatch("/bugs/1").reply(200, { id: 1, resolved: true });
    fakeAxios.onPost("/bugs").reply(200, { id: 1 });

    await store.dispatch(addBug({}));
    await store.dispatch(resolveBug(1));

    expect(bugsSlice().list[0].resolved).toBe(true);
  });

  it("should not mark the bug as resolved if it`s not saved to the server", async () => {
    // AAA
    fakeAxios.onPatch("/bugs/1").reply(500);
    fakeAxios.onPost("/bugs").reply(200, { id: 1 });

    await store.dispatch(addBug({}));
    await store.dispatch(resolveBug(1));

    expect(bugsSlice().list[0].resolved).not.toBe(true);
  });

  it("should add the bug to the store if it`s saved to the server", async () => {
    const bug = { description: "a" };
    const savedBug = { ...bug, id: 1 };
    fakeAxios.onPost("/bugs").reply(200, savedBug);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toContainEqual(savedBug);
  });

  it("should not add the bug to the store if it`s not saved to the server", async () => {
    const bug = { description: "a" };
    fakeAxios.onPost("/bugs").reply(500);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toHaveLength(0);
  });

  describe("selectors", () => {
    it("getUnresolvedBugs", () => {
      const state = createState();
      console.log(state);
      state.entities.bugs.list = [
        { id: 1, resolved: true },
        { id: 2 },
        { id: 3 },
      ];

      const result = getUnresolvedBugs(state);

      expect(result).toHaveLength(2);
    });
  });
});
```

### Solution - loadingBugs

- loading bugs
  - if they exist in the cache
    - they should come from the cache
  - if they don`t exist in the cache
    - they should be fetched from the server
    * loading indicator
      - should be true while fetching
      - should be false after bugs are fetched
      - should be false if the server fails

To add `return` in action creator

```JavaScript
// Action Creators
const url = "/bugs";

// () => fn(dispatch, getState), the fn is the function returning
// These two new parameters will be called eventually in index.js by store
export const loadBugs = () => (dispatch, getState) => {
  const { lastFetch } = getState().entities.bugs;
  const diffInMinutes = moment().diff(moment(lastFetch), "minutes");
  if (diffInMinutes < 10) return;
  return dispatch(
    apiCallBegan({
      url: url,
      // method: "get",
      // data: {},
      onStart: bugsRequested.type,
      onSuccess: bugsReceived.type,
      onError: bugsRequestFailed.type,
    })
  );
};
```

```JavaScript
// src.store/tests/bugs.specs.js
import { loadBugs, addBug, getUnresolvedBugs, resolveBug } from "../bugs";
import configureStore from "../configureStore";
import MockAdapter from "axios-mock-adapter";
import axios from "axios";

describe("bugsSlice", () => {
  let fakeAxios;
  let store;

  beforeEach(() => {
    fakeAxios = new MockAdapter(axios);
    store = configureStore();
  });

  const bugsSlice = () => store.getState().entities.bugs;

  const createState = () => ({
    entities: {
      bugs: { list: [] },
    },
  });

  describe("loading bugs", () => {
    describe("if the bugs exist in the cache", () => {
      it("they should not be fetched from the server again", async () => {
        fakeAxios.onGet("/bugs").reply(200, [{ id: 1 }]);

        await store.dispatch(loadBugs());
        await store.dispatch(loadBugs());

        expect(fakeAxios.history.get.length).toBe(1);
      });
    });
    describe("if the bugs don't exist in the cache", () => {
      it("they should be fetched from the server and put int the store", async () => {
        fakeAxios.onGet("/bugs").reply(200, [{ id: 1 }]);
        await store.dispatch(loadBugs());

        expect(bugsSlice().list).toHaveLength(1);
      });

      describe("loading indicator", () => {
        it("should be true while fetching", () => {
          fakeAxios.onGet("/bugs").reply(200, [{ id: 1 }]);
          fakeAxios.onGet("/bugs").reply(200, () => {
            expect(bugsSlice().loading).toBe(true);
            return [200, [{ id: 1 }]];
          });

          store.dispatch(loadBugs());
        });

        it("should be false after the bugs are fetched", async () => {
          fakeAxios.onGet("/bugs").reply(200, [{ id: 1 }]);
          await store.dispatch(loadBugs());

          expect(bugsSlice().loading).toBe(false);
        });

        it("should be false if the server returns an error", async () => {
          fakeAxios.onGet("/bugs").reply(500);
          await store.dispatch(loadBugs());

          expect(bugsSlice().loading).toBe(false);
        });
      });
    });
  });

  it("should mark the bug as resolved if it`s saved to the server", async () => {
    // AAA
    fakeAxios.onPatch("/bugs/1").reply(200, { id: 1, resolved: true });
    fakeAxios.onPost("/bugs").reply(200, { id: 1 });

    await store.dispatch(addBug({}));
    await store.dispatch(resolveBug(1));

    expect(bugsSlice().list[0].resolved).toBe(true);
  });

  it("should not mark the bug as resolved if it`s not saved to the server", async () => {
    // AAA
    fakeAxios.onPatch("/bugs/1").reply(500);
    fakeAxios.onPost("/bugs").reply(200, { id: 1 });

    await store.dispatch(addBug({}));
    await store.dispatch(resolveBug(1));

    expect(bugsSlice().list[0].resolved).not.toBe(true);
  });

  it("should add the bug to the store if it`s saved to the server", async () => {
    const bug = { description: "a" };
    const savedBug = { ...bug, id: 1 };
    fakeAxios.onPost("/bugs").reply(200, savedBug);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toContainEqual(savedBug);
  });

  it("should not add the bug to the store if it`s not saved to the server", async () => {
    const bug = { description: "a" };
    fakeAxios.onPost("/bugs").reply(500);

    await store.dispatch(addBug(bug));

    expect(bugsSlice().list).toHaveLength(0);
  });

  describe("selectors", () => {
    it("getUnresolvedBugs", () => {
      const state = createState();
      console.log(state);
      state.entities.bugs.list = [
        { id: 1, resolved: true },
        { id: 2 },
        { id: 3 },
      ];

      const result = getUnresolvedBugs(state);

      expect(result).toHaveLength(2);
    });
  });
});
```

## Integrating with React

### Install redux

Copy the [store] folder into the React project
`npm i redux @reduxjs/toolkit axios moment1`

### Providing the Store

Create a component [bugs.jsx]

Create a folder [contexts] with a new file [storeContext.js]

```jsx
// src/contexts/storeContext.js

import { createContext } from "react";

const StoreContext = createContext();

export default StoreContext;
```

```jsx
// App.js

import React, { Component } from "react";
import "./App.css";
import Bugs from "./components/bugs";
import configureStore from "./store/configureStore";
import StoreContext from "./contexts/storeContext";

const store = configureStore();

function App() {
  return (
    <StoreContext.Provider value={store}>
      <Bugs />
    </StoreContext.Provider>
  );
}

export default App;
```

```jsx
import React, { Component } from "react";
import StoreContext from "../contexts/storeContext";

class Bugs extends Component {
  static contextType = StoreContext;

  componentDidMount() {
    console.log(this.context);
  }

  render() {
    return <div>Bugs</div>;
  }
}

export default Bugs;
```

### Subscribing and Dispatching

```jsx
import React, { Component } from "react";
import StoreContext from "../contexts/storeContext";
import { loadBugs } from "../store/bugs";

class Bugs extends Component {
  static contextType = StoreContext;

  state = { bugs: [] };

  componentDidMount() {
    // subscribe
    // dispatch(loadBugs)

    const store = this.context;

    this.unsubscribe = store.subscribe(() => {
      const bugsInStore = store.getState().entities.bugs.list;
      if (this.state.bugs !== bugsInStore) this.setState({ bugs: bugsInStore });
    });

    store.dispatch(loadBugs());
  }

  componentWillUnmount() {
    this.unsubscribe();
  }

  render() {
    return (
      <ul>
        {this.state.bugs.map((bug) => (
          <li key={bug.id}>{bug.description}</li>
        ))}
      </ul>
    );
  }
}

export default Bugs;
```

### Connecting Components Using react-redux

`npm i react-redux`

Then we can get rid of [contexts] folder.

```jsx
import React, { Component } from "react";
import { connect } from "react-redux";
import { loadBugs } from "../store/bugs";

class Bugs extends Component {
  componentDidMount() {
    this.props.loadBugs();
  }

  render() {
    return (
      <ul>
        {this.props.bugs.map((bug) => (
          <li key={bug.id}>{bug.description}</li>
        ))}
      </ul>
    );
  }
}

// state.entities.bugs.list
const mapStateToProps = (state) => ({
  bugs: state.entities.bugs.list,
});

const mapDispatchToProps = (dispatch) => ({
  loadBugs: () => dispatch(loadBugs()),
});

// Container
// Presentation (Bugs)
export default connect(mapStateToProps, mapDispatchToProps)(Bugs);

// export default Bugs;
```

### Hooks

Using the new code doesn't need to wrap via connect and define mapStateToProps & mapDispatchToProps

```jsx
import { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { loadBugs, getUnresolvedBugs } from "../store/bugs";

const BugsList = () => {
  const dispatch = useDispatch();

  // useSelector(state => state.entities.bugs.list)
  const bugs = useSelector(getUnresolvedBugs);

  useEffect(() => {
    dispatch(loadBugs());
  }, []);

  return (
    <ul>
      {bugs.map((bug) => (
        <li key={bug.id}>{bug.description}</li>
      ))}
    </ul>
  );
};

export default BugsList;
```

### Connect One or Many Components?

If you connect App component to the store, it gets notified every time the list of bugs or projects is modified. So if you add a bug, App component gets notified and the list of the bugs as well as the list of projects will be re-rendered. This unnecesssary and can cause a performance penalty.

So, as a best practice, each component should independently subscribe to a small slice of the store it is interested in. This way it won`t be re-rendered if other slices of the store are updated.

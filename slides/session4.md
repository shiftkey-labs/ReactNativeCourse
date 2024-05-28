# ShiftKey Academy Up 
## React Native  
### Session 4
### ShiftKey Labs
#### Allan Lavell

---

# Land Acknowledgement

ShiftKey Labs is located in Mi'kma'ki, the ancestral and unceeded territory of the Mi'kmaq people. We are all treaty people.

---

# Slides Link

* Direct Link to Session 4 posted in Notion (https://bit.ly/skrn) under Course Slides / Session 4 - https://github.com/shiftkey-labs/ReactNativeCourse/#/136
* Contains Sessions 1, 2, 3 & 4
* Use arrow keys to move around the presentation
* Press "esc" to get a zoom-out view and use the arrow keys to move around it, press "space" in this view to choose a slide
* If you don't see Session 4 you may need to force refresh your browser (Command + Shift + R on MacOS, Control + Shift + R on Windows)

---

# Submission Information

* We're asking for Github links when we sign you in tonight
* The last commit on your main branch at the end of June 5th will be considered your submission
* You can also email the link to me at alavell@dal.ca

---

# Session 4 Overview

* Reintroduction to State
* useState
* State Management Scenarios
* Redux Approach to State
* Redux Toolkit - Counter App
* Redux Toolkit - Slices, Root Reducer, useSelector & useDispatch
* Redux Toolkit - Counter App w/ Undo 

---

# Re-introduction to State

* In React Native, "state" encompasses any data within a component that can change over time and influence the component's behaviour or appearance
* This data can include variables representing user input, application status, or any other dynamic information that impacts the component's rendering
* Some general State Examples:
   * Form Input State: State management is used to track the values entered by users in various form fields, such as text inputs, checkboxes, or dropdowns
   * UI Component State: properties like visibility, enabled/disabled status, or active/inactive states
   * User Authentication State: information about whether a user is logged in or not, as well as details like user tokens or authentication credentials

---

# useState 

* The simplest way to interact with and modify state is via the `useState` hook, covered earlier in the course
* It takes an initial state value as an argument and returns a state variable and a function to update that variable
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-text-visibility-state?iframeId=ux1y41p8lb&amp;preview=true&amp;platform=web&amp;theme=light" height="450px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# State Management Scenarios

* You might be having a hard time imagining why you’d ever need something more complex than useState
* Here are some common scenarios why you might need something more advanced, such as Redux:
* Undo/Redo: useState doesn’t keep track of each change as it happens. More advanced state management solutions represent actions in the app as discrete objects, which are tracked, allowing you to move backward / forward through the events of the app
* Global State Management: When you need to share state across multiple components or manage application-wide state, useState becomes cumbersome. In such cases, you might consider using a global state management solution like Redux, Recoil, or Context API, which provides a centralized store for managing shared state across your application
* Asynchronous State Updates: useState is synchronous and doesn't handle asynchronous operations well. If you need to fetch data from an API, handle user input with debouncing, or manage complex asynchronous workflows, you'll need a more sophisticated solution like Redux

---

# Redux Approach to State

* Redux represents state management through three fundamental principles: the `store`, `actions`, and `reducers`
* The `store` acts as a single source of truth for application state
* `Actions` represent events or changes in the application
* `Reducers` determine how the application state should be updated in response to dispatched actions

---

# Redux Approach to State

* Redux follows a unidirectional data flow
* `Actions` are `dispatched` by event handlers within the app
* Once dispatched, `actions` go to the `store` which chooses the appropriate `reducer` to apply to the existing state to produce the new state for the given action
* The new state is then rendered to the UI
* <img src="./images/redux.gif" width="500px"/>

---

# Redux Toolkit 

* Redux Toolkit provides the standard & recommended way of writing Redux logic
* Redux Toolkit simplifies the process of setting up Redux by providing a set of tools and conventions that streamline store configuration, action creation, and reducers
* It eliminates boilerplate code, making Redux easier to use and more accessible to developers

---

# Redux Toolkit - Counter App

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-redux-toolkit-simple?iframeId=k5friuxbja&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Redux Toolkit - Slices

* Slices are a way to organize your Redux logic into smaller, more manageable pieces
* Slices encapsulate a piece of the Redux store's state along with the related reducers and actions that operate on that state
* `State`: Each slice defines its own initial state, which represents a portion of the overall state managed by Redux
* This initial state can be any JavaScript value, such as an object, array, or primitive value.
* `Reducers`: Slices define reducer functions that specify how the state should be updated in response to dispatched actions
* These reducers take the current state and an action as arguments, and return a new state object
* Redux Toolkit uses the createSlice function to automatically generate reducer functions based on the initial state and a set of "case reducers" that define how to handle each action type
* `Actions`: Slices automatically generate action creators for each case reducer, making it easy to dispatch actions to update the state
* These action creators can be imported and used in your components to trigger state updates
* `Selectors`: Slices can also define selector functions that extract specific pieces of state from the Redux store
* Selectors are useful for accessing slice-specific state in your components without having to know the internal structure of the state object

---

# Redux Toolkit - Slices
```js
const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
  },
})

const { increment, decrement } = counterSlice.actions
```
* The slice has a name, initialState, and reducer definitions
* In our example, the state is initialized to have a value object with a value of 0
* increment and decrement simply add / subtract 1 to that value
* We can get the increment and decrement action creators by destructuring the counterSlice.actions object

---

# Redux Toolkit - Root Reducer

* It’s common practice in Redux Toolkit to create a bunch of slices, and then combine them all using combineReducers into 1 single “root reducer”.
* We only have 1 slice here, but we’ll still follow that pattern
```js
const rootReducer = combineReducers({
  counter: counterSlice.reducer
})

export const store = configureStore({
  reducer: rootReducer,
})
```
* We use the counterSlice.reducer property to access all of the reducers on the counterSlice, combining them into the counter portion of the rootReducer
* We then configure the store to use the rootReducer as its primary reducer

---

# Redux Toolkit - useDispatch, useSelector

* Now comes time to thread everything together, and use our RTK Slices in the UI
* useSelector is used to access state values 
* useDispatch is used to access the dispatch function which can trigger actions in the system
```js
const MainScreen = () => {
  const value = useSelector(state => state.counter.value)
  const dispatch = useDispatch()
  
  return (
    <View style={tw`w-full flex-1 bg-black text-white`}>
      <View style={tw`mx-auto mt-12`}>
        <Text style={tw`text-white mx-auto text-4xl mb-2 font-bold`}>{value}</Text>
        <View style={tw`flex flex-row gap-x-0.5`}>
          <Button title="+" onPress={() => {dispatch(increment())}} />
          <Button title="-" onPress={() => {dispatch(decrement())}} />
        </View>
      </View>
    </View>
  );
}
```
* To access the value in the state, we utilize useSelector(state ⇒ state.counter.value)
* You’ll notice how we used the “counter” name of the slice to access that specific value.
* We have a Text component displaying that {value}, updating whenever the state changes
* We also have two Buttons, one that dispatches the increment action creator and the other, decrement

---

# Redux Toolkit - Undo

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-redux-toolkit-simple-undo?iframeId=95w5ubcazc&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Redux Toolkit - Undo

* The goal of using Redux to manage state is to enable us to access higher-level functionality with ease - one of the prime use cases is undo management
* Without Redux, this is a difficult task
* With Redux, it’s as simple as adding a dependency, redux-undo, and changing a few lines of code
```js
import undoable from 'redux-undo'
import { ActionCreators } from "redux-undo"
```
* The counterSlice remains the same
```js
const rootReducer = combineReducers({
  counter: undoable(counterSlice.reducer)
})
```
* When defining the root reducer, we apply undoable to the counterSlice.reducer
```js
const MainScreen = () => {
  const value = useSelector(state => state.counter.present.value)
  const dispatch = useDispatch()
  
  ...
}
```
* In the MainScreen, useSelector changes - before it was `state => state.counter.value` but now we have to add the keyword `present` which accounts for the undo stack's *current value*

---

# Redux Toolkit - Undo 

```js
const MainScreen = () => {
  ...  

  return (
    <View style={tw`w-full flex-1 bg-black text-white`}>
      ...
        <View style={tw`mx-auto flex flex-row gap-x-0.5`}>
          <Button title="undo" onPress={() => {dispatch(ActionCreators.undo())} } />
          <Button title="redo" onPress={() => {dispatch(ActionCreators.redo())} } />
        </View>
      </View>
    </View>
  );
}
```
* We also add the undo and redo buttons, which dispatch the automatically generated ActionCreators.undo() and ActionCreators.redo() from undoable
* Now our simple counter app supports undo/redo ~

---

# Redux Toolkit Recap

* Redux Toolkit is the preferred way to write Redux Code
* Redux Toolkit comes bundled with and powers RTK Query, which is what we're using for our DB
* Redux Toolkit uses createSlice to define functionality
* RTK Query instead uses createAPI to define functionality
* Both of those generate actions and reducers for Redux
* Redux Toolkit can be enhanced with undo functionality by adding a library and wrapping slices with it

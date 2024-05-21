# ShiftKey Academy Up 
## React Native  
### Session 3
### ShiftKey Labs
#### Allan Lavell

---

# Land Acknowledgement

ShiftKey Labs is located in Mi'kma'ki, the ancestral and unceeded territory of the Mi'kmaq people. We are all treaty people.

---

# Slides Link

* https://github.com/shiftkey-labs/ReactNativeCourse
* Contains Sessions 1, 2 & 3
* Use arrow keys to move around the presentation
* Press "esc" to get a zoom-out view and use the arrow keys to move around it, press "space" in this view to choose a slide
* Direct Link to Session 3 posted in Notion (https://bit.ly/skrn) under Course Slides / Session 3 - https://github.com/shiftkey-labs/ReactNativeCourse/#/101
* If you don't see Session 3 you may need to force refresh your browser (Command + Shift + R on MacOS, Control + Shift + R on Windows)

---

# Session 3 Overview

* Refs and useRef
* React Navigation Top Bar Styling, Content & Functionality
* React Navigation Events
* Route Prop & Passing Props to React Navigation Screens
* useLayoutEffect

---

# Session 3 Overview

* Debugging Tips
* Sizing & Positioning - The Box Model
* Tailwind - Absolute Positioning (Floating Action Button)
* Tailwind - Sizing & Positioning Units
* Tailwind - Centering 

---

# Session 3 Overview

* Tailwind - Hex Color Codes
* useEffect - With dependencies
* useEffect & RTK Query
* Object Destructuring
* Object Destructuring - Aliasing

---

# Session 3 Overview

* Reintroduction to State
* useState
* State Management Scenarios
* Redux Approach to State
* Redux Toolkit - Counter App
* Redux Toolkit - Slices, Root Reducer, useSelector & useDispatch
* Redux Toolkit - Counter App w/ Undo 

---

# Refs and useRef

* Refs (short for references) provide a way to access and interact with React Native components directly
* They are commonly used to manage focus, text selection, or trigger animations
* Refs are created using the useRef hook
* useRef is a hook that returns a mutable ref object whose .current property is initialized with the passed argument
* The returned object will persist for the full lifetime of the component

---

# Refs and useRef - TextInput Focus

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-useref-textinput-focus?iframeId=nlhsvlabrv&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# React Navigation Top Bar Styling, Content & Functionality

* When you use React Navigation, it automatically generates UI components for you - such as a Top Bar when using Stack Navigation
* By default, the Top Bar has a relatively plain style - what if you want to customize how it looks, or what content it displays?
* There are a couple of techniques to aid you here
* There's a prop called options that can be set at initialization time when you define the Screen 
```js
<Stack.Screen 
    options={{
        headerStyle: tw`bg-purple-300 border-0`,
        headerTintColor: '#fff',
        headerTitleStyle: tw`font-bold`,
        headerShadowVisible: false, // gets rid of border on device
        headerRight: () => ( <Button onPress={() => { console.log("hey"); }} title="Button" color="#000"/> )
    }}
    name="Home" component={HomeScreen} />
```

---

# React Navigation Top Bar Styling, Content & Functionality

* You can also use the navigation prop passed into a Screen component to set the options dynamically 
* This can be useful if you have specific data in your component that you want reflected in how the Top Bar is behaving, that may not be known at the time of definition of the Screen
* Here's an example the sets the title of the Screen to a random integer every time you navigate to that Screen - data that couldn't be known at initialization time
```js
const getRandomInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;

function DetailsScreen({ navigation }) {
  useEffect(() => {
    navigation.setOptions({ title: getRandomInt(0, 100)});
  }, []);

  return (
    <View style={tw`flex-1 items-center justify-center bg-purple-400`}>
      <Text style={tw`text-lg text-white`}>Details Screen</Text>
    </View>
  );
}
```

---

# React Navigation Top Bar Styling, Content & Functionality 

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-react-navigation-header-customization?iframeId=alfb2p3u7i&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# React Navigation Events

* Sometimes you want to perform an action automatically when the user performs a certain navigation event
* React Navigation provides event streams that your component can subscribe to in order to perform those actions
* The core events are as follows:
    * focus: emitted when the screen comes into focus
    * blur: emitted when the screen goes out of focus.
    * state: emitted when the navigator's state changes - receives the navigator's state in the event data (event.data.state)
    * beforeRemove: emitted when the user is leaving the screen - provides the opportunity to prevent the user from leaving, as well

---

# React Navigation Events

```js
const Screen =  ({ navigation }) => {
  useEffect(() => {
    const unsubscribe = navigation.addListener('focus', () => {
      console.log("screen focused");
    });

    return unsubscribe;
  }, []);

  return <Text>Example</Text>;
}
```
* The navigation.addListener function returns an "unsubscribe" function, which manages the lifecycle of the subscription
* Remember how useEffect will execute a function that's returned on unmount - so in this case we return the unsubscribe function, which will cancel the subscription when the Screen component is unmounted

---

# React Navigation Events - beforeRemove

<iframe src="https://snack.expo.dev/embedded/@alavell/15d265?iframeId=vmmb3wq2ei&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Route Prop & Passing Props to React Navigation Screens

* In order to go to a screen, you use the navigation.navigate function
* But how do you pass props to the screen at the time of navigation?
* Normally with a component, you'd pass the props into it directly, at the time that it is declared in the View hierarchy 
* But with React Navigation, you're declaring the Screen component as a route, at the start, meaning you can't just pass the props in directly at the "right" time
* In addition to the "navigation" prop, each screen is provided with a "route" prop, that contains a params object that can be passed info with the navigation.navigate function
* https://reactnavigation.org/docs/route-prop

---

# React Navigation Route Prop

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-react-navigation-route-prop?iframeId=w61rmsckhw&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# useLayoutEffect

* You may have noticed, in the last example we used a hook called "useLayoutEffect" instead of "useEffect"
* useEffect runs asynchronously, during and after the time the UI is rendered
* This makes useEffect very performant, but can cause some visual glitches when the component loads & renders new information (for example, a title from the route prop)
* useLayoutEffect runs synchronously, *before* the UI is rendered, effectively blocking full UI rendering until it's done running
* This is less performant, but will result in a fully rendered UI that only gets rendered once
* In certain cases this is less visually jarring than loading quickly & changing values like useEffect does

---

# Debugging Tips

* When it comes to UI development, sometimes things get tricky and it's hard to tell what's going on 
* There can be subtle differences in how React Native handles layout on different platforms, making things even harder
* It's key to test your app on a variety of devices periodically to ensure your layouts are working
* Rule of thumb when it's not working, it often involves an issue in the View hierarchy
* Try setting different debug background colors on Views, and see if they are sized properly
* Often a containing View may not actually fill the space you're expecting, resulting in child elements not being displayed
* Another common issue is forgetting to include a "return" statement when using map()
* Another issue is attempting to import components from the wrong libary (react-native-web instead of react-native, for example)
* Sometimes an import requires curly braces around the name of the imported { Component }, sometimes it doesn't 

---

# Sizing & Positioning - The Box Model

* CSS, which is what Tailwind is based on, defines something called "The Box Model" to lay out elements
* ![](./images/box-model.png)
* This is what you're modifying when you use utilities like `mt-3` or `px-2`
* A great place for brushing up on the fundamentals is https://learn.shayhowe.com 

---

# Tailwind - Absolute Positiong (Floating Action Button)

* It can be useful to lay out elements relative to the screen itself, rather than other elements
* To do this, you can use absolute positioning, along with the top-, left-, bottom- and right- directives
* Each of those specifies the distance from the respective side of the screen 
* This is useful for making a FAB (Floating Action Button)
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-fab?iframeId=myhk7tn2xm&amp;preview=true&amp;platform=web&amp;theme=light" height="318px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Tailwind Sizing & Positioning Units

* Tailwind has a variety of possible units that you can use to lay elements out on screen
* There's the standard option (ex. w-32) which actually translates to 4px per unit - useful for quick, constant sizing & positioning
* <img src="./images/tailwind-unit.png" width="300px"/>

---

# Tailwind Sizing & Positioniong Units

* There's the percentage-based utilities, such as `w-full`, `w-1/2` and `w-2/5`
![](images/tailwind-percentage-unit.png)
* You can also specify a more specific percentage by using `w-[55%]` or `h-[98%]` etc.
* Whenever you see [square brackets] in tailwind, you're invoking Tailwind's just-in-time (JIT) compiler to provide "arbitrary values" (i.e. values that weren't built-into their design system)
* There's the option of sizing elements to the viewport itself, using `w-screen` or `h-screen`

---

# Tailwind - Centering

* To center an element horizontally, you use `mx-auto` which means "set margin along the x-axis automatically", or `my-auto` for vertical centering
* This only works if the element has a clearly defined size that's less than the full amount along that axis of the screen - if it's set to width-full for example, it won't do anything as the width of the element is set to take up the full space, and the margins will thus be zero
* To center text use `text-center`

---

# Tailwind - Centering

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-tailwind-centering?iframeId=su5i08c0e3&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Tailwind - Hex Color Codes

* Tailwind has a variety of default colors, using the `color-number` syntax, such as `bg-purple-300` or `text-purple-500`, producing various shades of the named color
* If you want more customizability, you can use Tailwind's JIT compiler to specifiy a hex color
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-tailwind-hex-color?iframeId=v5tpn9cy9z&amp;preview=true&amp;platform=web&amp;theme=light" height="280px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# useEffect - With Dependencies

* We've covered useEffect in the context of component mount - with an empty dependency array
```js
useEffect(() => {
  console.log("component mounted");
}, []);
```
* And component unmount - by returning a function from useEfffect
```js
useEffect(() => {
  return () => {
    console.log("component unmounted");
  }
}, [])
```
* But what happens when you populate that dependency array with some actual dependencies?

---

# useEffect - With Dependencies

* The dependencies array specifies what variables React Native should monitor to know to run the side effect code when they change
* Think of a variable changing like an event, and putting that variable in the dependencies array of an effect is like subscribing to that event stream
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-useeffect-dependencies-modal?iframeId=4zpjdz1h9v&amp;preview=true&amp;platform=web&amp;theme=light" height="450px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# useEffect & RTK Query 

* When looking at the RTK Query DB API, you might expect that when you call addNote, you should directly get the result of adding the note as a return value from that function
* This would look something like:
```js
// This code doens't do what you might expect
<TouchableOpacity onPress={() => { const data = addNote({title: "test", content: "content"}); }}>
```
* React Native often forces you to think a bit differently than normal imperative programming - the data variable is actually the result of calling the useAddNoteMutation hook, it's not returned directly when you call addNote - so how do you get access to it and its data?
* You have to employ useEffect dependencies! 
* The data variable starts off as undefined - but when you call addNote, it will be populated with title & content strings (which are likely initially empty if the user hasn't input any actual information yet), as well as a unique ID that's automatically generated for you at creation time
* By placing the `data` variable in the dependencies array of a useEffect call, you can react to changes and perform actions (such as when the user adds a note)

---

# useEffect & RTK Query

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-rtk-query-addnote?iframeId=twpg5o0qjr&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Object Destructuring

* Object destructuring allows you to extract multiple properties from an object and assign them to variables using a syntax that mirrors the structure of the object
```js
const user = { name: 'Alice', age: 25 };
const { name, age } = user;
console.log(name); // Output: Alice
console.log(age); // Output: 25
```
* Object destructuring is what we're using when we're getting our functions and variables from RTK Query
* For example, the useAddNoteMutation hook is returning an array with a function to trigger the mutation (addNote) and an object that contains the mutation state (data, error, isLoading)

---

# Object Destructuring 

```js
const [ addNote, { data, error, isLoading }] = useAddNoteMutation();
```
* Here, `addNote` will be assigned the function to trigger the mutation
* `{ data, error, isLoading }` is an object destructuring assignment on the second element of the array, which is an object containing various properties about the mutation state
* By using `{ data, error, isLoading }`, you are extracting the `data`, `error`, and `isLoading` properties from this object directly into variables named `data`, `error`, and `isLoading`
* You can then use the function & variables elsewhere in your code (such as with useEffect) to apply the mutation and access the results

---

# Object Destructuring - Aliasing

* Sometimes you want to use a different name in the local context for a destructured variable from an object 
* With our RTK Query DB API, it may be necessary to do so - say you want to use the useSearchNotesQuery and useAddNoteMutation in the same Component - both of these hooks return an object with a `data` property, which has different information in it
  * The useSearchNotesQuery returns a `data` object that represents all of the notes in the DB that contain continous text matching the search string
  * The useAddNoteMutation returns a `data` object that represents the note that was just added to the DB
* Clearly, these are different `datas` and they serve a different purpose, but they are both called data in the returned object - we can't use the same name twice

---

# Object Destructuring - Aliasing 

* It may be tempting to do something like the following:
```js
const { data, error, isLoading } = useSearchNotesQuery("");
const [ addNote, { data2, error2, isLoading2 }] = useAddNoteMutation(); // won't work
```
* This doesn't work however, because the object returned by the hook doesn't contain the `data2`, `error2`, or `isLoading2` properties - it's always `data`, `error`, `isLoading`
* To do this: you use something called `Aliasing`
```js
const { data: searchNotesData, error: searchNotesError, isLoading: searchNotesIsLoading } = useSearchNotesQuery("");
const [ addNote, { data: addNoteData, error: addNoteError, isLoading: addNoteIsLoading }] = useAddNoteMutation(); 
```
* The syntax is: 
```js
{ property: newVariableName } = useX();
```
* This creates local variables that extract the information from the property, but assign the value to the newVariableName - such as `addNoteData` from `data` or `searchNotesIsLoading` from `isLoading`
* Using this technique, you can use as many RTK Query hooks in one component as you want 

---

# Object Destructuring - Aliasing

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-rtk-query-data?iframeId=98m76qv9li&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

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
* Open question for the class - can you use the `undoable` library to add Undo functionality to our RTK Query DB API? 
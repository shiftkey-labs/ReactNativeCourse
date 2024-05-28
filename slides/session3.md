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
* Contains Sessions 1, 2, 3 & 4
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

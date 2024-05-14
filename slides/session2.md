# ShiftKey Academy Up 
## React Native  
### Session 2
### ShiftKey Labs
#### Allan Lavell

---

# Land Acknowledgement

ShiftKey Labs is located in Mi'kma'ki, the ancestral and unceeded territory of the Mi'kmaq people. We are all treaty people.

---

# Slides Link

* https://github.com/shiftkey-labs/ReactNativeCourse
* Contains Sessions 1 and 2
* Use arrow keys to move around the presentation
* Press "esc" to get a zoom-out view and use the arrow keys to move around it, press "space" in this view to choose a slide
* Direct Link to Session 2 posted in Notion (https://bit.ly/skrn) under Course Slides / Session 2 - https://github.com/shiftkey-labs/ReactNativeCourse/#/62

---

# Session 2 Overview

* Side-Effects
* useEffect & Component Lifecycle
* FlatList - Lists & Grids
* MasonryList 

---

# Session 2 Overview

* Routing & React Navigation - Overview
* React Navigation - Stack
* React Navigation - Tab
* React Navigation - Drawer
* Project Setup
* Project Dependencies

---

# Session 2 Overview

* Redux & Redux Toolkit - Introduction
* RTKQuery - Overview
* RTK Query createAPI, Queries & Mutations
* RTK Query Tags
* RTK Query - fetch & add
* RTK Query baseQuery
* RTKQuery in Practice

---

# Side-Effects

* A **Side Effect** is anything that results in changes when the execution of a function is completed, other than the return value 
* Examples: 
	* Fetching data asynchronously from an API
	* Subscribing to an event stream
	* Modifying global variables 
	* Console.logging 
* For managing side-effects in React Native, we have the hook - useEffect

---

# useEffect - Running Side-Effects on Component Mount

* We'll build our understanding of the multi-facted useEffect hook step-by-step 
* Here's the simple form of useEffect:
```js
useEffect(() => {

}, []); 
```
* Notice how it accepts two arguments: a callback function, and an array of dependencies (in this simple case it's empty)
* The function represents the code to be run
* An empty dependency array means "run on mount"
* Here it is in the context of a containing component:
```js
const MyComponent = () => {
	useEffect(() => {
		console.log("Component mounted");
	}, []);

	return <Text>Test Component</Text>;
}
```

---

# useEffect - Running Code on Component Unmount

* useEffect can also be useful to execute logic when components unmount
* To do so, return a function from useEffect
```js
const MyComponent = () => {
	useEffect(() => {
		console.log("Component mounted");

		return () => {
			console.log("Component unmounted");
		};
	}, []);

	return <Text>Test Component</Text>;
}
```
* This is just a brief intro to useEffect, you'll see it more in the coming slides

---

# FlatList - Lists & Grids

* Inevitably in apps, there are collections of items that the user needs to scroll through
* It can be useful to display these collections as either lists (1-dimensional) or grids (2-dimensional)
* React Native provides the versatile FlatList component, which can be used to render either a list or a grid
* FlatList is "lazily loaded" - meaning it knows to render only the current items on screen, and loads more as the user scrolls 
* Lazy Loading ensures that FlatList stays performant even when there are a large number of items in the collection

---

# FlatList - Basic Syntax & Form

```js
const App = () => {
  // other code including data generation

  return (
    <FlatList
      data={data}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => <Card item={item} />}
      numColumns={1}
      contentContainerStyle={tw`p-4`}
    />
  );
};
```
 
* Declare the FlatList component
* Pass it the data prop (which should be an array)
* Provide the keyExtractor function prop, which is run on each element of the array, & should isolate & return a property from the element to use as a unique ID
	* Providing a unique id "key" helps React Native know how to re-render the elements efficiently
* Provide the renderItem function prop, which also runs on each array element and returns a Component to be used to render that element
* Provide the numColumns prop, which tells FlatList how many columns to render
* Provide the contentContainerStyle, which gives styling to the content scrolling container

---

# FlatList - List

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-flatlist-list?iframeId=yfiognikxi&amp;preview=true&amp;platform=web&amp;theme=light" height="560px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# FlatList - Grid

* Sometimes it's beneficial to display items in a grid, rather than a list
* It allows for visual comparison of more items at once
* Can also be achieved with a FlatList by changing the numColumns:

```js
const App = () => {
  return (
    <FlatList
      data={data}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => <Card item={item} />}
      numColumns={3}
      contentContainerStyle={tw`p-4`}
    />
  );
};
```

---

# FlatList - Grid

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-flatlist-grid?iframeId=ygtaihikab&amp;preview=true&amp;platform=web&amp;theme=light" height="560px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# MasonryList

* What if you want the elements of a grid to have different sizes vertically? 
* FlatList enforces a uniform vertical height across rows - meaning the largest element in a row will determine the vertical height for all elements in that row
* Often when users are inputting their own information, such as in our SKNotes app, each element will have its own size
* This is where MasonryList comes in - a variation on FlatList that allows for individually sized elements
* We get our MasonryList from the following dependency - @react-native-seoul/masonry-list

---

# MasonryList

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-masonry-list?iframeId=po71wjrskz&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# App Routing aka Navigation

* As your app grows in complexity, it will begin to accommodate more than 1 screen
* There are various ways of users navigating those screens
* Commonly used:
	* Tab bars on the bottom of the screen
	* Deep links to specific points in the app
	* Stack navigation where each new screen is pushed to the top of the stack
* This area of concern is commonly known as Routing, or Navigation

---

# React Navigation

* React Navigation is a routing management framework for React Native
* Specifically designed for mobile platforms, offering navigation patterns & components optimized for touch-based interactions
* Provides stack navigation, tab navigation, drawer navigation & more
* It has flexible configuration options
* It automatically handles navigation state for you

---

# Stack Navigation

* Stack navigation is where one screen gets "pushed" on top of another, and then you have the option to go back 
* Similar to how a web browser works - every time you visit a link, you're pushing to the stack, which lets you go back
* On iOS and Android, the convention is that the top bar shows a back button
* On iOS you can also swipe from the left side of the screen to go back

---

# Stack Navigation 

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-stack-navigation?iframeId=28i320poer&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Stack Navigation

* Import relevant dependencies:
```js
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
```
* Create the Screen components which accept a "navigation" prop, which can be used for various purposes including moving to other screens
```js
function HomeScreen({ navigation }) {
  return (
    <View style={tw`flex-1 items-center justify-center`}>
      <Text style={tw`text-lg mb-4`}>Home Screen</Text>
      <Button
        title="Go to Details"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
}

function DetailsScreen() {
  return (
    <View style={tw`flex-1 items-center justify-center`}>
      <Text style={tw`text-lg`}>Details Screen</Text>
    </View>
  );
}
```

---

# Stack Navigation

* Create the Stack Navigator
```js
const Stack = createNativeStackNavigator();
```
* Wrap the App content in a NavigationContainer, declare the Stack.Navigator, and setup the screens
```js
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
```
* Each screen has a "name" for its route, and a corresponding component that it renders

---

# Tab Navigation

* Tab Navigation is where different screens are displayed as "Tabs" on the bottom of the screen
* Selecting a Tab changes you over to the screen at that route
* Very common pattern in a lot of apps

---

# Tab Navigation

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-react-navigation-tabs?iframeId=gmivaq0aas&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Tab Navigation

* Import relevant dependencies:
```js
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
```
* Define some screen components:
```js
const Screen1 = () => {
  return (
    <View style={tw`flex-1 items-center justify-center`}>
      <Text>Screen 1</Text>
    </View>
  );
}

const Screen2 = () => {
  return (
    <View style={tw`flex-1 items-center justify-center`}>
      <Text>Screen 2</Text>
    </View>
  );
}
```
* Create the Tab Navigator
```js
const Tab = createBottomTabNavigator()
```

---

# Tab Navigation

* Wrap everything in a NavigationContainer, and then create a Tab.Navigator with Tab.Screens
```js
 <NavigationContainer>
  <Tab.Navigator>
    <Tab.Screen name="Screen1" component={Screen1} />
    <Tab.Screen name="Screen2" component={Screen2} />
  </Tab.Navigator>
</NavigationContainer>
```

---

# Drawer Navigation

* Another common pattern is to have a “drawer”, usually on the left side of the screen, which is a pull-out menu you can access by either tapping a button or swiping right from the side of the screen
* React Navigation supports this as well

---

# Drawer Navigation

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-drawer-navigation?iframeId=rrnlrzhe7o&amp;preview=true&amp;platform=web&amp;theme=light" height="550px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Project Setup

* We have moved from React Native CLI to Expo as the basis of our project
* Expo provides a streamlined install process that only takes a few minutes & doesn't require the installation of Android Studio or Xcode
* There's now a default project you can "fork" on Github to create your own version

---

# Project Setup

https://github.com/shiftkey-labs/SKNotesStarter

---

# Project Dependencies

* @react-native-seoul/masonry-list: MasonryList interface, similar in form to FlatList but with variable vertical height on cells
* @react-navigation/native, @react-navigation/native-stack, react-native-screens, react-native-reanimated: Interface for routing between screens, with Stack Navigation support and animations
* @reduxjs/toolkit, react-redux: Redux + Redux Toolkit, a state management solution for React Native, which comes bundled with RTK Query, which is how we setup our DB API
* twrnc (Tailwind React Native Classes): A React Native implementation of the Tailwind CSS Utility framework for app styling
* @react-native-async-storage/async-storage: A storage mechanism that keeps key/value pairs, very simple interface for setting up a local DB (as done in db.js)
* react-native-uuid: UUID (Universally Unique Identifer) library for creating IDs for Database entries

---

# Redux 

* Redux is the classic state management library that's used with React, originally created in 2015 by Dan Abramov, a Meta employee
* Based on the "Flux Architecture" that Meta introduced in 2014, where data is always flowing in one direction, to simplify reasoning about data flow
* 3 fundamental principles: the store, actions, and reducers
* The store acts as a single source of truth for application state
* Actions represent events or changes in the application
* Reducers determine how the application state should be updated in response to dispatched actions

---

# Redux Toolkit

* Plain Redux requires the programmer to write a lot of boilerplate code
* Enter Redux Toolkit, which is now the official way to write Redux code
* Simplifies store setup, creating reducers, creating async logic and more
* Introduces the concept of a "Slice" of state
* Comes packaged with RTK Query, which we're using in SKNotes

---

# RTK Query - Overview

* RTK Query is a data-fetching, caching & synchronization tool built into Redux Toolkit
* It is designed to simplify common cases for loading data in a web application, eliminating the need to hand-write data fetching & caching logic yourself
* Some problems it helps solve:
  * Tracking loading state in order to show UI spinners
  * Avoiding duplicate requests for the same data
  * Optimistic updates to make the UI feel faster
  * Managing cache lifetimes as the user interacts with the UI
* RTK Query works by defining an API that defines a set of endpoints that describe how to retrieve data from backend APIs and other async sources

---

# RTK Query createAPI, Queries & Mutations

* The core function we'll use from RTK Query is called createAPI, which creates a Redux Tookit "Slice" defining your API
* The API consists of number of endpoints - in our case, we have:
  * fetchNotes
  * searchNotes
  * addNote
  * deleteNote
  * updateNote
* Our endpoints take on one of 2 types: query, and mutation
* A query is designed to fetch data and return results without changing anything 
* A mutation is designed to modify data and return results
* RTK Query uses the information given to it in createAPI to generate a set of hooks you can use in your application to perform the defined actinos
  * For us, this looks like useFetchNotesQuery, useSearchNotesQuery, useAddNoteMutation, useUpdateNoteMutation, useDeleteNoteMutation 

---

# RTK Query Tags 

* In order for RTK Query to know when to refresh the data in the cache, it has the concept of Tags
* Tags provide a way to define relationships between queries and mutations, allowing RTK Query to automatically refetch data when necessary
* Tags are defined in the API Slice using the "tagTypes" array
* Each tag is a string that represents a type of data that can be invalidated and refetched
* Queries can use the "providesTags" property to specify which tags they provide
* Mutations can use the "invalidatesTags" property to specify which tags they invalidate
* When a mutation invalidates a tag, any query that provides that tag will automatically refetch its data
* This ensures that the data displayed in your application is always up-to-date after performing create, update, or delete operations

---

# RTK Query Example - Simplified from db.js

```js
export const dbApi = createApi({
  reducerPath: 'dbApi',
  tagTypes: ['Notes'],
  baseQuery: fakeBaseQuery(),
  endpoints: (build) => ({
    fetchNotes: build.query({
      async queryFn() {
        const serializedNotes = await AsyncStorage.getItem('notes');
        const notes = JSON.parse(serializedNotes);

        return { data: [notes] }
      },
      providesTags: (result) => ['Notes']
    }),
    addNote: build.mutation({
      async queryFn(note) {
        const serializedNotes = await AsyncStorage.getItem('notes');
        const notes = JSON.parse(serializedNotes) || [];
        note.id = uuid.v4();
        notes.unshift(note);
        await AsyncStorage.setItem('notes', JSON.stringify(notes));
        return { data: note }
      },
      invalidatesTags: ['Notes'],
    })
  })
})

export const { useFetchNotesQuery, useAddNoteMutation } = dbApi
```

---

# RTK Query - baseQuery, fetchBaseQuery & fakeBaseQuery()

* The "baseQuery" is a foundational function that handles the actual data fetching logic for your API endpoints
* It abstracts the details of how requests are made, providing a consistent interface for interacting with various types of backends (e.g., REST APIs, GraphQL APIs, etc.)
* For many online API calls, its sufficient to use the fetchBaseQuery, which wraps the 'fetch' API (which is a way of making HTTP requests)
* In our case, our database is local, so we don't need to "fetch" anything - instead we use one called fakeBaseQuery
* This essentially lets us pass off all the logic to the queryFn, which is where we perform our data handling logic

---

# RTK Query In Practice

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-rtk-query-simple?iframeId=yaa2kiswfk&amp;preview=true&amp;platform=web&amp;theme=light" height="550pxgg" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>
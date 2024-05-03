# Side-Effects

* A **Side Effect** is anything that results in changes when the execution of a function is completed, other than the return value 
* Examples: 
	* Fetching data asynchronously from an API
	* Subscribing to an event stream
	* Modifying global variables 
	* Console.logging 
* For managing side-effects in React Native, we have the hook - useEffect

---

# useEffect - Simplest Use Case: Running Side-Effects on Component Mount

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

# useEffect - Cleaning up on Component Unmount

* It can also be useful to execute logic when components unmount
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

---

# useEffect - Making an API Call

* x
* y
* z

---

# JSX Fragments

* X
* y
* z

---


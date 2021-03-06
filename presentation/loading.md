# Working with JSON data

## Promises and async await

ES6 introduced the [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) method to load external data. The fetch method returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). 

`let promise = fetch(url)`

A **Promise** object allows us to define code that will be executed once `fetch` has returned data. We do that by calling `then()` on the Promise object. This way, our application won't freeze and wait until the data is loaded.
```
promise.then(data => {
     console.log("data has finished loading!")
})
```
In the `fetch` function we use the new [async await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) syntax. This returns the Promise object that contains the data.
```
async getStarWarsData() {
    let promise = await fetch("https://swapi.co/api/films/")
    return await promise.json()
}
```

## Let's load JSON

The [Star Wars API](https://swapi.co) allows us to load a list of all star wars movies. After calling the [films url](https://swapi.co/api/films/) we get a JSON file.

```
export default class App extends Vue {
    films: Film[] = []
    created(){
        this.getStarWarsData().then(data => {
            this.films = data.results
        })
    }
    async getStarWarsData() {
        let res = await fetch("https://swapi.co/api/films/")
        return await res.json()
    }
}
```
*note: The `created` method is automatically called when the component is added to the DOM. Also, we call `then()` directly on the `getStarWarsData` function, so we don't need a separate `promise` variable.*

## Sending headers

We can send headers and POST data with `fetch` as well!
```
export default class App extends Vue {
    async getWebserviceData() {
        const myHeaders:Headers = new Headers();

        const myInit:RequestInit = { method: 'GET',
                    headers: myHeaders,
                    mode: 'cors',
                    cache: 'default' };

        const url = "your webservice url here"

        let res = await fetch(url, myInit)
        return await res.json()
    }
}
```


![state](./state.png)

Use the [Chrome Vue plugin](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd) to check the state of your component.

## Displaying data

If we assign the JSON to a reactive array, we can automatically populate the UI. You can bind array values to a repeating DOM element with `v-for`. 

In this example Vue will render a `<div>` for every film in our Films array. The variable `f` will contain one film.
```
<template>
    <div>
        <div v-for="f in films" :key="f.episode_id">{{f.title}}</div>
    </div>
</template>
```
*note that Vue wants us to supply a key. This should be a unique value, for example the movie's id*

## JSON Type definitions

Note that the variable that holds the Star Wars JSON is an array of type `Film`. We have defined this type in a `.d.ts` file. VS Code will give you code completion for known types. 

![actors](dts.png)

*Check the `starwars.d.ts` file to see how you can declare types for your own RESTful API data.*

## Reading List

- [MDN docs async await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [Why async await is better than Promises](https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9)

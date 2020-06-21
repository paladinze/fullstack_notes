# Vue

## vue
dom interaction 
vuejs instance
vue cli
vuex
components
directives
filters
mixins
animation & transitions
accessing db
routing
vuepress

## installation
- npm install -g @vue/cli

## the vue instance
- data: the state
- methods: ways to change the state
- computed: use cached result if no varaible changed
	- limitation: not suitable for async task, since has to return something sync
- watch: a manual version of computed
	- best practice to use computed instead
	- can run async task


## string interpolation
- {{}} can be used inside html element
- {{}} cannot be used in html element attribute
- can include simple Js statement

## dynamic css
- `:class="{red: isRed}"`
- `:class="[someColor, {red: isRed}]"`

## directive:
- v-bind: bind data to html attribtue
	- shorthand: just ":"
- v-model: two directional binding
- v-on: listen to event
	- shorthand: @
	- v-on:click
	- v-on:mousemove
		- v-on:mousemove.stop
		- v-on:mousemove.prevent
		- v-on:keyup.enter
- v-if
  - template: a way to group elements without div (like React fragments)
  - v-show: only hide not removing element from dom
- v-for
  - loop through simple list
    ```html
    <li v-for="(item, i) in itemList">{{item}} : {{i}}</li>
    ```
  - loop through object
    ```html
    <li v-for="person in persons">
      <div v-for="(value, key, idx) in person">
        {{value}} : {{key}} : {{index}}
      </div>
    </li>
    ```
  - loop through numbers
    ```html
    <li v-for="num in 10" :key="num">{{num}}</li>
    ```
- v-once: only the initial value will be used for interpolation
- v-html: render raw html

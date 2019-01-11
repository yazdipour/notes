# Vue

* `v-on:` == @
* `v-bind:` == :

* `<p>You are {{ age>18?  'adult' : 'kid'}}</p>`

* `<p :class="{hide: boolVar}" />` : if boolVar==true, class=hide, else it will not set class

## Tools and plugins

vue-router - vue-resource (Handle web requests) - vue-async-data (async data loading) - vue-validator (Form validation plugin) - vue-touch(Touch gestures using HammerJS)

## Release GithubPage

* https://github.com/KieferSivitz/vue-gh-pages
* Need a bit configuration
* `npm run deploy`

## Run on Create

```js
export default{
      created: function()
      {
          this.fetchProducts();
      },
      methods: {
        fetchProducts(){}
```

## Load Components from File

```js
import Footer from './components/Footer'
export default{
	components:{
		Footer
	}
}
<Footer/>
```

## Directive (v-)

Custom HTML attr that add extra functionality to our DOM el.

```
v-directive:param.ma.mb="expression"
   --------  ----  ----
   DirName   Arg   Modifiers
```

### Hook Functions
* bind: called only once, when the directive is first bound to the element. This is where you can do one-time setup work.
* inserted: called when the bound element has been inserted into its parent node (this only guarantees parent node presence, not necessarily in-document).
* update: called after the containing component’s VNode has updated, but possibly before its children have updated. The directive’s value may or may not have changed, but you can skip unnecessary updates by comparing the binding’s current and old values (see below on hook arguments).
* componentUpdated: called after the containing component’s VNode and the VNodes of its children have updated.
* unbind: called only once, when the directive is unbound from the element.

### Hook Arguments

* el: The element the directive is bound to. This can be used to directly manipulate the DOM.
* binding: An object containing the following properties.
* name: The name of the directive, without the v- prefix.
* value: The value passed to the directive. For example in v-my-directive="1 + 1", the value would be 2.
* oldValue: The previous value, only available in update and componentUpdated. It is available whether or not the value has changed.
* expression: The expression of the binding as a string. For example in v-my-directive="1 + 1", the expression would be "1 + 1".
* arg: The argument passed to the directive, if any. For example in v-my-directive:foo, the arg would be "foo".
* modifiers: An object containing modifiers, if any. For example in v-my-directive.foo.bar, the modifiers object would be { foo: true, bar: true }.
* vnode: The virtual node produced by Vue’s compiler. See the VNode API for full details.
* oldVnode: The previous virtual node, only available in the update and componentUpdated hooks.

### Custom Directive

```js
<p v-suffix="'cm'">34</p>
<p v-suffix.caps.caps2="'cm'">34</p>

Vue.directive('suffix',{
	bind(el,bindings){
		const suf = bindings.value;
		if(bindings.modifiers.caps.caps2){
			suffix = suffix.toUpperCase();
		}
		el.innerHTML = el.innerHTML + ' ' + suf;
	}
});
```

### Events

```js
v-on:click="foo()"
@click="foo()"				//short form

v-on:dblclick="foo()"
v-on:change="foo()"

v-on:click.prevent="foo()" // to prevent HyperLink Click Behavior

Vue.methods:foo(){}
```

### if / show

`<div v-if="boolVar"></div>`  //if boolVar=false -> will not render
`<div v-show="boolVar"></div>`  //if boolVar=false -> will render but inVisible

### bind

```html
<img v-bind:src="srcInVar">
<img :src="srcInVar">
```

### model 

(i guess it is only for input type elements)

```html
<input type="text" v-model="varName">	// 2 Way Bind

<select v-model="genderVar">			// Will put value inside genderVar
	<option value="Male">Male</option>
	<option value="Female">Female</option>
</select>
```

### for (ListView)

```html
<ul>
	<li v-for="user in users">{{user.name}}</li>
</ul>
```

## Components

### Simple + Nested Component

```js
<x></x>
Vue.component('x',{
	template:'<p>Hello {{name}}   <nested></nested></p>',
	data: function(){
		return {
			name: "Shahriar"
		}
	},
	components:{
		'nested':{
			template:'<p>Hey</p>'
		}
	}
})
new Vue(...)
```

### Props :prop

```js
<x name="shahriar"></x>
<x :name="xnamex"></x>

Vue.component('x',{
	props:['name'],
	template:'<p>Hello {{name}}</p>'
})

new Vue({
	el: '#app',
	data:{ xnamex:"SHAHRIAR" }
})
```

#### Validate Props

```js
props:{
	name: {
		type: String,
		required: true,
		default: "SHERY"
	},
	nrChild: Number
}
```

### SLOTS

```js
<x>shahriar</x>

Vue.component('x',{
	template:'<p>Hello <slot></slot></p>'
})
```

#### Multi Slot

```js
<x>
	<sth1 slot="sth1">Hello</sth>
	shahriar
	<sth2 slot="sth2">, BYE</sth2>
</x>

Vue.component('x',{
	template:
	'<p><slot name="sth1"></slot> <slot></slot> <slot name="sth2"></slot></p>' // Hello Shahriar, BYE
})
```

### Component Events *


```js
<x v-show="isOpen" v-on:close-btn="isOpen=false"/>

Vue.component('x',{
	template:'<button @click="closeBtn()"/>',
	methods:{
		closeBtn(){
			this.$emit('close-btn'); //emit customo event up to tree
			//this.$emit('close-btn', this.paramData); //pass param
		}
	}
})

new Vue(data=>isOpen:true)
```

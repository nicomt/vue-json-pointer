# vue-json-pointer

Basic fork of [json-pointer](https://github.com/manuelstofer/json-pointer) using **Vue.set** and **Vue.delete** to work with Vue reactivity system.
*If you're not using Vue is safer to use the [original library](https://github.com/manuelstofer/json-pointer)*



## Installation

[node.js](http://nodejs.org)

```bash
$ npm install vue-json-pointer
```


## API

```Javascript
var pointer = require('vue-json-pointer');
```


### .get(object, pointer)

Looks up a JSON pointer in an object.

Array of reference tokens, e.g. returned by api.parse, can be passed as a pointer to .get, .set and .remove methods.

```Javascript
...
state: {
    obj: {
        example: {
            bla: 'hello'
        }
    }
}
...
pointer.get(state.obj, '/example/bla');
```


### .set(object, pointer, value)

Sets a new value on object at the location described by pointer.

```Javascript
...
state: {
    obj: {}
}
...
pointer.set(state.obj, '/example/bla', 'hello');
```


### .remove(object, pointer)

Removes an attribute of object referenced by pointer.

```Javascript
...
state: {
    obj: {
        example: 'hello'
    }
}
...
pointer.remove(state.obj, '/example');
// state.obj -> {}
```


### .dict(object)

Creates a dictionary object (pointer -> value).

```Javascript
var obj = {
    hello: {bla: 'example'}
};
pointer.dict(state.obj);

// Returns:
// {
//    '/hello/bla': 'example'
// }
```


### .walk(object, iterator)

Just like:

```Javascript
each(pointer.dict(obj), iterator);
```


### .has(object, pointer)

Tests if an object has a value for a JSON pointer.

```Javascript
var obj = {
    bla: 'hello'
};

pointer.has(obj, '/bla');               // -> true
pointer.has(obj, '/non/existing');      // -> false
```


### .escape(str)

Escapes a reference token.

```Javascript
pointer.escape('hello~bla');            // -> 'hello~0bla'
pointer.escape('hello/bla');            // -> 'hello~1bla'
```


### .unescape(str)

Unescape a reference token.

```Javascript
pointer.unescape('hello~0bla');         // -> 'hello~bla'
pointer.unescape('hello~1bla');         // -> 'hello/bla'
```


### .parse(str)

Converts a JSON pointer into an array of reference tokens.

```Javascript
pointer.parse('/hello/bla');            // -> ['hello', 'bla']
```


### .compile(array)

Builds a json pointer from an array of reference tokens.

```Javascript
pointer.compile(['hello', 'bla']);      // -> '/hello/bla'
```


### pointer(object, [pointer, [value]])

Convenience wrapper around the api.

```Javascript
pointer(object)                 // bind object
pointer(object, pointer)        // get
pointer(object, pointer, value) // set
```

The wrapper supports chainable object oriented style.

```Javascript
var obj = {anything: 'bla'};
var objPointer = pointer(obj);
objPointer.set('/example', 'bla').dict();
```

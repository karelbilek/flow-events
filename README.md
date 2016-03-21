## Flow-events

Simple wrapper for EventEmitters, so your code is typesafe while still using traditional node EventEmitter.

Heavily inspired by [kimamula/ts-eventemitter](https://github.com/kimamula/ts-eventemitter) that does similar thing, for TypeScript.

### How to use it

Copy `flow-events.js` somewhere to your project. Then:

```javascript
/* @flow */

'use strict';

import 'babel-polyfill';
import {EventEmitter} from 'events';
import {Event0, Event1, Event2} from './flow-events';

class MyClass extends EventEmitter {
  
  // Note: for this syntax to work, you need
  // * turn on `esproposal.class_instance_fields=enable` in `.flowconfig` in `[options]`
  // * add `transform-class-properties` plugin to babel
  fooEvent: Event1<string> = new Event1("foo", this);
  barEvent: Event2<string, number> = new Event2("bar", this);

  doThings() {
    this.fooEvent.emit("whoop de doo");
    this.barEvent.emit("whoop de doo", 2);
  }
}

var myThing = new MyClass();

// you can use the Event objects, will be typechecked
myThing.fooEvent.on(s => console.log(s));
myThing.barEvent.on((s, n) => console.log(s + n.toString()));

// ...or traditional eventEmitter, unchecked
myThing.on('foo', s => console.log(s))

myThing.doThings();
```

### Npm?

I am too lazy to add figure out how exactly npm works and what all would be necessary. Sorry!

If you want to add this to npm yourself, go ahead!

### License

MIT

(C) Karel Bilek, 2016

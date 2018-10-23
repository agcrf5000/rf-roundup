### Non Strict Mode

* Undeclared variables will become properties to the window object.

### Strict Mode

```javascript
"use strict";
// all code in strict mode
```

```javascript
// non strict mode environment
function newCode(){
  "use strict";
  // all code in strict mode
}
```

* "use strict" is a string so that older browsers will ignore as a string.
* Using an undeclared variable will cause an error, in strict mode.
* Will not let you use reserved words as the variable name.
* Cannot delete variables, functions, or function arguments.
* Prevents variables in the eval function from leaking into the outside code.

---

# Javascript
Understanding Javascript better

## Table of Contents
1. [Function](#function)
1. [Closure](#closure)
1. [Prototype](#prototype)
1. [Object](#object)
1. [Pattern](#pattern)
1. [Best Practice] (#best-practice)
1. [Common Knowledge](#common-knowledge)
1. [Common Mistakes](#common-mistakes)

## Function
- [1.1](#1.1) <a name='1.1'></a> **Different Functions Definitions**

> Function Declaration
>
> Function Declaration is parsed from the start.
> Function Declarations loads before any code is executed (Hoisting).

```javascript
  function functionName(a) {
    return a;
  }
  // Semicolons are used to separate executable JavaScript statements.
  // Function declaration is not an executable statement,  so it is not common to end it with a semicolon
```

> Function Expression
>
> Function Expression is stored in a variable and defined at run-time

```javascript
  // 
  // The function here is actually anonymous function
  // Functions stored in variables do not need function names. 
  // They are always invoked (called) using the variable name.
  var x = function (a) {
    return a;
  };
```

> Function Constructor
> 
> Notice this is not the 'normal object' constructor, but the costructor for function

```javascript
  // To create function object, notice we use the keyword "Function" and "new"
  var functionName = new Function("a", "return a");
```  

- [1.2](#1.2) <a name='1.2'></a> **Interesting case: Function and Object**

> Object literals don't provide closures, only functions do.
> In addition, the properties of app1 will not be assigned until the function is called in the first example, 
> but will be immediately for app2.
>
> Constructor Pattern 

Constructor Function Diagram

![server diagram](Obj%20Constructor%20Function.png)

Creating a new object

![server diagram](new%20Object.png)

Setting prototype object

![server diagram](Set%20Object's%20Prototype.png)


```javascript
  // The name and printName will not be to assigned to 'Owner' Object 
  // until we use key word 'new'.
  // And the name and printName will be assigned to the window object from the start
function Obj(){
  this.name = 'obj';
  this.printName = function(){
    console.log(this.name);
  }
  function functionInsideObj(){
    console.log("test");
  }
  // This function will be execute when we call 'new'
  functionInsideObj();
}

var obj = new Obj();
```  
  
> Object Literal

```javascript
  // TODO Why Object Literal does not have closure?        
  // Refer to: http://www.akawebdesign.com/2010/10/22/javascript-singletons-object-literals-vs-closures/
  var app2 = {
    firstKey: function(){
       //something
    },
    secondKey: function(){
       //something
    }
    
    // The following code will be error
    /*
    function functionInsideObj(){
      console.log("test");
    }
    functionInsideObj();
    */
  };
  // Object literal vs Constructor Prototype
  // Refer to: http://stackoverflow.com/questions/17260603/object-literal-vs-constructorprototype
```

- [1.3](#1.3) <a name='1.3'></a> **Passed by Value or by Reference**

>Item passed in is passed by value. But the item that is passed by value is itself a reference.  
>Refer to => called call-by-sharing.
>If you change the parameter itself (as with num and obj2), that won't affect the item that was fed into the parameter. 
>But if you change the INTERNALS of the parameter, that will propagate back up (as with obj1)

```javascript
  function changeStuff(a, b, c)
  {
    a = a * 10;
    b.item = "changed";
    c = {item: "changed"};
  }

  var num = 10;
  var obj1 = {item: "unchanged"};
  var obj2 = {item: "unchanged"};

  changeStuff(num, obj1, obj2);
  
  console.log(num); // 10
  console.log(obj1.item); // changed    
  console.log(obj2.item); // unchanged
  
```

http://elegantcode.com/2010/10/22/basic-javascript-part-1-functions/

http://www.w3schools.com/js/js_function_definition.asp

http://stackoverflow.com/questions/4559207/difference-between-a-constructor-and-an-object

http://stackoverflow.com/questions/10328449/what-difference-is-there-in-javascript-between-a-constructor-function-and-funct

https://stackoverflow.com/questions/1013385/what-is-the-difference-between-a-function-expression-vs-declaration-in-javascrip

http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/

**[⬆ back to top](#table-of-contents)**






## Closure
http://howtonode.org/why-use-closure

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

http://spin.atomicobject.com/2014/10/20/javascript-scope-closures/

http://javascriptissexy.com/understand-javascript-closures-with-ease/

http://stackoverflow.com/questions/111102/how-do-javascript-closures-work

**[⬆ back to top](#table-of-contents)**






## Prototype
- [2.1](#2.1) <a name='2.1'></a> **Constructor Function and Prototype Object**:
  ![server diagram](Constructor%20and%20Prototype.png)
    1. When we create a function like function Foo() {}, JavaScript creates a Function instance.
    2. Every Function instance (the constructor function) has a property prototype which is a pointer.
    3. The prototype property of the constructor function points to its prototype object.
    4. The prototype object has a property constructor which is also a pointer.
    5. The constructor property of the prototype object points back to its constructor function.
    6. When we create a new instance of Foo like new Foo(), JavaScript creates a new object.
    7. The internal [[proto]] property of the instance points to the prototype of the constructor.
    
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

http://stackoverflow.com/questions/3564238/object-oriented-javascript-with-prototypes-vs-closures

http://stackoverflow.com/questions/15472005/setting-prototype-for-object-literal

**[⬆ back to top](#table-of-contents)**





## Object

http://stackoverflow.com/questions/14934831/new-operator-before-declaring-function

http://howtonode.org/what-is-this

https://javascriptweblog.wordpress.com/2010/08/30/understanding-javascripts-this/

http://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work

http://stackoverflow.com/questions/17260603/object-literal-vs-constructorprototype

http://www.quirksmode.org/js/this.html

http://blog.kevinchisholm.com/javascript/difference-between-object-literal-and-instance-object/

http://stackoverflow.com/questions/8093057/javascript-inheritance-and-the-constructor-property

http://robdodson.me/javascript-design-patterns-singleton/

http://stackoverflow.com/questions/22401553/what-are-all-the-difference-between-function-and-constructor-function-in-javascr

http://stackoverflow.com/questions/5958417/javascript-function-and-object

http://stackoverflow.com/questions/14934831/new-operator-before-declaring-function

http://www.akawebdesign.com/2010/10/22/javascript-singletons-object-literals-vs-closures/

**[⬆ back to top](#table-of-contents)**







## Pattern

Module patterns

http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/

http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

**[⬆ back to top](#table-of-contents)**


## Best Practice and Performance
http://www.w3.org/wiki/JavaScript_best_practices

http://desalasworks.com/article/javascript-performance-techniques/

http://ejohn.org/blog/dom-documentfragments/

http://gregfranko.com/blog/javascript-performance-tips/

**[⬆ back to top](#table-of-contents)**



## Common Knowledge

http://hangar.runway7.net/javascript/guide

http://www.quora.com/What-is-a-simple-explanation-of-higher-order-functions-and-callbacks-in-JavaScript

http://stackoverflow.com/questions/9053842/advanced-javascript-why-is-this-function-wrapped-in-parentheses

http://stackoverflow.com/questions/20824558/why-use-parentheses-when-returning-in-javascript

http://www.crockford.com/javascript/private.html

http://stackoverflow.com/questions/10328449/what-difference-is-there-in-javascript-between-a-constructor-function-and-funct

http://www.sitepoint.com/oriented-programming-1-4/

http://stackoverflow.com/questions/2917175/return-multiple-values-in-javascript

http://alistapart.com/article/getoutbindingsituations

http://robertnyman.com/2008/10/09/explaining-javascript-scope-and-closures/

https://javascriptweblog.wordpress.com/2010/08/09/variables-vs-properties-in-javascript/

http://ericleads.com/2013/01/javascript-constructor-functions-vs-factory-functions/

http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/#more-1037

http://eloquentjavascript.net/05_higher_order.html

**[⬆ back to top](#table-of-contents)**


## Common Mistakes
http://www.toptal.com/javascript/10-most-common-javascript-mistakes

**[⬆ back to top](#table-of-contents)**


## Interview

http://www.toptal.com/javascript/interview-questions

**[⬆ back to top](#table-of-contents)**


## Good Reference Sites
https://developer.mozilla.org/en-US/docs/Web/JavaScript
http://eloquentjavascript.net/


## ECMA 6
http://www.ecma-international.org/ecma-262/6.0/index.html

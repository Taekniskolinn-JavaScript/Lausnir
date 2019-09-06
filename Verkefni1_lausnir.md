# Verkefni 1 JavaScript lausnir

1. Hvað er null og undefined?

  	`null` og `undefined` þýða í raun bæði það sama, ekkert!
  	`undefined` breyta hefur ekki verið úthlutað þ.e.a.s. það vantar gildi (type undefined with value undefined).


     ```javascript
        var b;        // breyta er búin til með upphafsgildið undefined (sem þýðir að breytan vantar gildi).
        typeof(b)     // undefined, tegundin (e. type) er líka undefined.
     ```

    fall (e. function) skilar undefined ef gildi er ekki skilað (vantar `return`).
     
     ```javascript
      console.log(b);   // console.log() fallið sjálft birtir b, en skilar undefined.
                        // sem þýðir að engu var skilað (e. returned).
     ```

    Margar aðgerðir í máli skila engum merkingalegum gildum en verða að skila einhverju og nota þá <em>undefined</em>.
     
    ```javascript
      var x = 5;        // = virkin (e. operator) skilar undefined, ekki gildi 
    ```
    Athyglisvert er að gera `typeof()` á breytu með null gildi, því það skilar `object` sem er í raun galli í ECMAScript og ætti að vera null. `undefined == null` skilar `true`, en `undefined === null` skilar false.

2. Hvað gerir 'use strict' í JavaScript kóða?

    "use strict" er segð sem ECMAScript 5 skilur, en ekki eldri útgáfur. Með "use strict" er þýðandinn strangari og leyfir ekki ákveðna hluti eins og að nota breytur sem hafa ekki verið skilgreindar. 

3. Hver er munurinn á let og var?

  `let` kom með ES2015.

    **Global:**
    They are very similar when used like this outside a function block
    ```javascript
      let me = 'go';  // globally scoped
      var i = 'able'; // globally scoped

    ```
    However, global variables defined with `let` will not be added as properties on the global windowobject like those defined with `var`.

    ```javascript
      console.log(window.me); // undefined
      console.log(window.i);  // 'able'

    ```
    **Function:**
    They are identical when used like this in a function block.
  ```javascript
      function f() {
        let a = 'local';    // function block scoped
        var b = 'me too!';  // function block scoped
      }

  ```
    **Block:**
  Here is the difference. let is only visible in the for() loop and var is visible to the whole function.  
  ```javascript
   function a() {
      // i is not visible out here
      for( let i = 0; i < 5; i++ ) {
          // i is only visible in here (and in the for() parentheses)
          // and there is a separate i variable for each iteration of the loop
      }
      // i is not visible out here 
    }

    function b() {
        // t is visible out here
        for( var t = 0; t < 5; t++ ) {
            // t is visible to the whole function
        }
        // t is visible out here
    }
    // t is not visible out here, because of function scope


  ```

4. Endurskrifaðu eftirfarandi kóða með for lykkjunni.

  ```javascript
    let x = 9;
    while (x >= 1) {
      console.log("hello " + x);
      x = x - 1;
}
    // Lausn
     for (let x = 9; x >= 1; x--){
           console.log("hello " + x);
    }

  ```

5. Skilgreindu sama fallið á þrjá mismunandi vegu.

  ```javascript
    function foo(a, b) {
      return a + b;
    }
    let bar = function(a, b) {
        return a + b;
    }
    let baz = (a, b) => a + b;

  ```

6. Útskýrðu hvað eftirfarandi kóði gerir, hvað gera svigarnir?
    ```javascript

        (function() { alert('Hello World'); })(); 

    ```
    Þetta er *Immediately-Invoked Function Expression (IIFE)*, fall sem keyrir strax og það er skilgreint í run-time. 
    Fyrsta (ysta) svigaparið tekur fallið saman í segð (e. expression) og síðasta parið (aftasta) keyrir fallið. `(function( ) ...)` býr til function scope utan um kóðann í slaufusvigum `{}`.

7. Af hverju birtist 1 en ekki 10?
Í hvaða röð er kóðinn keyrður í raun eftir að JS þýðandinn (e. interpreter) er búinn að fá hann til sín? Raðaðu kóðanum rétt fyrir JS þýðandann.

. 
  ```javascript
      "use strict";
      let a = 1;
      function b() {
        a = 10;
        return;
        function a() {}
      }
      b();
      console.log(a);

  ```
  Þetta er dæmi um hoisting. Þýðandinn dregur upp innra fallið (í þeirri röð sem það er skilgreint) og endar það fyrir ofan `return;`. Breytan a í fallinu b() er local.

  ```javascript
      let a;  // undefined
      a = 1; 

      function b() {
        // Hoisted to the top of enclosing function b()
        function a() {} 
          // Statement is changing the local a from function to an integer value of 10. 
          a = 10;       
          return;
      }
      b();
      // Since we are logging the global a, the output is 1.
      console.log(a) 
      // Had the statement function a() {} not been there, the output would have been 10.

  ```

8. Leystu lið 20 í lesson 6 í Arrays á Udacity https://classroom.udacity.com/courses/ud803 
  ```javascript
    let test = [12, 929, 11, 3, 199, 1000, 7, 1, 24, 37, 4,
        19, 300, 3775, 299, 36, 209, 148, 169, 299,
        6, 109, 20, 58, 139, 59, 3, 1, 139
    ];

    // Write your code here
    test.forEach(function (element) {
        if (element % 3 === 0)
        {
            test[test.indexOf(element)] += 100;
        }
    });

  ```

9. Leystu lið 22 í lesson 6 í Arrays á Udacity https://classroom.udacity.com/courses/ud803 
  
     Map býr til nýtt array með því að kalla á fall fyrir hvert element í array

  ```javascript
    let bills = [50.23, 19.12, 34.01,
      100.11, 12.15, 9.90, 29.11, 12.99,
      10.00, 99.22, 102.20, 100.10, 6.77, 2.22
    ];

    let totals = bills.map(i => Number((i * 1.15).toFixed(2)));
    console.log(totals);

  ```
10. Skrifaðu forrit í JavaScript sem sprengir staflan (stack overflow).

```javascript
    // Sýnidæmi 1
    function recurse(){
      recurse();
    }
    recurse();

    // Sýnidæmi 2
    function doSomething(){
      doSomethingElse();
    }

    function doSomethingElse(){
        doSomething();
    }

    doSomething();
```
The browser will end up stopping your code and (hopefully) display a message about the issue:

- Edge:
- Firefox:”Too much recursion”
- Chrome: n/a
- Opera: “Abort (control stack overflow)”
- Safari:”RangeError: Maximum call stack size exceeded.”

 
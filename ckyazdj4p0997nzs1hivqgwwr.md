# Bug in Codesandbox's VanillaJS Container

One of my fellow students at  [neoG camp](https://neog.camp/) faced an issue while trying out some code in the Vanilla Sandbox.

The code goes like this
```
const array = [1, 5, 3, 5, 6, 8];

const checkFun = (num1, num2) => {
  for (let i = 0; i < array.length; i++) {
    if (array[i] === num1) array[i] = num2;
  }
};

console.log("before", array); // should print "before [1, 5, 3, 5, 6, 8]", 
// but prints "before  [1, 10, 3, 10, 6, 8]"
checkFun(5, 10);
console.log("after", array); // prints "after [1, 10, 3, 10, 6, 8]"
```
The reason for this anomaly could be improper rendering of console logs

Inspecting further in the browser console, I found this
![Screenshot 2022-01-12 at 8.42.43 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641957207092/BKN4st1JZ.png)

The code was running as expected in the browser console, but not on codesandbox's console.
This is the link for above codesandbox => https://codesandbox.io/s/laughing-antonelli-06f4d?file=/src/index.js

In order to demostrate what could be happening inside I made a React app mimicing the faulty behaviour of codesandbox's console log.

You can find the code here => https://codesandbox.io/s/delicate-cookies-pm66u?file=/src/App.js

If you check, even in the browser console of the above app, the results were as expected.

Now, to conclude, I know that in the `checkFun` function, the original array is being mutated and hence the codesandbox's console is rendering the same array. But ideally, the codesandbox's console should be functionally similar to browser console, but it is failing to do that, and hence is faulty.
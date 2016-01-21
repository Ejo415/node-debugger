# Node Debugger

## Overview

This lesson teaches how to use the built-in Node CLI debugger.

## Objectives

1. Describe how to start Node debugger
1. Describe debugger and the commands

## Describe how to start Node debugger

Have you ever had a pesky bug that you couldn't track with simple print or log statements? Console.log (print statements in JavaScript/Node) are okay until they are not enough. Sometimes, it's painful not to be able to stop the execution process to look around the scope and investigate further. Node comes with a built-in debugger. All you need to do is to start the program in a debug mode:

```
$ node debug program.js
```

The prompt will turn into `debug>`. You can get the list of command with the `help` command.

## Describe debugger and the commands

The debugger commands won't be new to a person familiar with debugging in other languages like Ruby or browser JavaScript (with the help of DevTools). There are:

* run: run program
* cont (`c`): proceed with the execution
* next (s): next step
* step (s): step in
* out (o): step out
* backtrace (bt)
* setBreakpoint (sb): put the break point
* clearBreakpoint (cb): remove the break point

Other commands are: watch, unwatch, watchers, repl, restart, kill, list, scripts, breakOnException, breakpoints, version. We won't bore you and spend time covering all of them, just the bare minimum to give you the skills to start debugging.

Often times the bugs don't cause crashes. If you have a crash, you can examine the stack trace which contains the line numbers of the failed code. However, subtle bugs are harder to trace. They don't crash programs but the results are not what we expect. Consider this example of a program which generate head or tail similar to a coin flip, only there is a bug:

```js
var a = Math.floor(Math.random())
if (a>=0.5) {
  console.log('head')
} else {
  console.log('tail')
}
```

The bug is that we get tail every time. How can you debug it? Lauch the script in the debug mode with `$ node debug program.js`. You'd see this:

```
$ node debug program.js
< Debugger listening on port 5858
debug> . ok
break in program.js:1
> 1 var a = Math.floor(Math.random())
  2 if (a>=0.5) {
  3   console.log('head')
```

Type `n` and hit enter to proceed to the next statement:

```
debug> n
break in program.js:2
  1 var a = Math.floor(Math.random())
> 2 if (a>=0.5) {
  3   console.log('head')
  4 } else {
debug>
```

Now enter REPL with `repl` and check for value of `a`:

```
debug> repl
Press Ctrl + C to leave debug repl
> a
0
>
```  

The value is 0. You can restart the program with `restart`. Upon closer examination of the first line, we can detect that `Math.floor` will always round to the lowers integer which is 0 in this case. What we want to use in this program is `Math.round()`, not `Math.floor()`.

You can exit the debugger with `.exit`.

Note: You can also use REPL in debugger to change values. For example, we can manually change the value of `a` to 1 and the program will print `head`.


To put a breakpoint programmatically, simply write `debugger` in your code akin to the DevTools debugging:

```
var a = Math.floor(Math.random())
debugger
if (a>=0.5) {
  console.log('head')
} else {
  console.log('tail')
}
```

There are other ways to debug. The built-in debugger is the most low-level approach. The benefit is that it's available in any environment as long as you have Node.


## Resources

1. [Official Debugger Docs](https://nodejs.org/dist/latest-v5.x/docs/api/debugger.html)
1. [Quick demonstration of the node.js debugger](https://www.youtube.com/watch?v=V1vwGDVtAkM)
2. [Comparing Node.js Debug Options](http://spin.atomicobject.com/2015/09/25/debug-node-js)
3. [How to debug Node.js?](http://www.100percentjs.com/best-way-debug-node-js)
4. [Node.js Debugging with the Built-in Debugger](http://technosophos.com/2011/10/28/nodejs-debugging-built-debugger.html)

---

<a href='https://learn.co/lessons/node-debugger' data-visibility='hidden'>View this lesson on Learn.co</a>

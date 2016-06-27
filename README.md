# Brainfuck

> Brainfuck is an esoteric programming language created in 1993 by Urban Müller, and notable for its extreme minimalism.
> The language consists of only eight simple commands and an instruction pointer. While it is fully Turing-complete, it is not intended for practical use, but to challenge and amuse programmers. [source Wikipedia](https://en.wikipedia.org/wiki/Brainfuck)

For more information about the language itself go to the [article](https://en.wikipedia.org/wiki/Brainfuck).

This library let's you run any brainfuck programs.

## Basic usage

Create a brain fuck object and initialize it with the memory object of your choice. 

```javascript
var Brainfuck = require('./src/brainfuck.js'),
    BrainfuckMemoryInfinite = require('./src/memory/infinite.js');

brainfuck = new Brainfuck(new BrainfuckMemoryInfinite());
```

Each memory implementation has its own characteristics. Infinite memory for instance, can store infinite amount of cells, allows negative pointer and each cell can contain maximum possible value all within JS constraints. This is not a typical brainfuck implementation.

Let's set some brainfuck code:

```javascript
brainfuck.code.source('+++.[-].');
```

You will most probably need to set ``onInput`` and maybe ``onOutput`` handlers. They are called when ``,`` or ``.`` respectively in the brainfuck code are run. The library implements default ``onOutput`` behaviour which displays data as ASCI characters via standard console.

```javascript
brainfuck
    .onInput(function () { /* implementation */ })
    .onOutput(function (_output) { /* implementation */ });
```

Brainfuck code runs asynchronously after you call ```run``` method. It takes the callback function which is fired if the program reaches the end. Keep in mind that some brainfuck programs run forever. 

```javascript
brainfuck.run(function () { /* implementation */ });
```

You can check the status of the execution and abort it at any time.

```javascript
var state = brainfuck.isRunning();

brainfuck.stop();
```

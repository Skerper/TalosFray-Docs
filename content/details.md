---
weight: 15
title: Details
---

# Details

## CPU
### Specs
Cores|Threads|Clock     
-----|-------|-----
1    |1      |200hz

> Warning: This program will not function in battle. If you want to try it out, please do so in the emulator.

```haxe
var a = 5;
if(a > 3)
{ 
	log('hello, there!');
}
```

```javascript
EVar('a',null,EConst(CInt(5))), 							//3 ops
EIf(EBinop('>',EIdent('a'),EConst(CInt(3))), 				//4 ops
EBlock([												    //1 op
	ECall(EIdent('log'),[EConst(CString('hello, there!'))]) //3 ops
]),null)
```

> Switch between the 'Usage' and 'Bytecode' tabs to see how the program translates to machine code. Each keyword beginning with "E" represents one expression, taking one CPU clock cycle to execute. This program takes 11 clock cycles to run - 0.055 seconds at default clock speed. 

### Overview
Your bot's CPU is a single-threaded, single-core [CISC processor](https://en.wikipedia.org/wiki/Complex_instruction_set_computer). While it has a very slow clock speed, it is capable of achieving a lot with each instruction.

The CPU's machine code is [hscript](https://github.com/HaxeFoundation/hscript) bytecode, and hscript itself is a subset of the [Haxe](https://haxe.org/) programming language. Hscript can do many things Haxe can do, so it is a good stepping stone if you are interested in learning Haxe. 

In the Haxe language, [everything is an expression](https://code.haxe.org/category/principles/everything-is-an-expression.html). In your bot CPU, every expression is an operation, taking one clock cycle to execute.


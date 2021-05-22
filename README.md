# prepas
prePas is a Pascal to Pascal compiler. This compiler allows me to modify the pascal programming language as needed, while compiling to a Source that is valid ObjecPascal. Think of CoffeeScript for Pascal.

## Overview

prePas will take a modified pascal syntax, Lex and Parse it into valid ObjectPascal. If prePas completes the compile, it must compile by Pascal. It should not be possible/legal to have prePas output invalid code. (You can still write broken logic)
**If prePas compiler doesn't throw an error, fpc will compile**

### Language/Compiler Rules

- prePas is a Superset of ObjectPascal. If it is valid Pascal, it is valid prePas.
- If prePas succeeds, it will ocmpile in freepascal
- 

### Language Features & Examples

#### Basic hello world

Notice, this is a valid pascal program; this is the first requirement on prePas. If it is valid Pascal, it is valid prePas.

```pascal
program ppc;

uses System, Classes;

begin
  WriteLn('Hello World.');
end.

```

#### Conditionals

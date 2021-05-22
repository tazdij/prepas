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

One of my primary, esthetic objections to Pascal is the usage of begin and end (unlike other, I think the use of semi colons make perfect sense). I think it is easier when scanning, to see scoped blocks of code deliniated with Braces, instead of words. Now this does cause a little issue, that the brace is a comment. So, the parse needs to to be a little smart. I am not entirely sure, if I can pull this one off yet.

```
program ppc;

// These are directives
{$MODE OBJFPC}{$H+}

// Compiler constants
{$DEFINE MY_OVER override}

uses System, Classes;

begin

var a : Int32 = 0;

if (a <> 0) {
  WriteLn('We have a really big problem');
} else {
  WriteLn('Hello Sane World!');
};

end.
```

#### Enumerations

Pascal enums are super featureful, with automatic Bitmasking and "Set" operations. You can pretty much forget about having to manually shift bits, and use bitwise math, to match enums to values. This is all built into the language and syntax. But it lacks one of the most useful features that I can think of. It does not namespace Options/Values of and Enum to the definition, such as C# and I think recent versions on C++. While they are namespaced to the unit (which is a little better) It is often the case that another similar enum in the same unit, has already used the identifier that you need. (fpc does have a directive for scopedenums)

```
unit datelib;

type
  EDayOfWeek = enum
    Monday = 1;
    Tuesday = 2;
    Wednesday = 3;
    Thursday = 4;
    Friday = 5;
    Saturday = 6;
    Sunday = 0;
  end;
  
  EDayOfWeekOptions = enum
    Monday;
    Tuesday;
    Wednesday;
    Thursday;
    Friday;
    Saturday;
    Sunday;
  end;
  
function GetDayOfWeek() : EDayOfWeek;
begin
  // do some internal logic to determine day of week
  Result := EDayOfWeek.Monday;
end;
 
function SetDaysOpen(days : set of EDayOfWeekOptions) : Boolean;
begin
   
end;

// Call Example
// The type is infered by the functions declaration.
// As long as we don't overload a function with the set of both enum types, it will not be ambiguous. And, type solving will be possible.

SetDaysOpen([EDayOfWeekOptions.Monday, Tuesday, Wednesday, Thursday]);

end.
```

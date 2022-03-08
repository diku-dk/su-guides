# DIKU — Software Development — C# Coding Style

Coding style is a social construct: When joining a new software development
project, it is forced upon you. In return, when new peers join your project,
you can force it upon them. You must gather clout before you get to change
things. Keeping consistency in code layout makes it easier to collaborate with
other people, especially when the project stretches over thousands of lines of
code.

Let us now make a social contract: We aim to keep our code consistent in style
to make it easy for you to drop into new code handouts. In return, you stick to
our style in your extensions, to make it easy for us to drop in and give you
(more valuable) feedback.

We also try to give the reasons for our choices. If you disagree, you *can*
take it up with your TA, but your time is better spent _programming_.

This style guide has also been enforced using the [editorconfig project](https://editorconfig.org/)
in the file [.editorconfig](../files/.editorconfig).

## Using EditorConfig via the Terminal
Start off by placing the [.editorconfig](../files/.editorconfig) inside the project/solution folder. Then navigate inside the project/solution folder and run the following command.
```sh
$ dotnet format . -v diag --report .
```
The first dot specifies the path to the project/solution folder, the last dot specifies the path to where the report should be placed. When running this command the formatter will try to make the code follow the style guide specified in this document.

The report generated will tell the user all the problems with the code style that could not be automatically fixed. It is important to look this report through and fix the problems it found.

## Origins

This style guide makes a sacrifice between the style of the code found
in [C# precisely, 2nd ed., by Peter Sestoft and Henrik I.
Hansen](http://www.itu.dk/~sestoft/csharpprecisely/), and what you
might see in a large-scale C# development project. Here's why: The
style of the code in the textbook intends to conserve space, whereas,
in practice, software developers reach for a compromise between
utility and maintainability.

## Indentation

**4 spaces.**

Using spaces (rather than tabs) ensures to always retain the hierarchical
presentation of the code, as intended by the author, regardless of the reader's
system settings (e.g., tab width).

4 is not too many (e.g., 8), and not too little (e.g., 2). This is not a
reason, but a _compromise_.

## Line width

**100 characters.**

Code is like prose, and as with prose, shorter lines [make for a
faster
read](https://web.archive.org/web/20171025201838/http://www.humanfactors.com/newsletters/optimal_line_length.asp).
In short, you avoid forcing your readers to shift eye-focus along
multiple dimensions, and avoid the risk that they will have to scroll
left/right, in addition to up/down, to get an overview of your code.

You can add a vertical ruler in Visual Studio Code in the settings.json file found by opening the Command Palette (Ctrl+Shift+P or Cmd+Shift+P) then type "Open Settings (JSON)" and press enter. Then paste this in after the first opening curly bracket. 
```
"editor.rulers": [100],
```
You might have to reload VS Code, this is done by opening the Command Palette and finding "Reload Window".

## Braces

Opening braces are to be placed on the same line as the declaration
opening (K&R style). Closing braces are to be placed on a _line of
their own_, except when both the opening and closing brace fit on a
line, or when both the _closing and opening_ brace fit on a line, and
are part of the same statement.

Braces are _always_ required. Even around one-line blocks. This way, if you
ever want to add a line to what originally was a one-liner, you still retain the
control flow.

For instance,
```csharp
class MyClass : BaseClass {
    public string MyOtherProperty {
        get;
        private set;
    }

    // All rules have exceptions.
    public int MyProperty { get; }
    
    public void MyFunc(int a, int b) {
        for (int i = 0; i < 15; i++) {
            if (i < 5) {
              // ...
            } else if (i < 10) {
              // ...
            } else {
              // ...
            }
        }
    }
}
```

## Line breaks

In general, you should use line breaks to group code vertically. In
particular, you should, at least:

* Use a line break between using and namespace declarations.
* Use blank lines between class members.

## Spacing out

Use spaces to space out the syntactical elements along a line. In
particular, you should:

* Use a space before any opening parentheses that is used for a `for`-, `while-` or `if`- statement.
* Use a space before an opening curly brace.
* Use a space after each parameter in a parameter list.
* Have a space on each side of an infix operator.

For instance,
```csharp
(-b+Math.Sqrt(d))/(2*a)
```
is regarded as less readable than
```csharp
(-b + Math.Sqrt(d)) / (2 * a)
```

## Comments

Well-placed, well-named, and well-typed things need no comments:
Comment on your code only if there is no way to refactor it to make
its operation clearer. Here's why: Code doesn't lie, but comments
might.

If you have to comment, you can use either multi-line (`/* */`) or
single-line (`//`) comments. We recommend single-line comments for
everything.

For commenting out code, always use `//`. This is a great chance for you to get
acquainted with your text-editor.  Please also _consider removing commented out
code completely_, or add a comment as to why the code is commented out, if you
want someone else to sort it out.

Another useful option is to mark code with the following attribute:

```csharp
[System.Obsolete("This is obsolete. Use that instead.")]
```

Make sure that the comment you give as to what the user should use
instead is sensible.

When writing comments for something (e.g., a member method), describe
what it does, but refrain from commenting on how it is doing it — that
should be obvious from just reading the code.

## Naming

In general, we follow the naming conventions mentioned in C#
Precisely, Section 3, on page 4. In addition, constants and static
read-only fields are written in `SCREAMING_SNAKE_CASE`.

Private fields, local variables and method paramerters are named with `camelCase` and everything else is named using `PascalCase`.

Interfaces are named with an `I` in front followed by the interfaces name in `PascalCase`.

## Accessibility and Modifiability

It is the public and protected members of a class the determine its
responsibility. Hence, you should mark your members as `private`,
unless it is intensional that they are exposed as part of your
inheritance or public interface.

Also, mark fields as `const` or `readonly` when possible. When used on
static fields, let `readonly` come after `static` (i.e., `static
readonly`, not `readonly static`).

## Files

There should be one class per file. This is to keep source files small. An
exception is made for partial classes, where a part of the class is written by
an automated tool (e.g., a GUI designer). You will most likely not encounter or need partial classes in this course.

## Namespaces
There should be one namespace per file. This is done to keep source files small. To make sure this is done correctly the file scoped namespace is always used. The file scoped namespace is defined like so `namespace MyNamespace;` and has the added benefit of removing one unnecessary indent in your code. You should add this to the top of your code before packages such that you do not override existing packages.

Your namespaces should represent the file path you are in, so you might have a namespace insides your project folder called `MyNamespace`. If one were to add a folder inside the project folder called IO, then the namespace for all the code in that folder should be `MyNamespace.IO`. And if a folder is added inside the aforementioned IO folder called Console, then the name for all the code inside that folder should be `MyNamespace.IO.Console`.

## Minimize indentation when doing control flow

It was mentioned in the **Line width** section it is prefered to have short lines such that the code can be read faster. One way to make lines shorter is by considering the control flow in ones code. Let us start by considering a case with for loops, this is a code snippet from the method `ProcessEventsSequentially` in the GameEventBus class from DIKUArcade in the commit from 2021 Mar 26, 2021.
```csharp
foreach (GameEventType eventType in processOrder) {
    if (_eventQueues != null) {
        while (!_eventQueues[eventType].IsEmpty()) {
            var currentEvent = _eventQueues[eventType].Dequeue();
            if (currentEvent.To != default(IGameEventProcessor)) {
                currentEvent.To.ProcessEvent(currentEvent);
            }
            else if (_eventProcessors != null) {
                foreach (var eventProcessor in _eventProcessors[eventType]) {
                    eventProcessor.ProcessEvent(currentEvent);
                    if (_breakExecution) return;
                }
            }
        }
    }
}
```
One can start by considering the first if statement which reads "execute the code if `_eventQueues` is not null". One can get less indentation by considering the negation of this which is "skip the code if `_eventQueues` is null". This can be directly translated into code by using the `continue` keyword, this will result in the following code which will have one less indent.

```csharp
foreach (GameEventType eventType in processOrder) {
    if (_eventQueues == null) {
        continue;
    }

    while (!_eventQueues[eventType].IsEmpty()) {
        var currentEvent = _eventQueues[eventType].Dequeue();
        if (currentEvent.To != default(IGameEventProcessor)) {
            currentEvent.To.ProcessEvent(currentEvent);
        }
        else if (_eventProcessors != null) {
            foreach (var eventProcessor in _eventProcessors[eventType]) {
                eventProcessor.ProcessEvent(currentEvent);
                if (_breakExecution) return;
            }
        }
    }
}
```
Note the same can again be done for the else if statement.

The same idea can be applied to methods when returning. One can take a look at the example below.
```csharp
public void IsInInterval(int val, int min, int max) {
    if (min <= max) {
        if (min <= val && val <= max) {
            Console.WriteLine($"{val} is in [{min}; {max}].");
        } else {
            Console.WriteLine($"{val} is not in [{min}; {max}].");
        }
    } else {
        Console.WriteLine("Max must be greater or equal to min.");
    }
}
```
And now considering the negation of the first predicate you get.
```csharp
public void IsInInterval(int val, int min, int max) {
    if (min > max) {
        Console.WriteLine("Max must be greater or equal to min.");
        return;
    } else if (min <= val && val <= max) {
        Console.WriteLine($"{val} is in [{min}; {max}].");
        return;
    }

    Console.WriteLine($"{val} is not in [{min}; {max}].");
}
```

# Example C# Formatting

This is an example of how we would like your C# code to be formatted. 

```csharp
namespace MyNamespace;

using System;

public class MyClass<MyType> : IMyInterface {
    public int MyProperty { get; private set; }
    
    protected int myValue;
    
    public MyClass(int myValue) {
        this.myValue = myValue;
    }
    
    public override string ToString() {
        return $"myValue: {myValue}";
    }
    
    public void MyInterfaceMethod(int arg1, int arg2) {
        if (myValue < arg1) {
            myValue += arg2;
        } else {
            myValue -= arg1;
        }
    }
}
```

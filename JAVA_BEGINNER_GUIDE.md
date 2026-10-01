# Java Beginner Guide

A practical introduction to the core ideas behind Java programs. Each topic includes an explanation and a small example. The exercises at the end are prompts only; there is no answer key in this guide.

## Contents

1. [A first Java program](#1-a-first-java-program)
2. [Variables and data types](#2-variables-and-data-types)
3. [Operators and expressions](#3-operators-and-expressions)
4. [Making decisions](#4-making-decisions)
5. [Loops](#5-loops)
6. [Methods](#6-methods)
7. [Arrays and lists](#7-arrays-and-lists)
8. [Classes and objects](#8-classes-and-objects)
9. [Errors, input, and good habits](#9-errors-input-and-good-habits)
10. [Exercises](#10-exercises)

## 1. A first Java program

Java is a programming language used for applications ranging from desktop software to web services and Android apps. Java source code is written in `.java` files, compiled, and run by the Java Virtual Machine (JVM).

Here is a small complete program:

```java
public class Greeting {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

The source file should be named `Greeting.java`, matching the public class name. Java is case-sensitive: `Greeting`, `greeting`, and `GREETING` are different names.

- `public class Greeting` declares a class. A class is a named structure that can contain data and behavior.
- The braces `{ }` mark the beginning and end of a class or method body.
- `main` is the entry point Java looks for when starting this kind of application.
- `System.out.println(...)` prints a value and then starts a new line. `System.out.print(...)` prints without starting a new line.
- A semicolon `;` ends most Java statements.

Comments are notes for people reading the source; Java does not execute them.

```java
// A single-line comment

/* A comment can also
   continue across lines. */
```

Whitespace and indentation usually do not change what Java means, but consistent indentation makes blocks easier to understand. Indent the statements inside each pair of braces.

## 2. Variables and data types

A variable is a named place to store a value. Every variable has a type, which determines what kind of value it can hold and what operations make sense for it. Declare a variable by writing its type and name; you may also assign an initial value.

```java
int age = 19;
double heightInMeters = 1.72;
boolean isLearning = true;
char initial = 'A';
String name = "Mina";

age = 20; // The value can be reassigned.
```

The equals sign in a declaration assigns the value on its right to the variable on its left. A variable can be declared first and assigned later, but it must have a value before it is used.

### Common types

| Type | What it stores | Example |
| --- | --- | --- |
| `int` | Whole numbers | `int score = 42;` |
| `long` | Larger whole numbers | `long population = 8_000_000_000L;` |
| `double` | Decimal numbers | `double price = 3.50;` |
| `float` | Decimal numbers with less precision | `float ratio = 0.5f;` |
| `boolean` | `true` or `false` | `boolean finished = false;` |
| `char` | One character | `char grade = 'B';` |
| `String` | Text (a reference type) | `String city = "Lima";` |

The first six types in this table, except `String`, are primitive types. `String` is a class provided by Java. Text uses double quotes; a single `char` uses single quotes. For example, `"Q"` is a string and `'Q'` is a character.

Use `final` for a variable whose value should not be reassigned:

```java
final int DAYS_IN_WEEK = 7;
```

By convention, variable and method names use `lowerCamelCase`, such as `totalPrice`. Class names use `UpperCamelCase`, such as `ShoppingCart`. Names should describe what the value represents.

### Converting between types

Some conversions are automatic when no information is lost, such as assigning an `int` to a `double`. Other conversions need an explicit cast and may lose information.

```java
int wholeNumber = 7;
double approximate = wholeNumber; // 7.0

double measurement = 9.8;
int truncated = (int) measurement; // 9; the decimal part is discarded
```

When combining values of different types, be aware of the result type. For example, dividing two integers produces an integer result, so `7 / 2` is `3`, not `3.5`. If a decimal result is needed, make at least one operand a `double`, as in `7.0 / 2`.

## 3. Operators and expressions

An operator performs an action on one or more values. An expression combines values and operators to produce another value.

### Arithmetic

| Operator | Meaning | Example |
| --- | --- | --- |
| `+` | Addition, or string concatenation | `3 + 4`, `"Hi " + name` |
| `-` | Subtraction | `10 - 6` |
| `*` | Multiplication | `5 * 3` |
| `/` | Division | `9.0 / 2` |
| `%` | Remainder after division | `10 % 3` |

Parentheses make the intended order clear. In `2 + 3 * 4`, multiplication happens first; in `(2 + 3) * 4`, the addition happens first. The remainder operator is useful for questions such as whether a number is even: an even integer has a remainder of zero when divided by two.

The `+` operator joins strings when at least one operand is a string:

```java
String message = "Score: " + 12;
System.out.println(message);
```

### Comparisons and logic

Comparison operators produce a `boolean`:

- `==` means equal to; `!=` means not equal to.
- `<` and `>` mean less than and greater than.
- `<=` and `>=` include equality.

Logical operators combine or reverse boolean values:

- `&&` is true only when both conditions are true.
- `||` is true when at least one condition is true.
- `!` reverses a boolean value.

```java
int temperature = 22;
boolean comfortable = temperature >= 18 && temperature <= 26;
```

For objects such as `String`, `==` compares whether two references point to the same object, not whether their text is equal. Use `.equals(...)` to compare string contents:

```java
String answer = "yes";
boolean agreed = answer.equals("yes");
```

### Updating a variable

These forms update a numeric variable:

```java
int count = 0;
count = count + 1;
count += 2;
count++;
```

They are all ways to increase `count`; `+=` works with other arithmetic operators too. Prefer the clearest form for the situation.

## 4. Making decisions

An `if` statement runs code only when a condition is true. Add `else if` for another condition, and `else` for the remaining case.

```java
int score = 84;

if (score >= 90) {
    System.out.println("Excellent");
} else if (score >= 60) {
    System.out.println("Passed");
} else {
    System.out.println("Try again");
}
```

Conditions must evaluate to `boolean`. Braces are recommended even when a branch contains only one statement; they make the block boundaries clear and prevent mistakes when the code changes.

Use `switch` when one value is being compared with several specific alternatives:

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Another day");
}
```

In this traditional `switch` form, `break` prevents execution from continuing into the next case. `default` handles values that did not match a listed case. Java also has a newer arrow-style `switch`, but the traditional form is useful to recognize in existing code.

## 5. Loops

Loops repeat code. Choose a loop based on whether you know the number of repetitions and whether the body should run before checking the condition.

### `while`

A `while` loop checks its condition before every repetition. It may run zero times if the condition starts false.

```java
int countdown = 3;

while (countdown > 0) {
    System.out.println(countdown);
    countdown--;
}
```

Make sure something in the loop can eventually make its condition false. Otherwise, the program may get stuck in an infinite loop.

### `do-while`

A `do-while` loop checks its condition after running the body, so it always runs at least once.

```java
int attempts = 0;

do {
    attempts++;
} while (attempts < 1);
```

### `for`

A `for` loop is convenient when counting. Its header contains an initial value, a condition, and an update, separated by semicolons.

```java
for (int number = 1; number <= 5; number++) {
    System.out.println(number);
}
```

The counter begins at `1`, the loop continues while the condition is true, and `number++` runs after each pass. The counter declared in the header is only available inside that loop.

### Enhanced `for`

Use an enhanced `for` loop to visit every item in an array or collection when you do not need its index.

```java
String[] colors = {"red", "green", "blue"};

for (String color : colors) {
    System.out.println(color);
}
```

`break` exits the nearest loop. `continue` skips the rest of the current pass and moves on to the next one. Use them sparingly: a loop with a clear condition is often easier to follow.

## 6. Methods

A method is a named block of code that can be called when needed. Methods help split a program into understandable, reusable pieces. A method can receive inputs called parameters and can return a result.

```java
public class Calculator {
    public static int add(int first, int second) {
        return first + second;
    }

    public static void main(String[] args) {
        int total = add(4, 6);
        System.out.println(total);
    }
}
```

In `public static int add(int first, int second)`, `int` before the method name is the return type, and the values inside the parentheses are parameters. The call `add(4, 6)` supplies arguments. `return` sends the result back to the caller.

Use `void` when a method does not return a value. A `return` statement in a non-`void` method must provide a value of the declared return type. A method can also validate its inputs or perform an action such as printing.

Methods declared `static` belong to the class and can be called from `main` without creating an object. Methods that describe the behavior of a particular object are usually instance methods; those appear in the next section.

Keep methods focused. A method with a name such as `calculateAverage` should perform one clear task. Helpful method names let a reader understand a program without tracing every statement.

## 7. Arrays and lists

An array stores a fixed number of values of the same type. Each item has an index, starting at zero.

```java
int[] scores = {88, 92, 75};
System.out.println(scores[0]); // First item
System.out.println(scores.length); // Number of items
```

For an array of length three, valid indexes are `0`, `1`, and `2`. Trying to access an index outside the valid range causes an `ArrayIndexOutOfBoundsException` at runtime. Arrays have a fixed length after creation, though their elements can be updated.

```java
scores[1] = 95;

for (int index = 0; index < scores.length; index++) {
    System.out.println(scores[index]);
}
```

For a resizable sequence, use `ArrayList` from the Java collections library. Because `ArrayList` stores objects rather than primitive values directly, use wrapper types such as `Integer` in place of `int`.

```java
import java.util.ArrayList;

ArrayList<String> tasks = new ArrayList<>();
tasks.add("Read");
tasks.add("Practice");
System.out.println(tasks.get(0));
System.out.println(tasks.size());
tasks.remove("Read");
```

Use `.add(...)` to add an item, `.get(index)` to read one, `.set(index, value)` to replace one, `.remove(...)` to remove one, and `.size()` to find the current number of items. Collection indexes also start at zero. The `import` statement makes the `ArrayList` type available by its short name.

Choose an array when the number of items is fixed and an `ArrayList` when the sequence needs to grow or shrink. Both are useful; neither is automatically the right choice for every task.

## 8. Classes and objects

A class defines the structure and behavior of a kind of object. An object is one instance of that class. For example, a `Book` class describes what book objects contain; each actual book is a separate object with its own values.

```java
public class Book {
    private String title;
    private int pageCount;

    public Book(String title, int pageCount) {
        this.title = title;
        this.pageCount = pageCount;
    }

    public String getTitle() {
        return title;
    }

    public void describe() {
        System.out.println(title + " has " + pageCount + " pages.");
    }
}
```

The variables declared in the class are fields. Each `Book` object has its own `title` and `pageCount`. The constructor, named after the class, runs when a new object is created and initializes its fields. `this.title` means the field belonging to the current object; it distinguishes the field from the constructor parameter also named `title`.

Create and use an object like this, for example in another class's `main` method:

```java
Book libraryBook = new Book("Small Worlds", 240);
System.out.println(libraryBook.getTitle());
libraryBook.describe();
```

The `new` keyword creates the object and calls its constructor. The variable `libraryBook` refers to that object. The dot operator calls one of the object's accessible methods.

### Encapsulation and access

Encapsulation means keeping an object's internal data under its control and exposing a clear public interface. Fields are often marked `private`, so other classes cannot change them directly. Public methods provide the operations other code is allowed to use.

Java uses access modifiers to control visibility:

- `public`: accessible from other classes.
- `private`: accessible only inside the declaring class.
- `protected` and package-private (no modifier): additional options used as programs grow.

A getter returns a field's value. A setter may update it, but should check rules that keep the object valid. Not every field needs a setter: restricting changes can make behavior more predictable.

Classes, methods, and objects work together: classes define a useful concept, fields hold an object's state, constructors establish that state, and methods provide behavior. For tiny one-file examples, static methods are convenient; larger programs commonly divide responsibilities among objects.

## 9. Errors, input, and good habits

Errors usually fall into a few broad groups:

- **Compile-time errors**: the compiler cannot understand or type-check the code, such as a misspelled variable name, missing semicolon, or incompatible types.
- **Runtime errors**: the program compiles but encounters a problem while running, such as dividing an integer by zero or using an invalid array index.
- **Logic errors**: the program runs but produces the wrong result because the instructions do not match the intended behavior.

Read compiler messages from the first error onward; later errors may be consequences of the first one. When a program behaves unexpectedly, inspect the values involved and follow the control flow one step at a time. Printing a variable temporarily can help reveal what the program is doing.

### Reading console input

The `Scanner` class can read simple input typed in the console. This example shows how it is connected; try it in a complete class with a `main` method.

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
System.out.print("What is your name? ");
String name = scanner.nextLine();
System.out.println("Hello, " + name);
scanner.close();
```

`nextLine()` reads a line of text. `nextInt()` reads an integer, and `nextDouble()` reads a decimal number. Mixing token-reading methods such as `nextInt()` with `nextLine()` can be surprising because the line break after a number may still be waiting to be read. For a first project, reading complete lines and converting them deliberately can make input behavior easier to reason about.

### Practical habits

- Use descriptive names and consistent indentation.
- Keep each method focused and avoid duplicating the same block of logic.
- Check boundary cases: empty input, zero, negative values, and the first or last array index.
- Test small pieces as you build them instead of writing the whole program before the first run.
- Separate a program's input, calculations, and output when that makes the code easier to change.
- Do not assume a program is correct just because it compiles; verify the behavior with test values.

## 10. Exercises

These exercises are for you to solve. The guide does not include their solutions. Start with a new class for each exercise, and run your code as you go.

### Warm-up

1. Write a program that prints your name, a hobby, and one goal on separate lines.
2. Declare variables for a product name, its price, and how many are in stock. Print a sentence containing all three values.
3. Given a number of minutes, calculate and print the equivalent number of whole hours and remaining minutes.
4. Given an integer, print whether it is even or odd.

### Decisions and repetition

5. Ask for a test score and print a result category of your choice. Decide and document the score boundaries.
6. Print the integers from 1 through 100, but print a special word instead of numbers divisible by three, another word for numbers divisible by five, and a combined word for numbers divisible by both.
7. Given a positive integer, calculate the sum of all integers from 1 up to that number.
8. Keep asking the user to enter a number until they enter zero. At the end, report how many nonzero numbers they entered and their total.

### Methods and collections

9. Write a method that accepts a temperature in Celsius and returns the equivalent temperature in Fahrenheit. Call it with several values and print the results.
10. Store five numbers in an array. Find and print the smallest and largest values without using a sorting library.
11. Create an `ArrayList<String>` of tasks. Let the user add tasks, list them, and remove a task by its position.
12. Write a method that accepts an integer array and returns its average. Decide how your method should behave for an empty array.

### Classes and a small project

13. Create a `BankAccount` class with a private balance, a constructor, a method to deposit money, and a method to withdraw money. Decide what should happen when a deposit or withdrawal is invalid.
14. Create a `Student` class with a name and a collection of test scores. Add methods to record a score and calculate the average.
15. Build a console-based number guessing game. Choose a secret number, ask for guesses, tell the player whether each guess is too high or too low, and count attempts. Add input validation as a stretch goal.

For each exercise, try at least three test cases, including an edge case where appropriate. When something fails, record the input, expected behavior, and actual behavior before changing the code; that makes debugging much more systematic.
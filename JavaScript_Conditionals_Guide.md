# JavaScript Conditionals — Student Guide

*AP CSP: Programming in JavaScript*

Conditionals let your program **make decisions**. Instead of running the same code every time, your program can check something and choose a different path depending on what's true. This is one of the core building blocks of programming — right up there with variables and functions.

---

## 1. The Basic `if` Statement

An `if` statement runs a block of code **only if** a condition is `true`.

```js
const age = 17;

if (age >= 18) {
  console.log("They are an adult");
}
```

**How to read it:** "IF `age` is greater than or equal to 18, THEN print 'They are an adult'."

If the condition is `false`, the code inside the `{ }` is simply skipped.

---

## 2. `if...else` — Two Paths

What if you want something to happen when the condition is **false** too? That's where `else` comes in.

```js
const age = 17;

if (age >= 18) {
  console.log("They are an adult");
} else {
  console.log("They are a child");
}
```

Since `age` is 17, the condition `age >= 18` is `false`, so the program runs the `else` block and prints `"They are a child"`.

Think of it like a fork in the road — the program *must* take one path or the other, never both.

---

## 3. `if...else if...else` — Multiple Paths

Sometimes two options aren't enough. `else if` lets you check several conditions in order.

```js
const age = 17;

if (age >= 65) {
  console.log("Senior Citizen");
} else if (age <= 18) {
  console.log("They is child");
} else {
  console.log("they re an adult");
}
```

**Important:** JavaScript checks these top to bottom and stops at the **first** condition that's true.
- Is `age >= 65`? No (17 is not ≥ 65) → move on
- Is `age <= 18`? Yes (17 ≤ 18) → run this block, print `"They is child"`, and **skip the rest**

You can chain as many `else if` blocks as you need, but only **one** block ever runs.

---

## 4. Comparison Operators (What Goes Inside the `()`)

| Operator | Meaning | Example |
|---|---|---|
| `===` | equal to (strict) | `age === 18` |
| `!==` | not equal to | `age !== 18` |
| `>` | greater than | `age > 18` |
| `<` | less than | `age < 18` |
| `>=` | greater than or equal to | `age >= 18` |
| `<=` | less than or equal to | `age <= 18` |

> **Tip:** Always use `===` and `!==` (not `==` or `!=`) in JavaScript. The triple-equals checks both value *and* type, which avoids weird bugs.

---

## 5. Complex Conditionals — Combining Conditions

Real-world decisions often depend on **more than one thing**. Logical operators let you combine conditions.

| Operator | Name | Meaning |
|---|---|---|
| `&&` | AND | Both sides must be true |
| `\|\|` | OR | At least one side must be true |
| `!` | NOT | Flips true to false (and vice versa) |

### Example: AND (`&&`)

```js
let age = 35;
let citizen = true;

if (age >= 35 && citizen === true) {
  console.log("Can run for President");
} else {
  console.log("cannot run");
}
```

Both conditions must be true at the same time: you need to be **at least 35** *and* a **citizen**. If either one is false, the whole thing is false.

### Example: OR and NOT together

```js
let hasKey = true;
let hasMagic = false;
let isBanned = false;

function enter(hasKey, hasMagic, isBanned) {
  if ((hasKey || hasMagic) && !isBanned) {
    console.log("can enter");
  } else {
    console.log("cannot enter");
  }
}

enter(hasKey, hasMagic, isBanned);
```

Break this down piece by piece:
1. `(hasKey || hasMagic)` → true if you have **either** a key **or** magic (or both)
2. `!isBanned` → true only if `isBanned` is **false** (the `!` flips it)
3. The whole condition needs **both** of those pieces to be true

This shows how conditionals and functions work together — the function takes in different values as **parameters** each time it's called, so `enter()` can give a different answer depending on what's passed in.

### Truth Table Reference

| `A` | `B` | `A && B` | `A \|\| B` |
|---|---|---|---|
| true | true | true | true |
| true | false | false | true |
| false | true | false | true |
| false | false | false | false |

---

## 6. The `switch` Statement — A Cleaner Way to Handle Many Cases

When you're checking the **same variable** against many possible values, a long `if/else if` chain gets messy. A `switch` statement is often cleaner.

```js
const key = 3;

switch (key) {
  case 1: // if value is 1
    console.log("monday");
    break;
  case 2:
    console.log("tuesday");
    break;
  case 3:
    console.log("Weds");
    break;
  case 4:
    console.log("tthurs");
    break;
  default:
    // the else essentially
    console.log("time is wierd");
}
```

**How it works:**
- JavaScript compares `key` against each `case` value, top to bottom.
- When it finds a match (`case 3`), it runs that block — printing `"Weds"`.
- `break;` tells JavaScript to **stop** and exit the switch. Without it, the code would "fall through" and keep running the *next* case too!
- `default` is like the `else` in an if/else chain — it runs if **none** of the cases match.

> **Common bug:** Forgetting `break;`. Try removing the `break;` after `case 2` and see what happens — you'll get both `"tuesday"` *and* `"Weds"` printed. This is called **fall-through**.

### `if/else` vs. `switch` — When to Use Which

| Use `if / else if` when... | Use `switch` when... |
|---|---|
| You're checking ranges (`age >= 18`) | You're checking one variable against many exact values |
| You're combining conditions with `&&` / `\|\|` | The values are simple (numbers, strings) |
| You only have 2–3 branches | You have many branches (4+) and want readability |

---

## 7. Quick Reference: Anatomy of a Conditional

```js
if (condition) {
  // runs if condition is true
} else if (anotherCondition) {
  // runs if the first condition was false, AND this one is true
} else {
  // runs if none of the above were true
}
```

- The `( )` holds a condition that evaluates to `true` or `false` (a **Boolean**).
- The `{ }` holds the code that runs when that condition is met.
- Only **one** block in an if/else-if/else chain ever runs.

---

## 8. Try It Yourself

Using the ideas above, try writing these on your own:

1. Write an `if/else` that checks if a number is even or odd (hint: use the `%` operator — `num % 2 === 0`).
2. Write a function `canRide(height)` that prints `"You can ride!"` if height is 48 inches or more, and `"Sorry, too short"` otherwise.
3. Write a `switch` statement that takes a `season` variable (`"winter"`, `"spring"`, `"summer"`, `"fall"`) and prints a typical activity for each season.
4. Combine `&&` and `||`: write a condition for a movie ticket discount that applies if the person is a `student` **or** a `senior`, **and** it's a `weekday`.

---

## 9. Key Vocabulary

| Term | Meaning |
|---|---|
| **condition** | An expression that evaluates to `true` or `false` |
| **Boolean** | A data type with only two values: `true` or `false` |
| **branch** | One possible path of code the program can take |
| **fall-through** | When a `switch` case keeps running into the next case because `break` was missing |
| **logical operator** | `&&`, `\|\|`, `!` — used to combine or invert conditions |
| **comparison operator** | `===`, `!==`, `>`, `<`, `>=`, `<=` — used to compare values |

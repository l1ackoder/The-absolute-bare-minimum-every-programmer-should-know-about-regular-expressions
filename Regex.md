-- Hey Mike. If you find this repo and dont want this to be online. please let me know. I will take this down. I found this blog on web archive. so kind of a backup for my own -- 

---

# WTF is a Regular Expression?

Regular expressions are strings formatted using a special pattern notation that allow you to describe and parse text. Many programmers (even some good ones) disregard regular expressions as line noise, and it’s a damned shame because they come in handy so often. Once you’ve gotten the hang of them, regular expressions can be used to solve countless real world problems.

Regular expressions work a lot like the filename “globs” in Windows or \*nix that allow you to specify a number of files by using the special `*` or `?` characters. But with regular expressions, the special characters (or **metacharacters**) are far more expressive.

Like globs, regular expressions treat most characters as literal text. The regular expression `mike`, for example, will only match the letters **m - i - k - e**, in that order. But regular expressions sport an extensive set of metacharacters that make the simple glob look downright primitive.

---

## Meet the Metacharacters

```
^ [] () {} . * ? \ | + $ and sometimes -
```

I know, they look intimidating, but they’re really nice characters once you get to know them.

---

## The Line Anchors: `^` and `$`

The `^` (caret) and `$` (dollar) metacharacters represent the **start** and **end** of a line of text, respectively.

* `mike` will match anywhere in a line (`I'm mike`, `carmike`, etc.).
* `^mike` matches only if the line starts with "mike".
* `mike$` matches only if the line ends with "mike".
* `^mike$` matches lines that **only** contain "mike".
* `^$` matches **empty lines**.

---

## The Character Class: `[]`

Square brackets define a **character class** and let you match **any one of several characters**.

* `gr[ae]y` matches both `gray` and `grey`.

To **negate** a class (match anything except listed characters):

* `[^aeiou]` matches any character **except** vowels.

> Note: `^` has a **different meaning** inside vs. outside a character class.

---

## The Character Class Metacharacter: `-`

Within a character class, `-` indicates a **range**:

* `[0-9a-fA-F]` matches a single hex digit.

If `-` is the **first or last character**, it is treated literally:

* `[-0-9]` includes the dash and digits.

Other characters like `.` or `?` **lose their special meaning** inside a character class.

---

## Matching Any Character: `.`

The dot (`.`) matches **any single character** (except newline in some flavors).

* `c.t` would match `cat`, `cut`, `c9t`, etc.

> Inside a character class like `[.]`, it just means a literal dot.

---

## Alternation: `|`

The pipe (`|`) means **OR**.

* `Mike|Michael` matches either `Mike` or `Michael`.
* `Mi(ke|chael)` does the same but groups the alternatives.

> Parentheses group subexpressions and improve readability.

---

## Optional Items: `?`

The question mark (`?`) makes the preceding character **optional** (0 or 1 times).

* `flavou?r` matches both `flavor` and `flavour`.

---

## Other Quantifiers: `+` and `*`

These define how many times a character can repeat:

* `+` — one or more
* `*` — zero or more

Example:

* `go+al` matches `goal`, `goooal`, but **not** `gal`.

> These are called **quantifiers**.

---

## Interval Quantifier: `{}`

You can set **min/max repetitions** with curly braces:

* `go{1,5}al` matches `goal`, `goooal`, up to 5 `o`s.
* `{0,1}` is the same as `?`.

---

## Escape Character: `\`

The backslash (`\`) **escapes** metacharacters to treat them literally:

* To match `?` or `\`, use `\?` or `\\`.

In some flavors (like PCRE), backslash before letters has special meaning (e.g., `\d`, `\w`, etc.).

---

## Using Parentheses: `()`

Parentheses can **capture** submatches for reuse or extraction.

Example:

```regex
http://([^/]+)
```

Breakdown:

* Matches `"http://"`
* `([^/]+)` captures everything after `http://` **until the next `/`**

In `http://immike.net/blog/Some-blog-post`, the captured part would be: `immike.net`.

---



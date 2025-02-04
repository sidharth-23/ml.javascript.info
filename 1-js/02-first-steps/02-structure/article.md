# Code ന്റെ രൂപം

നമ്മൾ ആദ്യം പഠിക്കാൻ പോകുന്നത് കോഡിങിന്റെ അടിസ്ഥാനപരമായ ചില കാര്യങ്ങളാണ്.

## Statements

Statements are syntax constructs and commands that perform actions.

 "Hello, world!" message കാണിക്കുന്ന statement ആയ `alert('Hello, world!')` നമ്മൾ ഇതിനു മുൻപ് തന്നെ ഒരു കണ്ടിട്ടുണ്ടായിരുന്നു.

നമുക്ക് ആവശ്യമുള്ള എത്ര statements വേണമെങ്കിലും കോഡിൽ നമുക്ക് ചെയ്യാം. Semicolon ഉപയോഗിച്ചാണ് നമ്മൾ ഓരോ statement ഉം വേർതിരിക്കുന്നത്.

ഉദാഹരണത്തിന്, ഇവിടെ നമ്മൾ "Hello World" രണ്ട് alertകളായിട്ടു തിരിക്കുന്നു:

```js run no-beautify
alert('Hello'); alert('World');
```

സാധാരണയായി, statementകൾ വായിക്കാൻ എളുപ്പത്തിനായി പല പല വരികളിലായിട്ടാണ് എഴുതുന്നത്:

```js run no-beautify
alert('Hello');
alert('World');
```

## Semicolons [#semicolon]

ഒരു line break വന്നാൽ പിന്നെ അവിടെ നമുക്ക്‌ semicolon ഒഴിവാക്കാവുന്നതാണ്.
ഇതും work ആകും:

```js run no-beautify
alert('Hello')
alert('World')
```

ഇവിടെ, ഒരു പുതിയ ലൈനിനെ JavaScript തനിയെ ഒരു semicolon ആയിട്ടു കണക്കാക്കും. ഇതിനെ [automatic semicolon insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion) എന്നു വിളിക്കുന്നു.

**മിക്കപ്പോഴും, ഒരു newline ,ഒരു semicolon നു തുല്യമായിരിക്കും. പക്ഷെ "മിക്കപ്പോഴും" എന്നു പറഞ്ഞാൽ "എപ്പോഴും" അല്ല!**
ചില സന്ദർഭങ്ങളിൽ ഒരു newline, ഒരു semicolon നു പകരമാവില്ല.ഉദാഹരണത്തിന്:
```js run no-beautify
alert(3 +
1
+ 2);
```

The code outputs `6` because JavaScript does not insert semicolons here. It is intuitively obvious that if the line ends with a plus `"+"`, then it is an "incomplete expression", so a semicolon there would be incorrect. And in this case, that works as intended.

**But there are situations where JavaScript "fails" to assume a semicolon where it is really needed.**

Errors which occur in such cases are quite hard to find and fix.

````smart header="An example of an error"
If you're curious to see a concrete example of such an error, check this code out:

```js run
alert("Hello");

[1, 2].forEach(alert);
```

No need to think about the meaning of the brackets `[]` and `forEach` yet. We'll study them later. For now, just remember the result of running the code: it shows `Hello`, then `1`, then `2`.

Now let's remove the semicolon after the `alert`:

```js run no-beautify
alert("Hello")

[1, 2].forEach(alert);
```

The difference compared to the code above is only one character: the semicolon at the end of the first line is gone.

If we run this code, only the first `Hello` shows (and there's an error, you may need to open the console to see it). There are no numbers any more.

That's because JavaScript does not assume a semicolon before square brackets `[...]`. So, the code in the last example is treated as a single statement.

Here's how the engine sees it:

```js run no-beautify
alert("Hello")[1, 2].forEach(alert);
```

Looks weird, right? Such merging in this case is just wrong. We need to put a semicolon after `alert` for the code to work correctly.

This can happen in other situations also.
````

We recommend putting semicolons between statements even if they are separated by newlines. This rule is widely adopted by the community. Let's note once again -- *it is possible* to leave out semicolons most of the time. But it's safer -- especially for a beginner -- to use them.

## Comments [#code-comments]

As time goes on, programs become more and more complex. It becomes necessary to add *comments* which describe what the code does and why.

Comments can be put into any place of a script. They don't affect its execution because the engine simply ignores them.

**One-line comments start with two forward slash characters `//`.**

The rest of the line is a comment. It may occupy a full line of its own or follow a statement.

Like here:
```js run
// This comment occupies a line of its own
alert('Hello');

alert('World'); // This comment follows the statement
```

**Multiline comments start with a forward slash and an asterisk <code>/&#42;</code> and end with an asterisk and a forward slash <code>&#42;/</code>.**

Like this:

```js run
/* An example with two messages.
This is a multiline comment.
*/
alert('Hello');
alert('World');
```

The content of comments is ignored, so if we put code inside <code>/&#42; ... &#42;/</code>, it won't execute.

Sometimes it can be handy to temporarily disable a part of code:

```js run
/* Commenting out the code
alert('Hello');
*/
alert('World');
```

```smart header="Use hotkeys!"
In most editors, a line of code can be commented out by pressing the `key:Ctrl+/` hotkey for a single-line comment and something like `key:Ctrl+Shift+/` -- for multiline comments (select a piece of code and press the hotkey). For Mac, try `key:Cmd` instead of `key:Ctrl` and `key:Option` instead of `key:Shift`.
```

````warn header="Nested comments are not supported!"
There may not be `/*...*/` inside another `/*...*/`.

Such code will die with an error:

```js run no-beautify
/*
  /* nested comment ?!? */
*/
alert( 'World' );
```
````

Please, don't hesitate to comment your code.

Comments increase the overall code footprint, but that's not a problem at all. There are many tools which minify code before publishing to a production server. They remove comments, so they don't appear in the working scripts. Therefore, comments do not have negative effects on production at all.

Later in the tutorial there will be a chapter <info:code-quality> that also explains how to write better comments.

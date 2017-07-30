# Writing a "Hello, World!" program in JS using only `!()*+,-/[]{}`

JavaScript has some strange handling of objects, allowing us to do crazy stuff like this. For example:

```javascript
({}+[]) -> "[object Object]"
!![]+!![] -> 2
```

So we can do stuff like this

```javascript
({}+[])[!![]+!![]] -> "b"
```

## So now what?

That gives use a limited ammount of characters, but nowhere near enough to write "Hello, World!". So how would we do that?

```javascript
String.fromCharCode(72, 101, 108, 108, 111, 44, 32, 87, 111, 114, 108, 100, 33) -> "Hello, World!"
```

We somehow need to get the `String.fromCharCode` function. But how can we do that without any letters?

Well, we can get a string using `[]+[]`, and every string has a `constructor` which is `String`. But how do we get that?

You can access properties like this:

```javascript
"string"["constructor"]
```

So we just need to get the string "constructor".

Let's see what characters we can get:

```javascript
({}+[])[!![]+!![]+!![]+!![]+!![]] -> "c"
({}+[])[+!![]] -> "o"
([][[]]+[])[(!![]+!![]+!![])*(!![]+!![])] -> "n"
(![]+[])[!![]+!![]+!![]] -> "s"
({}+[])[(!![]+!![]+!![])*(!![]+!![])] -> "t"
(!![]+[])[+!![]] -> "r"
([][[]]+[])[+[]] -> "u"
```

(If you're wondering where the `u` came from, `[][[]]` is `undefined`, and adding `[]` to that makes it `"undefined"`)

Sweet! So we can get `String` by using something like this:

```javascript
([]+[])[({}+[])[!![]+!![]+!![]+!![]+!![]]+({}+[])[+!![]]+([][[]]+[])[(!![]+!![]+!![])*(!![]+!![])]+(![]+[])[!![]+!![]+!![]]+({}+[])[(!![]+!![]+!![])*(!![]+!![])]+(!![]+[])[+!![]]+([][[]]+[])[+[]]+({}+[])[!![]+!![]+!![]+!![]+!![]]+({}+[])[(!![]+!![]+!![])*(!![]+!![])]+({}+[])[+!![]]+(!![]+[])[+!![]]]
```

Yes, that looks like a mess already. But if we look at what that's really doing:

```javascript
""["c"+"o"+"n"+"s"+"t"+"r"+"u"+"c"+"t"+"o"+"r"]
```

Which makes much more sense.

## Well we have String, now what?

Now that we have `String`, we still need `"fromCharCode"`

Some of those letters we already have, but some just aren't possible with what we've already done.

But wait... If we can get `btoa`, we can just base64 encode using characters we have, and hope we get what we need.

```javascript
({}+[])[(!![]+!![]+!![])**(!![]+!![])] -> "b"
({}+[])[(!![]+!![]+!![])*(!![]+!![])] -> "t"
({}+[])[+!![]] -> "o"
([]["constructor"]+[])[(!![]+!![]+!![])**(!![]+!![]+!![])-((!![]+!![]+!![])*(!![]+!![]))] -> "a"
```

Sweet! We have `btoa`! But it's just a string, we need some way of calling it.

Luckily, we can get `Function` fairly easily. So all we have to do is eval some code

```javascript
[]["fill"]["constructor"] -> function Function() { [native code] } // `fill` could be any method of `Array`, but `fill` was the easiest.
Function("return btoa")() -> function btoa() { [native code] }
```

We have all the characters for that! So now that we have `btoa`, we need to use it to get some letters.

The letters we still need are `C`, `m`, and `h`. So let's see if we can get those.

```javascript
btoa("[object Object]") -> "W29iamVjdCBPYmplY3Rd"
btoa(",,a") -> "LCxh"

"W29iamVjdCBPYmplY3Rd"[9] -> "C"
"W29iamVjdCBPYmplY3Rd"[5] -> "m"
"LCxh"[3] -> "h"
```

Awesome! We now have all the characters we need for `fromCharCode`!

Next we just jam them all together.

```javascript
[]["constructor"]["fromCharCode"](72, 101, 108, 108, 111, 44, 32, 87, 111, 114, 108, 100, 33) -> "Hello, World!"
```

Now we can replace all the characters and numbers with the roundabout ways we obtained them!

```javascript
"No, I'm not gonna paste all 7164 characters here. See out.js"
```

## Now what?

Nothing. That entire thing was completely pointless. But it was fun!

## Character count

Note: I'm pretty sure this can be reduced a fair bit, as we weren't too worried about efficiency.

```
'!' Count: 1802
'[' Count: 1489
']' Count: 1489
'+' Count: 1006
'(' Count: 493
')' Count: 493
'*' Count: 130
'{' Count: 102
'}' Count: 102
'-' Count: 34
',' Count: 15
'/' Count: 8
TOTAL CHARACTERS: 7163
```

# Overview

Yo.

So, with our projects in Lua so far, I'm a bit worried that I've gotten you started on the wrong foot with programming,
and have thrown you into the deep end, so to speak, before learning how to tread water.

So, this should hopefully serve as a decent introduction to the bare fundamentals of programming, and hopefully aid you
in your projects moving forward.

I'll be using Python 3 as the coding language for the examples in this document, since it's fairly easy to read and
understand, and it doesn't come with nearly the shortcomings as Lua when it comes to some things (which I'll get into
later), but the ideas should be applicable to any language that you decide to use in the future.

## The Fundamentals

### _Variables_

Variables are a way for us to store data for later. You can think of them like a bucket with a name, which we use to
store certain pieces of data, like numbers _(e.g. 1, 5, 24)_, or strings of text _(e.g. "Hello, World!")_. We can use
this bucket to store a piece of data, say the result of a big calculation, or some user input text, and then refer back
to the bucket by name when we want to use the data contained in it.

Much like buckets in real life, you're not committed to keeping the same data in it when you first fill it up -- you 
can put a piece of data in there now, and then overwrite it with something else later if you need.

In Python, declaring a variable is easy:

```python
  x = 5
```

This will create a bucket/variable named `x`, and place the value `5` into it.

By convention, the variable name goes on the left-hand side of the equals sign, and the value we want to place into it
goes on the right.

Then, if we want to use the data contained in `x`, all we have to do is refer to it by name.

So, if we want to print out whatever 2 times the value contained in `x` is, we would just write

```python
   print(2 * x)
```

That line will take whatever value is contained in `x`, multiply it by `2`, and then print it out on the screen.

### _Data/Variable Type_

Not all pieces of data are the same.

For example, when we write `x = 5` to write `5` to the variable `x`, the computer running the code needs to keep track 
of the fact that the value we've put into `x` is a *number*, as opposed to some other kind of data, like a string or 
something else.

This is called the variable's _type_, and helps the computer know how to interpret the data contained in that variable,
and know what to do when we eventually use the data contained in that variable.

Why is that important?

Firstly, at the very lowest level, all of the data for the program (including the code itself!) is stored in RAM as a
continuous stream of ones and zeroes. The computer might know where our variable is in that stream of ones and zeroes,
but if it doesn't know what kind of data it's looking for, it won't know how to convert those ones and zeroes into, 
say, the number that we wanted to refer back to.

Secondly, it affects how the code interprets expressions.

Consider the following code:

```python
  print(var + var)
```

Without knowing what _type_ `var` is, we can't say for sure what this code will do.

If `var` is a number, this line will print whatever that number plus itself is -- so if `var` contains the number `10`,
this line will print `20`.

However, if `var` is a string, this line will do something completely different -- the plus (`+`) operator in Python
means "add" when dealing with numbers, but when dealing with strings, it means "combine these two strings together".

So, if `var` contained the string `"Hello!"`, this line would print `"Hello!Hello!"`.

Python takes care of the whole rigamarole of determining the type of a variable for you, and will even change the type
of a variable if you later decide to store a different type of data in it. However, some languages require you
to tell the computer _explicitly_ the type of data that you intend to store, and won't let you change the type of that
variable later.

### _But what types of data are there?_

Good question.

At the base level, most programming languages deal with much of the same kinds of data.

* Integers
  * These are whole numbers, which can either be positive or negative.
  * _e.g. 1, 5 , -20_
* Floats
  * These are decimal numbers, which can also be either positive or negative. The name "float" refers to the fact that
  the decimal point is "floating", in the sense that we're not necessarily constrained to have a certain amount of
  numbers before or after the decimal point.
  * _e.g. 1.5, 0.33, -9.9999999_
* Booleans
  * Named after George Boole, these are `true` or `false` values that act as an easy way for us to answer yes-or-no
  questions, like "is this number even?", or "did this function succeed?"
  * _e.g. True, False (these are capitalized in Python, but most languages don't capitalize them)_
* Strings
  * A piece of text. The name "string" refers to the fact that the data is a "string" of characters, like "a", "b", etc. 
    which in some programming languages are a type unto themselves.
  * _e.g. "Hello, World!", "Lorem ipsum dolor sit amet"_
* Lists
  * A list of other pieces of data. Some programming languages enforce that all elements contained in a list are of the
    same type, but Python doesn't have that restriction, so go wild!
  * You can grab an element of a list at a certain position by using square-brackets next to the variable that contains
    the list -- position numbers start at 0 at the beginning of the list, and count upwards.
  * _e.g. [1, 2, 3], ["a", "b", "c"]_

There are many more data types out there, including some that allow you to organize and store collections of other
pieces of data, but these are the core types that you'll be working with on a regular basis.

### _Expressions_

Programming would be boring if we only had to deal with one piece of data at a time -- we need tools to be able to
operate on and combine pieces of data!

At a high level, an expression is a piece of code containing *values* and *operators* (like `+`, `/`, etc.) that resolve
to a single value.

For example, let's start with arthmetic expressions to get our feet wet.

Consider the following piece of code:

```python
  5 + 10 * 3
```

This is an expression that resolves to a number -- 35, to be exact. All of these numbers are pieces of data, and the
operators between them _(the `+` and `*`)_ combine them into one single value.

We're not restricted to just using numbers, though; remember that example from earlier?

```python
   print(var + var)
```

Earlier, we had said that if `var` was a string, that this would print that string combined with itself, i.e. if `var`
was equal to `"Hello!"`, then this would print `"Hello!Hello!"`

That thing inside the print function is also an expression -- it has two pieces of data (both of them `var`), as well as
an operator (`+`) that *resolves* to the single value of `"Hello!Hello!"`, which the print function then takes and
prints to the screen for the user to see.

Expressions on their own aren't terribly useful -- if you type one straight out into your code, like we did with that
numbers example just above, the expression will resolve, but will then disappear into the ether because we aren't really
*doing* anything with it.

However, we can use the end result of an expression to, say, pass off to a function, like we did with the `print()`
example above, or we can assign the end result of an expression to a variable, like so:

```python
  x = 5 + 10 * 3
  y = x * 2
  z = "Hello" + " there"
```

Expressions don't always have to resolve to the same type of data that it's operating on, however.

Very often, we'll want to convert data that we have on hand into statements of _truth_, for example, "is this number
odd?", or "are these two pieces of text the same?"

Consider the following expression:

```python
 x == y
```

This expression asks the question "are `x` and `y` equal to one another?", and will resolve to `True` if they are, or
`False` if they aren't.

The equality-check operator (`==`) is one of many operators that allows you to ask questions of data, others include
the less-than and greater-than operators (`<` and `>`), not-equal-to operator (`!=`), and many more. The equality-check
operator is special, however, in that it doesn't just work on numerical types, it can work on any two pieces of data of
the same type (with some exceptions).

### _Flow Control: if/elif/else and Conditionals_

The one place where expressions shine is when used in if/else structures.

Sometimes, we only want to execute a piece of code when a certain set of criteria are met. Maybe we only want a bot to
grab an item in front of it if that item is valuable, or maybe we're having the user guess a number, and we only want to
print a success message if they guess correctly.

We can do that with `if` statements.

An `if` statement takes the following form:

```python
  if <expr>:
    <code to execute>
```

The code contained in `<code to execute>` will only run if the expression `<expr>` resolves to `True`.

(Note: in Python, the program determines the code contained in the "`if`" based on the indentation level of the code --
everything indented one level above the "`if`" up until the next line at the same indentation level as the "`if`" itself
is considered part of the code that will run if the expression is true.)

So, if we wanted to implement that number-guessing game mentioned before, we would do the following:

```python
  secret_number = 12

  # This line will take input from the user, and convert it into a number
  number_guessed = int(input("Guess a number! "))

  if number_guessed == secret_number:
    print("Woah, how'd you know?")
```

Here, we supply the `if` statement with a simple expression that checks to see if the number that the user guessed is
equal to the number that we have stored -- if the two are the same, the success message is printed out.

What if we also wanted to print out a message if they were wrong?

We could use an `else` statement underneath the previous `if` to define a piece of code that will execute if the
expression supplied to the `if` resolves to `False`.

So, we could do something like:

```python
  secret_number = 12

  # This line will take input from the user, and convert it into a number
  number_guessed = int(input("Guess a number! "))

  if number_guessed == secret_number:
    print("Woah, how'd you know?")
  else:
    print("Sorry, try again.")
```

Now, if the user got the number wrong, the program will skip over all of the code defined inside the above `if`, and
will instead execute the code inside of the `else`, and we print out a message saying that they were incorrect.

The converse is also true -- if the user got the number right, the program will only execute the code inside of the
`if`, and will skip over the code inside of the `else`.

What's neat about `if` and `else` is that you can actually chain together a bunch of different checks together.

Let's say we change our number guessing game to include three different numbers that the user could guess.

We want to check to see if the user guessed any of the three numbers correctly, and print out a unique message depending
on which number they guessed, or a failure message if they didn't guess any of the numbers correctly.

We could write that like this:

```python
  first_secret_number = 12
  second_secret_number = 35
  third_secret_number = 4

  # This line will take input from the user, and convert it into a number
  number_guessed = int(input("Guess a number! "))

  if number_guessed == first_secret_number:
    print("You guessed the first number!")
  else:
    if number_guessed == second_secret_number:
      print("You guessed the second number!")
    else:
      if number_guessed == third_secret_number:
        print("You guessed the third number!")
      else:
        print("Sorry, try again")
```

If the number that the user guesses isn't equal to the first secret number, the code will drop into the first `else`
block, and then check to see if it's equal to the second secret number; if it isn't, then it'll drop into the second
`else` block, and check to see if it's equal to the third secret number, etc.

This code works, but it's a bit difficult to visually parse -- it's not immediately obvious that what we're going is
performing a series of checks on the data we were provided; it takes a bit of reading and understanding to tell that's
what the code is doing.

Luckily, we can use another flow-control keyword, `elif`, short for `else if`.

We can use them like this:

```python
  if <expr A>:
    <code to execute if A is true>
  elif <expr B>:
    <code to execute if A isn't true, but B is true>
  else:
    <code to execute if neither are true>
```

`elif` is like an `else` and an `if` combined; an `elif`, when placed underneath an `if`, will
execute only when the expression contained in the above `if` resolves to `False` *and* the expression
contained in the `elif` resolves to `True`.

We can also chain `elif`s together, which is pretty neat.

So, we could re-write our new guessing game like so:

```python
  first_secret_number = 12
  second_secret_number = 35
  third_secret_number = 4

  # This line will take input from the user, and convert it into a number
  number_guessed = int(input("Guess a number! "))

  if number_guessed == first_secret_number:
    print("You guessed the first number!")
  elif number_guessed == second_secret_number:
    print("You guessed the second number!")
  elif number_guessed == third_secret_number:
    print("You guessed the third number!")
  else:
    print("Sorry, try again")
```

Now, the nature of this code more easily reveals itself to us -- if the user guesses the first number, then the first
success message is printed. If not, the code jumps down to the next `elif` to see if the user guessed the second number
correctly. If they did, the second success message is printed, if not, the code jumps down to the next `elif` to check
the third number, and so on. If none of the `ifs` or `elifs` end up being `True`, the `else` will execute.

### _Boolean Logic_

The expressions used in `if` blocks don't have to just rely on one check -- what if we only want to
run a piece of code if a bunch of different checks turn out to be true?

For example, what if we wanted to modify our guessing game to only o print a success message if the user guesses all
three secret numbers correctly?

We could chain together a bunch of `ifs`, but there's an easier way.

Enter the humble `and` operator; this operator takes two Boolean true/false values, and resolves to true if both values
are true, and resolves to false otherwise.

For example, consider the following code:

```python
  a = 5
  b = 10
  c = 20

  if a < b and b < c:
    print("nice")
```

The above print statement will only execute if `a` is less than `b` *and* `b` is less than `c`. And, since that's the
case, it will!

We can use this to update our guessing game like so:

```python
  first_secret_number = 12
  second_secret_number = 35
  third_secret_number = 4

  first_number_guessed = int(input("Guess your first number: "))
  second_number_guessed = int(input("Guess your second number: "))
  third_number_guessed = int(input("Guess your third number: "))

  # Each check indented for clarity, you wouldn't necessarily write this with this indentation in real code
  if first_secret_number == first_number_guessed and 
      second_secret_number == second_number_guessed and
      third_secret_number == third_number_guessed:
    print("You guessed them all right!")
  else:
    print("Sorry, try again")
```

Now, each of those checks will need to resolve to true before that print statement will run.

Similar operators that help us combine Boolean values exist, including `or` (takes two values, resolves to true if
either value is true, resolves to false otherwise), and `not` (takes one value, resolves to true if the value is false,
resolves to false if the value is true)

### _Loops: Two Different Flavors_

Sometimes we want to execute some piece of code multiple times; for example, we might want a bot to move a certain
number of spaces forward, or maybe we want to print out some data we have stored in a table, row by row.

But we don't want to copy and paste the same lines of code over and over again.

That's cringe.

Instead, we can use loops to allow us to execute a certain piece of code multiple times.

Loops come in two flavors: `for` loops, and `while` loops.

`for` loops are good for when you know exactly how many times you need to loop; say you want a bot to move forward a
certain number of spaces, or you want to print out the contents of a list you have stored.

With `for` loops, there is a definite end to the loop, and a definite number of times that it will loop -- once it 
hits the last number you're counting, or the last element in the list you're looking at, the `for` loop stops and 
your code continues onwards.

`while` loops, by contrast, are good for when you're not really sure how many times you need to loop, and want to
continue executing a bit of code while some condition is true -- say, you want to modify the guessing game above to keep
running over and over until the user gets the number right. We can't know how long that's going to take, but we can tell
when the criteria are met for the end of the game, so a `while` loop is appropriate.

Now, the syntax and semantics of `for` loops in Python differs a decent bit from other programming languages, but this
difference also makes it incredibly powerful.

A `for` loop in Python is constructed as follows:

```python
  for <variable name> in <some list>:
    <code to execute in loop>
```

_(Again, the indentation for the code inside the loop is important!)_

For this loop, Python will take the first element in the list, and place it into a variable with the name that we
provide in the `for` statement. It then runs the code inside the loop, and jumps back up to the `for` statement. Python
will then place the second element in the list into that variable, and run the code inside the loop again. This
continues until the variable has taken the value of each element of the list, and then the `for` loop will stop, and
your code will continue onwards.

(This is often called _iterating_ over the list -- in fact, in Python, any data structure that you can plop into the
`<some list>` field of a `for` loop is called an _iterable_)

Compared to the `for` loops you might be used to in Lua, which pre-define the start and end number, this might be a
little uncomfortable at first. Let's start with a simple example.

Python provides for us a function called `range()`, which returns a list containing the numbers between 0 and whichever
number we supply to the function, with the number we supplied to the function not included.

Consider the following piece of code:

```python
  range(10)
```

This function call will return the list `[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`

We can use this, for example, to print out the numbers between 0 and 10:

```python
  for i in range(10):
    print(i)
```

Python will take the first element of the list, `0`, and place it into the variable `i`. Python then runs the code
inside the loop, which prints out whatever is currently contained in `i`, which right now, is `0`.

Python, hitting the bottom of the loop, then jumps back up to the top of the `for` loop, and places the next element of
the list, `1`, into the variable `i`. Python then runs the print function again, and prints out whatever's currently
contained in `i` again, which right now, is `1`.

This continues until the print function has run for each element in the list. Python will then jump back up to the top
of the list, realize that there's no more new elements in the list to assign to `i`, and exit the loop.

We're not limited to just using `range()` in our `for` loops, however; we can use any list!

Say we modified our guessing game above to have *even more* secret numbers, and we want to see if our user has guessed
any one of them.

Putting each secret number into its own variable would get messy and tiresome to write _very_ quickly, so putting all of
the secret numbers in the list is a sensible thing to do.

We can then use that list in a `for` loop to check each secret number in the list against the number the user has
guessed -- if there's a match, then we can print out a success message!

```python
  # Creates a list containing all of the secret numbers the user can guess, and places it into the variable named "secret_numbers"
  secret_numbers = [12, 35, 4, 18, 67]

  guessed_number = int(input("Guess a number! "))

  for number in secret_numbers:
    if guessed_number == number:
      print("You guessed one of the numbers!")
```

This loop looks over the list of secret numbers, and one-by-one, places each into the variable called `number`. It then
uses this variable to compare against the user's guess, and print out a success message if the user is correct.

However, there's one small optimization that we might want to make -- say the user guesses the number `35`, the second
element in the list. When the loop gets to the number `35` in the list, it'll print out the success message like we
might expect, but then _the loop keeps going_, checking the guess against all of the other secret numbers.

We already know that the user has guessed correctly, and that there's nothing else to check, so this loop would just be
checking numbers unnecessarily, wasting time.

Luckily, Python (and most other programming languages that implement loops) provides us an easy way to "break" out of a
loop early -- funnily enough, called `break`.

So, we can simply modify our loop like this:

```python
  # Creates a list containing all of the secret numbers the user can guess, and places it into the variable named "secret_numbers"
  secret_numbers = [12, 35, 4, 18, 67]

  guessed_number = int(input("Guess a number! "))

  for number in secret_numbers:
    if guessed_number == number:
      print("You guessed one of the numbers!")
      break
```

Now, if we see that the user has guessed one of the numbers correctly, we print out the success message, and then
execute the `break` statement, which immediately breaks us out of the loop, and jumps us to the next bit of code outside
of the loop.

`break` statements don't just work in `for` loops, they can also be used in `while` loops as well.

Oh, speaking of which...

`while` loops in Python are constructed as follows:

```python
  while <expr>:
    <code to execute in loop>
```

Here, the `while` loop will continue executing the code inside of the loop while the expression we provide to it
resolves/evaluates to true.

The flow works much the same as a `for` loop: Python will start at the `while` loop line, and evaluate the expression
provided to the loop. If the expression evaluates to true, the code inside of the loop will run once, and then Python
will return to the `while` loop line, and evaluate the expression again, checking to see if it's still true. This will
continue, over and over until the first time that Python checks the expression and it evaluates to false; Python will
then exit the loop.

This structure isn't great for counting up to a certain number or looking over a list, but it's great for executing a
piece of code until something specific happens.

We can use this to re-work our guessing game -- currently, the game will simply run once, only allowing the user to
guess once, and then the program will exit, regardless of whether or not the user was correct. It'd be much better if
the game kept running until the user guessed correctly.

We can modify the game like so:

```python
  guessed_correctly = False
  
  # Creates a list containing all of the secret numbers the user can guess, and places it into the variable named "secret_numbers"
  # I put this list outside of the loop because we don't need to keep creating this variable over and over -- just once is sufficient.
  secret_numbers = [12, 35, 4, 18, 67]
  
  # This loop will continue running until guessed_correctly is True (the not will flip the value so that we can keep executing the loop while guessed_correctly is False)
  while not guessed_correctly:
    guessed_number = int(input("Guess a number! "))

    for number in secret_numbers:
      if guessed_number == number:
        print("You guessed one of the numbers!")
        guessed_correctly = True
        break
```

Here, we've added an extra variable `guessed_correctly` to help keep track of the game state. `guessed_correctly` will
be false to start with, since the user hasn't guessed yet, and therefore has not yet guessed correctly. We will then set
`guessed_correctly` to true once the user guesses one of the numbers in the list.

Since `while` loops will continue executing while the expression provided to it resolves to true, but we want this loop
to continue executing while `guessed_correctly` is false (we want to keep playing the game while the user *hasn't*
guessed correctly), we add the `not` Boolean operator before `guessed_correctly` in the `while` statement so that the
loop keeps executing while the user hasn't guessed the number.

And now, we've got a functional game on our hands!

But wait, you might ask, isn't there a problem with that break statement?

```python
  guessed_correctly = False
  
  # Creates a list containing all of the secret numbers the user can guess, and places it into the variable named "secret_numbers"
  # I put this list outside of the loop because we don't need to keep creating this variable over and over -- just once is sufficient.
  secret_numbers = [12, 35, 4, 18, 67]
  
  # This loop will continue running until guessed_correctly is True (the not will flip the value so that we can keep executing the loop while guessed_correctly is False)
  while not guessed_correctly:
    guessed_number = int(input("Guess a number! "))

    for number in secret_numbers:
      if guessed_number == number:
        print("You guessed one of the numbers!")
        guessed_correctly = True
    ---> break <---
```

I had said that `break` statements can work for both `for` and `while` loops. Wouldn't this line break us out of the
`while` loop we just created, making our use of the `guessed_correctly` flag kind of pointless?

Not necessarily.

`break` statements can be used for both `for` and `while` loops, but they will only ever break us out of *one* loop at a
time, that loop being the inner-most loop relative to the `break` statement. So, the `break` above will break out of the
`for` loop, since that's the inner-most loop the `break` is contained within, but the code execution will stay within 
the outer `while` loop. So, we're totally fine to use it here!

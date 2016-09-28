Let's try simplifying things by doing a simpler calculation - it's less confusing. We'll look at a `factorial` method for calculating `n-factorial` (see [this](https://en.wikipedia.org/wiki/Factorial) if you need more info).

One definition of how to calculate n-factorial (written as `n!`) is:

-   1! is 1
-   n! = n * (n-1)!

This leads to a recursive method for calculating factorials:

```ruby
def factorial(n)
  if n == 1
    1
  else
    n * factorial(n - 1)
  end
end
```

Now, let's walk through this to calculate `factorial(4)`.

```
Call factorial(4)
  On line 5, we end up having to calculate 4 * factorial(3)
  So, we need calculate factorial(3)
    On line 5 again, we end up having to calculate 3 * factorial(2)
    So, we need calculate factorial(2)
      On line 5 again, we end up having to calculate 2 * factorial(1)
      So, we need calculate factorial(1)
        This time, with n == 1, we execute line 3 instead of line 5
        Thus, factorial(1) returns 1
      We are now back in the factorial(2) call
      We now know that factorial(1) is 1
      Thus, 2 * factorial(1) is 2
      factorial(2) now returns 2
    We are now back in the factorial(3) call
    We now know that factorial(2) is 2
    Thus, 3 * factorial(2) is 6
    factorial(3) now returns 6
  We are now back in the factorial(4) call
  We now know that factorial(3) is 6
  Thus, 4 * factorial(3) is 24
  factorial(4) now returns 24
We're now back at the top level, and factorial(4) has returned 24.
This is out answer.
```

Note that this walkthrough uses indentation to show "depth" in the recursion. The first line is at depth 1; the next two lines are at depth 2; the next at depth 3; the next at depth 4; and the final level is depth 5. At depth 5, we are calculating `factorial(1)`, which returns 1.

When `factorial(1)` returns, it only returns by one level in the "call stack"; in this case, it returns to depth 4, which is responsible for calculating `factorial(2)`. `factorial(2)` returns to depth 3, which is responsible for calculating `factorial(3)`. `factorial(3)` returns to depth 2, which is responsible for calculating `factorial(4)`. Finally, `factorial(4)` returns to depth 1, which made the original request.

Looked at another way, it's exactly as though we did this instead:

```ruby
def factorial1
  1
end

def factorial2
  2 * factorial1
end

def factorial3
  3 * factorial2
end

def factorial4
  4 * factorial3
end

puts factorial4
```

The difference with recursion is that we need just one method and it is general purpose, but the calls and returns work exactly the same way. Each call increases the depth of the call stack, and each return returns to the previous level.

The translation to calculating the Fibonacci sequence is the same; however, at each depth, we need to make two separate recursive calls. This makes it harder to explain, but the behavior is identical - first you work your way down to the final depth, then you work your way back.

Is this any more helpful?

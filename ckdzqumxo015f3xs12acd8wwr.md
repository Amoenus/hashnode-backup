## No method too small | Amoenus Dev

This story starts with a call from the 1st line support that users were getting intermittent-production-only error in one of the key application my team were working on.

The problem was that the application was behind the hardened environment that we had no access to.

The only thing we could do is enable logging which in itself took a whole week to get approved. And the result the Developers favourite - `NullReferenceException` in one of the biggest methods, I've ever seen in my whole career. Needless to say, that was not very helpful and we were no closer to the solution.

What. A. Pain.

Frustrated with the issue and with business breathing down my neck I started slicing this Monster of a method into smaller and smaller chunks. Even if some action was just a one-liner that would not stop me to create a method. At one point I could no longer care for method names resorting to such classics like `Method1`, `FooBar123` and `DoStuff`.

But. It. Worked.

After the next deployment logs were showing the same `NullReferenceException` but now the stack trace pointed me to some `Method13.`

The resulting stack trace finally allowed to pinpoint the issue. The fix then was just a simple null check.

While Dev team who did not appreciate my creative method naming it was obvious to everyone that even that was better than one big blob of code.

It might seem silly to separate the most obvious one-liners into their own methods and sometimes even whole classes but not living through that experience alone is worth it for me.

Did you ever found yourself in a situation where you wished your stack trace was just a little bit more in-depth? Tell me in the comments ^_^

So now go and look at your code and see if you can pepper it with smaller methods so that you stack traces can pave your way to your debugging success.
# gitworkshop

## git bisect

This branch has a simple `test.sh` script that echoes a word then exits.

It has about 120 commits, and 10 tags.

When run, the script *should* exit with exit code 0.

A user comes along and says:

> Your code doesn't work! It used to work flawlessly!
> It was fine until I upgraded from **bisect-v5** to **bisect-v6**.

Bingo! When you hear those words you can reach for `git bisect` to tell you which commit broke it.

## The manual way

```sh
# start up git bisect
git bisect start

# give git a commit where there is not a bug
git bisect good bisect-v5

# give git a commit where there is a bug
git bisect bad bisect-v6
```

It drops you at a commit. Test your code!

```sh
./test.sh
```

Now check the exit code. Was is good?

```sh
git bisect good
```

Was is bad?

```sh
git bisect bad
```

It drops you at a commit. Test your code! Was it good or bad?
Repeat until you find the first bad commit!


## The automated way

This time, another user comes along and says:

> Your code doesn't work! It used to work flawlessly!
> It was fine until I upgraded from **bisect-v1** to **bisect-v10**.

If you can write an automated [unit] test, we can automate all those boring steps.

Here, we already have a test script, it's `test.sh`. In real life, you can write a unit test. (Bonus side effect: you have a new test to prevent future regressions!)

```sh
# get it ready
git bisect start
git bisect good bisect-v1
git bisect bad bisect-v10

# give git a command to run against each commit
git bisect run ./test.sh
```


## Thanks

https://robots.thoughtbot.com/git-bisect


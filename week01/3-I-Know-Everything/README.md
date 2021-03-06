# The last set of problems for those who know everything

## 100 SMS

Before the smartphones, when you had to write some message, the keypads looked like that:

![Nokia 3310 Keypad](nokia.jpg)

For example, on such keypad, if you want to write **Ruby**, you had to press the following sequence of numbers:

```
7778822999
```

Each key contains some letters from the alphabet. And by pressing that key, you rotate the letters until you get to your desired one.

It's time to implement some encode / decode functions for the old keypads!

### `numbers_to_message(pressedSequence)`

First, implement the function that takes a list of integers - the sequence of numbers that have been pressed. The function should return the corresponding string of the message. 

There are a few special rules:

* If you press `1`, the next letter is going to be capitalized
* If you press `0`, this will insert a single white-space
* If you press a number and wait for a few seconds, the special breaking number `-1` enters the sequence. This is the way to write different letters from only one keypad!

Few examples:

```
numbers_to_message([2, -1, 2, 2, -1, 2, 2, 2]) = "abc"
numbers_to_message([2, 2, 2, 2]) = "a"
numbers_to_message([1, 4, 4, 4, 8, 8, 8, 6, 6, 6, 0, 3, 3, 0, 1, 7, 7, 7, 7, 7, 2, 6, 6, 3, 2])
=
"Ivo e Panda"
```

### `message_to_numbers(messsage)`

This function takes a string - the `message` and returns the **minimal** keystrokes that you ned to write that `message`

Few examples:

```
message_to_numbers("abc") = [2, -1, 2, 2, -1, 2, 2, 2]
message_to_numbers("a") = [2]
message_to_numbers("Ivo e panda")
=
[1, 4, 4, 4, 8, 8, 8, 6, 6, 6, 0, 3, 3, 0, 1, 7, 2, 6, 6, 3, 2]
message_to_numbers("aabbcc") = [2, -1, 2, -1, 2, 2, -1, 2, 2, -1, 2, 2, 2, -1, 2, 2, 2]
```

## Spam and Eggs

This is a problem from the [Python 2012 course in FMI](http://2012.fmi.py-bg.net/).

You can see the original problem statement here - http://2012.fmi.py-bg.net/tasks/1

Implement a function, called `prepare_meal(number)` that takes an integer and returns a string, generated by the following algorithm:

__Еggs:__

If there is an integer `n`, such that `3^n` divides `number` and `n` is the largest possible,
the result should be a string, containing `n` times `spam`.

For example:

```ruby
prepare_meal(3) == 'spam'
prepare_meal(27) == 'spam spam spam'
prepare_meal(7) == ''
```

__Spam:__

If number is divisible by 5, add `and eggs` to the result.

For example:

```ruby
prepare_meal(5) == 'eggs'
prepare_meal(15) == 'spam and eggs'
prepare_meal(45) == 'spam spam and eggs'
```

__Notice that in the first case, there is no "and". In the rest - there is.__


```ruby
prepare_meal(5) == "eggs"
prepare_meal(3) == "spam"
prepare_meal(27) == "spam spam spam"
prepare_meal(15) == "spam and eggs"
prepare_meal(45) == "spam spam and eggs"
prepare_meal(7) == ""
```

## Reduce file path

A file path in a Unix OS looks like this - `/home/radorado/code/hackbulgaria/week0`

We start from the root - `/` and we navigate to the destination fodler.

But there is a problem - if we have `..` and `.` in our file path, it's not clear where we are going to end up.

* `..` means to go back one directory
* `.`  means to stay in the same directory
* we can have more then one `/` between the directories - `/home//code`

So for example : `/home//radorado/code/./hackbulgaria/week0/../` reduces to `/home/radorado/code/hackbulgaria`.


Implement a function, called `reduce_file_path(path)` which takes a string and returns the reduced version of the path.

* Every `..` means that we have to go one directory back
* Every `.` means that we are staying in the same directory
* Every extra `/` is unnecessary
* Always remove the last `/`

**Few examples:**

```ruby
reduce_file_path("/") == "/"
reduce_file_path("/srv/../") == "/"
reduce_file_path("/srv/www/htdocs/wtf/") == "/srv/www/htdocs/wtf"
reduce_file_path("/srv/www/htdocs/wtf") == "/srv/www/htdocs/wtf"
reduce_file_path("/srv/./././././") == "/srv"
reduce_file_path("/etc//wtf/") == "/etc/wtf"
reduce_file_path("/etc/../etc/../etc/../") == "/"
reduce_file_path("//////////////") == "/"
reduce_file_path("/../") == "/"
```

## Word from a^nb^n

Implement a function, called `is_an_bn(word)` that checks if the given `word` is from the `a^nb^n for n>=0` language.
Here, `a^n` means a to the power of n - __repeat the character "a" n times.__

Lets see few words from this language:

* for `n = 0`, this is the empty word `""`
* for `n = 1`, this is the word `"ab"`
* for `n = 2`, this is the word `"aabb"`
* for `n = 3`, this is the word `"aaabbb"`
* and so on - first, you repeat the character "a" n times, and after this - repeat "b" n times

The function should return true if the given `word` is from `a^nb^n for n>=0"` for some n.

**Test examples:**

```ruby
is_an_bn("") == true
is_an_bn("rado") == false
is_an_bn("aaabb") == false
is_an_bn("aaabbb") == true
is_an_bn("aabbaabb") == false
is_an_bn("bbbaaa") == false
is_an_bn("aaaaabbbbb") == true
```

## Credit card validation

Implement a function, called `is_credit_card_valid(number)`, which returns true/false based on the following algorithm:

* Each credit card number must contain odd count of digits.
* We transform the number with the following steps (based on the fact that we start from index 0)
  - All digits, read from right to left, at even positions (index), **remain the same.**
  - Every digit, read from right to left, at odd position is replaced by the result, that is obtained from doubling the given digit.
* After the transformation, we find the sum of all digits in the transformed number.
* The number is valid, if the sum is divisible by 10.

For example: `79927398713` is valid, bacause:

* When we double and replace all digits at odd position we get: `7 (18 = 2 * 9) 9 (4 = 2 * 2) 7 (6 = 2 * 3) 9 (16 = 2 * 8) 7 (2 = 2 * 1) 3`
* The sum of all digits of the new number is 70, which is divisible by 10 => the card number is valid.

More examples:

* `79927398713` is a valid number
* `79927398715` is invalid number

## Goldbach Conjecture

Implement a function, called `goldbach(n)` which returns a list of tuples, that is the goldbach conjecture for the given number `n`.

The Goldbach Conjecture states:

> Every even integer greater than 2 can be expressed as the sum of two primes.

Keep in mind that there can be more than one combination of two primes, that sums up to the given number.

__The result should be sorted by the first item in the tuple.__

For example:

* `4 = 2 + 2`
* `6 = 3 + 3`
* `8 = 3 + 5`
* `10 = 3 + 7 = 5 + 5`
* `100 = 3 + 97 = 11 + 89 = 17 + 83 = 29 + 71 = 41 + 59 = 47 + 53`

**Few examples:**

```ruby
goldbach(4) == [(2,2)]
goldbach(6) == [(3,3)]
goldbach(8) == [(3,5)]
goldbach(10) == [(3,7), (5,5)]
goldbach(100) == [(3, 97), (11, 89), (17, 83), (29, 71), (41, 59), (47, 53)]
```

## Magic Square

Implement a function, called `magic_square(matrix)` that checks if the given array of arrays `matrix` is a magic square.

A magic square is a square matrix where the numbers in each row, and in each column, and the numbers in the forward and backward main diagonals, all add up to the same number.


```ruby
magic_square([[1,2,3], [4,5,6], [7,8,9]]) == false

magic_square([[4,9,2], [3,5,7], [8,1,6]]) ==  true
magic_square([[7,12,1,14], [2,13,8,11], [16,3,10,5], [9,6,15,4]]) ==  true
magic_square([[23, 28, 21], [22, 24, 26], [27, 20, 25]]) == true
magic_square([[16, 23, 17], [78, 32, 21], [17, 16, 15]]) == false
```

\|[pyutils](https://subimal.github.io/pyutils/#pyutils)\|

# python3-SimpleStuff

* TOC
{:toc}

## The structure of the package

Let us got through the implementation details
* `SimpleStuff` : This is the name of the package. As of now there is only one module in it:
  * ``math`` with these functions defined
    * ``IsPrime``
    * ``gcd``
    * ``lcm``

## Implementation details

### ``SimpleStuff.math.IsPrime``
It is trivial that all prime numbers except 2 and 3 will have a remainder of 1 or 5. In case you missed why, here is the reason.

Any number (`n`) can be expressed as `n=6k+r` where 

`k` is an integer

`r` is the remainder upon dividing `n` by `6`

So the number `n` can be expressed as

`n = 6k` or `n = 6k+1` or `n = 6k+2 = 2(3k+1)` or `n = 6k+3 = 3(2k+1)` or `n = 6k+4 = 2(3k+2)` or `n = 6k+5`

So we see that only those numbers that yield a remainder of 1 or 5 will be candidates for being prime. The others are composite. Be sure to understand that 

a remainder of 1 or 5 when an integer is divided by 6 means that the number *may* be prime. It is not necessarily prime. As an example consider 35.


In this module we use this fact to speed up the test for 2/3 of the integers.

#### Algorithm
* Is the remainder upon dividing `n` by `6` either `1` or `5`?
  * if `Yes`, the number *may* be prime.
    * Check if `n` is divisible by any of odd integers from `1` to `n/2`.
      * If divisible, it is not prime.
      * If not, it is prime.
  * if `No`, the number is definitely composite.


#### Examples

##### Is `n` a prime number?

```python
>>> import SimpleStuff.math as m
>>> m.IsPrime(1)
False
>>> m.IsPrime(15)
False
>>> m.IsPrime(17)
True
>>> m.IsPrime(171)
False
>>> m.IsPrime(10101)
False
>>> m.IsPrime(97)
True
>>>
```

##### Generating a list of primes between 1 and 100

```python
>>> import SimpleStuff.math as m
>>> ans = []
>>> for i in range(1,101):
...     if m.IsPrime(i):
...             ans.append(i)
... 
>>> ans
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
>>>
```

### ``SimpleStuff.math.gcd``
This function is an implementation of [Euclid's algorithm](https://en.wikipedia.org/wiki/Greatest_common_divisor#Euclid's_algorithm) for finding the [greatest common divisor](https://en.wikipedia.org/wiki/Greatest_common_divisor) of a list of atleast two numbers.

#### Algorithm
##### GCD of two numbers `a` and `b` 

* Is `a<b`?
  * `Yes`: Go to the next step 
  * `No` : Exchange `a` and `b`
* As long as `b` is positive 
  * a <- b
  * b <- a%b
* The answer is `a`

##### GCD of a list of integers `l[0]`, `l[1]`, `l[2]`, `l[3]`, ... and `l[n]`

```
                          GCD of `l[0]` and `l[1]`
                          |
                          V
                 GCD of `ans` and `l[2]`
                  |
                  V
         GCD of `ans` and `l[2]`
          |
          V
          .
          .
          .
          .
 GCD of `ans` and `l[n]`
  |
  V
  The GCD of `l[0]`, `l[1]`, `l[2]`, `l[3]`, ... and `l[n]`
```

#### Examples

```python
>>> import SimpleStuff.math as m
>>> m.gcd(8,12)             # ERROR: the argument must be a list of numbers
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: gcd() takes 1 positional argument but 2 were given
>>> m.gcd([8,12])
4
>>> m.gcd([8,12,16])
4
>>> m.gcd([8,16, 64])
8
>>> 
```

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

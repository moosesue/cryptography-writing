Greatest Common Divisor: From Factor Lists To Elegant Python

Finding the greatest common divisor (GCD) of two integers is a simple but useful problem in Mathematics. It’s usually taught in primary school and describes finding the largest whole number that divides into both numbers. Sometimes it is called finding the highest common factor (HCF). It’s also sometimes referred to as Euclid’s algorithm, named after the ancient Greek mathematician, Euclid, who lived c300BC. 

A simple example would be finding the highest common factor of 28 and 35.
In primary school, you might list the factors of both of these numbers.

Factors of 28: 1, 2, 4, 7, 14, 28

Factors of 35: 1, 5, 7, 35

So it’s easy to see with a simple example that the largest factor common to both lists is 7.

Euclid formed an algorithm that can be used to find this largest factor with bigger numbers, when writing out lists might be a bit long and tedious. The basic idea is that the largest factor doesn’t change if you replace the bigger number with the difference between it and the smaller number. This is then repeated this until the numbers are the same. This final number is the largest factor of both numbers. So, in our simple example Euclid's original method is:

35 - 28 = 7

28 - 7 = 21

21 - 7 = 14

14 - 7 = 7

So the GCD is 7.

In programming, finding the difference repeatedly is equivalent to using the modulus operator % , which gives the remainder after division. This is much more efficient and gives the same result.

35 % 28 = 7

28 % 7 = 0

The remainder is 0 and so the GCD is 7.

We could write this in Python as follows:

```python
def gcd(a: int, b: int)->int:
  #check if either of the numbers passed in is zero
  if (a !=0) and (b!=0) :
    #check if a is bigger than b
    if a > b:
       #if it is then set new_number_a to be the remainder of a #divided by b and set new_number_b to be b.
       new_number_a = a%b
       new_number_b = b
    else:
        #if it isn’t then set new_number_a to be the remainder of b #divided by a and set new_number_b to be a.
        if a < b:
           new_number_a = b%a
           new_number_b = a
  #check if new_number_a is the same as new_number_b and that
  #new_number_b is not zero. If so, call the function again 
  #with the new numbers.
  if (new_number_a != new_number_b) and (new_number_b!=0):
     return gcd(new_number_a, new_number_b)
  else:
     #if not then we must be finished and so the result is 
     #new_number_a
     return new_number_a
```

However, this is not a very elegant solution as it is multiple lines and calculations and the same result can be found with a lot fewer operations. If the numbers are not the same and are not zero then the same function can be called by itself. This is called a recursive function. You could actually just write the following to do exactly the same thing.

```python
def gcd(a,b):return gcd(b%a,a) if a else b
```

In Rust you could write:

```rust
fn gcd(a: u32, b: u32) -> u32 {
  if a == 0 {
     b
 }
  else {
     gcd(b % a, a)
     }
}
``` 

Or non-recursively:

```rust
fn gcd(mut a: u32, mut b: u32) -> u32 {
 while a != 0 {
    let temp = a;
    a = b % a;
    b = temp;
  }
 b
}
``` 

Finding the GCD of two numbers is powerful, but what if we wanted to express the GCD as a combination of those numbers?

For example, what if we wanted to find two numbers $x$ and $y$ such that

$a \cdot x + b \cdot y = \gcd(a, b)$

This is called Bézout’s identity and is the basis for finding modular inverses. A modular inverse (or modular multiplicative inverse) is a number c such that

$a \cdot c \bmod b \equiv 1 $

Understanding this is foundational for algorithms in modern cryptography and forms the backbone of algorithms such as RSA, where modular arithmetic and prime factors are key. Look out for my next article on these topics. 

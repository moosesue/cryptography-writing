Greatest Common Divisor: From actor lists to elegant Python
Finding the greatest common divisor (GCD) of two integers is a simple but useful problem in mathematics. It’s usually taught in primary school and describes finding the largest whole number that divides into both numbers. Sometimes it is called finding the highest common factor (HCF). It’s also sometimes referred to as Euclid’s algorithm, named after the ancient Greek mathematician, Euclid who lived c300BC. 
A simple example would be finding the highest common factor of 28 and 35.
In primary school, you might list the factors of both of these numbers.
Factors of 28: 1, 2, 4, 7, 14, 28
Factors of 35: 1, 5, 7, 35
So it’s easy to see with a simple example that the largest factor common to both lists is 7.
Euclid formed an algorithm that can be used to find this largest factor with bigger numbers, when writing out lists might be a bit long and tedious.
The basic idea is that the largest factor doesn’t change if you replace the bigger number with the difference between it and the smaller number. This is then repeated this until the numbers are the same. This final number is the largest factor of both numbers. So, in our simple example this becomes:
35, 28 -> 28,7 -> 7, 21 -> 7, 14 -> 7,7
Mathematically, the difference between these numbers is the same as finding the remainder of dividing the larger number by the smaller number and is called the modulus. In programming, finding the difference repeatedly is equivalent to using the modulus operator % , which gives the remainder after division. If the numbers are not the same and are not zero then the same function is called by itself. This is called a recursive function.
We could write this in Python as follows:
```python
def gcd(a: int, b: int)->int:
 #set both of these variables to zero
 new\_number\_a = 0
 new\_number\_b = 0
 #check if either of the numbers passed in is zero
 if (a !=0) & (b!=0) :
 #check if a is bigger than b
 if a > b:
#if it is then set new\_number\_a to be the remainder of a #divided by b and set new\_number\_b to be b.
 new\_number\_a = a%b
 new\_number\_b = b
 else:
#if it isn’t then set new\_number\_a to be the remainder of b #divided by a and set new\_number\_b to be a.

 if a < b:
 new\_number\_a = b%a
 new\_number\_b = a
 
 #check if new\_number\_a is the same as new\_number\_b and that
 #new\_number\_b is not zero. If so, call the function again 
 #with the new numbers.
 if (new\_number\_a != new\_number\_b) & (new\_number\_b!=0):
 return gcd(new\_number\_a, new\_number\_b)
 else:
 #if not then we must be finished and so the result is 
 #new\_number\_a
 return new\_number\_a
```
```python
However, this is not a very elegant solution as it is multiple lines and calculations and the same result can be found with a lot fewer operations. 
You could actually just write the following to do exactly the same thing.
```python
def gcd(a,b):return gcd(b%a,a) if a else b
```python
In Rust you could write:
```rust
fn gcd(a: u32, b: u32) -> u32 {
 if a == 0 {
 b
 } else {
 gcd(b % a, a)
 }
}
```rust
Or
```rust
fn gcd(mut a: u32, mut b: u32) -> u32 {
 while a != 0 {
 let temp = a;
 a = b % a;
 b = temp;
 }
 b
}
```rust
Understanding GCD is foundational for algorithms in modern cryptography, including RSA and modular arithmetic.
# LosslessStringConvertable in Swift

>Rosencrantz: I don’t believe in it anyway.
Guildenstern: What?
Rosencrantz: England.
Guildenstern: Just a conspiracy of cartographers, then? 

- Tom Stoppard, *Rosencrantz and Guildenstern Are Dead*

That was basically my reaction when I learned about Swift's `LosslessStringConvertable` protocol from Oleg's blog post, TODO. It's just a conspiracy of mathematicians. Or more likely, computer programmers.

I looked into it a bit, and I'm convinced that some of the classes that conform to the protocol don't satisfy the contract. In fact, it's pretty easy to construnct instances that don't.

Let's take a look...

## The Contract
Apple's documentation describes `LosslessStringConvertable` as 
> A type that can be represented as a string in a lossless, unambiguous way.

It then goes into more detail:
> The description property of a conforming type must be a value-preserving representation of the original value. As such, it should be possible to re-create an instance from its string representation.

OK, the two moving parts of this are...
1. the "description property," and
2. the ability to "re-create an instance from its string representation."

Let's tackle the second part first, since this is defined by the protocol itself.

### Re-Creating an Instance

When it comes to "creating" (or in this case, "re-creating") an instance, the documentation shows that there's a required initializer:

`init?(String)`
>Instantiates an instance of the conforming type from a string representation.
Required.

For those who don't speak Swift, the `?` following `init` indicates that this is a *failable initializer* that returns an `Optional` value. `Optional` means that it returns a "real" value if things make sense, or `nil` if everything goes pear-shaped.  So,

```swift
let x = Int("17")
// x -> 17
```
but

```swift
let y = Int("Now is the winter of our discontent")
// y -> nil
```
That was pretty straightforward (that whole `Optional` thing will rear its head again, but we'll walk through it). 

What about the "description property?"

### Description
"Description" isn't described in any more detail in `LosslessStringConvertable`, but it inherits from CustomStringConvertable`, and *that* has a required `description` property:

> `var description: String`
A textual representation of this instance.
Required. Default implementations provided.

So, in this case, 

```swift
let s = 17.description
// s -> "17"
```

### Putting them Together
OK, given those definitions of "re-create" and "description," I think it's clear that, 

For all x where x is an instance of `LosslessStringConvertable`,
```swift
let y = (x == ClassOfX(x.description))
// y should be true.
```

So for example, if x is an `Int`,
```swift
let y = (x == Int(x.description))
// y should be true.
```

### The (Obvious?) Exception
There's an exception that I want to discuss, and then ignore from now on -  `NaN` for floating point types. Since all of our floating-point is done using we're doing IEEE 754 floating-pont values, we have to deal with the fact that...

```swift
let n = Double.nan
let y = (n == n)
// y is false
```

So 



What is that "description"property?

I worked at The MathWorks on data editing and visualization tools for over a decade, and I've written plenty of functions designed to exchange data between tools and apps as strings. In that time, I picked up a thing or two about representing floating-point values, and the promise of `LosslessStringConvertable` just sounds impossible.


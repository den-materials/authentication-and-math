# <img src="https://cloud.githubusercontent.com/assets/7833470/10899314/63829980-8188-11e5-8cdd-4ded5bcb6e36.png" height="60"> An Intro to Auth and Modular Arithmetic

<!--Hook: Raise your hand if you fully understood our authentication class a week ago.  Raise your hand if you realized that was a week ago.  Today, we're going to try a more fun approach to this, to try and put things in more real terms. -->

### Objectives:

* **Understand** the basic math concepts behind modular arithmetic
* **Apply** this concept to server authentication
* **Warm up** your brains, have fun (with MATH!)

<!--10 minutes 10:40-->

### Warm-up:  The Russian Postal Problem
Today we're going to enact a metaphor for auth inspired by [The Russian Postal Problem](http://www.jwstelly.org/BrainTeaser/Problem.php?id=14)

Form groups and try to solve the problem. (If you've seen this one already, you can give hints, but please don't give it away.)

<!----
<details>
<summary>Solution:</summary>

* Boris puts the jewel in the box with one lock and sends it to Natasha.
* Natasha puts her own lock on the box and returns it to Boris (with both locks).
* Boris removes his lock with his own key and sends it back with just Natasha's lock.
* Natasha can unlock the box with her key.

</details>
---->

<!--15 minutes 10:50-->

### An Introduction to Modular Arithmetic

![](remainders.gif)

Remember remainders from division?  That's what modular arithmetic is all about.  In mathematics, modular arithmetic is a system of arithmetic for integers, where numbers "wrap around" upon reaching a certain value, also knows as the **modulus**.

Let's see what that looks like on the white board...

<!--Main points: Start by dividing a big number like 1230 by 10, then 1233...where does the remainder go?  Now let's try a number like 7.  What about binary?  What happens when we multiply two semi-big numbers by each other?  18*30 mod 17, for instance....  Notice that we can just take the remainders off the top and multiply them together.  That's because the rest is all 0 mod 17...and 0*anything = 0. -->

<!-- 5 minutes 11:05 -->
### [Video: How does this relate to computer passwords?](http://www.wimp.com/how-encryption-works-in-your-web-browser/)

<!--10 minutes 11:15 -->

_Note: This is an excellent video, with two gotchas. First, the narrator says "forty-two" when the display shows "46" several times. (46 is correct.) Second, there is a moment when `16^54 mod 17` is converted to `3^(24*54) mod 17` without explanation. This can be simplified and proven more easily using 3^6 and 3^8.  Let's do that now..._

Suppose Alice chose `6` as her random number. She would perform the equation: 
<code>3^6 mod 17 &equiv; 15</code> and send 15 to Bob.
Suppose too that Bob chose `8` as his random number. He would perform the equation:
<code>3^8 mod 17 &equiv; 16</code>, and send 16 to Alice.

Now Alice can start with Bob's public key (16) and raise to the exponent of her secret key:
<code>16^6 mod 17 &equiv; 1</code>
Bob does the same by raising Alice's public key by *his* secret:
<code>15^8 mod 17 &equiv; 1</code>

Now they both know the password, but Eve cannot determine it, because she does not know Alice's `6` or Bob's `8`

The simplified math can be hacked in a reasonable amount of time, but if the secret key was (for example) a 40-digit hexidecimal value, it would take a long, long time.

<!--10 minutes 11:25 -->

#### Pairing Activity: Test the math
<!--(Whoever finishes first can prepare their simplified algorithm for Activity 2)-->

* Developers begin with the simplified algorithm `3^n mod 7` as the "shared secret"
* Each developer selects a random number `n`  -- this is your "secret key" -- don't share it.
* Perform the calculation `3^n mod 7` and share only the remainder. This is your "public key"
* Take your partner's public key and raise it to your secret key.
* Did you get the same, new remainder?


-----
Refer to the table below to get the math.
-----


#### `3^n mod 17` vs `3^n mod 7` Reference Table

17 and 7 are prime numbers. One of these will be our prime modulus.
The primitive root of a number is one that has no factors in common where, if you raise the root by any exponent, the modulus will return a different value, until the sequence repeats itself.

primitive <br >root | exponent | value | mod 17 | mod 7
----|:----:| ----:|----:|----:
3 | 1 | 3 | **3** | **3**
3 | 2 | 9 | 9 | 2
3 | 3 | 27 | 10 | 6
3 | 4 | 81 | 13 | 4
3 | 5 | 243 | 5 | 5
3 | 6 | 729 | 15 | 1
3 | 7 | 2,187 | 11 | **3**
3 | 8 | 6,561 | 16 | 2
3 | 9 | 19,683 | 14 | 6
3 | 10 | 59,049 | 8 | 4
3 | 11 | 177,147 | 7 | 5
3 | 12 | 531,441 | 4 | 1
3 | 13 | 1,594,323 | 12 | **3**
3 | 14 |  4,782,969 | 2 | 2
3 | 15 | 14,348,907 | 6 | 6
3 | 16 | 43,046,721 | 1 | 4
3 | 17 | 129,140,163 | **3** | 5
3 | 18 | 387,420,489 | 9 | 1
3 | 19 | 1,162,261,467 | 10 | **3**

<!--11:35 5 minutes -->

Modular math can also be illustrated with a clock:

![](mod17.png)

For positive numbers, move clockwise. (For negative numbers, move counter-clockwise.) Now we can see how <code>3^3 mod 17 &equiv; 10</code>

<!--I would love to do this, but we have no time, and it's hard to do right -->

<!--11:55 25 minutes -->

<!--#### Activity 2: Candy from a Lockbox

_NOTE: The following exercise description DOES NOT reveal the real combinations of the locks. Make sure you know the combinations before you begin._

In our version of the story, Alice (a developer) has a bunch of candy. Bob (another developer) wants Alice to send him some candy without sharing with the rest of the class. Bob has a lock box and a combination lock with a given combination. Alice has another lock with her own combination. (Alice does not know Bob's combo, and vice-versa.)

Before the exercise begins, developers playing Bob and Alice must also agree upon a shared secret--a simple mathematical formula or algorithm to decrypt each others' combinations.  For example, they can use <code>7 * n mod 100</code>. If Bob's `n` is 16, Bob will send a public key of 12.  If Alice's `n` is 42, she will send a public key of 94. Alice or Bob can then multiply these together to get a multiplier, or shared key, for their combinations.

> Challenge: What is Alice and Bob's shared key / multiplier?

Now let's ship some candy!

Bob sends his request (candy, please!) inside the locked box, with his public key written on a Post-It on the outside. This will be multiplied by the shared key that only Alice and Bob know.  Bob must pass the box around the class before it gets to Alice. The class can hypothesize and guess one combination per person. Before we begin, let's discuss a few points to get on the right track. -->

<!--For example, this is a 3-digit combo, so don't do math with very large numbers, negative numbers or decimals.-->

<!--Alice will be able to unlock the box, put in the candy and then return it to Bob with her public key.  Unfortunately, now there will be two locks!  Now the class has both public keys and everyone in the class can make two more attempts at figuring out the combinations. If it makes it back to Bob, he will be able to unlock both locks.

If anyone can crack the combination, they get to decide how to share the candy.  If no one does, Bob and Alice get to decide.

> "It's like a nerdy piñata!" -Wayne Banks, Former WDI Student

<!-- 12:20 10 minutes -->

#### Discussion:  How are these things related?

<!--* Did we figure out the combination? Any lessons on making this easier/harder?
* How would we change the math to make this more realistic?-->
* What is modular math and how does it work?
* [How does bcrypt use modular math?](https://en.wikipedia.org/wiki/Blowfish_(cipher))


#### More Math (if you're interested)
- [Here is a good explanation of modular math](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)
- [Modular arithmetic description](https://en.wikipedia.org/wiki/Modular_arithmetic)



## Licensing
All content is licensed under a CC­BY­NC­SA 4.0 license.
All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.

# <img src="https://cloud.githubusercontent.com/assets/7833470/10899314/63829980-8188-11e5-8cdd-4ded5bcb6e36.png" height="60"> An Intro to Auth and Modular Arithmetic


### Objectives:

#### Warm-up:  The Russian Postal Problem (5-10 minutes)
Today we're going to enact a metaphor for auth inspired by [The Russian Postal Problem](http://www.jwstelly.org/BrainTeaser/Problem.php?id=14)

#### Video: How does this relate to computer passwords? [Video](http://www.wimp.com/how-encryption-works-in-your-web-browser/)

#### Activity: Candy from a Lockbox (20 minutes)

In our version of the story, Alice (played by a student) has a bunch of candy. Bob (played by a different student) wants Alice to send him some candy without sharing with the rest of the class. Bob has a lock box and a combination lock with a given combination, say 240. Alice has another lock with a given combination, say 512. (Alice does not know Bob's combo, and vice-versa.)

Before the exercise begins, the students playing Bob and Alice must also agree upon a shared secret--a simple mathematical formula or algorithm to decrypt each others' combinations. Instuctors may bring a clock with a given circumference and a string of a given length, but it is not necessary. Our student volunteers could wrap the string around the clock a number of times to determine a multiplier. If the multiplier is 16, Bob will send a public key of 15 and Alice will know that Bob's combo is 15 * 16, or 240.

This is an incredibly simple algorithm, but that's what makes it fun as an in-class activity. _(If the algorithm is more complex, it will be exponentially more difficult for the class to unlock the box, which makes the exercise kind of pointless.)_

Bob sends his request inside the locked box, with public key written on a Post-It on the outside. Bob must pass the box around the class before it gets to Alice. The class can hypothesize and guess different combinations, as many times as the instructor allows. (You might limit it to 3 - 10 attempts, or let the students self-regulate.) Before they begin, you can identify a few points to get them on the right track. (For example, this is a 3-digit combo, so don't do math with very large numbers, negative numbers or decimals.)

Alice will be able to unlock the box, put in the candy and then return it to Bob with her secret key (in this example, 32). Now the class has both public keys and the class can make several more attempts at figuring out the combinations. If it makes it back to Bob, he will be able to unlock both locks.

Whatever happens in class, unlock the box and share the candy.

#### Discussion:  How are these things related? (10 minutes)

* Did the class figure it out? Did they get close?
* How would we change the math to make this more realistic?
* What is modular math and how does it work?
* How does bcrypt use modular math?


#### More Math (time permitting)
[Here is a good explanation of modular math](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)

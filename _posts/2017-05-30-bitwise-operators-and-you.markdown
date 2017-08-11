---
layout:          post
title:           "Using JavaScript’s Bitwise Operators in Real Life"
subtitle:        "Let’s pretend we’re machine code programmers!"
date:            2017-05-30 12:00:00
header-img:      "img/post-bg-bitwise.jpg"
thumbnail-img:   "img/post-thumb-bitwise.jpg"
published:       true
category:        Code
readtime:        "11 minutes"
includeSyntax:   true
includeLightbox: false
---

<p><span class='illuminated-letter'>B</span>itwise operators in JavaScript introduce a weird, wild world where <code>(12 & 3) = 0</code> and <code>(12 & 4) = 4</code>. Seriously, try it out in your console right now. I’m not lying! If you don’t know how they work precisely, read on: They might just be the solution to a programming problem you aren’t quite sure how to solve.</p>

<p>Recently a coworker asked our team how to best store and check for the presence of four independent true/false variables in an object. Let's call these attributes <code>foo1</code> through <code>foo4</code>, so its representation in JavaScript (ES6) might look like this:</p>

<pre class='brush: js'>
const myObject = {
	foo1: false,
	foo2: true,
	foo3: false,
	foo4: true
};
</pre>

<p>Pretty straightforward. However, our app needed to check for many, many combinations of these four attributes. Adding to the difficulty, we might one day add an additional attribute. So our two most obvious options to solve this were:</p>

<strong>1) Just make all possible model objects, and then do a compare in the code when needed.</strong> Like so:

<pre class='brush: js'>
const hasFoo2andFoo4 = {
	foo1: false,
	foo2: true,
	foo3: false,
	foo4: true
}

const hasFoo3andFoo4 = {
	foo1: false,
	foo2: false,
	foo3: true,
	foo4: true
}

// ...You get the idea...

// Then later in the code:
if (isEqual(myObject, hasFoo2andFoo4)) {
	// This is how we know the object only has Foo2 and Foo4
}
</pre>

<p>As you can plainly see, this sucks. We might have to construct up to 16 model objects to compare against, which feels like too much overhead for so little information. Plus, if we add another attribute in the future, it’ll <i>double the number of our model objects</i>. Clearly, this should be avoided. But our other option might’ve been worse...</p>

<strong>2) Just do checks for each individual property within the conditional blocks:</strong>

<pre class='brush: js'>
if (myObject[2] && myObject[4] && !(myObject[1] || myObject[3])) {
	// We know the object only has Foo2 and Foo4
}
</pre>

<p>Another living nightmare. We’d have to stick about a million clauses into our client-side code—which is error-prone in the first place—and then it would require a gargantuan cleanup effort if any attribute ever changed or a new one was added. So what are we to do?</p>

<p>In my overly-caffeinated, under-informed state that morning, I recognized that we were basically mimicking the permission bit-masking function that a typical UNIX filesystem used. You know, “755”, read-write-execute, “rwxr-xr-x”? Although filesystem permissions are more complex, perhaps they could be pared down and used to solve our problem. In my head I started herding hair-brained ideas on how we’d have to assign numbers to each attribute, then just add them to come up with a unique number for each state, and...—</p>

<p>Then another coworker saved me from myself. “How about instead of reinventing filesystem permissions, we just use bitwise operators?” he said. Ah yes. Those. I had some vague idea what they were—I’d used the <code>~</code> a few times over the years—but I’d never fully understood them. Fortunately, this coworker had used them on a previous project and was able to enlighten us.</p>

<p>Bitwise operators do indeed operate on the same general concept as filesystem permissions, but much more elegantly than how I imagined. Instead of operating on integers, manually adding and subtracting, bitwise operators work on the <i>bits</i> that represent each integer, letting you compare and manipulate them directly. So you can use them to manipulate a 4-bit number (or 3-bit, or 12-bit, whatever) according to its zeroes and ones, with each bit representing one of your true/false attributes. I’ll explain.</p>

<p>All integers in JavaScript (up to 9,007,199,254,740,991 in 64-bit environments) can be represented in binary. You can see what they are by calling <code>toString(2)</code> on them:</p>

<pre class='brush: js'>
(1).toString(2);
// 1

(2).toString(2);
// 10

(3).toString(2);
// 11

(4).toString(2);
// 100

// ...

(3877494).toString(2);
// 1110110010101001110110
</pre>

<p>...You get the idea. Now comes the important part. The real trick behind the whole thing is this: <i>Bitwise operators let you compare and manipulate those binary strings directly</i>. So the bitwise operator <code>&lt;&lt;</code>, which puts zeroes on the right of the binary string, will increase your integer decimal-value according to binary rules. Here’s what I mean:</p>

<pre class='brush: js'>
// Let's set `fooBar` to the number 2
let fooBar = 2;

fooBar.toString(2);
// 10 (<- this is its binary representation)

foobar = fooBar << 1; // We're inserting (1) zero at the end of fooBar's
					  // binary representation

fooBar.toString(2);
// 100

// ...so this means fooBar, in decimal form, now equals 4. Rad!
console.log(fooBar);
// 4
</pre>

<p>You might be able to see where this is going. Given <a href="https://www.w3schools.com/js/js_bitwise.asp" target="new">the full gamut of bitwise operators</a>, we can now add, subtract and compare <b>in binary</b>. In my specific example above, we can store all four of our possible attributes in a single 4-bit number, between 0000 - 1111, with each bit representing either true (1) or false (0). So you can imagine that using this schema, the binary number <code>1111</code> would mean all attributes are true, the rest are false; <code>1000</code> would mean only the fourth attribute is true, etc. (keep in mind binary counts will go right-to-left; the “first” attribute would be 1, or 0001; the “fourth” would be 1000).</p>

<p>The two most important bitwise comparison operators are “&” and “|”. Their resemblance to “&&” and “||” is intentional, but perhaps misleading. “&” will return a binary representation of the intersection of the two numbers you’re comparing, “|” returns the union. So <code>1010 & 1001</code> will return <code>1000</code>, because the leftmost <code>1</code> is the <i>only</i> bit in common between the two; <code>1010 | 1001</code> will return <code>1011</code>, because those are <i>all</i> the bits in common.</p>

<p>I’m being longwinded. Let’s just get to the damn example.</p>

<pre class='brush: js'>
// Let's define an object that needs to be checked. In the real world,
// this might come from an API response, or user interactions, or a
// form, etc. You might not know it beforehand.
const myObject = {
	foo1: false,
	foo2: true,
	foo3: false,
	foo4: true
}

// Let's also set up some constants to make code easier to read later
// on. These could obviously take many forms, or be set up in different
// ways, but I find this the most intuitive to read:
const HAS_FOO1 = 1;			// 0001
const HAS_FOO2 = 1 << 1; 	// 0010
const HAS_FOO3 = 1 << 2; 	// 0100
const HAS_FOO4 = 1 << 3; 	// 1000

// Construct your bitwise number. How you do this will depend on your
// use-case, but here's one way to do it: Checking object keys manually
// and using if statements to add attributes one at a time.
let myBitNumber = 0;

if (myObject['foo1'] === true)
	myBitNumber = myBitNumber | HAS_FOO1;	// This uses the bitwise |
											// to form a union
if (myObject['foo2'] === true)
	myBitNumber = myBitNumber | HAS_FOO2;

if (myObject['foo3'] === true)
	myBitNumber = myBitNumber | HAS_FOO3;

if (myObject['foo4'] === true)
	myBitNumber = myBitNumber | HAS_FOO4;

console.log(myBitNumber.toString(2));
// 1010

/*
 * Our bitwise number is now "1010". That's because our second and
 * fourth attributes are true.
 * Think of it this way:
 *
 * | fourth | third | second | first | <= Attribute
 * |    1   |   0   |   1    |   0   | <= True/false
 *
 */
</pre>

<p>Now, on to the tests. If you’re checking your bitwise number for attributes, there are four possible states you can check for: whether your number <b>has ONE</b> of a certain attribute, whether it <b>has ANY</b> of an array of given attributes, whether it <b>has ONLY</b> the attributes specified, or it <b>has ALL</b> of an array of attributes. Here’s a helpful <a href="https://union.io/images/repo/20170531-00--895036.png" target="new">bitwise cheat-sheet</a>, followed by some code examples:</p>

<pre class='brush: js'>
// Test whether your bit number has a single attribute. '&' ensures
// an intersection between them.
if (myBitNumber & HAS_FOO1) {
	// False, in this example
}
if (myBitNumber & HAS_FOO2) {
	// True!
}

// Test whether your bit number has ANY of the specified attributes
if (myBitNumber & (HAS_FOO1 | HAS_FOO2)) {
	// True!
}
if (myBitNumber & (HAS_FOO1 | HAS_FOO3)) {
	// False
}

// Test whether your bit number contains ONLY the specified attributes
if (myBitNumber == (HAS_FOO2 | HAS_FOO4)) {
	// True
}
if (myBitNumber == (HAS_FOO2 | HAS_FOO3 | HAS_FOO4)) {
	// False
}

// Test whether your bit number contains ALL of the given attributes.
// This is slightly tricky: the union of ATTRIBUTES can't supersede
// `myBitNumber` alone, otherwise it contains a bit that `myBitNumber`
// doesn't.
if (myBitNumber == (myBitNumber | (HAS_FOO2 | HAS_FOO4))) {
	// True
}
if (myBitNumber == (myBitNumber | (HAS_FOO2 | HAS_FOO3 | HAS_FOO4))) {
	// False
}
</pre>

<p>And that’s the quick summary. A functional example of using bitwise operators to store and compare multiple true/false attributes efficiently. It’s fairly easy to read and understand, simple to update and maintain, and if you need to edit one clause or even add another attribute, it’s not exponentially difficult.</p>

<p>And the best part is you get to deal with zeroes and ones, so if you drink enough coffee and close your eyes, for a few fleeting moments you can almost pretend you’re 1950s machine-language coder.</p>

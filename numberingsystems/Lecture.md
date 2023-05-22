# Numbering systems and bases

- Everything on your computer - the code you write, the data you use, the images on your screen - is controlled by a series of two-state switches.
- Computers don’t understand words or numbers the way humans do.
- The binary is a base 2 number system. Base 2 means only two digits—1 and 0—correspond to the on and off states your computer can understand.

## Why do computers use binary?

- The short answer: hardware and the laws of physics.
- In the early days of computing, electrical signals were much harder to precisely measure and control. 
- Easy to distinguish between an “on” state and an “off” state.
- Modern computers use what’s known as a transistor to perform calculations with binary. 

## Why only base 2

- "Why only 0 and 1? Couldn’t you add another digit?”
- To add another digit would mean we would have to distinguish between different levels —not just “off” and “on,” but also states like “on a little bit” and “on a lot.”
- We can’t use ternary logic because of how transistors are stacked in a computer—called “gates”—and how they perform math. Gates take two inputs, operate on them, and return one output.
- Binary math is way easier for a computer than anything else. 
- Boolean logic maps easily to binary systems, with True and False represented on and off. 
- Gates in your computer operate on boolean logic: they take two inputs and operate on them like AND, OR, XOR, and so on.

## Binary to decimal

- You can easily convert from binary to decimal by computing the value of 2 raised to the power of its position and then multiplying that by the value of the bit in that position.

$10010101_2 = 1*2^7+0*2^6+0*2^5+1*2^4+0*2^3+1*2^2+0*2^1+1*2^0$

$128+16+4+1$

$149_{10}$

## Decimal to binary

$149_{10}$ divided by 2; the quotient is 74; the remainder is 1

$74_{10}$ divided by 2; the quotient is 37; the remainder is 0

$37_{10}$ divided by 2; the quotient is 18; the remainder is 1

$18_{10}$ divided by 2; the quotient is 9; the remainder is 0

$9_{10}$ divided by 2; the quotient is 4; the remainder is 1

$4_{10}$ divided by 2; the quotient is 2; the remainder is 0

$2_{10}$ divided by 2; the quotient is 1; the remainder is 0

The $149_2$ is 10010101. Start with the lowest quotient and move upward, writing all the remainder.

## Hexadecimal

- Sometimes, binary representation comes with so many series of ones and zeros.
- It is convenient to group the bit patterns.
- The hexadecimal has 16 digits, each of which can represent one group of 4 bits.
- The binary to hexadecimal representation is given in the table.

| Hexadecimal digit | Four binary digits (bits) |
| ----------------- | ------------------------- |
| 0                 | 0000                      |
| 1                 | 0001                      |
| 2                 | 0010                      |
| 3                 | 0011                      |
| 4                 | 0100                      |
| 5                 | 0101                      |
| 6                 | 0110                      |
| 7                 | 0111                      |
| 8                 | 1000                      |
| 9                 | 1001                      |
| A                 | 1010                      |
| B                 | 1011                      |
| C                 | 1100                      |
| D                 | 1101                      |
| E                 | 1110                      |
| F                 | 1111                      |

### Example

Based on the above concepts, practice base conversions (without the help of the Internet, calculator, or computer). Remember, when you go for an interview, you will have (most likely) no access to electronics.

1. Convert your first and last name in hexadecimal format. For example, Tom Tom in hexadecimal is 546F6D20546F6D. Remember that the name is case-sensitive.

Hint: Find your name characters in decimal format [using an ASCII table](https://www.asciitable.com/), convert them into binary, and finally, hexadecimal. Do not forget to add a space character if you have a space in your name.  

# Data organization

## Bits, bytes, words, and double words

- Sometimes abbreviated as b (lowercase), bit is short for binary digit. It's a single unit of information with a value of either 0 or 1 (off or on, false or true, low or high). Eight bits make a byte. So, if you had two bytes (word), it would be 16 bits (2 x 8=16), and 10 bytes would be 80 bits (10 x 8=80).
- With early computer processors (e.g., 8088 and 80286), the processors were 16-bit processors, which means the processors were capable of working with 16-bit binary numbers (decimal numbers up to 65,535). Anything larger and the computer would need to break up the number into smaller pieces. Later processors were 32-bit, capable of up to 32-bit binary numbers (decimal numbers up to 4,294,967,295). Today’s computers are 64-bit, capable of up to 64-bit binary numbers (decimal numbers over 18 quintillions).

# Logical operations

- Logical or Boolean operators are often used when evaluating multiple relational expressions to return a single value.
- Three basic logical operators; AND, OR, and NOT.
- For example, if the value of user_name is “student” and the value of the score is 55, then:

| Expression             | Evaluates as |
| ---------------------- | ------------ |
| score > 100            | False        |
| user_name == "student" | True         |

## AND, OR, and NOT operator

- Relational expressions can be combined with logical operators to form more complex logic.

`User_name is "student"`

`Score is 55`

`game_over is False`

**Logical operator**

AND

**Function**

Evaluates to True when all of the relational expressions evaluate to True

**An example that evaluates to True**

`score > 50 AND game_over == False`

**An example that evaluates False**

`score > 100 AND user_name == ”student"`

---

**Logical operator**

OR

**Function**

Evaluates to True when either or both of the relational expressions evaluate to True

**An example that evaluates True**

`score > 50 OR user_name == "Terri"`

**An example that evaluates False**

`score == 100 OR game_over == True`

---

**Logical operator**

NOT

**Function**

Evaluates to True when the relational expression evaluates to False

**An example that evaluates True**

`NOT user_name == “Terri”`

**An example that evaluates False**

`NOT score > 20`

> [Review the application of logical operators in the real world](https://www.servomagazine.com/magazine/article/robotics-how-to-get-started-part-6-logical-and-bit-wise-operators)

- To ensure that the relational expressions are evaluated in the correct order, you should use parentheses (brackets) to make the order clear. 
- Relational expressions in parentheses will be evaluated first. If there are no parentheses in a relational expression, then the default order of operations or order of precedence is applied:

**Order of precedence**

- The NOT operator has the highest precedence, so it is applied first
- Then, the AND operator is applied
- Then, the OR operator is applied

### Pseudocode (AND)

```
difficulty = "hard"
score = 55
game_over = False

if not game_over then
		if difficulty == "hard" and score > 60 then
				print("Wow, you are doing great!")
		elseif (difficulty == "normal" or difficulty == "easy") and score > 40 then
				print("Good stuff, keep it up!")
		else
				print("Keep going!")
		endif
endif
```

## NAND, NOR and XOR

- There are other logical operators which you can create from the combination of AND, OR and NOT operators. For example, NAND. Many programming languages do not provide NAND and NOR as single logical operators. 
- NAND = NOT AND also evaluated as NOT (A AND B). This means that an expression evaluates to True when both operands are False or only one is False. If both operands are True, then the output is False.
- NOR = NOT OR also evaluated as NOT (A OR B). This means that an expression evaluates to True when both operands are False. If either operands are True or both are True, then the output is False.
- **Order of precedence:** If NAND and NOR are used together in the same expression, NAND will take priority over NOR since AND has higher precedence than OR.

### Pseudocode (NAND)

```
cold = True
wet = False

if cold nand wet then
		print("It is okay to go outside") //statement A
else
		print("I am going to stay inside") //statement B
endif
```

If-then-else is a conditional statement. The statement A executes if the condition is true else statement B.

### Truth table (NAND)

A table of the outputs from all possible combinations of inputs. Every logical operator has a truth table. For example, the two input truth table of NAND is:

| Input 1 (cold) | Input 2 (wet) | Output (Go outside ?)     |
| -------------- | ------------- | ------------------------- |
| True           | True          | I am going to stay inside |
| True           | False         | Its okay to go outside    |
| False          | True          | Its okay to go outside    |
| False          | False         | Its okay to go outside    |

### Truth table (NOR)

| Input 1 | Input 2 | Output |
| ------- | ------- | ------ |
| True    | True    | False  |
| True    | False   | False  |
| False   | True    | False  |
| False   | False   | True   |

- The logical XOR (eXclusive OR) operator can be used to form a Boolean expression that evaluates True when only one relational expression is True. If both relational expressions are False or both are True, then the output is False.

### Truth table (XOR)

| Input 1 | Input 2 | Output |
| ------- | ------- | ------ |
| True    | True    | False  |
| True    | False   | True   |
| False   | True    | True   |
| False   | False   | False  |

Same inputs, the output is 0; with different inputs, the output is 1.

### Properties of XOR

There are 4 very important properties of XOR that we will be using. These are formal mathematical terms, but actually, the concepts are very simple.

1. Commutative  $A \oplus B = B \oplus A$

   This is clear from the definition of XOR: it doesn’t matter which way round you order the two inputs.

2. Associative $A \oplus (B \oplus C)=(A \oplus B) \oplus C$

   This means that XOR operations can be chained together and the order doesn’t matter. If you aren’t convinced of the truth of this statement, try drawing the truth tables.

3. Identity element $A \oplus 0 = A$

   This means that any value XOR’d with zero is left unchanged.

4. Self-inverse $A \oplus A = 0$

   This means that any value XOR’d with itself gives zero. 

There are many applications of XOR. [Review the real-world applications](https://github.com/d-khan/assembly/blob/main/All%20About%20XOR.pdf)

# Bitwise operations

In computer programming, a **bitwise operation** operates on a bit string. It is a fast and simple action, basic to the higher-level arithmetic operations, and directly supported by the processor. Most bitwise operations are presented as two-operand instructions where the result replaces one of the input operands.

On simple, low-cost processors, typically, bitwise operations are substantially faster than division, several times faster than multiplication, and sometimes significantly faster than addition. While modern processors usually perform addition and multiplication just as fast as bitwise operations due to their longer instruction pipelines and other architectural design choices, bitwise operations commonly use less power because of the reduced use of resources.

### Example - bitwise NOT

The **bitwise NOT**, or **bitwise complement**, is a unary operation that performs logical negation on each bit, forming the ones' complement of the given binary value. Bits that are 0 become 1, and those that are 1 become 0. For example:

```
NOT 	0111	(decimal 7)
			1000	(decimal 8)
```

```
NOT		10101011	(decimal 171)
			01010100	(decimal 84)
```

If you perform bitwise NOT to any number, the result would be **two's complement - 1**, or $\bar x = -x -1$, where $\bar x$ is called the x bar, which represents the NOT operator.

### Example - bitwise AND

A **bitwise AND** is a binary operation that takes two equal-length binary representations and performs the logical AND operation on each pair of the corresponding bits. Thus, if both bits in the compared position are 1, the bit in the resulting binary representation is 1 (1 × 1 = 1); otherwise, the result is 0 (1 × 0 = 0 and 0 × 0 = 0).

```
		0101 (decimal 5)
AND	0011 (decimal 3)
=		0001 (decimal 1)
```

The operation may be used to determine whether a particular bit is *set* (1) or *cleared* (0). For example, given a bit pattern 0011 (decimal 3), to determine whether the second bit is set we use a bitwise AND with a bit pattern containing 1 only in the second bit:

```
		0011 (decimal 3)
AND	0010 (decimal 2)
=		0010 (decimal 2)
```

Because the result 0010 is non-zero, we know the second bit in the original pattern was set. This is often called bit masking. (By analogy, the use of masking tape covers, or masks, portions that should not be altered or portions that are not of interest. In this case, the 0 values mask the bits that are not of interest.)

The bitwise AND may be used to clear selected bits (or flags) of a register in which each bit represents an individual Boolean state. This technique efficiently stores a number of Boolean values using as little memory as possible.

For example, 0110 (decimal 6) can be considered a set of four flags, where the first and fourth flags are clear (0), and the second and third flags are set (1). The third flag may be cleared by using a bitwise AND with the pattern that has a zero only in the third bit:

```
		0110 (decimal 6)
AND	1011 (decimal 11)
=		0010 (decimal 2)
```

Because of this property, it becomes easy to check the parity of a binary number by checking the value of the lowest-valued bit. Using the example above:

```
		0110 (decimal 6)
AND	0001 (decimal 1)
=		0000 (decimal 0)
```

Because 6 AND 1 is zero, 6 is divisible by two and, therefore, even.

```
		0111 (decimal 7)
AND 0001 (decimal 1)
=		0001 (decimal 1)
```

Since 7 AND 1 is non-zero, 7 is not divisible by two; therefore, 7 is not an even number.

### Example - bitwise OR

A bitwise OR is a binary operation that takes two bit patterns of equal length and performs the logical inclusive OR operation on each pair of corresponding bits. The result in each position is 0 if both bits are 0, while otherwise the result is 1. For example:

```
		0101 (decimal 5)
OR	0011 (decimal 3)
=		0111 (decimal 7)
```

The bitwise OR may be used to set to 1 the selected bits of the register described above. For example, the fourth bit of 0010 (decimal 2) may be set by performing a bitwise OR with the pattern with only the fourth bit set:

```
		0010 (decimal 2)
OR	1000 (decimal 8)
=		1010 (decimal 10)
```

### Example - bitwise XOR

A bitwise XOR is a binary operation that takes two-bit patterns of equal length and performs the logical exclusive OR operation on each pair of corresponding bits. The result in each position is 1 if only one of the bits is 1, but it will be 0 if both are 0 or 1. In this we perform the comparison of two bits, being 1 if the two bits are different, and 0 if they are the same. For example:

```
		0101 (decimal 5)
XOR	0011 (decimal 3)
=		0110 (decimal 6)
```

The bitwise XOR may be used to invert selected bits in a register (also called toggle or flip). Any bit may be toggled by XORing it with 1. For example, given the bit pattern 0010 (decimal 2) the second and fourth bits may be toggled by a bitwise XOR with a bit pattern containing 1 in the second and fourth positions:

```
		0010 (decimal 2)
XOR	1010 (decimal 10)
=		1000 (decimal 8)
```

Assembly language programmers and optimizing compilers sometimes use XOR as a short-cut to setting the value of a register to zero. Performing XOR on a value against itself always yields zero, and on many architectures, this operation requires fewer clock cycles and memory than loading a zero value and saving it to the register.

``` assembly
mov eax,10
xor eax,eax
```

The above example is written in an assembly language, where eax register is set to 10 at line 1. At line 2, the eax register is set to 0 by performing XOR on a value against itself.

# Signed numbering system

Up until now, things have been reasonably straightforward. Now it starts to get interesting. There are a few ways to represent negative numbers in binary. In normal decimal numbers, we may place a negative sign in front of the number to indicate that it is negative. In binary, we don't have this luxury as we are limited to only 1's and 0's.

We can represent negative numbers in several ways. The simplest is to use the leftmost digit of the number as a special value to represent the sign of the number: 0 = positive, 1 = negative. For example, a value of **positive** 12 (decimal) would be written as **0**1100 in binary, but **negative** 12 (decimal) would be written as **1**1100. Notice that in this system, it is important to show the leading 0 (to indicate a positive value).

For technical reasons, a different scheme called "two's complement" is often used to represent negative numbers.

A **ones' complement system** or **ones' complement arithmetic** is a system in which negative numbers are represented by the inverse of the binary representations of their corresponding positive numbers. In such a system, a number is negated (converted from positive to negative or vice versa) by computing its ones' complement. Let's look at an example (again with 8 bits):

For sign-magnitude

- 4 would be represented as: 00000100
- -4 would be represented as: 100000100

With 1's Complement, we have

- 4 would be represented as: 00000100
- -4 would be represented as: 11111011

Many early computers, including the [UNIVAC 1101](https://en.wikipedia.org/wiki/UNIVAC_1101), [CDC 160](https://en.wikipedia.org/wiki/CDC_160), [CDC 6600](https://en.wikipedia.org/wiki/CDC_6600), the [LINC](https://en.wikipedia.org/wiki/LINC), the [PDP-1](https://en.wikipedia.org/wiki/PDP-1), and the [UNIVAC 1107](https://en.wikipedia.org/wiki/UNIVAC_1100/2200_series#1107), used one's complement arithmetic. Successors of the CDC 6600 continued to use one's complement arithmetic until the late 1980s, and the descendants of the UNIVAC 1107 (the [UNIVAC 1100/2200 series](https://en.wikipedia.org/wiki/UNIVAC_1100/2200_series)) still do, but most modern computers use two's complement.

Two's complement is a mathematical operation to reversibly convert a positive binary number into a negative binary number with an equivalent negative value, using the binary digit with the greatest place value as the sign to indicate whether the binary number is positive or negative. It is used in computer science as the most common method of representing signed (positive, negative, and zero) integers on computers and, more generally, fixed point binary values. 

Two's complement is achieved by:

- Step 1: Start with the equivalent positive number.
- Step 2: inverting (or flipping) all bits – changing every 0 to 1, and every 1 to 0;
- Step 3: Add 1 to the entire inverted number, ignoring any overflow. Failing to ignore overflow will produce the wrong value for the result.

For example, to calculate the decimal number **−6** in binary:

- Step 1: *+6* in decimal is *0110* in binary; the leftmost significant bit (the first 0) is the sign. *+6* is not *110*, because *110* in binary is *−2* in decimal. $(1*-2^2)+(1*2^2)+(0*2^0)=-2$

- Step 2: flip all bits in *0110*, giving *1001*
- Step 3: add the place value 1 to the flipped number *1001*, giving *1010*

To verify that *1010* has a value of *−6*, add the place values together but *subtract* the sign from the final calculation. Because the first significant digit is the number sign, it must be subtracted to produce the correct result: $1010 = (1*−2^3) + (0*2^2) + (1*2^1) + (0*2^0) = 1*−8 + 0 + 1*2 + 0 = −6$

# Bit shifts and rotates

You need to know some connected topics before I start discussing bit shifts and rotates.

## Bit numbering

In computing, bit numbering is the convention used to identify the bit positions in a binary number.

The least significant bit (LSb) is the bit position in a binary integer representing the binary 1s place of the integer. Similarly, the most significant bit (MSb) represents the highest-order place of the binary integer. The LSb is sometimes referred to as the low-order bit or right-most bit, due to the convention in positional notation of writing less significant digits further to the right. The MSb is similarly referred to as the high-order bit or left-most bit. In both cases, the LSb and MSb correlate directly to the least significant digit and most significant digit of a decimal integer.

### LSb example

1001010**1**	(decimal 149)
The binary representation of decimal 149, with the LSb on the right-hand side. The LSb represents a value of 1.

### MSb example

**1**0010101 	(decimal 149)

The unsigned binary representation of decimal 149. The MSb represents a value of 128

## Bit weights

Every bit position has a weight. The following bits of decimal 149 are written vertically from MSb to LSb. This assumes LSb 0-bit numbering.

```
1 -> Bit 8 -> 2^7 -> 128 -> This is MSb
0 -> Bit 7 -> 2^6 -> Since this bit is 0, 2^6 is ignored
0 -> Bit 6 -> 2^5 -> Since this bit is 0, 2^5 is ignored
1 -> Bit 5 -> 2^4 -> 16
0 -> Bit 4 -> 2^3 -> Since this bit is 0, 2^3 is ignored
1 -> Bit 3 -> 2^2 -> 4
0 -> Bit 2 -> 2^1 -> Since this bit is 0, 2^1 is ignored
1 -> Bit 1 -> 2^0 -> 1 -> This is LSb
```

Using the above bit weights, the weight of the MSb is 128. If you add all the bit weights, which are 1s, the answer will be a decimal 149. Remember, it is an unsigned decimal number or simply 149. This assumes that you are using LSb 0-bit numbering, which means the LSB bit position starts with 0.

```
										1  0  0  1  0  1  0  1
bit positions
LSb 0 numbering -> 	7  6  5  4  3  2  1  0
MSb 0 numbering ->	0  1  2  3  4  5  6  7
```

> **Note: As discussed previously, the signed decimal representation of 10010101 (the same example mentioned above) will be decimal -107**

The value of an unsigned binary integer of LSb-0 bit numbering is
$$
\sum_{i=0}^{N-1}b_i.2^i
$$
The value of an unsigned binary integer of MSb-0 bit numbering is
$$
\sum_{i=0}^{N-1}b_i.2^{N-1-i}
$$
Where $b_i$ denotes the value of the bit with the number $i$, and $N$ denotes the number of bits in total.

##  Endianness 

In computing, endianness is the order or sequence of bytes of a word of digital data in computer memory. Endianness is primarily expressed as big-endian (BE) or little-endian (LE). A big-endian system stores the most significant byte of a word at the smallest memory address and the least significant byte at the largest. A little-endian system, in contrast, stores the least-significant byte at the smallest address. Bi-endianness is a feature supported by numerous computer architectures that feature switchable endianness in data fetches and stores or for instruction fetches. Other orderings are generically called middle-endian or mixed-endian.

## Bit shifts

The bit shifts are sometimes considered bitwise operations because they treat a value as a series of bits rather than as a numerical quantity. In these operations, the digits are moved, or shifted, to the left or right. Registers in a computer processor have a fixed width, so some bits will be "shifted out" of the register at one end, while the same number of bits are "shifted in" from the other end; the differences between bit shift operators lie in how they determine the values of the shifted-in bits.

### Arithmetic shift

In an arithmetic shift, the bits that are shifted out of either end are discarded. In a left arithmetic shift, zeros are shifted in on the right; in a right arithmetic shift, the sign bit (the MSB in two's complement) is shifted in on the left, thus preserving the sign of the operand.

This example uses an 8-bit register, interpreted as two's complement:

```
   00010111 (decimal +23) LEFT-SHIFT
=  00101110 (decimal +46)
```

```
   10010111 (decimal −105) RIGHT-SHIFT
=  11001011 (decimal −53)
```

<img width="213" alt="Screen Shot 2023-04-29 at 6 42 05 AM" src="https://user-images.githubusercontent.com/11669149/235305981-87c02298-47b4-4642-9fbb-0446e3a26d0b.png">

<img width="178" alt="image" src="https://user-images.githubusercontent.com/11669149/235306016-94a72d13-9267-4315-8452-343444990296.png">

### Logical shift

In a *logical shift*, zeros are shifted in to replace the discarded bits. Therefore, the logical and arithmetic left-shifts are exactly the same.

However, as the logical right-shift inserts value 0 bits into the most significant bit, instead of copying the sign bit, it is ideal for unsigned binary numbers, while the arithmetic right-shift is ideal for signed two's complement binary numbers.

<img width="389" alt="image" src="https://user-images.githubusercontent.com/11669149/235306399-fa9db0f5-0831-4fed-b717-0640b28b3357.png">

### Circular shift

In this operation, sometimes called *rotate no carry*, the bits are "rotated" as if the left and right ends of the register were joined. The value that is shifted into the right during a left-shift is whatever value was shifted out on the left, and vice versa for a right-shift operation. This is useful if it is necessary to retain all the existing bits, 

<img width="399" alt="image" src="https://user-images.githubusercontent.com/11669149/235306478-418dbb5e-ba91-4a8d-8abb-d70e4fe145cc.png">

*Rotate through carry* is a variant of the rotate operation, where the bit shifted in (on either end) is the old value of the carry flag, and the bit shifted out (on the other end) becomes the new value of the carry flag.

<img width="395" alt="image" src="https://user-images.githubusercontent.com/11669149/235306889-7be39621-fe35-4907-942e-e15a8309c567.png">

### Application of bitwise operations

Bitwise operations are necessary particularly in lower-level programming such as device drivers, low-level graphics, communications protocol packet assembly, and decoding.

Although machines often have efficient built-in instructions for performing arithmetic and logical operations, all these operations can be performed by combining the bitwise operators and zero-testing in various ways. For example, here is a pseudocode implementation of ancient Egyptian multiplication showing how to multiply two arbitrary integers a and b (a greater than b) using only bitshifts and addition:

```
c ← 0
while b ≠ 0
    if (b and 1) ≠ 0
        c ← c + a
    left shift a by 1
    right shift b by 1
return c
```

Another example is a pseudocode implementation of addition, showing how to calculate a sum of two integers `a` and `b` using bitwise operators and zero-testing:

```
while a ≠ 0
    c ← b and a
    b ← b xor a
    left shift c by 1
    a ← c
return b
```

The following is the Python implementation of addition.

``` python
def add(a,b):
    while a != 0:
        c = a & b
        b = b ^ a
        a = c << 1
    return b
```

## Boolean algebra

Sometimes it is useful to simplify complex expressions made up of bitwise operations, for example when writing compilers. The goal of a compiler is to translate a high level programming language into the most efficient machine code possible. Boolean algebra is used to simplify complex bitwise expressions.

### AND

- `x & y = y & x`
- `x & (y & z) = (x & y) & z`
- `x & 0xFFFF = x`
- `x & 0 = 0`
- `x & x = x`

### OR

- `x | y = y | x`
- `x | (y | z) = (x | y) | z`
- `x | 0 = x`
- `x | 0xFFFF = 0xFFFF`
- `x | x = x`

### NOT

- `~(~x) = x`

### XOR

- `x ^ y = y ^ x`
- `x ^ (y ^ z) = (x ^ y) ^ z`
- `x ^ 0 = x`
- `x ^ y ^ y = x`
- `x ^ x = 0`
- `x ^ 0xFFFF = ~x`

Additionally, XOR can be composed using the 3 basic operations (AND, OR, NOT)

- `a ^ b = (a | b) & (~a | ~b)`
- `a ^ b = (a & ~b) | (~a & b)`

### Others

- `x | (x & y) = x`
- `x & (x | y) = x`
- `~(x | y) = ~x & ~y`
- `~(x & y) = ~x | ~y`
- `x | (y & z) = (x | y) & (x | z)`
- `x & (y | z) = (x & y) | (x & z)`
- `x & (y ^ z) = (x & y) ^ (x & z)`
- `x + y = (x ^ y) + ((x & y) << 1)`
- `x - y = ~(~x + y)`

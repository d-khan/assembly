# Boolean algebra

Before discussing Boolean algebra, I need to explain some related content.

## Gates

Building complex circuits from transistors is hard. In 1938, Claude Shannon described how switching relays (a type of switch) could implement logic functions. Today logic functions are implemented using transistors based on his work. Common **logic functions** include AND, OR, and NOT.

A **logic gate** (or **gate**) is a transistor circuit that implements a logic function. The usefulness of gates will be shown later.

### NOT gate (also called Inverter)

A **NOT** gate outputs 1 if the gate's input is 0, and outputs 0 if the input is 1. A NOT gate is also called an **inverter**.

<img width="181" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/db1cbea5-7e45-43e7-a456-494331b74777">

### AND gate

An **AND** gate outputs 1 only if both the gate's inputs are 1's. The following transistor circuit implements an AND gate.

<img width="190" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/ca4aa137-2823-4621-82a6-3c2cadfea707">

### OR gate

An **OR** gate outputs 1 if either, or both, of the gate's inputs is a 1. The following transistor circuit implements an OR gate.

<img width="190" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/0ae31b6d-a6c7-4692-87b2-889d75279a84">

The following is the summary of NOT, AND and OR gates.

<img width="489" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/3e401de0-d82b-49fd-9171-a2238c9fdc94">

### NAND/NOR

A **NAND** gate is the opposite (the NOT, hence the "N") of an AND gate, outputting 0 if all inputs are 1s; else the output is 1.

<img width="365" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/937da7fe-ae02-48ec-aea8-3b915988ab65">

NAND gates are popular due to having a simpler CMOS transistor circuit implementation than AND gates: Recall that an AND gate is built from a NAND transistor circuit followed by a NOT circuit.

Furthermore, NAND gates are popular due to being a universal gate. A **universal gate** is a single gate type that can implement any combinational circuit. NAND can implement NOT, AND, and OR, as shown below, and is thus universal.

<img width="622" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/c3374846-40f7-404f-968d-9c5e622e15c6">

1. NAND can implement NOT. If input a is fed to both inputs of a 2-input NAND gate, the output is (aa)' = a' + a' (DeMorgan's Law) = a'.
2. NAND can implement AND. A 2-input NAND (ab)' followed by a NOT (also implemented with a 2-input NAND) yields ((ab)')' = (ab)'' = ab.
3. NAND can implement OR. A two-input NAND with NOTs at each input yields is (a'b')' = a'' + b'' (DeMorgan's Law) = a + b.
4. Because NAND can implement NOT, AND, and OR, then any circuit can be implemented with just NANDs. NAND is thus a "universal gate".

**Note: DeMorgan's law is discussed later**

NAND being a universal gate enables chip makers to pre-fabricate a chip consisting of millions of NAND gates. Any circuit of NAND gates can be implemented simply by adding wires. Pre-fabricating the chip with AND, OR, and NOT gates would involve complexities like deciding how many of each gate to pre-fabricate, and where to place each gate type. Using NAND is much simpler.

A chip with pre-fabricated gates is sometimes called a **gate-array ASIC**. **ASIC** is short for Application-Specific Integrated Circuit.

Converting an AND/OR/NOT circuit to a NAND-only circuit enables implementation using fewer transistors as well as enables implementation on a gate-array ASIC. The conversion can be done simply by replacing each AND, OR, and NOT gate by the equivalent structure of NAND gates, then removing double-inversions.

### NOR

A **NOR** gate is the opposite of an OR gate, outputting 0 if any of the inputs are 1s; else the output is 1.

A discussion analogous to the above NAND discussion exists for NOR. Such discussion is omitted here. Briefly, NOR's transistor structure is simpler than OR's. NOR is also a universal gate. NOT: (a + a)' = a'a' = a' (NOR with inputs tied together). OR: ((a + b)')' = (a + b)'' = a + b (NOR followed by NOT). AND: (a' + b')' = a''b'' = ab (NOR with each input NOTed).

<img width="316" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/9fb755ca-282f-4d67-ae40-7a8abea4a25e">

## Boolean algebra

In 1847, mathematician **George Boole** developed an algebra to capture human logic as mathematical equations. A later section will show how Boolean algebra became the foundation of digital circuit design.

In algebra, a **variable** is a symbol that represents a value. **Boolean algebra** is an algebra whose only values are true or false, and whose operators are AND, OR, and NOT. AND, OR, and NOT are known as **logic operators**.

<img width="668" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/b81f38c4-2776-4070-bfbd-f0a23cca732c">

> A Boolean expression is evaluated by evaluating parts and combining. NOT is evaluated first. AND is evaluated before OR.

> Note: Mathematicians use symbols like ∧, ∨, and ¬ for AND, OR, and NOT, respectively. This section uses the words for simple understanding; later sections use common digital-designer shorthand notation.

## Boolean equations

Boolean algebra was developed in the 1800s for purposes unrelated to digital circuits. In 1938, Claude Shannon applied Boolean algebra to design digital circuits. Previously, designing circuits directly as switches were hard and error-prone. Shannon showed that building and using logic gates (AND/OR/NOT) allowed use of Boolean algebra's properties to more easily and correctly design complex circuits.

In digital circuits, 1 (the high voltage value) is Boolean algebra's true, and 0 is false.

A **Boolean equation** has a Boolean variable (left), an equal sign, and a Boolean expression (right), defining the left variable's value based on the right variables' values. A Boolean equation can describe a digital circuit, with the output on the left and the inputs on the right.

<img width="646" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/9414d35c-ca32-4793-a1e0-95e3a0e30dc8">

## Boolean functions

In Boolean algebra, a **function** is a relation of inputs' values to an output's values. A function can be described in various ways:

- As English: When inputs a, b are both 1's, the output y is 1. Else, y is 0.
- As an equation: y = ab
- As a table:

| a    | b    | y    |
| ---- | ---- | ---- |
| 0    | 0    | 0    |
| 0    | 1    | 0    |
| 1    | 0    | 0    |
| 1    | 1    | 1    |

- As a circuit, as a drawing, a K-map (introduced later), etc.

<img width="960" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/66cdd550-437c-41a4-838b-40165256dd68">

## Timing diagrams

A **timing diagram** graphically shows a circuit's output values for given input values that change over time. Each signal (input or output) name is listed on the left. Time proceeds to the right. Each signal is drawn as a high line (1) or a low line (0).

<img width="281" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/b80828a9-3f0b-45ba-92ad-fa323ee093e1">

1. If a = 0 and b = 0, then y = 0.
2. If a = 1 and b = 0, then y = 0.
3. If a = 0 and b = 1, then y = 0.
4. If a = 1 and b = 1, then y = 1.

## Equations to circuits

An equation is one way to represent a Boolean function. Another way is using a circuit. An equation can be converted to a circuit by converting each operation to a gate. Conversion is done first for items within parentheses. In a term like cd', NOT is converted before AND or OR. Converting behavior (like an equation) to a circuit is called **design**.

<img width="352" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/cee3d767-8e43-450e-980c-ed581cfb8eee">

1. Convert inside parentheses first.
2. Convert NOT before converting AND (or OR).
3. Convert AND.

### Example

Cars have airbags that deploy during an accident to reduce injuries to occupants. Airbags can harm kids, and aren't needed for non-human objects. Thus, cars have sensors to help detect whether an airbag should be enabled by a large enough human being seated. In one car, a seat back sensor detects a heartbeat (h = 1). A seat bottom sensor indicates if over 60 pounds is detected (w = 1). A switch can be used to manually disable the airbags (d = 1). An output e indicates that the airbag is enabled (e = 1).

A designer specifies the system as: $e = hwd'$ (heartbeat detected, and enabled if weight over 60, and not manually disabled).

<img width="519" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/0df09cc0-a5c4-4751-be6d-4619cf1d6e9a">

## Circuits to equations

A circuit can be converted to an equation. Starting from the inputs, the process replaces gates by terms while moving towards the output, labeling gate outputs along the way. Converting a circuit to behavior (like an equation) is called **analysis**.

<img width="387" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/57b43fa2-5e35-405f-9bb3-b92627e50101">

1. Start from inputs, and replace gate by term.
2. Still, at inputs, replace gate by term.
3. Moving towards output, convert gate to term, involving earlier terms.
4. Write the final equation.

A circuit whose output value is determined solely by the present *combination* of input values is called a **combinational circuit**. A combinational circuit is also called **combinational logic**.

A circuit whose output values may depend on the past *sequence* of input values, and not just the present input values, is called a **sequential circuit**.

The following will show the circuit drawing conventions.

<img width="687" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/5764f36b-0408-4734-b52b-ed7c911a880f">

## Basic properties of Boolean algebra

The benefit of building circuits from logic gates, rather than directly from transistors, becomes clear after learning some basic properties of Boolean algebra.

| Property            | Name               | Description                                                  |
| ------------------- | ------------------ | ------------------------------------------------------------ |
| $a(b+c)=ab+ac$      | Distributive (AND) | Same as multiplication in regular algebra                    |
| $a+(bc)=(a+b)(a+c)$ | Distributive (OR)  | Different from regular algebra                               |
| $a+a'=1$            | Complement (OR)   | (AND) Clearly one of a, a' must be 0   1 + 0 = 1     |
| $aa'=0$             | Complement (AND)    | (AND) Clearly one of a, a' must be 1  1 + 0 = 0 + 1 = 1       |
| $a.1=a$             | Identity (AND)      | (OR) Result of a + 0 is always a's value  *0* + 0 = *0*   *1* + 0 = *1* |
| $a+0=a$             | Identity (OR)     | (AND) Result of a · 1 is always a's value   *0* · 1 = *0*  *1* · 1 = *1* |
| $ab=ba$             | Commutative (AND)  | Variable order does not matter. Good practice is to sort variables alphabetically. |
| $a+b=b+a$           | Commutative (OR)   | Variable order does not matter. Good practice is to sort variables alphabetically. |
| $ab(c)=a(bc)$       | Associative        | Same as regular algebra                                      |
| $(a+b)+c=a+(b+c)$   | Associative        | Same as regular algebra                                      |
| $a+1=1$             | Null elements      | Result doesn't depend on the value of a.                     |
| $a.0=0$             | Null elements      | Result doesn't depend on the value of a.                     |
| $a+a=a$; $aa=a$     | Idempotent         | Duplicate values can be removed.                             |
| $a.a=a$             | Idempotent         | Duplicate values can be removed.                             |
| $(a')'=a$           | Involution         | $(0')' = (1)' = 0$<br/>$(1')' = (0)' = 1$                    |
| $(a'+ab)=a'+b$      | Absorption law     |                                                              |
| $(a+a.b)=a$         | Absorption law     |                                                              |
| $(a'+ab)=a'+b$      | Absorption law     |                                                              |
| $a(a'+b)=a.b$       | Absorption law     |                                                              |
| $(ab)'=a'+b'$       | DeMorgan's Law     |                                                              |
| $(a+b)'=a'b'$       | DeMorgan's Law     |                                                              |

> The properties of Boolean algebra are useful to simplify an equation, yielding a simpler circuit

### Example

Lets say you have the following equation:

$s=un+un'$

The circuit looks like this:

<img width="260" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/d03c931b-ac8d-4977-aa26-a55d216c43be">

The simplification steps involved the following:

$s=un+un'$

$s=u(n+n')$ Distributive (in reverse)

$s=u(1)$ Complement

$s=u$ Identity

After applying properties of Boolean algebra to equation, a circuit becomes so simple (just a wire)

## Sum of products form

Circuits are commonly designed by creating a simplified expression in sum-of-products form, then converting to a simple circuit.

A **product term** is an ANDing of (one or more) variables, like ab'c. A product term is sometimes called just a *product* or just a *term*. An expression in **sum-of-products** form consists solely of an ORing of product terms, like ab'c + ab.

Due to similarities with regular algebra, convention uses the word "product" for AND and "sum" for OR; hence the name "sum-of-products". But AND is not really multiplication (product), and OR is not really addition (sum).

### Example

A sum-of-products equation can be easily converted to a circuit, consisting of a column of AND gates (one gate per product term), followed by an OR gate, which is known as a **two-level circuit**. (The NOT gates preceding the AND gates aren't considered a level).

<img width="692" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/fc5b3fd6-f1a2-4bcc-9c13-82ada9e6a446">

a) $y=efg+e'f$

b) $y=fg+e'$

c) $y=e'f'+ef$

d) $y=f+g$

### Example - Interrupt logic component

A processor executes computer programs. Various devices (like keyboards or USB ports) surrounding a processor may request the processor to execute a sub-program on behalf of that device, a request known as an **interrupt**. Devices may be in two categories, low-priority and high-priority, and the processor may disable either category or both.

- Low-priority: keyboard (k = 1), mouse (m = 1), USB port (u = 1). Disable all: p = 1.
- High-priority: network interface (n = 1), battery backup (b = 1). Disable all: q = 1.

An interrupt logic component determines whether interrupt requests from devices result in an actual interrupt to the processor (r = 1).

<img width="453" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/3d0703ec-131f-4d02-8f22-c196d8144d47">

## Sum of midterms form

Different equations may represent the same function. Ex: $y = a + b$, and $y = a + a'b$, represent the same function. The sameness is not obvious, so a standard equation form is desirable.



- A **canonical form** of a Boolean equation is a standard equation form for a function.
- **Sum-of-minterms** form is a canonical form of a Boolean equation where the right-side expression is a sum-of-products with each product a unique minterm.
- A **minterm** is a product term having exactly one literal for every function variable.
- A **literal** is a variable appearance, in true or complemented form, in an expression, such as b, or b'.

For a function of variables a and b, $y = ab + a'b + a'b'$ is in sum-of-minterms form, but $y = ab + a'$ is not because the second product term is missing variable b.

### Transforming to sum of minterms

A sum-of-products equation can be transformed to sum-of-minterms by multiplying each product term by (v + v') for any missing variable v to create minterm (removing redundant minterms). v + v' is 1, so multiplying a term by (v + v') doesn't change a product term's functionality. For example,

$y=ab+a'$ (sum of products but not sum of minterms)

$y=ab+a'(b+b')$ becomes $y=ab+a'b+a'b'$ (sum of minterms)

An equation not initially in sum-of-products form can first be multiplied out. Thus, transforming an equation to sum-of-minterms is done by:

- Initially multiplying out to sum-of-products
- Transform each product term to a minterm
- Remove redundant minterms

### Example - Transforming to sum-of-minterms

Given variables a, b, c. Convert $y = a(b + bc')$ to sum-of-minterms.

$y=a(b+bc')$

$y=ab+abc'$

$y=ab(1)+abc'$

$y=ab(c+c')+abc'$

$y=abc+abc'+abc'$ (remove redundant term)

$y=abc+abc'$

1. Given $y = a(b + bc')$, the first step is to multiply out into sum-of-products form (if not already in sum-of-products form), yielding $y = ab + abc'$.
2. The next step is to transform each term into a minterm. For ab, the identity property can be used to obtain ab(1).
3. The complement property can be used to transform ab(1) to ab(c + c').
4. ab(c + c') can be multiplied out to become abc + abc', both of which are minterms.
5. Duplicate terms should be removed. So $y = abc + abc' + abc'$ becomes $y = abc + abc'$. The equation is now in sum-of-minterms form.

### Example - Determining if two equations represent the same function

Because sum-of-minterms is canonical, one can determine whether two equations represent the same function by transforming each to sum-of-minterms equations and checking if the equations are the same.

<img width="362" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/5ba966fe-9eae-4696-a197-fea690e7ce0b">

The two sum-of-minterm equations are identical. Thus, the original two equations both represent the same function.

## Truth tables

A Boolean function can be represented in various ways, like an equation, a circuit, or a truth table. A **truth table** lists all possible variable value combinations on the left, and lists the function's value for each combination on the right. Each row corresponds to a possible minterm. Generating all combinations is done by counting up in binary.

Note: Minterms are sometimes written as m0, m1, ..., indicating their row's decimal equivalent: a'b'c' is 000 or m0, a'b'c is 001 or m1, etc..

A function with N variables will have a truth table with 2N rows:

- 2 variables yields $2^2$=4 rows
- 3 variables yields $2^3$=8 rows
- 4 variables yields $2^4$=16 rows, (and so on)

<img width="434" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/6990bcdd-2e9f-488d-93fd-af23120c7773">

1. A truth table lists on the left all possible variable value combinations (meaning all possible minterms). For a, b, possible combinations are 00, 01, 10, 11.
2. Note that the combinations are obtained by counting up in binary. Each row corresponds to a minterm.
3. For a given function, a truth table lists on the right for which rows (variable value combinations) that the output should be 1. Other rows get 0's.
4. A 3-input function's truth table will have $2^3$ or 8 rows. A 4-input would have $2^4$ or 16 rows, and so on.

### Example - converting a truth table to an equation

A function captured as a truth table can be transformed to a sum-of-minterms equation by summing the minterms in rows having a 1. That equation can then be converted to a circuit.

<img width="650" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/aa7294e9-e2d9-48d3-a5b8-0cad521d0b86">

1. A function may be captured as a truth table. Here, f is 1 for a'bc or abc'.
2. A truth table can be converted to an equation by summing the minterms for each row having a 1.
3. The equation can easily be converted to a two-level circuit.

## Two-level simplification

**Logic simplification** (also referred to as **logic minimization**) means to simplify a Boolean expression before converting to a circuit to yield a smaller circuit.

### Example - Simplifying an expression before converting to a circuit.

<img width="617" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/0449b851-3d5f-4b0a-b55f-3e7597dc51bd">

1. A system activates a ringer (r = 1) if motion sensed (a = 1) and daylight detected (b = 1) and no clerk (c = 0), or motion and no daylight and no clerk: $r = abc' + ab'c'$
2. The expression can be simplified to $ac'(b + b')$ (distributive), then $ac'(1)$ (complement), and finally $ac'$ (identity).
3. The circuit for $ac'$ is much simpler than for $abc' + ab'c'$.

The algebraic simplification process can be hard to do by hand.

For example:

$ab+a'$

$ab+a'(b+b')$

$ab+a'b+a'b'$

$ab+a'b+a'b+a'b'$

$(a+a')b+a'(b+b')$

$(1)b+a'(1)$

$a'+b$

1. Simplifying algebraically can be hard. First a designer converts to sum-of-minterms form.
2. Next the designer must create i(j + j') opportunities by replicating a term. The need for such replication may not be obvious.
3. Then the designer must apply i(j + j') simplifications. Again, the places where i(j + j') can be applied aren't obvious. And every step is prone to error.

## K-maps

A **K-map** is a graphical function representation that eases the simplification process for expressions involving a few variables, by adjacently placing minterms that differ in exactly one variable. K-map is short for **Karnaugh map**. "Map" is used like how a country map lays out cities next to each other. A K-map lays out minterms instead.

A K-map lays out possible minterms as adjacent cells (boxes). Adjacent minterm cells differ by exactly one variable. Each function minterm cell gets a 1; other cells get 0.

A K-map is a reoriented truth table.

$y=a'b'+ab'$

|      | 0      | 1     |
| ---- | ------ | ----- |
| 0    | $a'b'$ | $a'b$ |
| 1    | $ab'$  | $ab$  |

### Simplifying an expression with a K-map

Because adjacent minterm cells differ in exactly one variable, a K-map's key benefit is to make $i(j + j')$ simplification opportunities obvious: Adjacent 1's are an $i(j + j')$ opportunity. Circling two adjacent 1's graphically represents the algebraic simplification $i(j + j') = i(1) = i$. After drawing such a circle, a designer can write a product term with the differing variable omitted.

#### Example-1

Simplify $y=ab'+ab$

Using K-map, locate the terms of $ab'+ab$ in the table below.

|      | 0      | 1     |
| ---- | ------ | ----- |
| 0    | $a'b'$ | $a'b$ |
| 1    | $ab'$  | $ab$  |

As you see, $ab'$ and $ab$ are found at the bottom row in the table above.

<img width="255" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/806ecac0-04d1-47d0-a196-f41b1826121e">

1. Given a sum-of-minterms equation, a designer can just write 1's in the appropriate K-map cells (like for a truth table's rows). $y = ab' + ab$ yields 1's in the bottom two cells.
2. Adjacent 1's are an i(j + j') simplification opportunity. Algebraically, the circle represents $ab' + ab = a(b' + b) = a(1) = a$.
3. A designer need not write expressions. Instead, after drawing the circle, the designer eliminates the differing variable. Here b differs, a stays 1, so the circle's expression is a.

**The answer is a**

#### Example-2

Simplify $y=ab+a'b+a'b'$

<img width="281" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/a1f6bd5b-d115-4da6-9a3c-bd8889923a8d">

1. Given a sum-of-minterms equation $y = ab + a'b + a'b'$, a designer places 1's in the three cells corresponding to those three minterms.
2. The designer draws a circle around the top two 1's. For that circle, a = 0, and b differs, so the circle represents a'.
3. A second circle around the right two 1's has b = 1, and a differs, so represents b. Note that the 1 for minterm a'b is circled twice, which is like replicating a'b algebraically.
4. Drawing K-map circles is easier than algebraically simplifying. The designer just draws the two circles, and writes a term for each, so $y = a' + b$.

**Rules for simplifying a sum-of-minterms expression with a K-map.**

- Rule 1: *Cover every 1* at least once using circles. Add circle's term to expression.
- Rule 2: *Use fewest and largest circles* possible, to achieve simplest expression.

### 3 variable K-map

A K-map for three variables has two variables across the top. For adjacent columns to differ in only one variable, note that the columns don't count up in binary (00, 01, 10, 11), but rather are 00, 01, 11, 10. Cells on the far left and far right also differ by one variable so are also "adjacent"; the K-map wraps like a bracelet.

#### Example-1

$y=ab'c'+ab'c+a'bc+a'bc'$

<img width="476" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/a2b5168b-d7f8-4427-9913-a463fd7a1c07">

1. A 3-variable K-map has 8 cells: Four columns for bc (00, 01, 11, 10) and two rows for a (0, 1). Note the last two columns are NOT 10, 11 (counting up in binary).
2. Like a truth table, each cell represents a possible minterm.
3. Adjacent cells (including left-right) differ in one variable.
4. Like a truth table, a designer inserts 1's in the K-map to represent a function's minterms. The four terms in $y = ab'c' + ab'c + a'bc + a'bc'$ yield four 1's in the K-map.

<img width="589" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/9127b524-6335-4d6c-95bf-2f7b893f7145">

1. The designer first places 1's in the K-map for minterms. For y = ab'c' + ab'c + a'bc + a'bc', four 1's are placed.
2. An adjacent pair of 1's represents an i(j + j') simplification opportunity. The designer circles the two 1's for ab'c', ab'c. Those cells differ in c, yielding ab'.
3. The designer also circles the two 1's for minterms a'bc, a'bc'. Those cells differ in c, yielding a'b.
4. The designer adds the resulting terms to the simplified equation for y, yielding y = ab' + a'b.
5. The algebraic simplifications were shown just to illustrate what each circle represented; the designer never writes those equations.

#### Example-2

A circle may encompass four adjacent 1's, which removes two variables rather than just one.

<img width="559" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/55b1f8bd-39a9-4732-b28f-3f56a2168444">

1. Circling four 1's removes two variables. For y = ab'c' + ab'c + abc + abc', the 3-variable K-map has 1's in all four bottom cells. The designer circles those four 1's.
2. Intuitively, all b c combinations appears in that circle (b'c', b'c, bc, bc'), so one MUST be true.
3. Algebraically, a is factored out, yielding a(b'c' + b'c + bc + bc'). Then additional factoring yields a(b'(c'+c) + b(c+c')), which is a(b'(1) + b(1)) = a(b' + b) = a(1) = a.
4. Allowed 4-cell circle shapes are a 1x4, or 2x2. An L shape does not have a corresponding algebraic simplification, so is not allowed.

### 4 variable K-map

<img width="404" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/0c5a2eec-1ede-4d91-808b-8d4bcbf1809b">

**(J)**

Variables b and c differ, so they can be removed.
$a'b'c'd' + a'bc'd' + a'b'cd' + a'bcd'$
$a'c'd'(b' + b) + a'cd'(b' + b)$
$a'c'd' + a'cd'$
$a'd'(c' + c)$
$a'd'$

**(K)**

Variables c and d differ, so they can be removed.
$abc'd' + abc'd + abcd + abcd'$
$abc'(d' + d) + abc(d + d')$
$abc' + abc$
$ab(c' + c)$
$ab$

**(M)**

Variables b and c differ, so they can be removed.
$ab'c'd + ab'cd + abc'd + abcd$
$ab'd(c'+c) + abd(c'+c)$
$ab'd + abd = ad(b' + b)$
$ad$

**(N)**

Variables a, b, and d differ, so they can be removed.
$a'b'cd + a'b'cd' + a'bcd + a'bcd' + abcd + abcd' + ab'cd + ab'cd'$
$a'b'c(d + d') + a'bc(d + d') + abc(d + d') + ab'c(d + d')$
$a'b'c + a'bc + abc + ab'c$
$a'c(b' + b) + ac(b + b')$
$a'c + ac$
$c(a' + a)$
$c$

## DeMorgan's Law

**DeMorgan's Law** is a Boolean algebra property for complementing an expression, coming in two forms: (a + b)' = a'b', and (ab)' = a' + b'. Each literal is complemented, and ANDs / ORs swap.

<img width="669" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/f375e478-8eb7-49c1-9d6b-9658562a5e92">

### Example - Plane doors

<img width="628" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/e40d39f8-d853-4647-9f4c-3b6e8f8a68f3">

1. A plane can take off if both doors are closed (b = 1 and c = 1). That behavior captured as an equation is bc.
2. A warning light should illuminate (y = 1) if NOT both doors are closed. The equation is $y = (bc)'$, which is just the opposite of bc.
3. A designer can apply DeMorgan's Law to convert the equation to sum-of-products: $y = (bc)' = b' + c'$.
4. The meaning is intuitive: "NOT both doors closed" means the same as "Either door is open".

> DeMorgan's Law is not just used in digital design, but also by computer programmers. Computer programs use expressions to control decisions. Ex: A program may proceed as long as the input is not 3 or 5. The programmer may write: If NOT( x==3 OR x==5 ) then proceed.
>
> To simplify the expression, the programmer may apply DeMorgan's Law: If ( x != 3 AND x != 5) then proceed. (!= means not equal). The NOT was applied to the two items (so == became != in two places), and the OR was changed to AND. The resulting expression may be simpler to read.

## Sequential circuits

A **sequential circuit**'s output is dependent on the present and the past *sequence* of input values, which necessarily means the circuit stores at least one bit. In contrast, a **combinational circuit**'s output is dependent only on the present *combination* of input values.

The following system stores a bit to control a lamp.

<img width="600" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/1886154d-a64d-4e1b-8deb-3c8372f77eca">

1. The circuit stores a bit that controls the lamp: 1 illuminates, 0 doesn't.
2. The circuit remembers that the off button was pressed, and stays 0 after release.
3. The circuit remembers that the on button was pressed, and stays 1 after release.

### SR latch

The simplest circuit for storing a bit is called a **latch**. An **SR latch** stores one bit, with an input s to set the latch to 1, an input r to reset the latch to 0, and with the stored bit appearing on output q. S and s are for "set", and R and r for "reset".

Below is a circuit for an SR latch. Reminder: NOR outputs 0 if any input is 1.

<img width="588" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/7dad0913-2963-4ba1-a426-a515e4052306">

1. An SR latch can be designed with two cross-coupled NOR gates (the output of each is an input to the other), with s input to top gate and r input to the bottom (whose output is q).
2. When s = 1, r = 0, the top gate outputs 0 (1 NOR anything is 0). The bottom gate outputs 1 (because both inputs are 0's). Thus q is 1; the latch has been "set".
3. When s returns to 0, q remains 1. The top gate still has a 1 input (from the bottom gate), and 1 NOR anything is 0. Bottom gate still has both inputs 0's, so outputs 1.
4. Now if r = 1 and s = 0, the bottom gate outputs 0 (1 NOR anything is 0), so q = 0. (The top gate's inputs are both 0's, so the gate outputs 1). The latch has been "reset".
5. When r returns to 0, the bottom gate still has a 1 input (from the top gate), so q remains 0. The top gate still has both inputs as 0's, so outputs 1.

| s    | r    | q                     |
| ---- | ---- | --------------------- |
| 0    | 0    | Previously-stored bit |
| 0    | 1    | 0 (Reset)             |
| 1    | 0    | 1 (Set)               |
| 1    | 1    | Unknown               |

**SR latch behavior**

s = 1 and r = 1 causes a problem. The 1's cause the NOR gates to output 0's. When s and r return to 0's, then both gates output 1's. Those 1's propagate back to the gate inputs, causing the gates to output 0's. Those 0's propagate back, causing 1's again. No bit was stored, and instead the latch oscillates. **Oscillate** means to change from 0 to 1 to 0 to 1 repeatedly. Due to different gate and wire delays, eventually the latch will settle into a stored 0 or 1, but which one is unknown.

<img width="582" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/4e28188f-81f2-494f-b7cd-ac3da5152479">

1. In an SR latch, s =1 and r = 1 may cause a problem. Each NOR gate has a 1 input so outputs 0.
2. A problem occurs when input sr change from 11 to 00. At that moment, each NOR gate has two 0's input, so each NOR gate's output changes from 0 to 1.
3. Those NOR gates' output 1's propagate back to the NOR gates' inputs. Each NOR gate now has a 1 input, so the gate's output changes to 0.
4. The output q oscillates between 0 and 1. Because gates/wires delays vary slightly, eventually q will settle at either 0 or 1, but which one is unknown.

> **SR latches are uncommon**
>
> SR latches were previously common when gates were expensive. But with gates far cheaper (and smaller) today, the more robust D latch (discussed later), which extends an SR latch, is more common.



## Clocks, D latch, D flip-flops, and registers

A D latch can store a bit value, either 1 or 0. When its Enable pin is HIGH, the value on the D pin will be stored on the Q output. It builds upon the design of the S-R latch with a few added logic gates. You can see a D Latch circuit based on the S-R latch built with NAND gates below:

<img width="560" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/bc1ad743-ee5d-4aec-a30c-8c0f879e919b">

The inverter on the input makes sure the S and the R inputs are always opposites, to avoid the invalid state of both being 1. The two NAND gates create a new input, E (Enable), that lets you control when you want to change the output to whatever is on the D input.

This means that the output Q can only change when the enable signal is 1. If it’s 0, the output is unaffected by any changes on D.

> The D Latch can also be used to introduce delay in timing circuits, as a buffer, or for sampling data at specific intervals.

The terms *latch* and *flip flop* are sometimes incorrectly used as synonyms since both can store a bit (1 or 0) at their outputs.

While a *latch* can change its output at any time as long as it’s enabled, a *flip flop* is an edge-triggered device that needs a clock transition to change its output.

To build a D Flip Flop, you’ll need two D latches, like this:

<img width="744" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/ab11aa6e-1ee2-4f4f-acda-1cb27d661ef9">



Most digital circuits use an oscillating signal called a **clock** signal to control when to store bits (for reasons that will be clear later). Rather than bits being stored while an enable signal is high, bits are stored only at a clock's **rising edge**: The instant a clock signal changes from 0 to 1.

- A **clock cycle** is the time between two rising edges, that time being the **clock period**.
- **Clock frequency** is the cycles per second, in units of **hertz** (**Hz**) meaning cycles/second. Ex: A 1 MHz clock has 1 million cycles per second. Frequency is the inverse of period. Ex: A 1 microsecond (0.000001) period yields a frequency of 1 MHz (because 1 / 0.000001 s = 1,000,000 Hz).

<img width="576" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/970376d4-b4cd-473b-be06-1ecc1d0d4fc3">

1. Sequential circuits use a clock to synchronize storing of bits to only occur on rising clock edges. Such synchronization greatly simplifies sequential circuit design.
2. One clock cycle is one rising edge to the next. Clock period is the time for one cycle. Frequency is 1 / period.
3. A special device called an oscillator generates a clock at a specific frequency. On a component, a small triangle indicates the clock input.

Bits are usually stored in groups. A **register** is a circuit that stores a group of bits; a 3-bit register stores three bits. On a rising clock edge, all bits are stored simultaneously. Storing bits in a register is known as **loading** the register. A common register implementation uses flip-flops. (Registers are discussed more later).

### Example - Flight attendant call button using a D flip-flop

A flight attendant call button has two buttons: call and cancel. If the call button is pressed, the light is turned on. If the cancel button is pressed, the light is turned off. If both are pressed at the same time, the call button gets priority, so the light is turned on. If neither button is pressed, the light does not change.

A D flip-flop and an additional circuit can be used to capture the desired behavior.

<img width="459" alt="image" src="https://github.com/d-khan/assembly/assets/11669149/4de3e670-7615-42f8-9bf8-743cbb490d07">

1. If Call is pressed, a 1 is stored, and the blue light is turned ON.
2. If Cncl is pressed, a 0 is stored, and the blue light is turned OFF.
3. If neither button is pressed, the present value of Q is stored back in the flip-flop.
4. If both buttons are pressed, priority is given to Call, so a 1 is stored.

## Conclusion

Boolean algebra is used to simplify the circuit, use less number of gates, and so on. Always strike for a simple design. Remember, if the design is complicated, the implementation, the troubleshooting, and the maintenance will be complicated too. The topics in the lecture are superficially covered to provide you an introductory-level knowledge for Computer Science students. The advanced topics are suitable for students who are pursuing Computer Engineering/Electronics degrees.

---

## Boolean algebra properties (optional)

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

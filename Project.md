# Project

Apply the topics learned in the course. Pick one task.

## Prerequisites

- The tasks will only work if you run the code on a Linux platform using an Intel x86 platform. The online assembler will not work due to the lack of debugging features.
- Knowledge of how to run assembly code using nasm assembler in Linux OS.

> # Note
>  Use the registers which are taught in the class. Registers or instructions set used outside of the content will be graded as 0.



## Task 1 (Encryption and Decryption)

### Task 1 objective

Encrypt and decrypt using an XOR logical operator.

#### Encrypting a message

- Select a secret "one English word" message. Keep it secret.

- Create a secret “one English word” key. For simplicity, use the same length of the word key as the message.  For example, if the message is "Hello," select a key size equal to 5 characters, such as "March."

- Apply XOR bitwise operation between the message and the key.

#### Decrypting a message

- Use the "encrypted message" and the "secret key" and perform the bitwise XOR operation.

- Verify that the decrypted message is the same as the "plain text".

#### Output to display

The output should be saved in a text file (output.txt). For example:

```
Plain text: HELLO
Key: world
Encrypted text: ?*> +
Decrypted text: HELLO
```

The plain text and key are __case sensitive__. The encrypted text should display the result in printable ASCII characters. If you notice that there is a nonprintable character right after '>', which is a space. The XOR of 'L' and 'l' comes out to be 32 in decimal which corresponds to a space in ASCII.


## Task 2 (Functions and Recursions)
### Task 2 objective

Analyze the performance of function and recursion

Write a function (count) to perform the following task.

- Generate a counter (let's say 20,000) using the function. The function should have one integer argument (in this example, 20,000).
- Calculate the execution time of your code by using the [time command](https://en.wikipedia.org/wiki/Time_(Unix)) and redirect the output to the counter_fun.txt file.
- Append the counter in an already created text file (counter_fun.txt).

Use recursion to generate the same counter which you did above. [Check what is recursion](https://en.wikipedia.org/wiki/Recursion_(computer_science)) 

- Use the same function (count), but you will repeatedly call the same function (recursion) to generate the counter.
- Calculate the execution time of your code by using the [time command](https://en.wikipedia.org/wiki/Time_(Unix)) and redirect the output to the counter_rec.txt file.
- Append the counter in an already created text file (counter_rec.txt).
- Compare both the time and discuss which code (function or recursion) runs efficiently and why.

#### Output to display

- There should be two text files for this task. counter_fun.txt and counter_rec.txt
- Each file should have a time command output and a counter.


## What to submit?

1. Draw a flowchart of your thought process. I found this [online flowchart website](http://www.draw.io/) very useful. However, you can use any application of your choice. **(1 mark)**
2. Working and error-free code along with the output file(s). **(5 marks)**
3. Create a 5-mins video that explains the working of the code. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). **(3 marks)**
4. Submit the following files **(1 mark)**
   1. Flowchart **(pdf format)**
   2. Error-free code **(.txt format)**
   3. Video explaining the code **(.mp4 or .mov format)**


## How to submit it?

- Upload the work in Canvas and clearly define your responses.
- __Do not compress or zip your work.__

## Deadline

The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric

- All the questions are answered, and the working code is submitted. (Grade 100%)
- Questions are partially answered, and the code has errors or incorrect output. (Grade 50%)

------

Last updated: May 2024 by Dr. Danish Khan. 

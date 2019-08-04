# Homework 1

[TOC]

Homework_1 is mainly concerned about *the input and output of  C programs* and *debugger tools*. There are *three* major problems to deal with, which will be discussed in detail as follows:

## Problem 1

### Brief Introduction

In Problem 1, I write a simple C program to compute the price of a trip to Europe this summer for me and 8 of my best friends. Assuming that the cost per person is $977.50 each with a 5% discount and a 9.5% sales tax.

### Public Interface
```C
/*------------------------------------------------------------
Module name: program_1.c
Description:This is a simple C program to compute the price of a trip to Europe this summer for me and 8 of my best friends. Assuming that the cost per person is $977.50 each with a 5% discount and a 9.5% sales tax. The results are formatted in a stdout.
Author:Bo Yue
Rev. 0 14 Jul 2019
------------------------------------------------------------*/

//include standard input & output head files
#include <stdio.h>

//define four relevant constants
double cost_per_person = 977.50;
double discount        = 0.05;
double sales_tax       = 0.095;
double num_of_friends  = 8;

void main()
{
    //define the variable
    double price_of_trip   = 0;

    //calculate the price of the trip according to given assumption
    price_of_trip          = (1 + num_of_friends) * cost_per_person * (1 - discount) * (1 + sales_tax);

    //format the output
    printf("price_of_trip: $%.2f", price_of_trip);
}
```
### Side Effect

Well, since the program is that simple, and the type "double" covers a wide range of numbers, there is barely no side effect. Additionally, we can change the exact value of the four constants to make my program more adaptable.

### Test Cases

There are no test cases, since there are no codes indicating inputs, and the code is fixed one.

### Results

The outcomes are shown below:

![problem_1_result](C:\Users\Bobyue\Desktop\UW\Intro To C & Microprocessors\homework1\problem_1.jpg)



## Problem 2

### Brief Introduction

In Problem_2, I design a C program to ask the user how many friends will be traveling with them and then tell them how much the total bill will be. Just take a look, you will find it is not a simple program, since some misleading input circumstances are taken into consideration. 

**Public Interface 1** is the simplest program without taking complex situation into account, while **Public Interface 2** considers these situations.

### Public Interface 1

```c
/*------------------------------------------------------------
Module name: program_2_1.c
Description:This is a C program to ask the user how many friends will be
traveling with them and then tell them how much the total bill will be.
Assuming that the cost per person is $977.50 each with a 5% discount and a
9.5% sales tax. The results are formatted in a stdout.
Author:Bo Yue
Rev. 0 14 Jul 2019
------------------------------------------------------------*/

#include <stdio.h>
//define two constants based on the assumption
float discount = 0.05;
float sales_tax = 0.095;
void main()
{
	//define two input variables and one final-calculated variable
	int travelers;
	float cost_per_person;
	float price_of_trip;
    
	//input session
	printf("Please type how many friends will be traveling: ");
	scanf("%d", &travelers);
	printf("cost per person: $");
	scanf("%f", &cost_per_person);

    //calculate session
    price_of_trip = (1 + travelers) * cost_per_person * (1 - discount) * (1 + sales_tax);
    
	//format the output
	printf("price_of_trip: $%.2f", price_of_trip);
}
```

### Public Interface 2

```C
/*------------------------------------------------------------
Module name: program_2_2.c
Description:This is a C program to ask the user how many friends will be traveling with them and then tell them how much the total bill will be. Assuming that the cost per person is $977.50 each with a 5% discount and a 9.5% sales tax. The results are formatted in a stdout.
Author:Bo Yue
Rev. 0 14 Jul 2019
------------------------------------------------------------*/

#include <stdio.h>

//define bool type
typedef int bool;

//define two constants based on the assumption
float discount  = 0.05;
float sales_tax = 0.095;

int main()
{
    //define two input variables and one final-calculated variable
    int travelers = 0;
    float cost_per_person = -1.0;
    float price_of_trip = 0.0;

    //flush = false: fflush();flush = true: nothing to do
    bool flush = 1;

    //input session
    while(travelers < 1 || 0 == flush)        //not a positive number or not a number
    {
        printf("Please type how many people will be traveling: ");
        flush = scanf("%d", &travelers);
        if(0 == flush) {fflush(stdin);}       //clear the input buffer
    }

    // in case that "travelers" is not an integer
    while(cost_per_person < 0.0 || 0 == flush)//not a positive number or not a number
    {
        fflush(stdin);                        //clear the input buffer
        printf("cost per person: $");
        flush = scanf("%f", &cost_per_person);
        if(0 == flush) {printf("Please input again:\n");}
    }

    //calculate session
    price_of_trip = (1 + travelers) * cost_per_person * (1 - discount) * (1 + sales_tax);

    //format the output
    printf("price_of_trip: $%.2f", price_of_trip);
    return 0;
}
```

### Side Effect

- There is no obvious side effects, since much about mistaken input format is taken into account. 

### Test Case 1

![test2](C:\Users\Bobyue\Desktop\UW\Intro To C & Microprocessors\homework1\problem2_11.jpg)

### Result 1

- If there is a misleading input for the variable *travelers*, my program will ask the user to input it one more time.

- The variable *cost_per_person* will not accept ".9" from the remaining input buffer, as it is cleared by the function "fflush(stdin)".

### Test Case 2

![test1](C:\Users\Bobyue\Desktop\UW\Intro To C & Microprocessors\homework1\test2.jpg)

### Result 2

- If there is a misleading input for the variable *cost_per_person*, my program will ask the user to input it one more time.
- “a” from the input "11a" for the variable "travelers" will be ignored as it is cleared from the input buffer by the function "fflush(stdin)".



## Problem_3

### Brief Introduction

In Problem 3, I utilize *the debugger tool* to make my code a correct one.

### Error Occurrence

```c
||=== Build: Debug in test3 (compiler: GNU GCC Compiler) ===|
C:\Users\Bobyue\Desktop\test3\main.c||In function 'main':|
C:\Users\Bobyue\Desktop\test3\main.c|11|error: expected '=', ',', ';', 'asm' or '__attribute__' before 'anInt4'|
C:\Users\Bobyue\Desktop\test3\main.c|20|error: expected ';' before 'printf'|
C:\Users\Bobyue\Desktop\test3\main.c|26|error: 'anInt3' undeclared (first use in this function)|
C:\Users\Bobyue\Desktop\test3\main.c|26|note: each undeclared identifier is reported only once for each function it appears in|
C:\Users\Bobyue\Desktop\test3\main.c|30|error: 'anInt4' undeclared (first use in this function)|
||=== Build failed: 4 error(s), 0 warning(s) (0 minute(s), 0 second(s)) ===|

```

- However, after I go through these errors, there seems to be only **3** big errors. They are *missing comma between ‘anInt3’ and ‘anInt4'*, and *missing semicolon after anAnswer = anInt0\* anInt1*, and *two equal marks in "anAnswer == anInt0 + anInt1 + anInt4;"*
- I soon correct these two mistakes.

### Public Interface

- Using the *Debugger Tool*, I acquire the required values, and I put these values in the comment shown below.

```C
/*------------------------------------------------------------
Module name: program_3.c
Description:After correcting three problems. I set the specified breakpoints, rerun the program, using your debugger, stop at each breakpoint, inspect, and record the values of each of the variables indicated.
Author:Bo Yue
Rev. 0 14 Jul 2019
------------------------------------------------------------*/

#include <stdio.h>

// a global variable
int anInt0 = 9;

void main(void)
{
	// some local variables
	int anInt1 = 8;
	int anInt2, anInt3, anInt4;

	int anAnswer = 0;

	//  break point 0
    //anAnswer = 0, anInt0 = 9, anInt1 = 8
	anAnswer = anInt0 + anInt1;
	//  break point 1  
    //anAnswer = 17,anInt0 = 9,anInt1 = 8

	//  print the answer followed by a new line \n
	printf("the answer is: %d\n", anAnswer);

	anAnswer = anInt0 * anInt1;

	//  print the answer followed by a new line \n
	printf("the answer is: %d\n", anAnswer);

	//  break point 2  
    //anAnswer = 72, anInt2 = 67
	anAnswer = anAnswer + anInt2;
	//  break point 3  
    //anAnswer = 139,anInt2 = 67

	//  print the answer followed by a new line \n
	printf("the answer is: %d\n", anAnswer);

	anAnswer = anInt1 + anInt3;

	//  print the answer followed by a new line \n
	printf("the answer is: %d\n", anAnswer);

	//  break point 4 
    //anAnswer = 400824, anInt0 = 9, anInt1 = 8, anInt4 = 4200910
	anAnswer = anInt0 + anInt1 + anInt4;
	//  break point 5 
    //anAnswer = 4200824, anInt0 = 9, anInt1 = 8, anInt4 = 4200910

	//  print the answer followed by a new line \n
	printf("the answer is: %d\n", anAnswer);

	//  print variables followed by a new line \n
	printf("the variables are: %d %d %d\n", anInt2, anInt3, anInt4);
}
```

### Result

- I have recorded all the values required. These breakpoint values are stated above in corresponding annotation.
- One thing should be particular cautious of is that, if you *fail to initialize a variable at its definition point*, you might get an undesired random value at it. In another case, anInt2 equals to 72.

## Conclusion

In Homework 1, I learn the input and output methods of a C program, and I learn how to debug a bug-existing code to make it correct. 

I come to realize that many codes have side effects even if they are bug-free. As long as we manage to fail successfully, the tough coding process is meaningful.

## Statement

I do my homework on my own.  
Signature: 

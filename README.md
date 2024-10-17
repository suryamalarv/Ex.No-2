# Ex-2-GENERATION OF LEXICAL TOKENS LEX FLEX TOOL
# Reg No: 212223230224
# Name : Suryamalarv
# AIM
To write a lex program to implement lexical analyzer to recognize a few patterns.
# ALGORITHM
1.	Start the program.

2.	Lex program consists of three parts.

     a.	Declaration %%

     b.	Translation rules %%

     c.	Auxilary procedure.

3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form

    a.	P1 {action}

    b.	P2 {action}

    c.	…

    d.	…

    e.	Pn {action}

5.	Write a program in the vi editor and save it with .l extension.

6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.
# PROGRAM
# exp2.l
```
%{
#include <stdio.h>
#include <stdlib.h>
int COMMENT = 0;
%}

identifier [a-zA-Z][a-zA-Z0-9]*

%%
#.* { printf("PREPROCESSOR DIRECTIVE: %s\n", yytext); }
int|float|char|double|while|for|do|if|break|continue|void|switch|case|long|struct|const|typedef|return|else|goto { printf("KEYWORD: %s\n", yytext); }
"//".* { /* Ignore single-line comments */ }
"/*" { COMMENT = 1; }
"*/" { COMMENT = 0; }
[0-9]+ { printf("NUMBER: %s\n", yytext); }
\".*?\" { printf("STRING: %s\n", yytext); }  // Recognize strings
{identifier} { printf("IDENTIFIER: %s\n", yytext); }
\{ { printf("BLOCK BEGINS\n"); }
\} { printf("BLOCK ENDS\n"); }
"=" { printf("ASSIGNMENT OPERATOR: %s\n", yytext); }   // Assignment operator
"<="|">="|"<"|">"|"==" { printf("RELATIONAL OPERATOR: %s\n", yytext); }  // Relational operators


%%

int main(int argc, char **argv) {
    if (argc > 1) {
        FILE *file = fopen(argv[1], "r");
        if (!file) {
            printf("Could not open %s\n", argv[1]);
            exit(1);
        }
        yyin = file; // Set input to the file
        printf("Reading from file: %s\n", argv[1]); // Debugging output
    }
    yylex();
    return 0;
}

int yywrap() {
    return 0;
}
```
# var.c
```
#include<stdio.h>
int main()
{
int a,b;
return 0;
}
```
# Commands:
```
lex exp2.l 
gcc lex.yy.c
./a.out var.c
```
# OUTPUT
![image](https://github.com/user-attachments/assets/7eca2cd4-f0f2-4163-a141-5e1f14de52cb)

# RESULT
The lexical analyzer is implemented using lex and the output is verified.

# Ex.No:3
   RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
## Register Number:212224110061
## Date:23-09-25
## AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
## PROGRAM
```
arth.l
%{
#include "arth.tab.h"   // so it knows the token names from YACC
%}

%%

"="          { printf("\n Operator is EQUAL"); return '='; }
"+"          { printf("\n Operator is PLUS"); return PLUS; }
"-"          { printf("\n Operator is MINUS"); return MINUS; }
"/"          { printf("\n Operator is DIVISION"); return DIVISION; }
"*"          { printf("\n Operator is MULTIPLICATION"); return MULTIPLICATION; }

[a-zA-Z]*[0-9]* { printf("\n Identifier is %s", yytext); return ID; }

.            { return yytext[0]; }
\n           { return 0; }

%%

int yywrap() { return 1; }
```
```
arth.y
%{
#include <stdio.h>
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION

%%

statement:
    ID '=' E {
        printf("\nValid arithmetic expression");
        $$ = $3;   // semantic value (not needed here, but ok)
    }
;

E:
    E PLUS ID
  | E MINUS ID
  | E MULTIPLICATION ID
  | E DIVISION ID
  | ID
;

%%

extern FILE* yyin;

int main() {
    do {
        yyparse();
    } while (!feof(yyin));
    return 0;
}

void yyerror(char *s) {
    fprintf(stderr, "Error: %s\n", s);
}
```

## OUTPUT
## Commands 

<img width="1008" height="369" alt="image" src="https://github.com/user-attachments/assets/94b3330a-4b37-4a97-99f1-6a87c5645191" />

## Valid expression 

<img width="620" height="229" alt="image" src="https://github.com/user-attachments/assets/52276415-5b85-4b3f-81d8-8285ab1b0a2b" />

## invalid Expression 

<img width="433" height="287" alt="image" src="https://github.com/user-attachments/assets/b0daf79c-00d9-486a-af5d-fac45e081e5e" />

## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.

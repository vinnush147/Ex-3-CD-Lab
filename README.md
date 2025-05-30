# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# NAME: VINNUSH KUMAR L S
# REG NO: 212223230244
# Date:29/04/2025
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
# FLEX FILE:
C
%{
#include "y.tab.h"
%}

%%

"="     { printf("\nOperator is EQUAL"); return '='; }
"+"     { printf("\nOperator is PLUS"); return '+'; }
"-"     { printf("\nOperator is MINUS"); return '-'; }
""     { printf("\nOperator is MULTIPLICATION"); return ''; }
"/"     { printf("\nOperator is DIVISION"); return '/'; }

[a-zA-Z_][a-zA-Z0-9_]* {
    printf("\nIdentifier is %s", yytext);
    return ID;
}

[ \t]+  ;           // Ignore spaces and tabs
\n      { return 0; }

.       { return yytext[0]; }

%%

int yywrap() {
    return 1;
}

# BISON:
C
%{
#include <stdio.h>
#include <stdlib.h>
%}

%token ID

%%

statement:
      ID '=' E        { printf("\nAssignment expression is valid\n"); }
    | E               { printf("\nValid arithmetic expression\n"); }
    ;

E:
      E '+' ID        { }
    | E '-' ID        { }
    | E '*' ID        { }
    | E '/' ID        { }
    | ID              { }
    ;

%%

int main() {
    printf("Enter an expression:\n");
    return yyparse();
}

void yyerror(char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

# OUTPUT
![image](https://github.com/user-attachments/assets/6b9e4681-a315-417a-b93b-6e3690fcbfbd)

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.

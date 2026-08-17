# Ex.No:4
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
# Register Number:212224230052
# Date:17-08-26
# Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.

# ALGORITHM
Start the program.
Write a program in the vi editor and save it with .l extension.
In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
Write a program in the vi editor and save it with .y extension.
Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
Compile these with the C compiler as gcc lex.yy.c y.tab.c
Enter a statement as input and the valid variables are identified as output.
# PROGRAM
# exp4-0052.l
```
%{
#include "y.tab.h"
#include <string.h>
%}

%%
[a-zA-Z][a-zA-Z0-9]*    { yylval.str = strdup(yytext); return IDENTIFIER; }
\n                      { return '\n'; }
.                       { return yytext[0]; }
%%

int yywrap() {
    return 1;
}

```
# exp4-0052.y
```
%{
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

extern int yylex();
void yyerror(const char *msg);

%}

%union {
    char *str;
}

%token <str> IDENTIFIER

%%
start:
    IDENTIFIER '\n' {
        printf("Valid variable: %s\n", $1);
        free($1);  // clean up strdup memory
    }
    ;
%%

int main() {
    printf("Enter a variable name:\n");
    return yyparse();
}

void yyerror(const char *msg) {
    printf("Invalid variable name\n");
}

```
# Output
<img width="1919" height="394" alt="image" src="https://github.com/user-attachments/assets/b435030e-94c4-46c1-b1fa-5d863e7fb3d3" />

# Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.

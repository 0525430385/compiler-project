# compiler-project
program      : declaration_list

declaration_list
            : declaration_list declaration
            | declaration

declaration  : var_declaration
            | fun_declaration

var_declaration
            : type_specifier IDENTIFIER ';'
            | type_specifier IDENTIFIER '[' NUMBER ']' ';'

type_specifier
            : INT
            | FLOAT

fun_declaration
            : type_specifier IDENTIFIER '(' params ')' compound_stmt

params       : param_list
            | VOID

param_list   : param_list ',' param
            | param

param        : type_specifier IDENTIFIER
            | type_specifier IDENTIFIER '[' ']'

compound_stmt: '{' local_declarations statement_list '}'

local_declarations
            : local_declarations var_declaration
            | /* empty */

statement_list
            : statement_list statement
            | /* empty */

statement    : expression_stmt
            | compound_stmt
            | selection_stmt
            | iteration_stmt
            | return_stmt

expression_stmt
            : expression ';'
            | ';'

selection_stmt
            : IF '(' expression ')' statement
            | IF '(' expression ')' statement ELSE statement

iteration_stmt
            : WHILE '(' expression ')' statement

return_stmt  : RETURN ';'
            | RETURN expression ';'

expression   : var '=' expression
            | simple_expression

var          : IDENTIFIER
            | IDENTIFIER '[' expression ']'

simple_expression
            : additive_expression
            | simple_expression LT|GT|LE|GE|EQ|NE additive_expression

additive_expression
            : term
            | additive_expression '+' term
            | additive_expression '-' term

term         : factor
            | term '*' factor
            | term '/' factor

factor       : '(' expression ')'
            | var
            | call
            | NUMBER

call         : IDENTIFIER '(' args ')'

args         : arg_list
            | /* empty */

arg_list     : arg_list ',' expression
            | expression
            %{
                #include <stdio.h>
                #include <stdlib.h>
                
                int yylex();
                void yyerror(const char *msg);
                
                %}
                
                %union {
                  int number;
                  char *string;
                  struct AstNode *node;
                }
                
                %token INT FLOAT IDENTIFIER
                %token NUMBER STRING


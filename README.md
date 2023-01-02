# compiler-project
#include <stdio.h>
#include <stdlib.h>
#include <regex.h>

// A token consists of a type and a value
struct Token {
int type;
char *value;
};

// Define constants for the different token types
enum {
TOKEN_NUMBER,
TOKEN_STRING,
TOKEN_OPERATOR,
TOKEN_SYMBOL,
TOKEN_IDENTIFIER,
TOKEN_KEYWORD,
TOKEN_NEWLINE,
TOKEN_COMMENT,
// Add more token types here
};

// Define regular expressions for the different token types
const char REGEX_NUMBER = "[0-9]+(\.[0-9]+)?";
const char REGEX_STRING = ""[^"]"";
const char REGEX_OPERATOR = "[+\-/%=<>&|^]";
const char REGEX_SYMBOL = "[(){}\[\];,]";
const char REGEX_IDENTIFIER = "[a-zA-Z_][a-zA-Z0-9_]";
const char REGEX_KEYWORD = "if|else|while|for|do|break|continue|return";
const char REGEX_NEWLINE = "\n";
const char REGEX_COMMENT = "//.|/\[^]\+(?:[^/][^]\+)*/";
// Add more regular expressions here

// Tokenize the input source code and return a list of tokens
struct Token *tokenize(const char *input) {
// Compile the regular expressions
regex_t regex_number, regex_string, regex_operator, regex_symbol,
regex_identifier, regex_keyword, regex_newline, regex_comment;
regcomp(&regex_number, REGEX_NUMBER, REG_EXTENDED);
regcomp(&regex_string, REGEX_STRING, REG_EXTENDED);
regcomp(&regex_operator, REGEX_OPERATOR, REG_EXTENDED);
regcomp(&regex_symbol, REGEX_SYMBOL, REG_EXTENDED);
regcomp(&regex_identifier, REGEX_IDENTIFIER, REG_EXTENDED);
regcomp(&regex_keyword, REGEX_KEYWORD, REG_EXTENDED);
regcomp(&regex_newline, REGEX_NEWLINE, REG_EXTENDED);
regcomp(&regex_comment, REGEX_COMMENT, REG_EXTENDED);

// Initialize an array to store the tokens
struct Token *tokens = malloc(sizeof(struct Token));
int num_tokens = 0;

// Read the input source code character by character
int input_len = strlen(input);
for (int i = 0; i < input_len; i++) {
char c = input[i];
// Check if the character matches any of the regular expressions
regmatch_t match;
if (regexec(&regex_

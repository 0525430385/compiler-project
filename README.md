# compiler-project

//First, define data structures for the AST nodes and symbol table entries

// AST node types
enum {
  AST_VAR_DECL,
  AST_FUN_DECL,
  AST_BLOCK,
  AST_ASSIGN,
  AST_IF,
  AST_WHILE,
  AST_RETURN,
  AST_BIN_OP,
  AST_UN_OP,
  AST_FUN_CALL,
  AST_VAR,
  AST_NUMBER,
};

// AST node
struct AstNode {
  int type;
  struct AstNode *left;
  struct AstNode *right;
  union {
    char *string;
    int number;
  } value;
};

// Symbol types
enum {
  SYMBOL_VAR,
  SYMBOL_FUN,
};

// Symbol table entry
struct Symbol {
  int type;
  char *name;
  union {
    int var_type;
    struct {
      int return_type;
      int num_params;
      int *param_types;
    } fun;
  } info;
  struct Symbol *next;
};

// Symbol table
struct SymbolTable {
  struct Symbol *head;
};



//Next, write functions to create the AST and symbol table:



// Create a new AST node
struct AstNode *new_ast_node(int type, struct AstNode *left, struct AstNode *right) {
  struct AstNode *node = malloc(sizeof(struct AstNode));
  node->type = type;
  node->left = left;
  node->right = right;
  return node;
}

// Create a new symbol table
struct SymbolTable *new_symbol_table() {
  struct SymbolTable *table = malloc(sizeof(struct SymbolTable));
  table->head = NULL;
  return table;
}

// Add a symbol to the symbol table
void add_symbol(struct SymbolTable *table, int type, char *name, void *info) {
  struct Symbol *symbol = malloc(sizeof(struct Symbol));
  symbol->type = type;
  symbol->name = name;

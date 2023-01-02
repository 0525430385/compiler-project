# compiler-project
// Machine code instruction types
enum {
  INSTR_MOV,
  INSTR_ADD,
  INSTR_SUB,
  INSTR_MUL,
  INSTR_DIV,
  INSTR_CMP,
  INSTR_JE,
  INSTR_JNE,
  INSTR_JG,
  INSTR_JGE,
  INSTR_JL,
  INSTR_JLE,
  INSTR_PUSH,
  INSTR_POP,
  INSTR_CALL,
  INSTR_RET,
};

// Machine code instruction
struct Instruction {
  int type;
  int src;
  int dest;
};

// Machine code
struct MachineCode {
  int num_instructions;
  struct Instruction *instructions;
};

// Generate machine code instructions for an AST node
void generate_instructions(struct AstNode *node, struct MachineCode *code) {
  switch (node->type) {
    case AST_NUMBER:

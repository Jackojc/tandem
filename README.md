# tandem
An array processing DSL for generating straight-line SIMD instructions to embed in larger applications

### Notes
- Vector language with binary/unary/postfix ops
- "Complete" language that is guaranteed to terminate
- No functions or control flow
- Generate object file and C header for embedding
- Runtime dispatch for choosing best available SIMD instructions
- RISC-V and x86-64 code generation

### Operators
```
+ - * / %
& | ^ ~
<< >>
'
```

### Grammar
```
comment ::= ? #.+$ ?
literal ::= ? [0-9_]+ ? | ? 0x[0-9A-z_]+ ? | ? 0b[0-1_]+ ?

type ::= ? [iuf]\d+ ?

prefix ::= ( '+' | '-' | "'" | '~' ) <expr>
infix ::= <expr> ( '+' | '-' | '*' | '/' | '%' | '&' | '|' | '^' ) ( <expr> | <literal> )

expr ::= <prefix> | <infix> | ( <type> '[' <literal>+ ']' )
```

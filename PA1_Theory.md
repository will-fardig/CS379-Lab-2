# PA 1: Grammary Theory Thing

## A1

### Tree A
```
            <expr>
           /  |   \
       <expr> "+" <expr>
         |          |  \  \
      num(2)  <expr> "*" <expr>
                   |            |
                 num(3)       num(4)
```
Comes out to 14.

### Tree B
```
            <expr>
           /    |   \
       <expr>  "*" <expr>
        / | \        |
   <expr>"+" <expr>  num(4)
     |          |
    num(2)    num(3)
```
This one comes out to 20

Like in class these are both technically correct, but the problem is that there
is an expr on BOTH sides of the recursive issue. Why would it make the split in
any given spot instead of any other given spot? It doesn't because it's not that
smart, so it CAN turn out to be either of these things. As it stands, anyway.

## A2

```
<expr>   ::= <expr> "+" <term> | <expr> "-" <term> | <term>
<term>   ::= <term> "*" <factor> | <term> "/" <factor> | <factor>
<factor> ::= number | "(" <expr> ")"
```

This takes away any ambiguity because you can't reach the * "initially"
without going through the rest of the steps.

Because the expr is on the left hand of the operator,
the only way to treat 2-3-4 is to grab the first two parts because that's
what our rule says, group them as an expr, and then move onn.

## A3

```
<expr>
<term>              (because expr ::= term)
<term> "*" <factor>           (because term ::= term "*" factor)
<factor> "*" <factor>       (because term ::= factor)
"(" <expr> ")" "*" <factor>      (because factor ::= "(" expr ")")
"(" <expr> "+" <term> ")" "*" <factor>      (because expr ::= expr "+" term)
"(" <term> "+" <term> ")" "*" <factor>      (because expr ::= term)
"(" <factor> "+" <term> ")" "*" <factor>          (because term ::= factor)
"(" 5 "+" <term> ")" "*" <factor>        (because factor ::= number)
"(" 5 "+" <factor> ")" "*" <factor>         (because term ::= factor)
"(" 5 "+" 2 ")" "*" <factor>       (because factor ::= number)
"(" 5 "+" 2 ")" "*" 3        (because factor ::= number)
```

Turns out as `( 5 + 2 ) * 3`.

## 4. Declarations vs. Assignments (10 pts)

```
<declaration> ::= "let" IDENT "=" <expr> ";"
<assignment>  ::= IDENT "=" <expr> ";"
```

Because of the LET, it knows what it must be. If the LET is there, then
it is a declaration. If there's literally anything else, then it has to
just be an assignment. It's not "smart" in a sense where it detects what's
what, but as long as let is there or not there, there's a binary answer.

I don't think the redeclaring x thing twice issue being raised is overly necessary because
it's not something we can try and figure out here. This is just grammar and not like brains
or anything of the sort. I imagine that will be week like 5 or 6.

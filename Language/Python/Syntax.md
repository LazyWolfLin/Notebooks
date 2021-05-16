# Python Syntax

## [Lexical](https://docs.python.org/3/reference/lexical_analysis.html)

### [Line](https://docs.python.org/3/reference/lexical_analysis.html#line-structure)

### [Comment](https://docs.python.org/3/reference/lexical_analysis.html#comments)

A comment starts with a hash character `#` that is not part of a string literal, and ends at the end of the physical line.

### [Indent](https://docs.python.org/3/reference/lexical_analysis.html#indentation)

### [Identifier](https://docs.python.org/3/reference/lexical_analysis.html#identifiers)

### [Keyword](https://docs.python.org/3/reference/lexical_analysis.html#keywords)

The following identifiers are used as reserved words, or keywords of the language, and cannot be used as ordinary identifiers. They must be spelled exactly as written here:

``` Python
False      await      else       import     pass
None       break      except     in         raise
True       class      finally    is         return
and        continue   for        lambda     try
as         def        from       nonlocal   while
assert     del        global     not        with
async      elif       if         or         yield
```

### [Literal](https://docs.python.org/3/reference/lexical_analysis.html#literals)

### [Operator](https://docs.python.org/3/reference/lexical_analysis.html#operators)

The following tokens are operators:

```
+       -       *       **      /       //      %      @
<<      >>      &       |       ^       ~       :=
<       >       <=      >=      ==      !=
```

### [Delimiter](https://docs.python.org/3/reference/lexical_analysis.html#delimiters)

The following tokens serve as delimiters in the grammar:

```
(       )       [       ]       {       }
,       :       .       ;       @       =       ->
+=      -=      *=      /=      //=     %=      @=
&=      |=      ^=      >>=     <<=     **=
```

The period can also occur in floating-point and imaginary literals. A sequence of three periods has a special meaning as an ellipsis literal. The second half of the list, the augmented assignment operators, serve lexically as delimiters, but also perform an operation.

The following printing ASCII characters have special meaning as part of other tokens or are otherwise significant to the lexical analyzer:

```
'       "       #       \
```

The following printing ASCII characters are not used in Python. Their occurrence outside string literals and comments is an unconditional error:

```
$       ?       `
```

## Expression

## Statement

## Resource

* [The Python Language Reference](https://docs.python.org/3/reference/index.html)

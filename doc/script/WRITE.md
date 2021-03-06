# WRITE

{% method -%}

Evaluates code in a context of a new write transaction

Input stack: `code`

Output stack: result of `code` evaluation

This word is the only way one can write to the database, meaning
words like [ASSOC](ASSOC.md) are only possible in the context of
a WRITE. If changes are to be saved, [COMMIT](COMMIT.md) has to be
used as well. Read-transaction related words (such as [RETR](RETR.md))
can also be used.

{% common -%}

```
PumpkinDB> ["hi" "there" ASSOC COMMIT] WRITE
```

{% endmethod %}

## Allocation

Will allocate for `code` appended with an internal transaction end
marker word.

## Errors

[EmptyStack](./errors/EmptyStack.md) error if stack is less than two items on the stack.

[DatabaseError](./errors/DatabaseError.md) error if there's a problem with underlying storage.

[Decoding error](./errors/DECODING.md) error if the code is undecodable.

## Tests

```test
evals : [1] WRITE.
invalid_code : [1 WRITE] TRY UNWRAP 0x05 EQUAL?.
empty_stack : [WRITE] TRY UNWRAP 0x04 EQUAL?.
```

# Move Documentation Comments

This page is very rough and needs to be cleaned up.

Running comments/questions about the official Move documentation:

[Official Move Documentation](https://diem.github.io/move/)

How does 0xDEADBEEF work? How do you claim that named address?

[https://diem.github.io/move/references.html](https://diem.github.io/move/references.html)

\*e1 = e2 () where e1: &mut T and e2: T Update the value in e1 with e2.

What is the () referring to?

I think it may be an empty value of sorts
e.g "the type of any assignment is always ()"

[https://diem.github.io/move/variables.html](https://diem.github.io/move/variables.html)

---

This is confusing. Still not sure how the \* works

[https://diem.github.io/move/variables.html](https://diem.github.io/move/variables.html)

```move
fun example() {
  let y = Y { x1: new_x(), x2: new_x() };

  let Y { x1: X { f }, x2 } = &y;
  assert!(*f + x2.f == 2, 42);

  let Y { x1: X { f: f1 }, x2: X { f: f2 } } = &mut y;
  *f1 = *f1 + 1;
  *f2 = *f2 + 1;
  assert!(*f1 + *f2 == 4, 42);
}
```

Maybe it is the mutable reference value where f, f1, f2 is the mutable reference

---

[https://diem.github.io/move/equality.html](https://diem.github.io/move/equality.html)

Important optimization rule at the bottom: for any complex object do comparisons through references instead of directly to avoid copying large amounts of data:

```
x == y // Inefficient
&x == &y // Efficient
```

---

[https://diem.github.io/move/abort-and-assert.html](https://diem.github.io/move/abort-and-assert.html)

Has a bad example - missing a ```

---

[https://diem.github.io/move/functions.html#acquires](https://diem.github.io/move/functions.html#acquires)

Not sure I understand where signers are needed. Can you move_from an asset without a signature? Wouldn't that be like stealing?

---

[https://diem.github.io/move/structs-and-resources.html#destroying-structs-via-pattern-matching](https://diem.github.io/move/structs-and-resources.html#destroying-structs-via-pattern-matching)

```move
fun example_destroy_bar() {
  let bar = Bar { foo: Foo { x: 3, y: false } };
  let Bar { foo: Foo { x, y } } = bar;
  // ^ nested pattern
  // two new bindings
  // x: u64 = 3
  // foo_y: bool = false
}
```

Where does foo_y come from?

---

[https://diem.github.io/move/structs-and-resources.html#example-1-coin](https://diem.github.io/move/structs-and-resources.html#example-1-coin)

Does the end of this example:

```move
public fun destroy_zero(coin: Coin) {
  let Coin { value } = coin;
  assert!(value == 0, 1001);
}
```

Mean that the coin no longer exists in global storage because it has been deconstructed and its value dropped?

---

I don't understand this example:

[https://diem.github.io/move/generics.html#unused-type-parameters](https://diem.github.io/move/generics.html#unused-type-parameters)

How does this work:

```move
struct Coin<Currency> has store {
  value: u64
}
```

Where does Currency come from? Is it inferred from Currency1/2? Or is it a generic because it is not defined in the module?

It is (next paragraph): In this example, struct Coin<Currency> is generic on the Currency type parameter, which specifies the currency of the coin and allows code to be written either generically on any currency or concretely on a specific currency. This genericity applies even when the Currency type parameter does not appear in any of the fields defined in Coin.

---

I'm really not sure what this section means:
[https://diem.github.io/move/generics.html#phantom-type-parameters](https://diem.github.io/move/generics.html#phantom-type-parameters)

---

[https://diem.github.io/move/abilities.html#example-conditional-copy](https://diem.github.io/move/abilities.html#example-conditional-copy)

Why does this still say "drop" in the "copy" example?

---

[https://diem.github.io/move/standard-library.html#functions-2](https://diem.github.io/move/standard-library.html#functions-2)

What is going on here? You pass in a u64 and get another u64 back?
  
---
  
https://diem.github.io/move/packages.html#usage-artifacts-and-data-structures

Still really unclear how names work


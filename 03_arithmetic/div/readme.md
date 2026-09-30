# Division

The programs were assembled as 32-bit Linux executables using NASM and linked with `ld`. Both programs completed successfully and exited with status `0`.

Unlike ADD, SUB and MUL, the x86 `DIV` instruction does **not define the arithmetic status flags**. Therefore, CF, OF, SF, ZF, AF and PF must all be treated as undefined after division.

This means that a value displayed by GDB for one of these flags is not evidence that the flag was set or cleared by the division operation.

## div1.asm

The program performs unsigned 8-bit division.

The dividend is stored in `AX` and the divisor is stored in `BL`:

`100 ÷ 7 = 14 remainder 2`

After the division:

* `AL = 14` — quotient
* `AH = 2` — remainder

### Flags after DIV

* **CF = Undefined**
* **OF = Undefined**
* **SF = Undefined**
* **ZF = Undefined**
* **AF = Undefined**
* **PF = Undefined**

The `DIV` instruction does not define these flags. Therefore, their values should not be interpreted as indicating whether the quotient is zero, positive, negative, or has any particular parity.

## div2.asm

The program performs unsigned 16-bit division.

The dividend is represented by `DX:AX` and the divisor is stored in `BX`:

`50000 ÷ 300 = 166 remainder 200`

After the division:

* `AX = 166` — quotient
* `DX = 200` — remainder

### Flags after DIV

* **CF = Undefined**
* **OF = Undefined**
* **SF = Undefined**
* **ZF = Undefined**
* **AF = Undefined**
* **PF = Undefined**

Again, `DIV` does not define these arithmetic flags. Any flag values observed through GDB may simply reflect the state left by earlier instructions and cannot be used to explain the division result.

## Conclusion

Both division programs produce the expected quotient and remainder. `div1` produces a quotient of 14 and remainder of 2, while `div2` produces a quotient of 166 and remainder of 200. However, none of the six arithmetic status flags can be reliably classified as set or cleared after `DIV`, because the x86 instruction leaves their results undefined.

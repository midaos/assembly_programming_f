# Multiplication

The programs were assembled as 32-bit Linux executables using NASM and linked with `ld`. Both programs completed successfully and exited with status `0`.

For the `MUL` instruction, the important difference from `ADD` and `SUB` is that only **CF and OF have defined results**. The values of SF, ZF, AF and PF after `MUL` are undefined and therefore cannot be meaningfully described as set or cleared.

## mul1.asm

The program performs 8-bit unsigned multiplication:

`25 × 10 = 250`

The multiplication produces a 16-bit result in `AX`:

`AX = 0x00FA`

### Flags after MUL

* **CF = 0 (Cleared):** For an 8-bit `MUL`, the full product is stored in `AX`. CF is cleared when the upper half of the result, `AH`, is zero. Here the result is `0x00FA`, so `AH = 0`. The product therefore fits completely within the lower 8 bits.

* **OF = 0 (Cleared):** OF has the same condition as CF for `MUL`. Since the upper half of the product is zero, there is no overflow beyond the original 8-bit operand size.

* **SF, ZF, AF and PF: Undefined:** `MUL` does not define these flags. Therefore, any values displayed by GDB for these flags should not be interpreted as being caused by the multiplication.

## mul2.asm

The program performs 16-bit unsigned multiplication:

`3000 × 200 = 600000`

The 32-bit result is stored in `DX:AX`:

`DX:AX = 0x0009:0x27C0`

### Flags after MUL

* **CF = 1 (Set):** For a 16-bit `MUL`, the full result is stored in `DX:AX`. CF is set when the upper half of the result, `DX`, is non-zero. Here `DX = 0x0009`, meaning the result cannot fit completely within `AX`.

* **OF = 1 (Set):** OF is also set because the upper 16 bits of the product are non-zero. The product therefore requires more than 16 bits to represent.

* **SF, ZF, AF and PF: Undefined:** These flags are not defined by the `MUL` instruction. Their displayed values in GDB do not provide meaningful information about the multiplication result.

## Conclusion

`mul1` produces a product that fits completely within the original 8-bit operand size, so its upper half is zero and both CF and OF are cleared. `mul2` produces a product larger than 16 bits, leaving a non-zero value in DX. As a result, both CF and OF are set. The remaining arithmetic flags are undefined for `MUL`.

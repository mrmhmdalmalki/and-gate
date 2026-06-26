# AND Gate

An AND gate outputs `1` **only when both inputs are `1`** (`Y = A · B`).

It is built the simplest way — a **NAND gate followed by a NOT gate** — so there is nothing new
to build at the transistor level. Both sub-gates already exist in this project: the
[`nand`](https://github.com/mrmhmdalmalki/nand-gate) board and the
[`not`](https://github.com/mrmhmdalmalki/not-gate) board.

### Symbol

<img src="images/symbol.png" width="460">

### Truth table

| `A` | `B` | `Y` |
|:---:|:---:|:---:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | **1** |

`Y = A · B`

---

## How it is built

> AND = NOT( NAND(A, B) ) = A · B

A NAND gate gives `NOT(A·B)`; inverting it with a NOT gate gives `A·B`. Both stages use the
complementary (2N3904 + 2N3906) design, so the output is driven to a clean, strong
`~4.8 V` / `~0.2 V`.

<img src="images/circuit.png" width="760">

---

## Building it on a breadboard

This gate has **no transistors of its own**; it is a finished **NAND board** whose output feeds
a finished **NOT board**:

<img src="images/wiring.png" width="820">

| Block | Build guide | Input | Its output goes to |
|:------|:------------|:------|:-------------------|
| **NAND board** | [nand-gate](https://github.com/mrmhmdalmalki/nand-gate) | Inputs `A`, `B` | the input of the NOT board (this node is `‾A·B`) |
| **NOT board** | [not-gate](https://github.com/mrmhmdalmalki/not-gate) | `‾A·B` | Output `Y = A · B` |

Both boards share the **same +5 V rail and the same GND**. `+5 V` and `GND` are **nodes**, not
physical positions.

Quick test: Output is +5 V only when both inputs are +5 V.

---

## Components

An AND gate is a NAND gate plus a NOT gate, each already documented (and built from transistors)
in this project:

| Block | Folder | Transistors |
|:------|:-------|:-----------:|
| NAND | [`nand-gate`](https://github.com/mrmhmdalmalki/nand-gate) | 2 × 2N3904 + 2 × 2N3906 |
| NOT  | [`not-gate`](https://github.com/mrmhmdalmalki/not-gate)   | 1 × 2N3904 + 1 × 2N3906 |

**Total: 3 × 2N3904 + 3 × 2N3906**, plus each board's base resistors (10 kΩ), LED resistors
(220 Ω) and indicator LEDs. See the individual folders for the exact per-board wiring.

### Power

- One shared **+5 V** rail and a common **GND** for both boards.

---

## Standards and references

**Gate symbol.** The distinctive-shape symbol follows the ANSI/IEEE standard for logic graphic symbols:

- IEEE Std 91-1984 and 91a-1991, *Graphic Symbols for Logic Functions* ([standards.ieee.org](https://standards.ieee.org/ieee/91_91a/241/)). The distinctive shapes originate from US MIL-STD-806; the international equivalent is IEC 60617-12.
- Symbols and truth tables overview: *Logic gate*, Wikipedia ([wikipedia.org](https://en.wikipedia.org/wiki/Logic_gate)).

**Transistor circuit.** Each sub-gate is a complementary (CMOS-style) gate built from a matched 2N3904 / 2N3906 pair:

- *CMOS*, Wikipedia ([wikipedia.org](https://en.wikipedia.org/wiki/CMOS)).
- P. Horowitz and W. Hill, *The Art of Electronics*, 3rd ed., Cambridge University Press, 2015.
- A. S. Sedra and K. C. Smith, *Microelectronic Circuits*, Oxford University Press.
- T. L. Floyd, *Digital Fundamentals*, Pearson.

**Transistor parts.** 2N3904 NPN, onsemi datasheet ([PDF](https://www.onsemi.com/pdf/datasheet/2n3904-d.pdf)). 2N3906 PNP, onsemi datasheet ([PDF](https://www.onsemi.com/pdf/datasheet/2n3906-d.pdf)).

---

## Regenerating the diagrams

```bash
pdflatex circuit.tex
pdflatex symbol.tex
pdflatex wiring.tex
pdftoppm -png -r 400 circuit.pdf images/circuit   # -> images/circuit-1.png
pdftoppm -png -r 400 symbol.pdf  images/symbol     # -> images/symbol-1.png
pdftoppm -png -r 400 wiring.pdf  images/wiring     # -> images/wiring-1.png
```

> Use `pdftoppm`, not `pdftocairo`, at high DPI the Cairo backend can garble the fonts.

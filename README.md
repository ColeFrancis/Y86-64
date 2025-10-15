# Y86-64
Simulator for a reduced x86-64 ISA

# ISA Description

## Processor state

### 16 general-purpose registers
- %rax: 0
- %rcx: 1
- %rdx: 2
- %rbx: 3
- %rsp: 4
- %rbp: 5
- %rsi: 6
- %rdi: 7
- %r8: 8
- %r9: 9
- %r10: A
- %r11: B
- %r12: C
- %r13: D
- %r14: E
- NULL: F

### Condition codes
 - ZF: Zero flag
 - SF: Negative flag
 - OF: Overflow flag

### Others

- Program Counter
- Program Status Register
- Memory

## Op codes

| Byte | 0 | 1 | 2-10 |
| :-- | :--: | :--: | :--: |
| halt | 0 0 | NA | NA |
| nop | 1 0 | NA | NA |
| cmovXX rA, rB | 2 fn | rA rB | NA |
| irmovq V, rB | 3 0 | |F rB | V |
| rmmovq rA, D(rB) |  0 | rA rB | D |
| mrmovq D(rB), rA | 5 0 | rA rB | D |
| OPq rA, rB | 6 fn | rA rB | NA |
| jXX Dest | 7 fn | Dest (1-9) | NA |
| call Dest | 8 0 | Dest (1-9) | NA |
| ret | 9 0 | NA | NA |
| pushq rA | A 0 | rA F | NA |
| popq rA | B 0 | rA F | NA |

### cmovXX rA, rB

| code | byte 0 |
| :-- | :--: |
| rmovq | 7 0 |
| cmovle | 7 1 |
| cmovl | 7 2 |
| cmove | 7 3 |
| cmovne | 7 4 |
| cmovge | 7 5 |
| cmovg | 7 6 |

### OPq rA, rB

| code | byte 0 |
| :-- | :--: |
| addq | 6 0 |
| subq | 6 1 |
| andq | 6 2 |
| xorq | 6 3 |

### jXX Dest 

| code | byte 0 |
| :-- | :--: |
| jmp | 7 0 |
| jle | 7 1 |
| jl | 7 2 |
| je | 7 3 |
| jne | 7 4 |
| jge | 7 5 |
| jg | 7 6 |

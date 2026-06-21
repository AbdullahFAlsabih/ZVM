# ZVM

This repo adds core binary manipulation capabilities and critical runtime safeguards to the **ZVM (Zero Virtual Machine)**. 

---

#New Bitwise Instructions

The architecture now supports dynamic, hardware-level bitwise operations executed across the general-purpose registers:

- `AND(VMP, left, right, output)`: Computes the bitwise logical **AND** between two source registers and stores the result in the output register.
- `NOT(VMP, left, right)`: Inverts the bits of the `left` register (ones' complement) and saves the output into the `right` register.
- `SHL(VMP, left, right, output)`: Executes a dynamic **Logical Shift Left**, moving the bits of the `left` register by the value amount specified inside the `right` register.

---

#Added Exceptions & Safeguards

To maintain system stability and prevent hardware-level Undefined Behavior (UB), runtime exception handling has been embedded directly into the **Execute stage**:

- `INVALID_SHIFT_AMOUNT`: Since ZVM operates on an 8-bit registers layout, shifting bits by 8 or more positions is an illegal operation. The CPU safely monitors the `right` register right before processing a shift. If the dynamic value is found to be greater than 7 ($> 7$), the execution pipeline is immediately halted via `zvm_raise`, printing a clean error state instead of crashing the machine.

---


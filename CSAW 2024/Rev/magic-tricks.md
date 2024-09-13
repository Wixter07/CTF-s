# magic-tricks

So we have a golang stipped binary.

```
  local_140 = runtime.stringtoslicerune();
  for (lVar4 = 0; lVar4 < lVar2; lVar4 = lVar4 + 1) {
    iVar1 = *(int *)(local_140 + lVar4 * 4);
    *(int *)(local_140 + lVar4 * 4) =
         (int)((long)((long)iVar1 + 23U ^ (long)(iVar1 + -1)) % 4) + iVar1 * 2 + -0x20;
  }
  local_138 = runtime.slicerunetostring(uVar3);
```

That's the whole logic of how input is modified. The input is added by 23, XOR'd by the previous element, then modulo'd 4. Then add the result with the element * 2 and finally subtract by 32.

Cooked this solve script later.

```python
from z3 import *

with open('output.txt', 'r', encoding='utf-8') as f:
    target = [ord(c) for c in f.read().strip()]

s = Solver()

length = len(target)

inputs = [BitVec(f'char_{j}', 8) for j in range(length)]

for j in range(length):
    s.add(((inputs[j] + 23) ^ (inputs[j] - 1) << 1) % 4 + inputs[j] * 2 - 32 == target[j])

for j in range(length):
    s.add(inputs[j] >= 32, inputs[j] <= 126)

if s.check() == sat:
    m = s.model()
    solution = ''.join(chr(m[inputs[j]].as_long()) for j in range(length))
    print("Result: ", solution)
else:
    print("No solution available.")
```


The flag - ` csawctf{tHE_runE5_ArE_7H3_k3y_7O_th3_G0ph3r5_mA91C}`

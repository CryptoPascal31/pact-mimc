# MiMC for Pact
Pact implementation of the MiMC hash for Kadena.

Compatible with Circom Sponge construction with 220 Rounds:

https://iden3.io/circom

https://github.com/iden3/circomlib/blob/master/circuits/mimcsponge.circom

https://github.com/iden3/circomlibjs/blob/main/src/mimcsponge.js

Constants are generated by keccak256 using the seed `mimcsponge`

## API

```
(defun feistel-hash:object (key:integer input:object)
```
* `key`: key
* `input`: hashing object : {'L:integer 'R:integer}

Returns an hashing object: {'L:integer 'R:integer}

Gas consumption (pact 4.6.0): 27,697

Equivalence:

| Circomlib        | JS                |
| ---------------- | ----------------- |
| MiMCFeistel(220) | MIMCSponge.hash() |


---

```
(defun feistel-multi-hash:[integer] (key:integer inputs:[integer] n-outputs:integer)
````

* `key`: key
* `inputs`: input list of integers
* `n-outputs`: Number of outputs integer to return

Returns the hash result as a list of integers.

| Circomlib                          | JS                     |
| ---------------------------------- | ---------------------- |
| MiMCSponge(nInputs, 220, nOutputs) | MIMCSponge.multiHash() |

Gas consumption:
 - 1 input/1 output: 27,716
 - 1 input/10 outputs: 27,7152
 - 10 inputs/1 output: 27,7181
 - 10 inputs/10 outputs: 526,630

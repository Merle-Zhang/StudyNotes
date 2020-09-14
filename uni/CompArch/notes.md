# Computer Architecture

## Boolean Algebra

## Number

* $\hat{x}$: representation of $x$
  * maps to $x$: the value of $x$
* **Endianness**
  * **Big-endian**: normal order, with **MSB(Most-Significant Bit)** on the left, **LSB(Least-Significant Bit)** on the right
  * **Little-endian**: reverse order, with MSB on the right, LSB on the left
* **Hamming weight**: the number of bits in $X$ that are equal to 1
  * $H(x)=\sum_{i=0}^{n-1}X_i$
* **Hamming distance**: the number of bits in $X$ that differ from the corresponding bit in $Y$, i.e., the number of time $X_i\neq Y_i$
  * $D(X,Y)=\sum_{i=0}^{n-1}X_i\oplus Y_i$
* Different representation
  * unsigned integer: $\sum_{i=0}^{n-1}x_i\cdot 2^i$
  * **Sign-magnitude**: $-1^{x_{n-1}}\cdot\sum_{i=0}^{n-2}x_i\cdot 2^i$
  * **Two's-complement**: $x_{n-1}\cdot-2^{n-1}+\sum_{i=0}^{n-2}x_i\cdot2^i$



* **Fan-in**: the number of inputs to a given gate

  **Fan-out**: the number of inputs the output of a given fate is connected to

  

* **Priority encoder**: one input is  given priority over another

* **Level**

* **Memory hierarchy**: Register, SRAM(L1 cache, L2 cache, L3 cache), Main memory(DRAM), Hard disk/SSD
* Addressing
  * Immediate addressing
  * Direct addressing
  * Memory-indirect addressing
  * Register-indirect addressing
  * Indexed addressing: base+offset
* Execution: "Fetch, decode, execute, write-back"
* Register
  * Program Counter
  * Flag register: conditional branching
  * Link-Register: sub-routines
    * Stack-based linking
* Machine type
  * Register-memory machine
  * Register-register machine
* Memory paradigms
  * Harvard
    * Segregation
    * Inefficient & physical duplicating
  * Von Neumann
    * unified
    * Bottleneck
      * Workarounds:
        * Caching
        * Harvard architecture in L1 cache
        * Branch prediction
        * 
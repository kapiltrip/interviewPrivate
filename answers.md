<a id="q1"></a>
## 1. How many bytes are there in 32 bits?

**Written answer:**

1 byte = 8 bits. [[S1]](#s1)  
So, 32 bits / 8 bits per byte = 4 bytes.  
Therefore, there are 4 bytes in 32 bits.

**Speak like this:**

"One byte contains 8 bits. So, to convert 32 bits into bytes, I divide 32 by 8. The answer is 4 bytes."

[Back to index](./index.md)

<a id="q2"></a>
## 2. Is a latch a combinational circuit or a sequential circuit?

**Written answer:**

A latch is a sequential circuit because it has memory. In a combinational circuit, the output depends only on the current input values. In a sequential circuit, the output can depend on the current inputs and the current state. Here, current state simply means the value already stored in the circuit. Since a latch can hold a state, it is classified as a sequential circuit. [[S2]](#s2)

**Speak like this:**

"A latch is a sequential circuit because it has memory. In standard terms, a sequential circuit output depends on the current inputs and the current state. Here current state just means the value already stored in the circuit. Since a latch can hold that state, it is sequential, not combinational."

[Back to index](./index.md)

<a id="q3"></a>
## 3. Differentiate between a latch and a flip-flop.

**Written answer:**

Both latch and flip-flop are bistable storage elements, which means both can store one bit of data, either 0 or 1. The main difference is how they respond to the control signal: a latch is level sensitive, while a flip-flop is edge sensitive. [[S3]](#s3)

**Latch:**

1. A latch is level triggered.
2. It responds as long as the enable level is active.
3. When enabled, it is transparent, meaning the output can follow the input.
4. It usually uses an enable signal, not a strict edge-triggered clock.
5. It is simpler and usually needs fewer gates.
6. Timing is less controlled because the input can pass through during the active enable level.
7. It can create race-through or transparency issues if used carelessly in synchronous designs.
8. It is used where level-sensitive storage is required, but it is generally avoided in simple synchronous RTL unless intentionally needed.
9. Examples: SR latch and D latch.

**Flip-flop:**

1. A flip-flop is edge triggered.
2. It responds only at the rising edge or falling edge of the clock.
3. It samples the input only at the active clock edge.
4. After capturing the input at the clock edge, it holds that value until the next active clock edge.
5. It is commonly built using two latches in a master-slave arrangement or using edge-triggered circuitry.
6. It is more complex than a latch, but it gives more predictable timing.
7. It is preferred in synchronous digital designs because all storage elements update at defined clock edges.
8. It is widely used in registers, counters, shift registers, pipelines, and FSM state registers.
9. Examples: D flip-flop, JK flip-flop, T flip-flop, and SR flip-flop.

**Speak like this:**

"Both latch and flip-flop are one-bit memory elements, but the main difference is timing control. A latch is level sensitive, so when enable is active it becomes transparent and the output can follow the input. A flip-flop is edge sensitive, so it samples the input only on a clock edge and then holds that value. Because flip-flops update only at defined clock edges, they give more predictable timing and are preferred in synchronous circuits like registers, counters, pipelines, and FSMs. Latches are simpler, but they need more care because transparency can cause race-through issues."

[Back to index](./index.md)

<a id="q4"></a>
## 4. Why is a latch level triggered?

**Written answer:**

A latch is called level triggered because its output responds to the level of the enable or clock signal. For example, in a D latch, when the enable signal is active, the latch becomes transparent and the output follows the input. When the enable signal becomes inactive, the latch stores the last input value. So, the latch is controlled by the level of the signal, not only by a single clock edge. [[S3]](#s3)

**Speak like this:**

"A latch is level triggered because it works based on the level of the enable signal. For example, when the enable is high, a D latch is transparent, so the output follows the input. When the enable goes low, it stores the last value. So it responds during the active level, not just at one clock edge."

[Back to index](./index.md)

<a id="q5"></a>
## 5. What is setup time and clock skew?

**Written answer:**

Setup time is the minimum time for which the input data must remain stable before the active clock edge so that a flip-flop or latch can capture the data correctly. If setup time is violated, the circuit may capture the wrong value or enter an unstable condition. [[S4]](#s4)

Clock skew is the difference in arrival time of the same clock signal at different flip-flops or sequential elements. Ideally, the clock should reach all flip-flops at the same time, but due to wire length, routing delay, load, or clock distribution, it may arrive earlier at one flip-flop and later at another. Too much clock skew can cause setup-time or hold-time violations. [[S4]](#s4)

**Speak like this:**

"Setup time means the data input must be stable for a minimum time before the active clock edge. If the data changes too close to the clock edge, the flip-flop may not capture it correctly. Clock skew means the same clock signal reaches different flip-flops at slightly different times because of routing or delay. If the skew is large, it can create timing problems like setup or hold violations."

[Back to index](./index.md)

<a id="q6"></a>
## 6. Explain Verilog operators.

**Written answer:**

Verilog operators are symbols used to write expressions in RTL and testbench code. They help describe arithmetic, comparison, bit-level logic, shifting, assignment, and selection operations. [[S5]](#s5)

**Main Verilog operator types:**

1. Arithmetic operators: `+`, `-`, `*`, `/`, `%`
   These perform mathematical operations. In hardware, addition and subtraction are common, but multiplication, division, and modulus can be expensive. Division is usually avoided unless it is by a constant or power of two.
2. Bitwise operators: `~`, `&`, `|`, `^`, `~^`
   These operate bit by bit on vectors. For example, `a & b` performs AND on each matching bit of `a` and `b`.
3. Reduction operators: `&a`, `|a`, `^a`, `~&a`, `~|a`, `~^a`
   These reduce a vector into a single bit. For example, `&a` is 1 only if all bits of `a` are 1. `^a` is often used for parity.
4. Relational and equality operators: `>`, `<`, `>=`, `<=`, `==`, `!=`
   These compare values and return a 1-bit result. Case equality operators `===` and `!==` also compare `x` and `z` values, so they are mainly useful in simulation and testbenches.
5. Logical operators: `!`, `&&`, `||`
   These treat the whole expression as true or false and return a 1-bit Boolean result.
6. Shift operators: `<<`, `>>`, `<<<`, `>>>`
   These shift bits left or right.

   `<<` is logical left shift. Bits move left and zeros are filled on the right.

   `>>` is logical right shift. Bits move right and zeros are filled on the left.

   `<<<` is arithmetic left shift. For left shift, `<<<` usually gives the same bit result as `<<`, because both shift bits left, the leftmost shifted-out bits are lost, and zeros are filled on the right. It does not preserve the rightmost bit. It exists mainly for language consistency and code readability: Verilog provides both logical shifts (`<<`, `>>`) and arithmetic shifts (`<<<`, `>>>`). So when a designer writes `<<<`, it clearly says, "I am treating this as an arithmetic or signed-style shift," even though the left-shift bit result is normally the same as `<<`.

   The important practical difference is on right shift. `>>` fills zeros on the left, but `>>>` can preserve the leftmost sign bit when the left operand is signed.

   `>>>` is arithmetic right shift. If the left operand is signed, it preserves the sign bit while shifting right. This is useful for signed numbers because the number keeps its positive or negative sign.

   Example:

   ```verilog
   reg signed [3:0] a;
   initial begin
       a = -4;        // binary 1100 in 4-bit signed form
       a >>  1;       // logical right shift gives 0110
       a >>> 1;       // arithmetic right shift gives 1110, sign bit is preserved
   enda
   ```
7. Assignment operators: `assign`, `=`, `<=`
   `assign` is used for continuous assignment. `=` is blocking assignment and is generally used in combinational always blocks. `<=` is non-blocking assignment and is generally used in clocked sequential always blocks.
8. Other useful operators: `?:`, `{}`, `{{}}`
   `?:` is the conditional operator, `{}` is concatenation, and `{{}}` is replication.

Important point: Verilog has operator precedence, but in interviews and real code it is better to use parentheses when an expression may be confusing.

**Speak like this:**

"Verilog operators are used to describe hardware expressions. The main types are arithmetic, bitwise, reduction, relational, logical, shift, assignment, and conditional operators. Bitwise operators work on each bit of a vector, while reduction operators reduce a whole vector to one bit. For assignments, I use blocking assignment for combinational logic and non-blocking assignment for sequential clocked logic. Also, although Verilog has operator precedence, I prefer using parentheses to make the intention clear."

[Back to index](./index.md)

<a id="q7"></a>
## 7. Explain latch, flip-flop, register, and FSM.

**Written answer:**

A latch, flip-flop, register, and FSM are all related to sequential logic. [[S2]](#s2)

1. Latch: A latch is a level-sensitive storage element. It stores one bit. When the enable signal is active, the latch is transparent, so the output follows the input. When enable becomes inactive, it holds the last value. [[S3]](#s3)
2. Flip-flop: A flip-flop is an edge-triggered storage element. It also stores one bit, but it captures the input only on the active clock edge, such as rising edge or falling edge. It then holds that value until the next active clock edge. [[S3]](#s3)
3. Register: A register is a group of flip-flops connected to the same clock. If we need to store an 8-bit value, we use 8 flip-flops together as an 8-bit register. Registers are used to store data, state, counters, addresses, and temporary values.
4. FSM: FSM stands for finite state machine. It is a sequential circuit with a finite number of states. An FSM usually has three parts: state register, next-state logic, and output logic. [[S2]](#s2)

Relationship: A latch and flip-flop store one bit. A register stores multiple bits using flip-flops. An FSM uses registers to store the current state and combinational logic to decide the next state and outputs.

**Speak like this:**

"A latch, flip-flop, register, and FSM are all part of sequential logic. A latch is level sensitive and stores one bit. A flip-flop is edge triggered and also stores one bit, but it updates only at the clock edge. A register is a group of flip-flops used to store multiple bits. An FSM is a finite state machine; it uses a state register to remember the current state, and combinational logic to calculate the next state and outputs."

[Back to index](./index.md)

<a id="q8"></a>
## 8. Draw encoder, mux, and 4:1 mux using 2:1 mux. Also write code.

**Written answer:**

**Encoder:**

General definition: An encoder is a combinational circuit that converts information from a larger number of input lines into a smaller binary code at the output. [[S6]](#s6)

Specific definition: In a normal 4-to-2 encoder, there are 4 input lines and 2 output lines. Only one input should be active at a time, and the output gives the binary code of that active input. If multiple inputs can become active at the same time, we use a priority encoder, where the highest-priority active input is encoded. [[S6]](#s6)

**Priority encoder Verilog code:**

```verilog
module priority_encoder4 (
    input  [3:0] d,
    output reg [1:0] y,
    output reg valid
);
always @(*) begin
    valid = 1'b1;
    if (d[3])
        y = 2'b11;
    else if (d[2])
        y = 2'b10;
    else if (d[1])
        y = 2'b01;
    else if (d[0])
        y = 2'b00;
    else begin
        y = 2'b00;
        valid = 1'b0;
    end
end
endmodule
```

**2:1 mux:** A multiplexer selects one input from many inputs. A 2:1 mux has two data inputs, one select line, and one output. If `sel = 0`, output is `d0`. If `sel = 1`, output is `d1`. [[S7]](#s7)

**2:1 mux Verilog code:**

```verilog
module mux2 #(parameter W = 1) (
    input  [W-1:0] d0,
    input  [W-1:0] d1,
    input          sel,
    output [W-1:0] y
);
assign y = sel ? d1 : d0;
endmodule
```

**4:1 mux using 2:1 mux:** A 4:1 mux can be built using three 2:1 muxes.

Connection idea:

1. First mux selects between `d0` and `d1` using `sel[0]`.
2. Second mux selects between `d2` and `d3` using `sel[0]`.
3. Third mux selects between those two intermediate outputs using `sel[1]`.

**4:1 mux using 2:1 mux Verilog code:**

```verilog
module mux4_using_mux2 #(parameter W = 1) (
    input  [W-1:0] d0,
    input  [W-1:0] d1,
    input  [W-1:0] d2,
    input  [W-1:0] d3,
    input  [1:0]   sel,
    output [W-1:0] y
);
wire [W-1:0] y0;
wire [W-1:0] y1;

mux2 #(.W(W)) m0 (.d0(d0), .d1(d1), .sel(sel[0]), .y(y0));
mux2 #(.W(W)) m1 (.d0(d2), .d1(d3), .sel(sel[0]), .y(y1));
mux2 #(.W(W)) m2 (.d0(y0), .d1(y1), .sel(sel[1]), .y(y));

endmodule
```

**Speak like this:**

"An encoder converts an active input line into a binary output code. If more than one input can be active, then we use a priority encoder. A mux does the opposite kind of selection: it selects one input and passes it to the output based on select lines. A 4-to-1 mux can be built using three 2-to-1 muxes. First, two muxes select between d0-d1 and d2-d3 using the lower select bit. Then the final mux selects between those two results using the higher select bit."

[Back to index](./index.md)

<a id="q9"></a>
## 9. Explain asynchronous and synchronous reset in flip-flops.

**Written answer:**

A reset is used to bring a flip-flop or sequential circuit to a known initial value. [[S8]](#s8)

**Synchronous reset:** A synchronous reset works only on the active clock edge. The reset signal is checked at the clock edge, and then the flip-flop output is reset.

```verilog
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

Advantages:

1. Easier timing analysis because reset is treated like normal synchronous logic.
2. Safer release from reset because it happens with the clock.

Limitation:

1. It needs a running clock to reset the flip-flop.

**Asynchronous reset:** An asynchronous reset works immediately, without waiting for the clock edge.

```verilog
always @(posedge clk or posedge rst) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

Advantages:

1. It can reset the circuit even when the clock is not running.
2. It is useful for power-up or emergency reset situations.

Limitation:

1. If asynchronous reset is released near a clock edge, it can cause metastability or recovery/removal timing problems. A common safe practice is asynchronous assertion and synchronous deassertion.

**Speak like this:**

"A synchronous reset is applied only at the active clock edge, so the flip-flop resets when the clock edge comes. It is easier for timing analysis, but it needs the clock to be running. An asynchronous reset resets the flip-flop immediately, independent of the clock. It is useful when we need reset even without a clock, but its release should be synchronized to avoid metastability. So a common practical method is asynchronous assert and synchronous deassert."

[Back to index](./index.md)

<a id="q10"></a>
## 10. What are universal gates and why are they called universal gates?

**Written answer:**

NAND and NOR gates are called universal gates. [[S9]](#s9)

They are called universal because we can build all other basic gates using only NAND gates or only NOR gates. Since any Boolean expression can be made using NOT, AND, and OR, and since NAND or NOR alone can create NOT, AND, and OR, they can be used to implement any combinational logic circuit. [[S9]](#s9)

Using only NAND:

1. NOT A = A NAND A
2. A AND B = (A NAND B) NAND (A NAND B)
3. A OR B = (A NAND A) NAND (B NAND B)

Using only NOR:

1. NOT A = A NOR A
2. A OR B = (A NOR B) NOR (A NOR B)
3. A AND B = (A NOR A) NOR (B NOR B)

**Speak like this:**

"NAND and NOR are called universal gates because either one alone can be used to build all other basic gates like NOT, AND, and OR. Once we can build NOT, AND, and OR, we can implement any Boolean expression. That is why NAND and NOR are very important in digital logic and IC design."

[Back to index](./index.md)

<a id="q11"></a>
## 11. Explain a combinational circuit using universal gates. What are the normal steps?

**Written answer:**

To design a combinational circuit using universal gates, we normally follow these steps: [[S9]](#s9)

1. Understand the required function.
2. Write the truth table.
3. Derive the Boolean expressions for the outputs.
4. Simplify the expression using Boolean algebra or K-map.
5. Convert the expression into only NAND gates or only NOR gates using De Morgan's theorem. De Morgan's theorem says that the complement of an AND becomes an OR of complements, and the complement of an OR becomes an AND of complements:

   ```text
   (A . B)' = A' + B'
   (A + B)' = A' . B'
   ```

   In simple words, when a NOT is pushed inside brackets, AND changes to OR, OR changes to AND, and each variable gets complemented. This is useful because it helps convert normal Boolean expressions into NAND-only or NOR-only form.
6. Draw the circuit or write structural Verilog.
7. Verify the circuit using the truth table or simulation.

**Example: Half adder using only NAND gates.**

Half adder equations:

```text
Sum = A xor B
Carry = A and B
```

NAND-only implementation:

```text
n1 = A NAND B
n2 = A NAND n1
n3 = B NAND n1
Sum = n2 NAND n3
Carry = n1 NAND n1
```

Verilog code:

```verilog
module half_adder_nand (
    input  a,
    input  b,
    output sum,
    output carry
);
wire n1;
wire n2;
wire n3;

assign n1 = ~(a & b);
assign n2 = ~(a & n1);
assign n3 = ~(b & n1);
assign sum = ~(n2 & n3);
assign carry = ~(n1 & n1);

endmodule
```

**Example: Half subtractor using only NAND gates.**

Half subtractor equations:

```text
Difference = A xor B
Borrow = (~A) and B
```

NAND-only implementation:

```text
n1 = A NAND B
n2 = A NAND n1
n3 = B NAND n1
Difference = n2 NAND n3
notA = A NAND A
borrow_n = notA NAND B
Borrow = borrow_n NAND borrow_n
```

Verilog code:

```verilog
module half_subtractor_nand (
    input  a,
    input  b,
    output diff,
    output borrow
);
wire n1;
wire n2;
wire n3;
wire not_a;
wire borrow_n;

assign n1 = ~(a & b);
assign n2 = ~(a & n1);
assign n3 = ~(b & n1);
assign diff = ~(n2 & n3);

assign not_a = ~(a & a);
assign borrow_n = ~(not_a & b);
assign borrow = ~(borrow_n & borrow_n);

endmodule
```

**Speak like this:**

"To design a combinational circuit using universal gates, I first write the truth table, then derive the Boolean equation, simplify it, and finally convert it into only NAND or only NOR gates using De Morgan's theorem. For example, in a half adder, the outputs are Sum equal to A xor B and Carry equal to A and B. Since XOR and AND can be built using only NAND gates, the complete half adder can be implemented using only NAND gates."

[Back to index](./index.md)

<a id="q12"></a>
## 12. Which universal gate is better and why?

**Written answer:**

The correct answer is that neither NAND nor NOR is logically better, because both are universal gates. That means any Boolean function can be implemented using only NAND gates or only NOR gates. [[S9]](#s9)

But in practical CMOS/VLSI design, NAND gates are often preferred over NOR gates. The main reason is transistor-level implementation. In a CMOS NAND gate, the PMOS transistors are in parallel and the NMOS transistors are in series. In a CMOS NOR gate, the PMOS transistors are in series and the NMOS transistors are in parallel. Since PMOS devices are generally weaker/slower than NMOS devices, having PMOS transistors in series, as in NOR, usually makes the pull-up path slower and larger. Because of this, NAND gates often give better speed, area, and delay characteristics in CMOS implementations. [[S10]](#s10)

However, the final choice depends on the circuit requirement. If a function maps more naturally to NOR logic, or if the standard-cell library gives a better NOR-based implementation for that case, NOR can still be used. So the interview-safe answer is: logically both are equally powerful, but practically NAND is often preferred in CMOS digital design.

**Speak like this:**

"Logically, NAND and NOR are equally powerful because both are universal gates. But in practical CMOS design, NAND is usually preferred. The reason is transistor implementation. In NAND, the PMOS devices are in parallel, but in NOR the PMOS devices are in series. Since PMOS is generally slower than NMOS, series PMOS in NOR makes the gate slower and sometimes larger. So NAND often gives better speed and area in CMOS. Still, I would not say NOR is useless; the best choice depends on the logic function and the technology library."

[Back to index](./index.md)

<a id="q13"></a>
## 13. Why do we need sequential circuits?

**Written answer:**

We need sequential circuits because digital systems often need memory. A combinational circuit produces output only from the current inputs. That is enough for simple operations like adders, multiplexers, and decoders. But many real systems must remember what happened before, store intermediate values, count events, control steps, or move through states over time.

A sequential circuit solves this by combining combinational logic with memory elements such as latches or flip-flops. The memory stores the current state, and the combinational logic uses the current inputs and current state to produce the output and the next state. [[S2]](#s2)

Sequential circuits are needed for registers, counters, shift registers, finite state machines, timers, control units, processors, and memory-based digital systems. Without sequential circuits, a digital system would not be able to remember data or perform multi-step operations over time.

**Speak like this:**

"We need sequential circuits because combinational circuits do not have memory. A combinational circuit only reacts to the current inputs. But real digital systems need to remember previous information, store data, count events, and move from one state to another. Sequential circuits provide that memory using latches or flip-flops. The stored state, together with the current input, decides the next output and next state. That is why sequential circuits are used in registers, counters, FSMs, timers, processors, and control units."

[Back to index](./index.md)

<a id="q14"></a>
## 14. Explain asynchronous and synchronous reset in FF in Verilog context. For synchronous reset, what circuit is inferred? How can reset logic be minimized?

**Written answer:**

In Verilog, reset coding style decides whether synthesis infers a flip-flop with asynchronous reset or synchronous reset. [[S5]](#s5)

**Asynchronous reset:**

An asynchronous reset affects the flip-flop immediately, without waiting for a clock edge. In Verilog, the reset signal is included in the sensitivity list along with the clock.

```verilog
always @(posedge clk or posedge rst) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

This coding style describes a D flip-flop with an asynchronous reset control. In hardware, synthesis normally maps this to a flip-flop/register primitive with an asynchronous clear or preset input, depending on the reset value. If reset forces `q` to `0`, it is like an asynchronous clear. If reset forces `q` to `1`, it is like an asynchronous preset or set. [[S21]](#s21)

The key point is that the reset path bypasses the normal `D` data input. When `rst` is asserted, the flip-flop output is forced to the reset value immediately, independent of the clock. The benefit is that reset can work even when the clock is not running. The risk is that reset deassertion must be handled carefully; many FPGA guidelines recommend asynchronous assertion but synchronous deassertion to avoid metastability or recovery/removal timing issues. [[S8]](#s8)

**Synchronous reset:**

A synchronous reset is checked only on the active clock edge. In Verilog, only the clock is in the sensitivity list.

```verilog
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

With synchronous reset, the reset signal is sampled only at the active clock edge. The block does not execute just because `rst` changes; it executes only when the clock edge arrives. Therefore, the flip-flop output changes to the reset value only on a clock edge.

The simple hardware model is a mux before the D input of the flip-flop:

```text
D_to_FF = rst ? reset_value : data_value
```

In this model, when `rst = 1`, the mux selects the reset value. When `rst = 0`, the mux selects the normal data value. So the reset decision is part of the clocked data path.

Actual FPGA synthesis can be more flexible. Depending on the FPGA architecture, coding style, fanout, and synthesis settings, the tool may implement synchronous reset as:

1. LUT or mux logic feeding the `D` input of the flip-flop.
2. A dedicated synchronous set/reset control input of the flip-flop.
3. Optimized logic combined with clock enable or other control logic. [[S20]](#s20)

So the strongest answer is: the Verilog describes a clocked D flip-flop with synchronous reset behavior, and synthesis maps that behavior to the best available flip-flop/control resources. Conceptually, it is safe to explain synchronous reset as a mux before the D input, but implementation can be tool and device dependent. [[S20]](#s20) [[S21]](#s21)

Timing point: because synchronous reset is sampled by the clock, it must meet normal setup and hold timing to that clock. Unlike asynchronous reset, it cannot reset the register unless the clock is running.

**Inference summary:**

| Reset type | Verilog style | What is inferred | Timing behavior |
|---|---|---|---|
| Asynchronous reset | `always @(posedge clk or posedge rst)` | D flip-flop with asynchronous clear/set control | Reset assertion does not wait for clock |
| Synchronous reset | `always @(posedge clk)` with `if (rst)` inside | Clocked D flip-flop with reset decision in clocked path; may map to D-input mux/LUT logic or a synchronous reset control | Reset is sampled only on clock edge |

**How to minimize reset logic:**

1. Reset only the registers that truly need a known startup value, such as FSM state registers, control registers, valid bits, and counters.
2. Avoid resetting pure datapath pipeline registers if their value is ignored until a valid signal becomes active.
3. For shift registers or delay pipelines, removing reset can allow the synthesis tool to use more efficient FPGA resources.
4. If only one bit controls whether a vector is meaningful, reset the valid/control bit instead of resetting every data bit.
5. Use a pipeline flush or valid/ready scheme where possible, instead of resetting every flip-flop in the datapath. [[S15]](#s15)

**Speak like this:**

"In Verilog, if reset is in the sensitivity list with the clock, it describes an asynchronous reset. That usually infers a D flip-flop with an asynchronous clear or set control, so the output can be forced to the reset value without waiting for the clock. If only the clock is in the sensitivity list and reset is checked inside the clocked block, it describes a synchronous reset. That means reset is sampled only at the clock edge. Conceptually, synchronous reset behaves like a mux before the D input: reset selects the reset value, otherwise normal data goes to the flip-flop. In real FPGA synthesis, that synchronous behavior may map to D-input LUT/mux logic or to a dedicated synchronous reset/control resource, depending on the device and tool. To minimize reset logic, I would reset only the registers that truly need a known value, like FSM state and valid bits, and avoid resetting unnecessary datapath pipeline registers."

[Back to index](./index.md)

<a id="q15"></a>
## 15. Explain timing criticality in flip-flops: setup time, hold time, and metastability.

**Written answer:**

Timing criticality in flip-flops means the data must reach the flip-flop at the correct time around the active clock edge. A flip-flop captures data on a rising or falling clock edge, but the data cannot change too close to that edge.

**Setup time:**

Setup time is the minimum time for which the data input must be stable before the active clock edge. If data reaches too late, the flip-flop may not capture the correct value. [[S4]](#s4)

**Hold time:**

Hold time is the minimum time for which the data input must remain stable after the active clock edge. If data changes too soon after the clock edge, the flip-flop may again capture the wrong value. [[S4]](#s4)

**Timing path view:**

For setup timing, data launched by one flip-flop must pass through combinational logic and reach the next flip-flop before the next capture edge:

```text
clock-to-Q delay + combinational delay + setup time <= clock period
```

For hold timing, the data must not reach the next flip-flop too early after the same clock edge.

**Metastability:**

Metastability happens when a flip-flop input changes too close to the active clock edge, violating setup or hold timing. The output may temporarily be neither a clean 0 nor a clean 1, and it may take an unpredictable time to settle. This can also happen when asynchronous signals or asynchronous reset deassertion are sampled by a clocked circuit. [[S11]](#s11)

**Speak like this:**

"Timing criticality in a flip-flop is about making sure data is stable around the clock edge. Setup time means data must be stable before the active clock edge. Hold time means data must remain stable after the clock edge. If either requirement is violated, the flip-flop may capture the wrong value or enter metastability. Metastability means the output is temporarily unpredictable before it settles to 0 or 1. That is why timing analysis checks setup and hold paths in synchronous designs."

[Back to index](./index.md)

<a id="q16"></a>
## 16. Is it okay to use blocking for combinational logic and nonblocking for sequential logic? Why?

**Written answer:**

Yes. In Verilog RTL coding, the common recommended style is:

1. Use blocking assignment `=` for combinational logic.
2. Use nonblocking assignment `<=` for sequential clocked logic. [[S12]](#s12)

**Blocking assignment `=`:**

Blocking assignment updates the left-hand side immediately in simulation, before the next statement executes. This matches combinational logic well because combinational logic is evaluated like a chain of logic equations.

```verilog
always @(*) begin
    y = a & b;
    z = y | c;
end
```

Here, `z` uses the new value of `y`, which is usually what we want in combinational logic.

**Nonblocking assignment `<=`:**

Nonblocking assignment evaluates the right-hand side first, then updates the left-hand side later in the same simulation time step. This matches flip-flop behavior because all registers update together at the clock edge.

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

Here, `q2` gets the old value of `q1`, just like real cascaded flip-flops.

**Why this rule matters:**

Using blocking in sequential logic can create simulation race issues. Using nonblocking carelessly in combinational logic can make simulation behavior harder to reason about. The clean interview rule is: blocking for combinational, nonblocking for sequential, and do not mix them for the same signal.

**Speak like this:**

"Yes, that is the standard RTL coding practice. I use blocking assignment for combinational logic because it behaves like immediate equation evaluation. I use nonblocking assignment for sequential logic because all flip-flops should sample inputs at the clock edge and update together. This avoids race conditions and makes simulation behavior closer to real hardware. So my rule is: equal sign for combinational always blocks, nonblocking less-than-equal for clocked always blocks."

[Back to index](./index.md)

<a id="q17"></a>
## 17. What is a sensitivity list?

**Written answer:**

In Verilog, a sensitivity list is the event control part of an `always` block. It tells the simulator when the block should execute. [[S5]](#s5)

**Combinational sensitivity list:**

For combinational logic, the block should run whenever any input used inside the block changes.

```verilog
always @(a or b or c) begin
    y = (a & b) | c;
end
```

In modern Verilog, `always @(*)` is preferred because it automatically includes the signals read inside the block:

```verilog
always @(*) begin
    y = (a & b) | c;
end
```

If a combinational sensitivity list is incomplete, simulation may not update the output when an input changes, causing simulation and synthesis mismatch.

**Sequential sensitivity list:**

For sequential logic, the sensitivity list usually contains clock edges and sometimes asynchronous reset edges.

```verilog
always @(posedge clk) begin
    q <= d;
end
```

```verilog
always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        q <= 1'b0;
    else
        q <= d;
end
```

The first example is a normal clocked flip-flop. The second example is a flip-flop with asynchronous active-low reset.

**Pure Verilog best practice:**

In pure Verilog, use `always @(*)` for combinational logic because it automatically includes the signals read inside the block and helps avoid missed sensitivity-list signals. [[S14]](#s14)

**Speak like this:**

"A sensitivity list tells an always block when to execute. For combinational logic, it should include every signal read inside the block, so the output updates whenever an input changes. In pure Verilog, I use `always @(*)` for combinational logic because it avoids missing signals in the sensitivity list. For sequential logic, I use `always @(posedge clk)` or `always @(posedge clk or negedge rst_n)` when there is an asynchronous reset."

[Back to index](./index.md)

<a id="q18"></a>
## 18. What is time borrowing?

**Written answer:**

**Definition to remember:** Time borrowing is a property of latch-based pipelines, not normal edge-triggered flip-flop pipelines. It is possible because a level-sensitive latch remains transparent during its active clock level. While the latch is transparent, late-arriving data can still pass through the latch and use part of the next stage's time. [[S16]](#s16) [[S56]](#s56)

**Why we need a latch instead of a flip-flop:**

A flip-flop samples data only at a clock edge. After that edge, the flip-flop closes. If data reaches the flip-flop late after the required setup time, it cannot "borrow" from the next cycle; it simply violates setup timing.

A latch is different. A latch is level-sensitive. During its active clock level, it is open or transparent. So if data arrives slightly late but still arrives before the latch closes, the data can pass into the next stage. That extra time used after the nominal boundary is called borrowed time.

```text
Flip-flop boundary:
Data must arrive before the clock edge setup window.
No transparency after the edge, so no normal time borrowing.

Latch boundary:
Data may arrive during the active latch-open window.
If it arrives late but before latch closing, it can borrow time.
```

**Pipeline idea:**

```text
Stage 1 logic -> Latch 1 -> Stage 2 logic -> Latch 2
```

If Stage 1 is slightly slow, its output may pass through `Latch 1` while `Latch 1` is still transparent. That means Stage 1 has effectively used some time that would otherwise belong to Stage 2.

**Important point: borrowed time is not free time.**

If one stage borrows time, the next stage has less time available. So the overall timing across adjacent latch stages must still satisfy setup and hold requirements. [[S16]](#s16) [[S56]](#s56)

**Simple numerical example:**

Assume two latch-based stages together have `10 ns` total available time.

```text
Stage 1 planned time = 5 ns
Stage 2 planned time = 5 ns
```

If Stage 1 actually takes `6 ns`, it borrows `1 ns` from Stage 2.

```text
Stage 1 uses = 6 ns
Stage 2 left = 4 ns
Total still = 10 ns
```

So time borrowing helps balance uneven stage delays, but it does not increase the total cycle budget.

**When it is used:**

1. Latch-based pipelines.
2. High-speed ASIC datapaths.
3. Designs where one stage is slightly slower and the next stage has slack.
4. Timing optimization with two-phase latch clocks.

**Interview warning:**

Do not say "flip-flops borrow time" in the normal sense. The standard time-borrowing concept comes from latch transparency. Flip-flop-based pipelines are easier to analyze, but they do not provide this latch-open window.

**Speak like this:**

"Time borrowing is possible because we use latches instead of normal edge-triggered flip-flops. A flip-flop samples only at the clock edge, so if data misses setup time, it cannot use time from the next stage. But a latch is level-sensitive and remains transparent during its active clock level. If data arrives slightly late but before the latch closes, it can still pass through, so the previous stage borrows some time from the next stage. The important point is that this is not free extra time. Whatever time is borrowed from the next stage is subtracted from that next stage's timing margin, so setup and hold timing must still be checked across the latch pipeline."

[Back to index](./index.md)

<a id="q19"></a>
## 19. Which application uses time borrowing?

**Written answer:**

Time borrowing is mainly used in latch-based pipeline designs and high-speed datapaths where delay is not perfectly balanced between stages. If one stage is slower and the next stage has some slack, latch transparency can help the slower stage borrow time from the next stage. [[S16]](#s16)

Typical applications are:
 
1. High-performance ASIC datapaths.
2. Latch-based pipelines.
3. Designs where timing needs to be balanced across adjacent stages.
4. Timing optimization where one stage is slightly critical and the next stage has available slack.

In normal FPGA or simple RTL design, flip-flop-based synchronous design is usually preferred because it is easier to analyze and less error-prone.

**Speak like this:**

"I would use time borrowing in a latch-based pipeline, especially in a high-speed datapath where one stage is slower and the next stage has slack. The latch can remain transparent for part of the clock cycle, so the slow stage can borrow some time. But I would use it carefully, because latch timing is more complex than normal flip-flop timing."

[Back to index](./index.md)

<a id="q20"></a>
## 20. Explain blocking and nonblocking assignments.

**Written answer:**

In Verilog, blocking and nonblocking assignments are procedural assignments, but they update values differently. [[S5]](#s5)

**Blocking assignment `=`:**

1. The right-hand side is evaluated and assigned immediately.
2. The next statement in the same procedural block waits until this assignment is completed.
3. It behaves like step-by-step execution.
4. It is normally used for combinational logic.

```verilog
always @(*) begin
    y = a & b;
    z = y | c;
end
```

**Nonblocking assignment `<=`:**

1. The right-hand side is evaluated immediately.
2. The left-hand side update is scheduled for later in the same simulation time step.
3. Other statements can continue without waiting for the update.
4. It models simultaneous flip-flop updates, so it is normally used for sequential logic. [[S12]](#s12)

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

**Best rule:**

Use blocking `=` for combinational logic and nonblocking `<=` for clocked sequential logic. Avoid assigning the same signal from multiple `always` blocks.

**Speak like this:**

"Blocking assignment uses `=`, and it updates immediately, so the next statement sees the new value. That is why it is commonly used in combinational logic. Nonblocking assignment uses `<=`; it evaluates the right-hand side now but schedules the update later in the same time step. That matches flip-flop behavior, where all registers update together on the clock edge. So my rule is: blocking for combinational logic, nonblocking for sequential logic."

[Back to index](./index.md)

<a id="q21"></a>
## 21. What is a MUX? Write the equation for a 2:1 MUX.

**Written answer:**

**General definition:** A multiplexer, or MUX, is a combinational circuit that selects one of several input lines and forwards it to a single output line using select lines. It works like a digital data selector. [[S7]](#s7)

**Specific definition:** A 2:1 MUX has two data inputs, `I0` and `I1`, one select input `S`, and one output `Y`. If `S = 0`, the output is `I0`. If `S = 1`, the output is `I1`.

**Equation for 2:1 MUX:** [[S19]](#s19)

```text
Y = (~S & I0) | (S & I1)
```

In Boolean notation:

```text
Y = S'I0 + SI1
```

**Verilog code:**

```verilog
assign y = s ? i1 : i0;
```

**Speak like this:**

"A MUX is a combinational data selector. In a 2:1 MUX, there are two inputs, `I0` and `I1`, one select line `S`, and one output `Y`. When `S` is 0, output is `I0`; when `S` is 1, output is `I1`. So the equation is `Y = S'I0 + SI1`, or in Verilog, `assign y = s ? i1 : i0;`."

[Back to index](./index.md)

<a id="q22"></a>
## 22. What is race around condition?

**Written answer:**

Race around condition occurs in a level-triggered JK flip-flop when `J = 1`, `K = 1`, and the clock stays active for longer than the propagation delay. In this condition, the output keeps toggling while the clock is active, so the final output becomes uncertain. [[S17]](#s17)

It can be avoided by:

1. Using an edge-triggered flip-flop.
2. Using a master-slave JK flip-flop.
3. Keeping the clock pulse width smaller than the propagation delay, although this is not a practical preferred solution. [[S17]](#s17)

**Why master-slave helps:**

In a master-slave JK flip-flop, the master and slave are active in opposite clock phases. The master samples the input during one phase, and the slave updates the output during the other phase. Since both are not transparent at the same time, repeated toggling in one clock pulse is prevented. [[S18]](#s18)

**Speak like this:**

"Race around condition happens in a level-triggered JK flip-flop when `J` and `K` are both 1 and the clock remains active for too long. Since JK with `J = K = 1` is a toggle condition, the output may toggle repeatedly during the same clock pulse, making the final state uncertain. We avoid it by using an edge-triggered JK flip-flop or a master-slave JK flip-flop, because the output changes only once per clock cycle."

[Back to index](./index.md)

<a id="q23"></a>
## 23. Design inverter and buffer using a MUX.

**Written answer:**

A 2:1 MUX can implement simple logic gates by fixing its data inputs to `0` or `1` and using the required variable as the select line.

For a 2:1 MUX: [[S19]](#s19)

```text
Y = S'I0 + SI1
```

**Inverter using 2:1 MUX:**

Set `S = A`, `I0 = 1`, and `I1 = 0`.

```text
Y = A' . 1 + A . 0
Y = A'
```

So the output is the complement of `A`.

**Buffer using 2:1 MUX:**

Set `S = A`, `I0 = 0`, and `I1 = 1`.

```text
Y = A' . 0 + A . 1
Y = A
```

So the output is the same as `A`.

| Function | Select `S` | `I0` | `I1` | Output |
|---|---|---:|---:|---|
| Inverter | `A` | `1` | `0` | `A'` |
| Buffer | `A` | `0` | `1` | `A` |

**Speak like this:**

"Using a 2:1 MUX equation `Y = S'I0 + SI1`, I can implement gates by tying the data inputs to constants. For an inverter, I take `A` as select, connect `I0` to 1 and `I1` to 0. Then output becomes `A'`. For a buffer, I again take `A` as select, connect `I0` to 0 and `I1` to 1. Then output becomes `A`."

[Back to index](./index.md)

<a id="q24"></a>
## 24. Explain the waveform of a master-slave JK flip-flop.

**Written answer:**

A master-slave JK flip-flop is made using two latch stages: master and slave. They are enabled on opposite clock levels. In one common arrangement, the master is active when the clock is high, and the slave is active when the clock is low. [[S18]](#s18)

**Waveform idea:**

1. When `CLK = 1`, the master is enabled and samples `J` and `K`.
2. During the same time, the slave is disabled, so final output `Q` does not change.
3. When `CLK` goes low, the master is disabled and holds its value.
4. The slave becomes enabled and copies the master's value to output `Q`.
5. Therefore, the final output changes only once per clock cycle, usually on the falling edge in this arrangement. [[S18]](#s18)

**JK operation table:**

| J | K | Next output |
|---:|---:|---|
| 0 | 0 | No change |
| 0 | 1 | Reset to 0 |
| 1 | 0 | Set to 1 |
| 1 | 1 | Toggle |

**For waveform explanation:**

If `J = K = 1`, the flip-flop toggles. But in a master-slave JK flip-flop, it toggles only once for a clock cycle because master and slave are not active together. This is why it avoids race around condition.

**Speak like this:**

"In a master-slave JK flip-flop, the master and slave work on opposite clock levels. When the clock is high, the master reads the JK inputs, but the slave is closed, so the final output does not change. When the clock goes low, the master closes and the slave opens, so the slave copies the master's value to `Q`. That means the output changes only once per clock cycle. For `J = K = 1`, it toggles once instead of toggling repeatedly, so race around is avoided."

[Back to index](./index.md)

<a id="q25"></a>
## 25. Which is preferred in circuits: NAND gates or NOR gates?

**Written answer:**

**Definition to remember:** NAND and NOR are both universal gates. That means any Boolean function can be implemented using only NAND gates or only NOR gates. [[S9]](#s9)

The preference between NAND and NOR depends on the circuit, technology, and design goals. Logically, neither is more powerful than the other, because both are universal. But in practical CMOS digital design, NAND gates are often preferred because they usually give better speed and area characteristics. [[S10]](#s10)

**Why NAND is often preferred in CMOS:**

1. **Ease of implementation:** NAND gates are simple, common, and efficient in CMOS standard-cell libraries. In practical digital design, many Boolean expressions are mapped into NAND-based structures because NAND cells are usually well optimized by the library vendor.

2. **Transistor structure:** In a 2-input CMOS NAND gate, the PMOS transistors are connected in parallel and the NMOS transistors are connected in series. In a 2-input CMOS NOR gate, the PMOS transistors are connected in series and the NMOS transistors are connected in parallel. This matters because the pull-up path is made of PMOS devices, and PMOS devices are generally weaker/slower than NMOS devices. So when NOR puts PMOS devices in series, the pull-up resistance increases and the output rising transition becomes slower. [[S10]](#s10)

3. **Size and power:** To make a NOR gate as fast as a NAND gate, the series PMOS devices in NOR often need to be made wider. Wider transistors reduce resistance, but they also increase area and capacitance. More capacitance can increase dynamic power and can also slow down the previous driving stage. So the speed improvement may come with area and power cost.

4. **Performance:** NAND often has better delay in CMOS because the weaker PMOS devices are not stacked in series. The NAND gate has series NMOS in the pull-down path, but NMOS devices are stronger than PMOS devices, so that stack is usually less harmful than the PMOS stack in NOR. This is why, for the same fan-in and comparable sizing, NAND is often faster than NOR.

5. **Fan-in effect:** As fan-in increases, stacking becomes worse. A 3-input or 4-input NOR has multiple PMOS devices in series, making the pull-up path very weak unless the PMOS devices are made large. High fan-in NAND also has stacked NMOS, but because NMOS is stronger, NAND usually scales better than NOR in many CMOS libraries.

6. **Design style and library dependence:** The final choice is not based only on theory. It also depends on the standard-cell library, transistor sizing, load capacitance, fan-in, routing, power goal, and the Boolean expression being implemented. A good synthesis tool may choose NAND, NOR, AOI, OAI, or inverter combinations depending on the best timing and area result.

7. **Application requirement:** Some functions naturally map better to NOR or OR-based logic. So NOR is not wrong or useless. The correct interview answer is that NAND is often preferred in CMOS, but the real design choice depends on the circuit and library.

**Final comparison:**

| Point | NAND | NOR |
|---|---|---|
| Logic power | Universal | Universal |
| CMOS PMOS network | Parallel | Series |
| CMOS NMOS network | Series | Parallel |
| Practical preference | Often preferred | Used when suitable |
| Reason | Usually better speed/area in CMOS | Can be useful depending on logic/library |

**Conclusion:**

The interview-safe answer is: NAND and NOR are logically equally powerful, but NAND is usually preferred in CMOS implementation because it is often faster and more area-efficient. However, the best gate still depends on the circuit, power, performance, and standard-cell library.

**Speak like this:**

"Both NAND and NOR are universal gates, so logically both are equally powerful. But in CMOS implementation, NAND is usually preferred. The reason comes from transistor structure. In NAND, PMOS devices are in parallel and NMOS devices are in series. In NOR, PMOS devices are in series and NMOS devices are in parallel. Since PMOS devices are generally weaker than NMOS devices, series PMOS in NOR makes the pull-up path weak, so the output rising delay becomes larger. To compensate, we may need bigger PMOS devices, which increases area and capacitance. So NAND often gives better speed and area in CMOS. But I would not say NAND is always best; the final choice depends on fan-in, load, power, timing, the Boolean expression, and the standard-cell library."

[Back to index](./index.md)

<a id="q26"></a>
## 26. Explain delay models in digital circuits and gates.

**Written answer:**

**Definition to remember:** A delay model describes how much time a signal transition takes to propagate through a gate, wire, combinational circuit, or flip-flop. [[S4]](#s4)

In real digital circuits, outputs do not change instantly when inputs change. Gates have internal transistor delay, wires have resistance and capacitance, and flip-flops have clock-to-Q delay. Delay modeling is used to estimate whether a circuit can meet timing.

**Important delay terms:**

1. **Propagation delay (`tpd`):** The maximum time from a valid input change to the time the output is guaranteed to become valid and stable. In timing analysis, propagation delay is used for setup checks because we must make sure data has enough time to travel through the combinational path before the next clock edge. [[S4]](#s4)
2. **Contamination delay (`tcd`):** The minimum time from an input change to the earliest time the output may start changing. In timing analysis, contamination delay is used for hold checks because we must make sure new data does not reach the next flip-flop too quickly after the clock edge. [[S4]](#s4)
3. **Rise delay:** Delay when output changes from `0` to `1`.
4. **Fall delay:** Delay when output changes from `1` to `0`.
5. **Gate delay:** Delay through a logic gate.
6. **Interconnect delay:** Delay caused by wires, routing, capacitance, and load.
7. **Clock-to-Q delay:** Time from active clock edge to valid flip-flop output.

**Timing equations:**

For setup timing:

```text
clock-to-Q delay + combinational propagation delay + setup time <= clock period
```

For hold timing:

```text
clock-to-Q contamination delay + combinational contamination delay >= hold time
```

**Delay in Verilog gate-level modeling:**

Verilog allows delay modeling using `#` delay. [[S5]](#s5)

```verilog
and #5 g1 (y, a, b);
```

This means the AND gate output is modeled as changing 5 time units after the input change.

Verilog can also model rise and fall delay separately:

```verilog
buf #(3, 5) b1 (y, a);  // rise delay = 3, fall delay = 5
```

**Speak like this:**

"Delay means a signal does not pass through hardware instantly. Propagation delay is the maximum time for output to become valid after an input change, and contamination delay is the minimum time before output can start changing. Propagation delay is important for setup timing, and contamination delay is important for hold timing. In Verilog gate-level modeling, we can write delays using `#`, but in real RTL design, actual delays are calculated by synthesis and static timing analysis."

[Back to index](./index.md)

<a id="q27"></a>
## 27. Draw a MUX using NAND gates.

**Written answer:**

**Definition to remember:** A multiplexer, or MUX, is a combinational circuit that selects one input from multiple inputs and passes it to the output using select lines. [[S7]](#s7)

For a 2:1 MUX:

```text
Y = S'I0 + SI1
```

Using only NAND gates, we implement this by making the complemented product terms and then applying De Morgan's theorem.

**NAND-only implementation:**

```text
nS = NAND(S, S)       = S'
n0 = NAND(I0, nS)     = (I0 . S')'
n1 = NAND(I1, S)      = (I1 . S)'
Y  = NAND(n0, n1)     = I0S' + I1S
```

So a 2:1 MUX can be made using four NAND gates.

**Connection diagram:**

```text
S ----+---- NAND ---- nS
      |      ^
      +------+

I0 -------- NAND ---- n0
nS --------/

I1 -------- NAND ---- n1
S ---------/

n0 -------- NAND ---- Y
n1 --------/
```

**Verilog structural code:**

```verilog
module mux2_nand (
    input  i0,
    input  i1,
    input  s,
    output y
);
wire ns;
wire n0;
wire n1;

nand g0 (ns, s, s);
nand g1 (n0, i0, ns);
nand g2 (n1, i1, s);
nand g3 (y, n0, n1);

endmodule
```

**Speak like this:**

"A 2:1 MUX equation is `Y = S'I0 + SI1`. To implement it with NAND gates, first I generate `S'` using a NAND as an inverter. Then I create `(I0S')'` and `(I1S)'` using two NAND gates. Finally, I NAND those two signals together. By De Morgan's theorem, the result becomes `I0S' + I1S`, which is the required MUX output."

[Back to index](./index.md)

<a id="q28"></a>
## 28. Comparison between BJT and MOSFET.

**Written answer:**

**Definition to remember:** A BJT is a bipolar junction transistor, usually treated in interviews as a current-controlled device because base current controls collector current. A MOSFET is a metal-oxide-semiconductor field-effect transistor, usually treated as a voltage-controlled device because gate-to-source voltage controls the channel and drain current. [[S22]](#s22) [[S45]](#s45)

| Point | BJT | MOSFET |
|---|---|---|
| Full form | Bipolar Junction Transistor | Metal-Oxide-Semiconductor Field-Effect Transistor |
| Main terminals | Base, emitter, collector | Gate, source, drain; body/substrate also exists |
| Control quantity | Base current controls collector current | Gate-to-source voltage controls channel |
| Input nature | Requires base current | Insulated gate draws almost no DC current ideally |
| Input impedance | Lower than MOSFET | Very high input impedance |
| Carrier type | Bipolar: uses both electrons and holes | Field-effect/unipolar behavior: majority-carrier conduction |
| Drive requirement | Needs continuous drive current in ON state | Needs gate charge/discharge current mainly during switching |
| ON behavior | Has `VCE(sat)` in saturation | Acts like resistance `RDS(on)` when ON |
| Switching | Can be slower in saturation due to stored charge | Usually faster for switching because it is majority-carrier based |
| Thermal behavior | Current sharing can be harder in parallel BJTs | Easier to parallel many power MOSFETs due positive `RDS(on)` temperature tendency |
| Digital IC use | Older bipolar logic, some analog/high-speed special cases | Dominant in CMOS digital ICs |
| Common applications | Analog amplifiers, current mirrors, low-noise/small-signal stages, simple switches | CMOS logic, power switching, motor drives, DC-DC converters, high input impedance circuits |

**Important distinctions:**

1. **Terminal difference:** A BJT has base, emitter, and collector. A MOSFET has gate, source, drain, and usually a body/substrate terminal internally.

2. **Current control vs voltage control:** In basic interview language, a BJT is current-controlled because base current is needed to control collector current. A MOSFET is voltage-controlled because gate-to-source voltage creates or removes the channel. [[S45]](#s45)

3. **Input impedance:** A BJT input junction behaves like a forward-biased diode when ON, so it needs input current. A MOSFET gate is insulated by oxide, so ideally no DC current flows into the gate; this gives very high input impedance. [[S45]](#s45)

4. **Power loss in drive circuit:** For a BJT, base drive current must be continuously supplied while it is ON. For a MOSFET, the gate mostly consumes current only while charging and discharging gate capacitance during switching. This makes MOSFET gate driving efficient for many switching applications. [[S45]](#s45)

5. **Switching speed:** A saturated BJT can store charge, which increases turn-off time. A MOSFET is a majority-carrier field-effect device, so it generally switches faster in power switching applications when driven properly. [[S46]](#s46)

6. **Digital circuits:** MOSFETs are the foundation of CMOS logic. CMOS is preferred in modern digital ICs because it gives high density and very low static power in steady state.

7. **Analog circuits:** BJTs are still valuable in analog design because they can provide high transconductance, good current gain, and useful analog characteristics for amplifiers, current mirrors, bandgap references, and precision circuits.

**Advantages of BJT:**

1. Good current gain, so a small base current can control a larger collector current.
2. Useful for analog amplification because it can provide high transconductance for a given bias current.
3. Often good in low-noise and precision analog circuits.
4. Simple to use as a small-signal amplifier or low-side switch when base current is available.
5. In some analog IC blocks, BJTs give predictable exponential `VBE` behavior, useful for references and temperature-related circuits.

**Advantages of MOSFET:**

1. Very high input impedance because the gate is insulated.
2. Needs almost no DC gate current ideally, so drive power can be low.
3. Very common in digital CMOS because CMOS has low static power and high integration density.
4. Often better for high-speed switching and power switching.
5. Low `RDS(on)` power MOSFETs can carry high current with low conduction loss.
6. Easier to drive from logic circuits because the gate is voltage-controlled.
7. Often easier to parallel in power applications than BJTs.

**When to choose which:**

| Situation | Better choice |
|---|---|
| Modern digital logic / VLSI | MOSFET, because CMOS uses MOSFETs |
| High input impedance required | MOSFET |
| Fast power switching | MOSFET |
| Simple current amplification | BJT |
| Analog gain stage with high transconductance | BJT can be attractive |
| Low static power digital IC | MOSFET/CMOS |
| Precision analog bias/reference circuits | BJT or BiCMOS may be useful |

**One-line summary:**

```text
BJT: current-driven, good for gain and analog behavior.
MOSFET: voltage-driven, high input impedance, best for CMOS digital and power switching.
```

**Speak like this:**

"A BJT is a bipolar device with base, emitter, and collector terminals. In interview language, I treat it as current-controlled because base current controls collector current. A MOSFET has gate, source, and drain terminals, and I treat it as voltage-controlled because gate-to-source voltage controls the channel. The MOSFET gate is insulated, so it has very high input impedance and ideally almost no DC gate current. That is why MOSFETs are widely used in CMOS digital circuits and power switching. A BJT needs continuous base current, but it is still very useful for analog amplification, current gain, low-noise stages, and precision analog circuits. So the practical distinction is: MOSFET is preferred for high-input-impedance, low-power digital and switching applications, while BJT is strong for gain-oriented analog applications."

[Back to index](./index.md)

<a id="q29"></a>
## 29. What gates are used in Verilog? What is a universal gate? Draw OR/NOR truth table and design NOR using OR/AND.

**Written answer:**

**Definition to remember:** Verilog gate primitives are built-in gate-level keywords used to model logic gates directly. Examples include `and`, `or`, `nand`, `nor`, `xor`, `xnor`, `not`, and `buf`. [[S5]](#s5)

**Common gates used in Verilog:**

```text
and, or, nand, nor, xor, xnor, not, buf
```

Verilog also has tri-state gate primitives. These primitives drive an output only when the control signal is active; otherwise the output goes to high impedance `z`. [[S5]](#s5)

| Primitive | Meaning |
|---|---|
| `bufif1` | Buffer with active-high enable: output = input when control is `1`, else `z` |
| `bufif0` | Buffer with active-low enable: output = input when control is `0`, else `z` |
| `notif1` | Inverter with active-high enable: output = inverted input when control is `1`, else `z` |
| `notif0` | Inverter with active-low enable: output = inverted input when control is `0`, else `z` |

Example:

```verilog
bufif1 b1 (bus, data, enable);  // bus = data when enable = 1, else z
notif0 n1 (bus, data, enable);  // bus = ~data when enable = 0, else z
```

**Universal gate:**

A universal gate is a gate that can be used by itself to build all other basic gates. NAND and NOR are universal gates because we can implement NOT, AND, OR, and any Boolean expression using only NAND gates or only NOR gates. [[S9]](#s9)

**OR and NOR truth table:**

| A | B | OR = A + B | NOR = (A + B)' |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 0 |

**Design NOR using OR gate:**

NOR means OR followed by NOT.

```text
Y = (A + B)'
```

```verilog
module nor_using_or_not (
    input  a,
    input  b,
    output y
);
wire or_out;

or  g1 (or_out, a, b);
not g2 (y, or_out);

endmodule
```

**Design NOR using AND gate also:**

Using De Morgan's theorem:

```text
(A + B)' = A' . B'
```

So we can invert both inputs and then use AND.

```verilog
module nor_using_and_not (
    input  a,
    input  b,
    output y
);
wire na;
wire nb;

not g1 (na, a);
not g2 (nb, b);
and g3 (y, na, nb);

endmodule
```

**Speak like this:**

"In Verilog, common gate primitives are `and`, `or`, `nand`, `nor`, `xor`, `xnor`, `not`, and `buf`. A universal gate is a gate from which we can build all other gates. NAND and NOR are universal gates. For OR, output is 1 when at least one input is 1. NOR is the complement of OR, so it is 1 only when both inputs are 0. To design NOR using OR, I use OR followed by NOT. Using De Morgan's theorem, I can also design NOR as `A'B'`, meaning invert both inputs and then AND them."

[Back to index](./index.md)

<a id="q30"></a>
## 30. Difference between sequential and combinational circuit.

**Written answer:**

**Definition to remember:** A combinational circuit output depends only on the present input values. A sequential circuit output depends on present inputs and stored state, so it has memory. [[S2]](#s2)

| Point | Combinational circuit | Sequential circuit |
|---|---|---|
| Output depends on | Present inputs only | Present inputs and previous stored state |
| Memory | No memory element | Has memory element |
| Clock requirement | Usually no clock needed | Usually controlled by clock or enable |
| Feedback | Normally no feedback for storage | Feedback or storage element is present |
| Timing | Mainly propagation delay matters | Setup time, hold time, clock-to-Q, and clock period matter |
| Basic building blocks | Gates, adders, muxes, encoders, decoders | Latches, flip-flops, registers, counters, FSMs |
| Example | Half adder, full adder, MUX | Counter, register, sequence detector, FSM |

**Simple example:**

```text
Combinational:
Y = A + B
Output changes only according to current A and B.

Sequential:
Q_next = D at clock edge
Output depends on clocked storage, not only current input.
```

**Important point:**

A sequential circuit is usually built by combining combinational logic with memory elements. The combinational logic calculates next state and output, and the memory element stores the state.

**Speak like this:**

"A combinational circuit has no memory. Its output depends only on the present inputs, like a mux or adder. A sequential circuit has memory, so its output depends on the present inputs and the stored state. Examples are flip-flops, counters, registers, and FSMs. In sequential circuits we also care about clock timing, setup time, hold time, and clock-to-Q delay."

[Back to index](./index.md)

<a id="q31"></a>
## 31. Draw a state machine of Mealy overlapping and non-overlapping sequences.

**Written answer:**

**Definition to remember:** A finite state machine (FSM) is a sequential circuit that can exist in only a finite number of states. In hardware, it is usually built from a state register, next-state combinational logic, and output combinational logic. The state register stores the present state; the next-state logic uses the present state and inputs to decide the next state; and the output logic produces the output. [[S2]](#s2) [[S53]](#s53)

For a sequence detector FSM, each state represents how much of the target bit pattern has already been matched. In a Mealy sequence detector, the output depends on the present state and the current input, so the detection output is written on the transition that completes the sequence. [[S23]](#s23) [[S53]](#s53)

Here I am using the common interview example sequence:

```text
Target sequence = 1010
Transition label = input/output
```

**State meaning:**

| State | Meaning |
|---|---|
| S0 | No useful match yet |
| S1 | Matched `1` |
| S2 | Matched `10` |
| S3 | Matched `101` |

### Overlapping Mealy sequence detector for 1010

In overlapping detection, after detecting `1010`, the last `10` can become the beginning of the next possible sequence. So after final detection, the FSM goes to `S2`.

**Transition table:**

| Present state | Input 0 | Input 1 |
|---|---|---|
| S0 | S0 / 0 | S1 / 0 |
| S1 | S2 / 0 | S1 / 0 |
| S2 | S0 / 0 | S3 / 0 |
| S3 | S2 / 1 | S1 / 0 |

**ASCII state diagram:**

```text
S0 --1/0--> S1 --0/0--> S2 --1/0--> S3 --0/1--> S2
^           |           |                         |
|           |1/0        |0/0                      |1/0
+----0/0---+           +-----------0/0-----------+--> S1
```

The important transition is:

```text
S3 --0/1--> S2
```

That means sequence `1010` is detected, output becomes `1`, and the ending `10` is reused for overlap.

### Non-overlapping Mealy sequence detector for 1010

In non-overlapping detection, after detecting one full `1010`, the FSM resets to the initial state and starts fresh.

**Transition table:**

| Present state | Input 0 | Input 1 |
|---|---|---|
| S0 | S0 / 0 | S1 / 0 |
| S1 | S2 / 0 | S1 / 0 |
| S2 | S0 / 0 | S3 / 0 |
| S3 | S0 / 1 | S1 / 0 |

**ASCII state diagram:**

```text
S0 --1/0--> S1 --0/0--> S2 --1/0--> S3 --0/1--> S0
^           |           |                         |
|           |1/0        |0/0                      |1/0
+----0/0---+           +-----------0/0-----------+--> S1
```

The important transition is:

```text
S3 --0/1--> S0
```

That means sequence `1010` is detected, output becomes `1`, and the machine resets to start detecting a new sequence.

**Speak like this:**

"For a Mealy sequence detector, outputs are written on transitions because output depends on state and input. For sequence `1010`, the states represent partial matches: no match, `1`, `10`, and `101`. In overlapping detection, when the final `0` comes from state `S3`, output becomes `1` and the machine goes to `S2`, because the ending `10` can start the next sequence. In non-overlapping detection, after the final `0`, output becomes `1` but the machine goes back to `S0`, because we do not reuse any bits."

[Back to index](./index.md)

<a id="q32"></a>
## 32. Difference between microprocessor and microcontroller.

**Written answer:**

**Definition to remember:** A microprocessor is a CPU-centric processing chip that usually depends on external memory, I/O, and peripheral chips to form a complete system. A microcontroller is a single-chip embedded controller that integrates a CPU, memory, and peripherals such as GPIO, timers, ADC, serial interfaces, and interrupt control on the same chip. [[S24]](#s24) [[S47]](#s47)

| Point | Microprocessor | Microcontroller |
|---|---|---|
| Short name | MPU | MCU |
| Basic idea | CPU-focused chip | Complete embedded controller on one chip |
| Main components | CPU/cache/MMU or memory controller depending on device | CPU + flash/ROM + RAM + GPIO + timers + peripherals |
| Memory | Usually external RAM and storage are required | On-chip flash and RAM are commonly included |
| I/O | Usually needs external peripheral/interface chips | I/O ports and serial interfaces are built in |
| Operating system | Can run large OS like Linux/Windows when paired with memory | Usually runs bare-metal code or RTOS |
| Performance | Higher processing power and higher clock speed | Lower/moderate processing power but optimized for control |
| Power consumption | Usually higher system power | Usually lower power, often has sleep/low-power modes |
| Cost | Higher total board/system cost | Lower total system cost for embedded tasks |
| Board complexity | More external components, more complex PCB | Fewer external components, simpler PCB |
| Real-time control | Possible, but OS and external memory can add complexity | Very suitable for deterministic real-time control |
| Application type | General-purpose computing and application processing | Dedicated embedded control |
| Examples | x86 CPUs, application processors, ARM Cortex-A MPUs | 8051, PIC, AVR, ARM Cortex-M MCUs |
| Used in | PCs, laptops, phones, high-end embedded Linux boards | Washing machines, remotes, sensors, motor control, IoT nodes |

**Important distinctions:**

1. **Integration:** The biggest difference is integration. A microprocessor mainly provides processing capability, while a microcontroller integrates processing plus memory plus I/O on one chip. [[S24]](#s24)

2. **External hardware:** A microprocessor-based system normally needs external RAM, storage, power management, and I/O support. A microcontroller-based system can often run with very few external components because flash, RAM, GPIO, timers, UART/SPI/I2C, ADC, and interrupt controller may already be inside the chip. [[S47]](#s47)

3. **Application goal:** A microprocessor is chosen when we need high computation, complex software, user interface, networking stack, graphics, or a large operating system. A microcontroller is chosen when we need low-cost, low-power, reliable control of a specific task.

4. **Power and cost:** Since microcontrollers include many blocks on one chip and are optimized for embedded tasks, they usually reduce board area, cost, and power. Microprocessors can be much more powerful, but the total system usually consumes more power and costs more.

5. **Software style:** Microprocessors often run OS-based applications. Microcontrollers often run firmware, bare-metal code, interrupt-driven code, or an RTOS.

6. **Real-time behavior:** Microcontrollers are commonly preferred for real-time control because the firmware directly controls peripherals and interrupts. Microprocessor systems can also do real-time tasks, but an OS and external memory can add latency unless designed carefully.

**Advantages of microprocessor:**

1. Higher processing capability for complex tasks.
2. Better for running large operating systems.
3. Can support high memory capacity.
4. Suitable for graphics, networking, multimedia, and application-level processing.
5. More flexible for general-purpose computing.

**Advantages of microcontroller:**

1. CPU, memory, and peripherals are integrated on one chip.
2. Lower cost and smaller board size.
3. Lower power consumption, with sleep and low-power modes.
4. Better suited for direct hardware control.
5. Easier to use for sensors, motors, buttons, displays, and embedded I/O.
6. Good for real-time and interrupt-driven tasks.

**When to choose which:**

| Requirement | Better choice |
|---|---|
| Run Linux/Windows or a rich OS | Microprocessor |
| Control a motor, sensor, relay, or embedded device | Microcontroller |
| Need high processing and large memory | Microprocessor |
| Need low power, low cost, small PCB | Microcontroller |
| Need direct GPIO/timer/ADC control | Microcontroller |
| Need graphics/multimedia/application processing | Microprocessor |

**Interview nuance:**

Modern SoCs can blur the boundary because some application processors include many peripherals, and some high-end microcontrollers are very powerful. But for interview basics, the clean distinction is: microprocessor is CPU-centric and usually needs external memory/I/O, while microcontroller is integrated and optimized for embedded control.

**Speak like this:**

"A microprocessor is mainly a CPU-focused chip. To build a complete system around it, we usually connect external memory, storage, and I/O peripherals. It is used when high processing power, large memory, and complex software are needed, like computers or application processors. A microcontroller integrates CPU, flash, RAM, GPIO, timers, ADC, communication interfaces, and interrupt control on one chip. Because of that, it is smaller, cheaper, lower power, and better for embedded control tasks like sensors, motor control, appliances, and IoT devices. So the simple distinction is: microprocessor is for computation-heavy general processing; microcontroller is for integrated embedded control."

[Back to index](./index.md)

<a id="q33"></a>
## 33. What are stack pointer and program counter?

**Written answer:**

**Program counter definition:** The program counter, or PC, is a processor register that holds the address of the next instruction to be fetched or executed. It is also called the instruction pointer in some architectures. [[S25]](#s25)

**Stack pointer definition:** The stack pointer, or SP, is a processor register that points to the top of the stack, or to the next stack location depending on the processor convention. The stack is used for function calls, return addresses, local variables, saved registers, and interrupts. [[S26]](#s26)

| Point | Program Counter (PC) | Stack Pointer (SP) |
|---|---|---|
| Stores | Address of next instruction | Address of top/current stack location |
| Main use | Controls instruction flow | Manages stack memory |
| Changes during | Normal instruction execution, branch, jump, call, interrupt, return | Push, pop, function call, interrupt, return |
| Related to | Fetch-decode-execute cycle | Function calls and temporary storage |
| Example | After branch, PC gets target address | On push, SP moves and data is stored on stack |

**Simple flow:**

```text
PC -> tells CPU which instruction to execute next.
SP -> tells CPU where stack data is stored.
```

**Speak like this:**

"The program counter stores the address of the next instruction, so it controls program flow. During normal execution it increments, and during jump, branch, call, or interrupt it loads a new address. The stack pointer points to the top of the stack. It changes during push, pop, function calls, returns, and interrupts. So PC is about instruction flow, while SP is about stack memory management."

[Back to index](./index.md)

<a id="q34"></a>
## 34. Difference between RISC and CISC processor.

**Written answer:**

**Definition to remember:** RISC means Reduced Instruction Set Computer, where the instruction set is simpler and usually optimized for fast pipelined execution. CISC means Complex Instruction Set Computer, where the instruction set has more complex instructions and more addressing modes. [[S27]](#s27)

| Point | RISC | CISC |
|---|---|---|
| Full form | Reduced Instruction Set Computer | Complex Instruction Set Computer |
| Instruction type | Simple instructions | Complex instructions |
| Instruction length | Usually fixed length | Often variable length |
| Addressing modes | Fewer addressing modes | More addressing modes |
| Memory access | Usually load-store: only load/store access memory | Many instructions can directly operate on memory |
| Execution | Often designed for one or few cycles per instruction | Some instructions may take multiple cycles |
| Hardware | Simpler control logic | More complex control logic, often microcode historically |
| Compiler role | Compiler does more work | Hardware can do more complex operations |
| Pipelining | Easier because instructions are regular | Harder because instruction length and behavior vary |
| Code size | Can be larger because more instructions are needed | Can be smaller because one instruction may do more work |
| Examples | ARM, MIPS, RISC-V, SPARC | x86, VAX, 8051 style CISC examples |

**Important nuance:**

Modern processors are not always purely RISC or purely CISC internally. For example, modern x86 processors may translate complex instructions into simpler internal micro-operations. But for interviews, the table above is the standard conceptual difference.

**Speak like this:**

"RISC uses a smaller and simpler instruction set, usually with fixed-length instructions and load-store architecture. That makes decoding and pipelining easier. CISC has more complex instructions, variable instruction lengths, and more addressing modes. A single CISC instruction can do more work, but it may take more cycles and can make hardware more complex. Modern CPUs blur the boundary, but conceptually RISC favors simpler instructions and speed, while CISC favors richer instructions and compact code."

[Back to index](./index.md)

<a id="q35"></a>
## 35. What is tri-state logic?

**Written answer:**

**Definition to remember:** Tri-state logic has three output states: logic `0`, logic `1`, and high impedance `Z`. In high-impedance state, the output is effectively disconnected from the circuit. [[S28]](#s28)

A normal digital output drives either `0` or `1`. A tri-state output can also go to `Z`, meaning it does not actively drive the line.

**Tri-state buffer behavior:**

| Enable | Input | Output |
|---:|---:|---|
| 0 | X | Z |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

**Why it is used:**

1. It allows multiple devices to share the same bus.
2. Only one device should drive the bus at a time.
3. Other devices stay in high-impedance state so they do not fight the active driver.

**Important warning:**

If two outputs drive the same bus at the same time and one drives `1` while another drives `0`, bus contention happens. That can cause wrong logic and may damage hardware.

**Verilog example:**

```verilog
assign bus = enable ? data : 1'bz;
```

**Speak like this:**

"Tri-state logic means the output can be `0`, `1`, or high impedance `Z`. High impedance means the output is not driving the line, almost like it is disconnected. This is useful for shared buses because only one device should drive the bus at a time, while others remain in `Z`. If two devices drive opposite values at the same time, bus contention can occur."

[Back to index](./index.md)

<a id="q36"></a>
## 36. Implement XOR logic using NOR gates.

**Written answer:**

**Definition to remember:** NOR is a universal gate, so any Boolean function, including XOR, can be implemented using only NOR gates. [[S9]](#s9) [[S29]](#s29)

XOR output is `1` when the two inputs are different.

```text
Y = A xor B = A'B + AB'
```

**Truth table:**

| A | B | XOR |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

**NOR-only implementation using 5 NOR gates:**

```text
n1 = NOR(A, B)       = (A + B)'
n2 = NOR(A, n1)      = A'B
n3 = NOR(B, n1)      = AB'
n4 = NOR(n2, n3)     = (A'B + AB')'   // XNOR
Y  = NOR(n4, n4)     = A'B + AB'      // XOR
```

**ASCII diagram:**

```text
A ----+---- NOR ---- n1
B ----+

A ----+---- NOR ---- n2
n1 ---+

B ----+---- NOR ---- n3
n1 ---+

n2 ---+---- NOR ---- n4
n3 ---+

n4 ---+---- NOR ---- Y
n4 ---+
```

**Verilog structural code:**

```verilog
module xor_using_nor (
    input  a,
    input  b,
    output y
);
wire n1;
wire n2;
wire n3;
wire n4;

nor g1 (n1, a, b);
nor g2 (n2, a, n1);
nor g3 (n3, b, n1);
nor g4 (n4, n2, n3);
nor g5 (y, n4, n4);

endmodule
```

**Speak like this:**

"Since NOR is a universal gate, XOR can be built using only NOR gates. I first generate `n1 = (A+B)'`. Then using `A NOR n1` and `B NOR n1`, I create the two XOR product terms `A'B` and `AB'`. NORing those terms gives XNOR, and one final NOR used as an inverter gives XOR."

[Back to index](./index.md)

<a id="q37"></a>
## 37. What are FFT and DFT?

**Written answer:**

**DFT definition:** The Discrete Fourier Transform converts a finite-length discrete-time signal from the time domain into frequency-domain components. It tells which frequencies are present in the sampled signal.

**FFT definition:** The Fast Fourier Transform is an efficient algorithm used to compute the DFT faster. [[S30]](#s30)

| Point | DFT | FFT |
|---|---|---|
| Full form | Discrete Fourier Transform | Fast Fourier Transform |
| Meaning | Mathematical transform | Algorithm to compute DFT |
| Purpose | Converts samples to frequency components | Computes same DFT result efficiently |
| Speed | Direct DFT is slow for large N | Much faster for large N |
| Complexity | About `O(N^2)` | About `O(N log N)` |
| Output | Frequency-domain samples | Same frequency-domain samples |
| Use | Signal analysis concept | Practical implementation in DSP/software/hardware |

**Simple idea:**

```text
DFT tells what frequencies are inside the signal.
FFT is the fast method used to calculate the DFT.
```

**Example:**

If we record a sound signal using a microphone, the time-domain samples show amplitude versus time. DFT/FFT helps convert that into frequency information, such as bass, mid, and high-frequency components.

**Speak like this:**

"DFT is the mathematical transform that converts discrete time-domain samples into frequency-domain components. FFT is not a different transform; it is a fast algorithm to compute the same DFT result. Direct DFT takes around `N^2` operations, while FFT takes around `N log N`, so FFT is used practically in DSP, communication, audio, image processing, and spectrum analysis."

[Back to index](./index.md)

<a id="q38"></a>
## 38. Explain Nyquist stability criterion.

**Written answer:**

**Definition to remember:** Nyquist stability criterion is a graphical method used in control systems to determine closed-loop stability from the open-loop frequency response, without directly solving for all closed-loop poles. [[S31]](#s31)

For a feedback system with loop gain:

```text
L(s) = G(s)H(s)
```

The Nyquist plot of `L(s)` is checked around the critical point:

```text
-1 + j0
```

**Nyquist formula:**

Using the common convention where clockwise encirclements of `-1 + j0` are positive:

```text
Z = N + P
```

Where:

| Symbol | Meaning |
|---|---|
| `Z` | Number of right-half-plane closed-loop poles |
| `N` | Number of clockwise encirclements of `-1 + j0` by the Nyquist plot |
| `P` | Number of right-half-plane open-loop poles |

For closed-loop stability:

```text
Z = 0
```

That means the closed-loop system should have no right-half-plane poles.

**Special case:**

If the open-loop system has no right-half-plane poles:

```text
P = 0
```

Then for stability:

```text
N = 0
```

So the Nyquist plot should not encircle the point `-1 + j0`.

**Why it is useful:**

1. It predicts closed-loop stability from open-loop frequency response.
2. It is useful when directly finding closed-loop poles is difficult.
3. It also gives insight into gain margin and phase margin.

**Speak like this:**

"Nyquist criterion checks closed-loop stability using the open-loop frequency response. We draw the Nyquist plot of `G(s)H(s)` and observe encirclements of the critical point `-1 + j0`. With clockwise encirclements taken as positive, the relation is `Z = N + P`, where `Z` is right-half-plane closed-loop poles, `N` is encirclements, and `P` is right-half-plane open-loop poles. For stability, `Z` must be zero. So if the open-loop system is stable, the Nyquist plot should not encircle `-1 + j0`."

[Back to index](./index.md)

<a id="q39"></a>
## 39. What is ADC?

**Written answer:**

**Definition to remember:** An ADC, or Analog-to-Digital Converter, converts a continuous analog signal into a digital number that a digital system can store, process, or transmit. [[S32]](#s32)

An analog signal can have any value within a range, but a digital system works with discrete binary values. So ADC conversion mainly involves three ideas:

1. **Sampling:** The analog signal is measured at discrete time instants.
2. **Quantization:** Each sampled value is mapped to the nearest available digital level.
3. **Encoding:** The quantized level is represented as a binary code.

**Simple ADC block:**

```text
Analog input -> Sample/Hold -> Quantizer -> Encoder -> Digital output
```

**Important terms:**

| Term | Meaning |
|---|---|
| Resolution | Number of bits in the ADC output |
| Sampling rate | How many samples are taken per second |
| Quantization step | Smallest voltage difference represented by one digital step |
| Reference voltage | Voltage range used for conversion |
| Quantization error | Difference between actual analog value and represented digital value |

**Resolution example:**

For an `N`-bit ADC:

```text
Number of levels = 2^N
```

For an 8-bit ADC:

```text
Number of levels = 2^8 = 256
```

If the reference range is `0 V` to `5 V`:

```text
Step size = 5 V / 256 = 19.53 mV approximately
```

**Speak like this:**

"ADC stands for Analog-to-Digital Converter. It converts a continuous analog signal into a digital binary value. The main steps are sampling, quantization, and encoding. Sampling measures the signal at discrete time instants, quantization maps each sample to the nearest digital level, and encoding converts that level into binary. Resolution tells how many digital levels are available. For example, an 8-bit ADC has 256 levels."

[Back to index](./index.md)

<a id="q40"></a>
## 40. Explain the communication channel from microphone analog input to receiver output.

**Written answer:**

**Definition to remember:** A communication system transfers information from a source to a destination through a transmitter, channel, and receiver. The channel is the medium or path through which the signal travels, and noise/interference can affect it. [[S33]](#s33)

For microphone audio, the source signal is analog sound pressure. The microphone converts sound into an electrical analog signal. If we transmit it digitally, the signal is converted to digital at the transmitter and converted back to analog at the receiver.

**Block diagram:**

```text
Speaker voice
    |
Microphone / input transducer
    |
Analog audio signal
    |
Pre-amplifier + filter
    |
ADC
    |
Source encoding / compression
    |
Channel encoding / error protection
    |
Modulation / transmitter
    |
Communication channel + noise
    |
Receiver / demodulation
    |
Channel decoding
    |
Source decoding
    |
DAC
    |
Amplifier + speaker
    |
Received sound
```

**Step-by-step explanation:**

1. **Microphone:** Converts sound waves into an analog electrical signal.
2. **Pre-amplifier:** Increases the weak microphone signal.
3. **Anti-aliasing filter:** Removes high-frequency components before sampling.
4. **ADC:** Converts analog samples into digital binary values.
5. **Source encoder:** Compresses or formats the data, for example audio coding.
6. **Channel encoder:** Adds redundancy so errors caused by noise can be detected or corrected.
7. **Modulator/transmitter:** Converts digital data into a signal suitable for the channel.
8. **Channel:** The physical or wireless medium. It may add noise, attenuation, distortion, or interference.
9. **Receiver/demodulator:** Recovers digital data from the received signal.
10. **Channel decoder:** Detects or corrects transmission errors.
11. **Source decoder:** Reconstructs the digital audio samples.
12. **DAC:** Converts digital samples back into an analog waveform.
13. **Speaker/amplifier:** Converts the analog electrical signal back into sound.

**Speak like this:**

"At the transmitter, the microphone converts sound into an analog voltage. That signal is amplified and filtered, then an ADC converts it into digital samples. The digital data may be compressed, encoded for error protection, and modulated for transmission. The channel carries the signal but can add noise and distortion. At the receiver, demodulation and decoding recover the digital data, a DAC converts it back to analog, and the speaker converts it back into sound."

[Back to index](./index.md)

<a id="q41"></a>
## 41. Draw CMOS diagram of AND and OR with inverter, NAND, and NOR.

**Written answer:**

**Definition to remember:** In static CMOS logic, the pull-up network is made using PMOS transistors connected to `VDD`, and the pull-down network is made using NMOS transistors connected to ground. The PMOS and NMOS networks are complementary. [[S34]](#s34)

### CMOS inverter

```text
          VDD
           |
        PMOS gate=A
           |
           +------ Y = A'
           |
        NMOS gate=A
           |
          GND
```

When `A = 0`, PMOS is ON and NMOS is OFF, so `Y = 1`.
When `A = 1`, PMOS is OFF and NMOS is ON, so `Y = 0`.

### CMOS NAND gate

For NAND:

```text
Y = (A . B)'
```

PMOS transistors are in parallel. NMOS transistors are in series.

```text
             VDD
            /   \
      PMOS A     PMOS B
            \   /
             +-------- Y = (A.B)'
             |
          NMOS A
             |
          NMOS B
             |
            GND
```

### CMOS AND gate

AND is made using NAND followed by inverter:

```text
A, B -> CMOS NAND -> inverter -> Y = A.B
```

```text
Y_nand = (A.B)'
Y      = ((A.B)')' = A.B
```

### CMOS NOR gate

For NOR:

```text
Y = (A + B)'
```

PMOS transistors are in series. NMOS transistors are in parallel.

```text
             VDD
              |
           PMOS A
              |
           PMOS B
              |
              +-------- Y = (A+B)'
             / \
       NMOS A   NMOS B
             \ /
             GND
```

### CMOS OR gate

OR is made using NOR followed by inverter:

```text
A, B -> CMOS NOR -> inverter -> Y = A+B
```

```text
Y_nor = (A+B)'
Y     = ((A+B)')' = A+B
```

**Why AND and OR use inverter:**

Basic static CMOS naturally gives inverting gates like NAND and NOR. So non-inverting gates like AND and OR are commonly made by adding an inverter after NAND or NOR.

**Speak like this:**

"In CMOS, PMOS forms the pull-up network to `VDD`, and NMOS forms the pull-down network to ground. A NAND gate has PMOS in parallel and NMOS in series. An AND gate is NAND followed by an inverter. A NOR gate has PMOS in series and NMOS in parallel. An OR gate is NOR followed by an inverter. So NAND and NOR are the basic CMOS structures, while AND and OR are obtained by adding inversion."

[Back to index](./index.md)

<a id="q42"></a>
## 42. Draw NMOS diagram, explain working, and explain characteristic regions.

**Written answer:**

**Definition to remember:** An NMOS transistor is an n-channel MOSFET in which gate-to-source voltage controls formation of an n-type channel between source and drain. [[S35]](#s35)

**Basic NMOS structure:**

```text
             Gate
              |
          +--------+
          | oxide  |
Drain n+  |        |  Source n+
   D -----+        +----- S
          p-type substrate/body
              |
             Body
```

**Symbol idea:**

```text
          D
          |
      ----|
G ----|   |---- S
      ----|
```

**Working:**

1. The NMOS has source and drain n+ regions in a p-type substrate.
2. The gate is insulated from the channel by oxide.
3. When `VGS < VTH`, no strong channel forms, so the transistor is OFF.
4. When `VGS > VTH`, an inversion channel forms under the gate.
5. If `VDS` is applied, electrons flow from source to drain, so conventional drain current flows from drain to source.

**Characteristic regions:**

| Region | Condition | Behavior |
|---|---|---|
| Cutoff | `VGS < VTH` | Channel is not formed; `ID` is approximately zero |
| Linear/Triode | `VGS > VTH` and `VDS < VGS - VTH` | NMOS behaves like a voltage-controlled resistor |
| Saturation | `VGS > VTH` and `VDS >= VGS - VTH` | Channel pinches near drain; current is controlled mainly by `VGS` |

**Drain characteristic graph idea:**

```text
ID
^
|                         VGS high
|                    ____---------
|               ____-
|          ____-
|     ____-       saturation
|____-
|  linear/triode
+-------------------------------> VDS
 cutoff is near ID = 0 when VGS < VTH
```

**Use in digital logic:**

In CMOS logic, NMOS is good at pulling output down to `0`. It turns ON when gate input is `1` and turns OFF when gate input is `0`.

**Speak like this:**

"An NMOS is an n-channel MOSFET. It has n+ source and drain regions in a p-type substrate, and the gate controls the channel through an oxide layer. When `VGS` is less than threshold voltage, it is in cutoff and no strong channel exists. When `VGS` is greater than threshold and `VDS` is small, it works in linear or triode region like a controlled resistor. When `VDS` becomes greater than or equal to `VGS - VTH`, it enters saturation, where current is mainly controlled by gate voltage."

[Back to index](./index.md)

<a id="q43"></a>
## 43. What is latch-up?

**Written answer:**

**Definition to remember:** Latch-up is a failure condition in CMOS ICs where a parasitic PNPN/SCR-like structure turns ON and creates a low-impedance path between `VDD` and `GND`. Once triggered, a large current can keep flowing even after the trigger is removed, and the IC may be damaged unless current is limited or power is removed. [[S36]](#s36) [[S48]](#s48) [[S49]](#s49)

**Why it happens:**

In a bulk CMOS process, PMOS and NMOS transistors are built inside wells and substrate. Because of these p-type and n-type regions, unwanted parasitic bipolar transistors are also formed inside the chip.

The important parasitic devices are:

```text
Parasitic PNP transistor
Parasitic NPN transistor
Well/substrate resistances
```

Together, the parasitic PNP and NPN transistors can form a PNPN structure, similar to an SCR or thyristor. If this structure gets triggered, it creates positive feedback: current in one parasitic transistor helps turn ON the other, and the second helps keep the first ON. [[S48]](#s48)

Once this happens, the chip can behave as if there is a near-short path:

```text
VDD -> parasitic path -> GND
```

This is why latch-up is dangerous: the normal MOS gates may lose control, supply current rises sharply, and the device can overheat or fail.

**Simple cross-section idea:**

```text
VDD
 |
P+ diffusion in N-well      N+ diffusion in P-substrate/P-well
      |                                  |
   parasitic PNP  <---- feedback ----> parasitic NPN
      |                                  |
   well/substrate resistance paths
      |
GND
```

Interview meaning: the CMOS structure unintentionally contains two BJTs connected like a thyristor. Latch-up is when this unintended thyristor turns ON.

**Causes:**

1. Input or output voltage going above `VDD` or below `GND`.
2. ESD, surge voltage, or transient current on an I/O pin.
3. Sharp supply-voltage changes or incorrect power sequencing.
4. Large substrate or well current.
5. Poor well/substrate contacts, causing voltage drops in substrate or well resistance.
6. Noise injection from nearby high-current or switching circuits.

**What happens during latch-up:**

1. A disturbance injects current into the substrate or well.
2. Voltage drop across substrate/well resistance forward-biases a parasitic junction.
3. A parasitic BJT turns ON.
4. That BJT turns ON the complementary parasitic BJT.
5. Positive feedback forms an SCR-like conduction path.
6. A large current flows from supply to ground.
7. The condition may stay latched until power is removed or current falls below the holding current. [[S48]](#s48)

**Prevention methods:**

1. **Guard rings:** Surround sensitive devices with guard rings to collect injected carriers and reduce substrate noise.
2. **Well taps and substrate contacts:** Add enough taps so well/substrate resistance is low and parasitic junctions are not easily forward biased.
3. **Proper spacing:** Increase spacing between PMOS and NMOS devices where latch-up risk is high.
4. **ESD protection:** Use proper ESD structures at I/O pads.
5. **Stay within voltage ratings:** Do not let input/output pins go above `VDD` or below `GND`.
6. **Good power sequencing:** Avoid powering I/O before supply rails if the IC does not allow it.
7. **Use latch-up resistant processes:** SOI or special CMOS processes can reduce parasitic paths.
8. **Current limiting:** In board design, series resistance or current limiting can reduce damage risk if abnormal current occurs.

**Short interview distinction:**

Latch-up is not a normal logic latch. A logic latch stores a bit intentionally. CMOS latch-up is an unwanted parasitic short-circuit condition inside the IC.

**Speak like this:**

"Latch-up is an unwanted failure condition in CMOS. Because of the p-type and n-type regions in a CMOS process, parasitic PNP and NPN transistors are naturally formed. These parasitic transistors can connect like a PNPN SCR structure. If an I/O overvoltage, ESD pulse, supply transient, or substrate current triggers it, a low-impedance path forms between `VDD` and ground. Then large current can continue flowing even after the trigger is removed, so the chip can heat up or get damaged. We prevent latch-up using guard rings, proper well and substrate contacts, enough spacing, ESD protection, correct power sequencing, and by keeping pins within supply limits."

[Back to index](./index.md)

<a id="q44"></a>
## 44. Difference between asynchronous and synchronous circuits.

**Written answer:**

**Definition to remember:** A synchronous sequential circuit uses a clock signal, so storage elements change state only at defined clock events, such as a rising or falling edge. An asynchronous sequential circuit does not use a global clock; its state/output can change whenever inputs change and internal delays settle. [[S37]](#s37) [[S50]](#s50)

| Point | Synchronous circuit | Asynchronous circuit |
|---|---|---|
| Clock | Uses a clock | No global clock |
| State change | At defined clock edges or clock levels | Immediately after input changes, depending on circuit delay |
| Timing reference | Clock period controls operation | Propagation delays and feedback paths control operation |
| Storage elements | Flip-flops/registers are common | Latches, feedback paths, or unclocked storage can be used |
| Predictability | More predictable because updates happen at clock boundaries | Less predictable unless delay/race conditions are carefully controlled |
| Timing analysis | Setup, hold, clock skew, clock-to-Q, max frequency | Races, hazards, stable states, fundamental-mode assumptions |
| Design difficulty | Easier to design, simulate, synthesize, and test | Harder to design and verify |
| Speed | Limited by worst-case clock period | Can be faster because it does not wait for a global clock |
| Power | Clock tree consumes dynamic power | No global clock tree, so potential power saving |
| Common use | Most CPUs, registers, counters, synchronous FSMs, pipelines | Handshake circuits, self-timed circuits, ripple counters, some interfaces |

**How synchronous circuits work:**

In a synchronous circuit, all important state elements are controlled by the clock. The input may change between clock edges, but the state is captured only at the active edge. This gives a clean design rule:

```text
Current state + input -> combinational logic -> next state
Next state is stored only at the clock edge
```

That is why synchronous design is easier to analyze. We mainly check setup time, hold time, clock skew, and whether the combinational logic delay fits inside the clock period. [[S4]](#s4)

**How asynchronous circuits work:**

In an asynchronous circuit, there is no global clock edge telling all storage elements when to update. The circuit reacts directly to input changes. The next state depends on logic delays and feedback paths:

```text
Input changes -> internal signals change after gate delays -> circuit reaches a new stable state
```

This can be fast, but it also means delay differences matter. If two internal signals change at different times, the circuit may temporarily go through an unwanted state. This creates race and hazard problems if not designed carefully. [[S50]](#s50)

**Advantages of synchronous circuits:**

1. Easier timing analysis because the clock defines update points.
2. Easier to design using flip-flops, registers, and FSMs.
3. Easier to synthesize and verify with standard EDA tools.
4. More predictable behavior in large systems.
5. Common design style for processors, digital controllers, pipelines, and SoCs.

**Disadvantages of synchronous circuits:**

1. Clock tree consumes power.
2. Maximum speed is limited by worst-case path delay.
3. Clock skew and jitter must be controlled.
4. Every block may wait for the clock even if some operations finish early.

**Advantages of asynchronous circuits:**

1. No global clock tree, so potential power saving.
2. Can be faster in some cases because operation happens when data is ready.
3. Useful for handshake-based communication and some clock-domain/interface designs.
4. Can reduce electromagnetic noise from a large global clock.

**Disadvantages of asynchronous circuits:**

1. More difficult to design correctly.
2. Sensitive to gate delays, wire delays, races, and hazards.
3. Harder to test and verify.
4. Tool support is less straightforward than synchronous RTL flow.
5. Glitches can become functional problems, not just temporary waveform noise.

**Important interview point:**

Most modern digital systems are mainly synchronous because clocked design is easier to analyze, simulate, synthesize, and test. Asynchronous circuits can be useful and even faster/lower power in some situations, but they require careful handling of races, hazards, and delay assumptions.

**One-line summary:**

```text
Synchronous = clock controls state changes.
Asynchronous = input changes and circuit delays control state changes.
```

**Speak like this:**

"A synchronous circuit uses a clock, so state changes happen only at defined clock edges or clock levels. That makes behavior predictable, because I can check setup time, hold time, clock-to-Q delay, and clock period. An asynchronous circuit does not use a global clock. It responds directly to input changes, and the final state depends on gate delays and feedback paths. Because it does not wait for a clock, it can be fast and may save clock power, but it is harder to design because races, hazards, and delay assumptions become critical. So in practice, most large digital systems are synchronous, while asynchronous design is used carefully in special cases like handshaking, ripple counters, or self-timed circuits."

[Back to index](./index.md)

<a id="q45"></a>
## 45. Write Verilog code for a 2-bit counter with circuit and truth table.

**Written answer:**

**Definition to remember:** A counter is a sequential circuit that advances through a fixed sequence of states on clock events. A 2-bit binary up counter counts from `00` to `11` and then rolls over to `00`. [[S21]](#s21)

**2-bit up-counter sequence:**

```text
00 -> 01 -> 10 -> 11 -> 00
```

**Truth table / state table:**

| Present Q1 | Present Q0 | Next Q1 | Next Q0 | Decimal |
|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 1 | 0 -> 1 |
| 0 | 1 | 1 | 0 | 1 -> 2 |
| 1 | 0 | 1 | 1 | 2 -> 3 |
| 1 | 1 | 0 | 0 | 3 -> 0 |

**Next-state equations:**

```text
Q0_next = Q0'
Q1_next = Q1 xor Q0
```

So a 2-bit synchronous counter can be built using two D flip-flops:

```text
D0 = Q0'
D1 = Q1 xor Q0
```

**Circuit idea:**

```text
             +---------+
 D1 <--------| XOR     |<---- Q1
             | Q1,Q0   |<---- Q0
             +---------+
                |
             +------+
 CLK ------->| DFF  |---- Q1
 RST ------->|      |
             +------+

 Q0 -- NOT --> D0
                |
             +------+
 CLK ------->| DFF  |---- Q0
 RST ------->|      |
             +------+
```

**Verilog code:**

```verilog
module counter_2bit (
    input        clk,
    input        rst,
    output reg [1:0] count
);

always @(posedge clk) begin
    if (rst)
        count <= 2'b00;
    else
        count <= count + 2'b01;
end

endmodule
```

**Verilog with explicit next-state equations:**

```verilog
module counter_2bit_logic (
    input  clk,
    input  rst,
    output reg q1,
    output reg q0
);
wire d0;
wire d1;

assign d0 = ~q0;
assign d1 = q1 ^ q0;

always @(posedge clk) begin
    if (rst) begin
        q1 <= 1'b0;
        q0 <= 1'b0;
    end else begin
        q1 <= d1;
        q0 <= d0;
    end
end

endmodule
```

**Speak like this:**

"A 2-bit up counter is a synchronous sequential circuit with four states: `00`, `01`, `10`, and `11`. On every active clock edge, it moves to the next state and after `11` it rolls over to `00`. The simple RTL is `count <= count + 1`. If I draw it using D flip-flops, then `D0 = Q0'` because the LSB toggles every clock, and `D1 = Q1 xor Q0` because the MSB toggles when `Q0` is 1."

[Back to index](./index.md)

<a id="q46"></a>
## 46. What is FIFO and how does it work?

**Written answer:**

**Definition to remember:** FIFO means First-In, First-Out. It is an ordered queue or memory buffer in which the first data item accepted on the write side becomes the first data item available on the read side. In other words, a FIFO always outputs the oldest unread entry first. [[S38]](#s38) [[S39]](#s39) [[S44]](#s44)

In digital design, a FIFO is used as a temporary hardware buffer between two blocks while preserving data order. One block writes data into the FIFO, another block reads data out of it, and the FIFO keeps the sequence unchanged. This is especially useful when the producer and consumer work at different speeds, or when data must safely move between different clock domains. [[S39]](#s39)

**Basic FIFO idea:**

```text
Write side                         Read side
---------                          ---------
data_in -> [ FIFO memory buffer ] -> data_out
          write pointer  read pointer
```

**How it works:**

1. **Write/enqueue:** New data is written at the location pointed to by the write pointer.
2. **Write pointer update:** After writing, the write pointer moves to the next location.
3. **Read/dequeue:** Data is read from the location pointed to by the read pointer.
4. **Read pointer update:** After reading, the read pointer moves to the next location.
5. **Empty condition:** FIFO is empty when there is no unread data.
6. **Full condition:** FIFO is full when there is no free location for new data.

**FIFO status flags:**

| Flag | Meaning |
|---|---|
| `empty` | No data available to read |
| `full` | No space available to write |
| `almost_empty` | Very few entries remain |
| `almost_full` | Very few empty locations remain |

**Example:**

```text
Write order: A, B, C, D
Read order : A, B, C, D
```

The first value written, `A`, is the first value read.

**Synchronous vs asynchronous FIFO:**

| Type | Meaning |
|---|---|
| Synchronous FIFO | Read and write use the same clock |
| Asynchronous FIFO | Read and write use different clocks |

An asynchronous FIFO is commonly used for clock-domain crossing because it safely transfers data between blocks running on different clocks. In that case, pointer synchronization and full/empty logic are very important.

**Speak like this:**

"FIFO stands for First-In, First-Out. It works like a queue: the first data written is the first data read. Internally, a FIFO usually has memory, a write pointer, a read pointer, and status flags like full and empty. On write, data goes into the write pointer location and the write pointer increments. On read, data comes out from the read pointer location and the read pointer increments. FIFOs are useful for buffering data and for transferring data between blocks, especially in clock-domain crossing when using asynchronous FIFO."

[Back to index](./index.md)

<a id="q47"></a>
## 47. Difference between behavioral, dataflow, structural, RTL, and testbench code.

**Written answer:**

**Definition to remember:** Verilog has multiple ways to describe a digital system. Structural, dataflow, and behavioral are modeling styles. RTL is a synthesizable design abstraction that describes registers and the combinational logic between registers. A testbench is not the design hardware; it is simulation code used to verify the design by applying inputs, generating clocks/resets, observing outputs, and checking correctness. [[S5]](#s5) [[S13]](#s13) [[S51]](#s51)

The clean interview distinction is:

```text
Structural / Dataflow / Behavioral = ways to write or model hardware
RTL = synthesizable hardware design level
Testbench = simulation and verification environment
```

### Main Verilog modeling styles

| Topic | What it means | Common constructs | Synthesis meaning | Typical use |
|---|---|---|---|---|
| Structural modeling | Describes the circuit as interconnected components | Gate primitives, module instantiation, wires | Synthesizable if the instantiated blocks are synthesizable | Netlists, gate-level circuits, connecting already-built modules |
| Dataflow modeling | Describes how data flows through equations | `assign`, operators, ternary `?:`, reductions | Usually synthesizable for combinational logic | Boolean equations, muxes, decoders, adders |
| Behavioral modeling | Describes behavior using procedural statements | `always`, `initial`, `if`, `case`, loops, tasks | Synthesizable only when written with synthesis-safe constructs | Combinational RTL, sequential RTL, FSMs, algorithms, simulation models |
| RTL modeling | Describes registers plus combinational logic between registers | `always @(posedge clk)`, `always @(*)`, `assign`, next-state logic | Intended for synthesis into flip-flops, gates, muxes, adders, etc. | Real FPGA/ASIC design |
| Testbench code | Verifies the design in simulation | `initial`, `#` delays, clock/reset generation, `$display`, `$monitor`, `$finish`, checkers | Usually not synthesizable | Stimulus, monitors, scoreboards, expected-output checks |
| Switch-level modeling | Describes transistor/switch behavior | `nmos`, `pmos`, `cmos`, `tran`, `pullup`, `pulldown` | Not normal RTL synthesis flow | Device-level teaching or special low-level experiments |

### The important difference

Structural, dataflow, and behavioral are about **how the design is written**.

RTL is about **whether the description represents real synthesizable hardware at register-transfer level**.

Testbench code is about **verification**, so it can use simulation-only constructs that are not meant to become hardware.

### 1. Structural modeling

**Definition:** Structural modeling describes hardware by explicitly instantiating lower-level blocks and connecting them using nets. It is like drawing a circuit diagram in code: "this gate/module output connects to this wire, and this wire goes into the next gate/module." Verilog supports gate primitives and module instantiation for this style. [[S5]](#s5) [[S51]](#s51)

Use structural modeling when the interconnection itself matters, for example gate-level netlists, top-level module connection, or when building a larger design from smaller verified modules.

**Example:**

```verilog
module and_structural (
    input  a,
    input  b,
    output y
);
and g1 (y, a, b);
endmodule
```

**Synthesis view:** The synthesis tool sees actual instances and connections. If the instantiated blocks are synthesizable, the structural design is synthesizable.

**Interview point:** Structural code answers "what blocks are connected?" It is closest to a schematic or netlist.

### 2. Dataflow modeling

**Definition:** Dataflow modeling describes hardware using continuous assignments. The left-hand side is continuously driven by the right-hand-side expression, so whenever any input in the expression changes, the output is updated by simulation and synthesis treats it as combinational logic. [[S5]](#s5) [[S51]](#s51)

Use dataflow modeling when the circuit is naturally an equation: mux logic, Boolean equations, adders, decoders, comparators, simple ALU expressions, and assign-based glue logic.

**Example:**

```verilog
module mux_dataflow (
    input  a,
    input  b,
    input  sel,
    output y
);
assign y = sel ? b : a;
endmodule
```

**Synthesis view:** `assign y = sel ? b : a;` usually infers a 2:1 mux. `assign y = a & b;` infers an AND function. The designer writes the equation, and synthesis chooses gates/cells to implement it.

**Interview point:** Dataflow code answers "what equation continuously drives this signal?"

### 3. Behavioral modeling

**Definition:** Behavioral modeling describes what the design should do using procedural statements. It uses blocks such as `always` and `initial`, and statements such as `if`, `case`, loops, tasks, and functions. It is more abstract than structural or dataflow modeling because it focuses on behavior rather than direct gate connections. [[S5]](#s5) [[S51]](#s51)

Behavioral code has two possible meanings:

1. **Synthesizable behavioral RTL:** written in a hardware-friendly way, such as `always @(*)` for combinational logic or `always @(posedge clk)` for flip-flops.
2. **Simulation-only behavioral code:** uses delays, file I/O, random stimulus, `$display`, `$finish`, or testbench-only constructs.

**Example:**

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        default: y = d;
    endcase
end
```

**Synthesis view:** If the `always` block has a complete combinational assignment style, it can infer combinational logic such as muxes. If it is edge-triggered, it can infer flip-flops. If it uses simulation delays or unsupported constructs, it is not normal synthesizable RTL.

**Important:** Behavioral does not automatically mean "not synthesizable." Many real RTL designs are written using behavioral `always` blocks. The question is whether the behavior maps to real hardware.

### 4. RTL code

**Definition:** RTL means Register Transfer Level. It describes a design in terms of state elements/registers and the combinational logic that computes the values transferred into those registers on clock edges. RTL is the normal design level used for FPGA and ASIC synthesis. [[S13]](#s13) [[S51]](#s51)

RTL usually has two parts:

1. **Sequential logic:** flip-flops/registers updated on a clock edge.
2. **Combinational logic:** equations, muxes, adders, comparators, and next-state logic between registers.

```verilog
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end

assign y = q & enable;
```

Here, `q` is a flip-flop/register, and `y` is combinational logic from the register output.

**Common RTL coding pattern:**

```verilog
// Sequential register
always @(posedge clk) begin
    if (rst)
        state <= IDLE;
    else
        state <= next_state;
end

// Combinational next-state logic
always @(*) begin
    next_state = state;
    case (state)
        IDLE: if (start) next_state = BUSY;
        BUSY: if (done)  next_state = IDLE;
    endcase
end
```

**Synthesis view:** The first block infers flip-flops. The second block infers combinational logic. Together, they form an FSM-style RTL design.

**Interview point:** RTL is not a Verilog keyword. It is a disciplined synthesizable design style. RTL may use behavioral blocks, dataflow assignments, and structural instantiations together.

### 5. Testbench code

**Definition:** A testbench is a simulation environment around the design under test (DUT). It instantiates the DUT, generates clocks and resets, applies input stimulus, observes outputs, compares actual results with expected results, and ends the simulation. [[S5]](#s5) [[S13]](#s13)

A good testbench commonly contains:

1. **DUT instantiation:** connects to the module being tested.
2. **Clock/reset generation:** creates simulation timing.
3. **Stimulus driver:** applies input cases.
4. **Monitor/checker:** observes and verifies outputs.
5. **Finish condition:** stops simulation using `$finish`.

```verilog
initial begin
    clk = 1'b0;
    forever #5 clk = ~clk;
end

initial begin
    rst = 1'b1;
    d   = 1'b0;
    #20 rst = 1'b0;
    #10 d = 1'b1;
    #10 d = 1'b0;
    #50 $finish;
end
```

This is for simulation only. The `#` delays, `forever` clock generation, and `$finish` are not normal synthesizable RTL design constructs.

### Behavioral vs RTL vs testbench

This is a common interview confusion:

| Code type | Meaning |
|---|---|
| Behavioral code | Uses procedural statements to describe behavior |
| RTL code | Synthesizable hardware description at register-transfer level |
| Testbench code | Simulation-only code to verify the RTL |

So behavioral code can be RTL if it is written in a synthesizable style. Testbench code is also often behavioral, but it is not RTL because it uses simulation-only constructs.

Example:

```verilog
// Behavioral and synthesizable RTL
always @(posedge clk)
    q <= d;

// Behavioral but testbench-only
initial begin
    #10 d = 1'b1;
    #20 $finish;
end
```

### Quick identification

1. If code instantiates gates or submodules, it is structural.
2. If code uses `assign` equations, it is dataflow.
3. If code uses `always`, `initial`, `if`, `case`, or loops, it is behavioral/procedural.
4. If behavioral/dataflow code describes real registers and combinational logic for synthesis, it is RTL.
5. If code generates stimulus, clocks, checks outputs, uses `#` delays, `$display`, `$monitor`, or `$finish`, it is testbench.
6. If code uses transistor primitives like `nmos`, `pmos`, or `tran`, it is switch-level modeling.

**Important interview distinction:**

Behavioral, dataflow, and structural are modeling styles. RTL is a synthesizable abstraction level used for real design. A testbench is verification code, not the design. One Verilog file can also mix styles. For example, an RTL module may use `always @(posedge clk)` for registers, `assign` for combinational logic, and module instantiation structurally to connect sub-blocks.

Also remember: a signal declared as `reg` in Verilog does not always mean a physical register. In older Verilog, `reg` often just means "assigned inside a procedural block." A real flip-flop is inferred from edge-triggered RTL such as `always @(posedge clk)`, not just from the word `reg`.

### Interview-safe summary table

| If interviewer asks | Answer in one line |
|---|---|
| Structural | I describe the exact hardware connection using gates or module instances. |
| Dataflow | I describe continuous equations using `assign`; it is best for combinational logic. |
| Behavioral | I describe operation using procedural blocks like `always` and `initial`; it may or may not be synthesizable. |
| RTL | I describe real synthesizable hardware using registers and combinational logic between registers. |
| Testbench | I write simulation-only code to verify the DUT by driving inputs and checking outputs. |

**Speak like this:**

"I separate these terms into modeling style, design level, and verification code. Structural modeling means I instantiate gates or modules and connect wires, so it looks like a schematic. Dataflow modeling means I use continuous `assign` statements and equations, so it is mainly used for combinational logic. Behavioral modeling means I use procedural blocks like `always` and `initial` with `if`, `case`, and loops to describe what should happen. RTL is the synthesizable register-transfer style: I describe flip-flops/registers and the combinational logic between them. A testbench is different from all of these because it is not the hardware design; it is simulation code that drives clocks, resets, inputs, and checks outputs. So behavioral code can be RTL if it is synthesizable, but behavioral testbench code with delays and `$finish` is not RTL."

[Back to index](./index.md)

<a id="q48"></a>
## 48. Difference between `always` and `initial` block.

**Written answer:**

**Definition to remember:** In Verilog, `initial` and `always` are procedural blocks. Both are enabled when simulation starts. An `initial` block executes once and then stops. An `always` block executes repeatedly forever, so it must contain a timing control such as an event control `@(...)`, delay control `#...`, or `wait` statement; otherwise it can keep executing at the same simulation time. [[S5]](#s5) [[S14]](#s14) [[S52]](#s52)

| Point | `initial` block | `always` block |
|---|---|---|
| Execution count | Runs once | Repeats forever |
| Start time | Starts at simulation time 0 | Starts at simulation time 0 |
| After the last statement | The process finishes | The process immediately starts again |
| Main simulation use | One-time setup, reset stimulus, file setup, `$finish` | Repeated behavior, clocks, monitors, RTL logic |
| Main RTL use | Generally avoided in ASIC RTL; FPGA tools may support some initial register/RAM values | Main procedural block for combinational and sequential RTL |
| Timing control | Optional, but common in testbenches | Required in practice, otherwise zero-time loop can happen |
| Event control use | Can wait for events, but still runs one sequence only | Commonly uses `@(posedge clk)` or `@(*)` to decide when to run |
| Delay use | Common in testbench stimulus | Common for testbench clock generation; not normal synthesizable RTL |
| Synthesizable? | Tool-dependent and limited; do not rely on it for portable ASIC RTL | Synthesizable when written as proper RTL |
| Typical examples | `initial begin ... end` | `always @(posedge clk)`, `always @(*)`, `always #5 clk = ~clk` |

**Important simulation point:** Multiple `initial` and `always` blocks in the same module are independent concurrent processes. They all start at simulation time 0, but statements inside one `begin...end` block execute sequentially.

**Key idea:**

```text
initial = run once
always  = run forever
```

Because `always` runs forever, it needs some statement that blocks the process and allows simulation time to advance or waits for an event.

### 1. `initial` block

An `initial` block is mainly used for one-time simulation behavior. It is very common in testbenches for initializing signals, applying a reset sequence, loading memory, opening files, and stopping the simulation.

```verilog
initial begin
    rst = 1'b1;
    #20 rst = 1'b0;
end
```

This runs once in simulation.

**Testbench example:**

```verilog
initial begin
    clk = 1'b0;
    rst = 1'b1;
    #20 rst = 1'b0;
    #100 $finish;
end
```

This is typical testbench code because it uses delays and `$finish`.

**Synthesis note:** In ASIC-style RTL, do not depend on `initial` for real hardware reset behavior. Use a reset circuit. In FPGA flows, some tools can map declaration-time initial values into device initialization resources, but that is tool/device dependent. AMD Vivado, for example, documents support for initial register values in specific forms. [[S14]](#s14)

### 2. `always` block

An `always` block is used when behavior must repeat. In RTL, it is used mainly for sequential logic and combinational logic. In a testbench, it is also commonly used for clock generation and repeated monitoring.

**Sequential RTL example:**

```verilog
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

This waits for every positive clock edge. In synthesis, this normally infers a flip-flop or register. AMD Vivado describes sequential `always` blocks using a mandatory clock event, with optional asynchronous set/reset events. [[S14]](#s14)

**Combinational RTL example:**

```verilog
always @(*) begin
    y = (a & b) | c;
end
```

This runs when a signal used inside the combinational block changes. `always @(*)` is preferred over manually writing `always @(a or b or c)` because it helps avoid missed-signal sensitivity-list bugs. AMD notes that `@*` helps eliminate simulation mismatches caused by incorrect sensitivity lists. [[S14]](#s14)

**Pure Verilog forms to remember:**

```verilog
always @(*) begin
    // combinational logic
end

always @(posedge clk) begin
    // flip-flop/register logic
end

always @(*) begin
    if (en)
        q = d;   // latch style: q holds when en = 0
end
```

Vivado lists these always procedures and distinguishes their intended use. [[S14]](#s14)

**Why an `always` block without delay/event control creates a zero-time infinite loop:**

Bad code:

```verilog
always begin
    clk = ~clk;   // bad without delay
end
```

Reason:

1. At simulation time 0, the `always` block starts.
2. `clk = ~clk` executes immediately.
3. There is no `#delay`, no `@(event)`, and no `wait`.
4. The block reaches `end`.
5. Because it is an `always` block, it immediately restarts.
6. The assignment runs again in the same simulation time slot.
7. This repeats forever at time 0, so the simulator cannot move to time 1, time 5, or the next event. [[S5]](#s5) [[S52]](#s52)

In short:

```text
always repeats forever + no blocking timing/event control = infinite zero-time loop
```

Correct testbench clock:

```verilog
always #5 clk = ~clk;
```

Here, `#5` blocks the process for 5 time units before each toggle. So simulation time advances:

```text
time 0  -> process starts, waits 5
time 5  -> clk toggles, waits 5
time 10 -> clk toggles, waits 5
...
```

**Equivalent safe style:**

```verilog
initial begin
    clk = 1'b0;
    forever #5 clk = ~clk;
end
```

This is also common in testbenches.

### 3. Synthesis meaning

The same keyword can mean different things depending on the timing control:

| Code pattern | Meaning in simulation | Usual synthesis meaning |
|---|---|---|
| `always @(posedge clk)` | Runs on a rising clock edge | Flip-flop/register |
| `always @(posedge clk or negedge rst_n)` | Runs on clock edge or reset edge | Flip-flop with asynchronous reset |
| `always @(*)` | Runs when used signals change | Combinational logic |
| `always #5 clk = ~clk` | Periodic testbench clock | Not normal synthesizable RTL |
| `initial begin ... end` | One-time simulation process | Usually testbench; limited FPGA initialization support |

AMD's synthesis documentation makes an important distinction: event controls such as `@(posedge clk)` are used to describe hardware events, but delay controls like `#5` are not useful for synthesis and are ignored by synthesis while logic may still be created for the assignment. [[S14]](#s14)

### 4. RTL examples

**Sequential logic:**

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This waits for a clock edge. It infers a flip-flop.

**Combinational logic:**

```verilog
always @(*) begin
    y = (a & b) | c;
end
```

This waits for changes in the signals used in the block. It infers combinational logic if all outputs are assigned in all cases.

**Testbench clock:**

```verilog
always #5 clk = ~clk;
```

This is simulation-only because `#5` delay is not normal synthesizable RTL.

**Common mistakes:**

1. `always begin clk = ~clk; end`
   This causes a zero-time infinite loop.

2. Missing signals in a combinational sensitivity list in old Verilog:

```verilog
always @(a or b) begin
    y = a & b & c;  // c missing from sensitivity list
end
```

This can cause simulation mismatch. Use `always @(*)` for combinational Verilog.

3. Using `initial` as a replacement for reset in portable ASIC RTL.
   A reset is real hardware behavior. An `initial` block is mainly a simulation construct, except for limited FPGA initialization cases.

4. Putting testbench delays inside design RTL:

```verilog
always @(posedge clk) begin
    #5 q <= d;  // do not write normal RTL like this
end
```

Simulation may show a delayed assignment, but synthesis does not implement arbitrary `#5` time delay as hardware.

5. Assigning the same register from multiple procedural blocks.
   This can create multiple-driver ambiguity. For RTL, drive one register from one clocked block.

### Best interview answer structure

1. Start with execution count: `initial` once, `always` forever.
2. Mention both start at time 0 in simulation.
3. Explain that `always` needs a timing/event control to avoid zero-time looping.
4. Say `always @(posedge clk)` is for sequential RTL and `always @(*)` is for combinational RTL.
5. Say `initial` is mostly testbench, with limited FPGA initialization support.

**Speak like this:**

"Both `initial` and `always` are procedural blocks and both are enabled at the start of simulation. The difference is that `initial` runs once and stops, while `always` repeats forever. So I use `initial` mainly in testbenches for one-time initialization, reset stimulus, file setup, and `$finish`. I use `always` when behavior must repeat. In RTL, `always @(posedge clk)` describes sequential logic like flip-flops, and `always @(*)` describes combinational logic. The important trap is that an `always` block must wait for time or an event. If I write `always begin clk = ~clk; end`, there is no delay or event control, so the block executes, reaches the end, immediately restarts, and keeps repeating at the same simulation time. That becomes an infinite zero-time loop. For a testbench clock I write `always #5 clk = ~clk`, but I do not use `#` delays in normal synthesizable RTL."

[Back to index](./index.md)

<a id="q49"></a>
## 49. Can a latch be clocked? Draw output waveforms for latch and flip-flop for a given input waveform.

**Written answer:**

**Definition to remember:** A latch can have an enable or clock control signal, but it is still level-sensitive. That means it is transparent during the active level and holds its previous value during the inactive level. A flip-flop is edge-sensitive and samples input only at the active clock edge. [[S3]](#s3)

So yes, a latch can be "clocked" in the sense that it can have a clock/enable input. But it should be called a clocked latch or gated latch, not an edge-triggered flip-flop.

**D latch behavior:**

Assume active-high enable:

| Enable/CLK | D | Q |
|---:|---:|---|
| 1 | 0 | 0 |
| 1 | 1 | 1 |
| 0 | X | Hold previous Q |

**D flip-flop behavior:**

Assume positive-edge triggered:

| Clock event | D | Q |
|---|---:|---|
| Rising edge | 0 | 0 after clock-to-Q delay |
| Rising edge | 1 | 1 after clock-to-Q delay |
| No edge | X | Hold previous Q |

**How to draw waveform from a given input:**

1. For latch, first mark the active level of enable/clock.
2. During the active level, copy `D` to `Q` after small propagation delay.
3. During the inactive level, keep `Q` constant.
4. For flip-flop, mark only the active clock edges.
5. At each active edge, sample the value of `D`.
6. Change `Q` after clock-to-Q delay and hold it until the next active edge.

**Example waveform idea:**

```text
time:     t0 t1 t2 t3 t4 t5 t6 t7
CLK/EN:   0  1  1  0  0  1  1  0
D:        0  0  1  1  0  1  0  0
Latch Q:  0  0  1  1  1  1  0  0   // follows D only while EN=1
FF Q:     0  0  0  0  0  1  1  1   // samples D only at rising edges
```

In the latch row, `Q` follows `D` during `CLK/EN = 1`. In the flip-flop row, `Q` changes only after the active edge.

**Speak like this:**

"A latch can have a clock or enable signal, but it is level-sensitive, not edge-sensitive. When the enable level is active, the latch is transparent and output follows input. When enable is inactive, it holds the previous value. A flip-flop samples input only at a clock edge and holds that value until the next active edge. So while drawing waveforms, for a latch I copy input during the active level; for a flip-flop I sample input only at the clock edge."

[Back to index](./index.md)

<a id="q50"></a>
## 50. Construct NOT and buffer from XOR.

**Written answer:**

**Definition to remember:** XOR can act as a controlled inverter. If one input is `0`, it passes the other input unchanged. If one input is `1`, it inverts the other input. [[S40]](#s40)

**XOR truth table:**

| A | B | A xor B |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### Buffer using XOR

Tie one input of XOR to `0`.

```text
Y = A xor 0 = A
```

```text
A ----\
      XOR ---- Y = A
0 ----/
```

### NOT gate using XOR

Tie one input of XOR to `1`.

```text
Y = A xor 1 = A'
```

```text
A ----\
      XOR ---- Y = A'
1 ----/
```

**Verilog:**

```verilog
assign buffer_out = a ^ 1'b0;
assign not_out    = a ^ 1'b1;
```

**Speak like this:**

"XOR can work like a controlled inverter. If I XOR a signal with `0`, the output is the same signal, so it acts as a buffer. If I XOR a signal with `1`, the output becomes the complement, so it acts as a NOT gate. Therefore `A xor 0 = A` and `A xor 1 = A'`."

[Back to index](./index.md)

<a id="q51"></a>
## 51. Draw the FSM for sequence 0111.

**Written answer:**

**Definition to remember:** A finite state machine (FSM) is a sequential circuit with a finite set of states. In a digital implementation, it normally has three parts: a state register to store the present state, next-state logic to decide where to go next, and output logic to generate the required output. [[S2]](#s2) [[S53]](#s53)

A sequence detector is an FSM that observes a serial input stream and asserts an output when a target bit pattern is detected. The states represent partial matches of the sequence. In a Mealy FSM, output depends on the present state and the current input, so the output is marked on transitions. [[S41]](#s41) [[S53]](#s53)

Target sequence:

```text
0111
```

**State meaning:**

| State | Meaning |
|---|---|
| S0 | No useful match |
| S1 | Matched `0` |
| S2 | Matched `01` |
| S3 | Matched `011` |

### Mealy FSM transition table for 0111

Transition format:

```text
next_state / output
```

| Present state | Input 0 | Input 1 |
|---|---|---|
| S0 | S1 / 0 | S0 / 0 |
| S1 | S1 / 0 | S2 / 0 |
| S2 | S1 / 0 | S3 / 0 |
| S3 | S1 / 0 | S0 / 1 |

**ASCII state diagram:**

```text
S0 --0/0--> S1 --1/0--> S2 --1/0--> S3 --1/1--> S0
^           ^           |           |
|           |           |0/0        |0/0
+---1/0----+           +-----> S1 <-+
            \--0/0 loops on S1
```

**Important point about overlapping:**

For sequence `0111`, after detection on `S3 --1/1`, the FSM returns to `S0`. This is true even for overlapping detection because the detected sequence `0111` has no proper suffix that is also a prefix of `0111`.

For example, suffixes after full detection are:

```text
111, 11, 1
```

None of these equals prefix `0`, `01`, or `011`. So the next state is `S0`.

**Speak like this:**

"For sequence `0111`, I create states based on partial matches. `S0` means no match, `S1` means `0` is matched, `S2` means `01` is matched, and `S3` means `011` is matched. When input `1` arrives in `S3`, the full sequence `0111` is detected, so output becomes `1`. After that, the FSM goes to `S0` because no suffix of `0111` is also a prefix of the same sequence."

[Back to index](./index.md)

<a id="q52"></a>
## 52. Can we use XOR as a delay element?

**Written answer:**

**Definition to remember:** An XOR gate has propagation delay like any real logic gate, so a signal passing through XOR is delayed by some amount. But an XOR gate is not a reliable delay element in normal RTL design because that delay is not a fixed design specification. It can change with synthesis optimization, technology library, placement, routing, load, process, voltage, and temperature. [[S4]](#s4) [[S54]](#s54) [[S55]](#s55)

**Short answer:**

The interview-safe answer is:

```text
Theoretically yes, practically no.
```

Yes, XOR has physical propagation delay. But no, I should not intentionally use a random XOR gate as a controlled delay element in synthesizable RTL. For real delay, use clocked registers, timing constraints, library delay cells, or vendor delay primitives.

### Three different meanings of "delay"

| Type of delay | Example | Meaning | Reliable for hardware? |
|---|---|---|---|
| Simulation delay | `#5 y = a;` | Delays behavior only in simulation | No for normal synthesis |
| Gate propagation delay | Signal passes through XOR/LUT/cell | Physical delay of a real implemented gate | Exists, but not controlled enough |
| Dedicated delay element | FPGA `IDELAYE3`/`ODELAYE3`, ASIC delay cell | Delay element intended for controlled delay | Yes, when used with tool/library rules |

Delay in RTL simulation is not the same as a guaranteed physical delay in hardware. AMD synthesis documentation notes that delay controls like `#5` are not useful for synthesis. [[S14]](#s14)

**Why it is not recommended:**

1. **Synthesis can optimize it away.**
   If you write `A ^ 1'b0`, the Boolean function is just `A`, so synthesis can replace it with a wire. If you write `A ^ 1'b1`, the function is just `~A`, so synthesis can replace it with an inverter or absorb it into nearby logic. Synthesis tools perform constant folding and simple expression rewriting during optimization. [[S55]](#s55)

2. **Even if it remains, the delay is not fixed.**
   The delay depends on the selected cell or LUT, routing length, fanout, load capacitance, operating voltage, temperature, and manufacturing process. Timing analysis treats this as a path delay to be checked, not as a precise delay block chosen by the RTL writer. [[S4]](#s4)

3. **FPGA implementation may change the physical path.**
   The same XOR equation may map into a LUT, be merged with other logic, be moved during placement, or have different routing delay after place-and-route. So the final delay can change when constraints, device, tool version, or surrounding logic changes.

4. **It is not portable.**
   A delay created by one XOR in one FPGA family or ASIC standard-cell library will not match the delay in another technology.

5. **XOR can create glitches.**
   XOR output changes whenever exactly one input changes. If the two inputs arrive at slightly different times, the output can produce a short pulse/glitch. That is useful in some special edge-detection circuits, but risky if used as an uncontrolled timing element.

6. **Static timing should control timing, not random gates.**
   For synchronous digital design, timing should be controlled using clock period constraints, setup/hold analysis, registers, and proper clock-domain crossing methods.

### What happens with common XOR delay ideas

**Case 1: Trying to use XOR as a buffer**

```verilog
assign delayed_a = a ^ 1'b0;
```

This is logically equal to:

```verilog
assign delayed_a = a;
```

So synthesis may remove the XOR. It is not a safe delay.

**Case 2: Trying to use XOR as an inverter delay**

```verilog
assign delayed_inv = a ^ 1'b1;
```

This is logically equal to:

```verilog
assign delayed_inv = ~a;
```

The tool may implement it as an inverter, merge it into a LUT, or absorb it into other logic.

**Case 3: XORing a signal with a delayed version**

```verilog
assign pulse = a ^ a_delayed;
```

This can produce a pulse when `a` changes, because for a short time `a` and `a_delayed` differ. But the pulse width depends on the delay path, so it is not stable unless the delay path is intentionally designed and constrained.

**Where XOR may appear in timing-related circuits:**

XOR gates are used in phase detectors, edge detectors, parity generators/checkers, CRC logic, adders, and transition-detection circuits. In those cases, XOR is being used for its logic function, not as a guaranteed delay cell.

### Correct ways to create delay

1. **For clock-cycle delay, use registers:**

```verilog
always @(posedge clk) begin
    d1 <= din;
    d2 <= d1;
end
```

This delays `din` by clock cycles, which is reliable in synchronous design.

2. **For FPGA I/O timing delay, use vendor delay primitives.**
   AMD devices provide dedicated delay resources such as `IDELAYE3` and `ODELAYE3`. AMD documents `IDELAYE3` as an input fixed or variable delay element, and in TIME mode it uses calibration and voltage/temperature compensation to maintain the requested delay. [[S54]](#s54)

3. **For ASIC small physical delay, use standard-cell delay buffers or library delay cells.**
   These should be placed, constrained, and verified with static timing analysis.

4. **For clock phase delay, use clocking resources.**
   Use PLL/MMCM phase shift or clock-management resources rather than random data-path gates. AMD notes that clocks should not be delayed using `IDELAYE3`; clock delay should use MMCM/PLL fine-phase shift where needed. [[S54]](#s54)

5. **For simulation-only delay, use `#` delay in a testbench.**
   This models time in simulation, but it is not normal synthesizable RTL. [[S14]](#s14)

### Final interview position

| Question | Best answer |
|---|---|
| Does XOR have delay? | Yes, every real gate has propagation delay. |
| Can I rely on XOR as a delay element in RTL? | No, not for reliable/portable design. |
| Why not? | Synthesis can optimize it, and physical delay varies with implementation and PVT. |
| What should I use instead? | Registers for cycle delay, dedicated delay cells/primitives for physical delay, and STA constraints for timing closure. |

**Speak like this:**

"An XOR gate does have propagation delay, so in a physical circuit a signal through XOR will arrive later than the input. But I would not use XOR as a reliable delay element in normal RTL. If I write `A ^ 0`, synthesis can optimize it into just `A`; even if the XOR remains, its delay depends on cell mapping, routing, fanout, voltage, temperature, and process. XOR can also generate glitches if its inputs arrive at different times. So my answer is: theoretically yes, XOR has delay; practically, no, I should not rely on it for controlled delay. For cycle delay I use flip-flops, for FPGA I/O delay I use vendor primitives like IDELAY/ODELAY, and for ASIC I use library delay cells or buffers verified by static timing analysis."

[Back to index](./index.md)

<a id="q53"></a>
## 53. If input is 1100, what will be the output in Johnson counter and ring counter?

**Written answer:**

**Definition to remember:** A ring counter feeds the last flip-flop output back to the first flip-flop. A Johnson counter, also called a twisted ring counter, feeds the inverted last flip-flop output back to the first flip-flop. [[S42]](#s42) [[S43]](#s43)

Assumption for this answer:

```text
State = Q3 Q2 Q1 Q0
Right shift is used.
Ring next state    = Q0 Q3 Q2 Q1
Johnson next state = Q0' Q3 Q2 Q1
Present state      = 1100
```

### Ring counter

For ring counter:

```text
Next = Q0 Q3 Q2 Q1
```

Given:

```text
Q3 Q2 Q1 Q0 = 1 1 0 0
Q0 = 0
```

So:

```text
Next = 0 1 1 0 = 0110
```

If it continues:

```text
1100 -> 0110 -> 0011 -> 1001 -> 1100
```

**Important note:** A standard one-hot ring counter normally has only one `1`, like `1000`, `0100`, `0010`, `0001`. So `1100` is not a valid one-hot ring counter state. But if the circuit is simply a circular shift register, it will rotate `1100` as shown.

### Johnson counter

For Johnson counter:

```text
Next = Q0' Q3 Q2 Q1
```

Given:

```text
Q0 = 0, so Q0' = 1
```

So:

```text
Next = 1 1 1 0 = 1110
```

If it continues:

```text
1100 -> 1110 -> 1111 -> 0111 -> 0011 -> 0001 -> 0000 -> 1000 -> 1100
```

**Speak like this:**

"Assuming a 4-bit right-shift counter with state `Q3 Q2 Q1 Q0`, a ring counter feeds `Q0` back to `Q3`, so from `1100` the next state is `0110`. A Johnson counter feeds inverted `Q0` back to `Q3`, so from `1100`, since `Q0` is `0`, inverted feedback is `1`, and the next state is `1110`. I should also mention that `1100` is not a valid one-hot state for a standard ring counter, but it will rotate if the circuit is just a circular shift register."

[Back to index](./index.md)

<a id="q54"></a>
## 54. Which is faster: NAND or NOR? Why?

**Written answer:**

**Definition to remember:** In CMOS logic, NAND is usually faster than NOR for the same fan-in and comparable sizing, mainly because NOR has series PMOS transistors in the pull-up path, and PMOS devices are generally weaker/slower than NMOS devices. [[S10]](#s10) [[S34]](#s34)

**CMOS structure comparison:**

| Gate | PMOS network | NMOS network |
|---|---|---|
| NAND | Parallel PMOS | Series NMOS |
| NOR | Series PMOS | Parallel NMOS |

**Why NAND is usually faster:**

1. For a NAND gate, the pull-up path uses PMOS in parallel.
2. For a NOR gate, the pull-up path uses PMOS in series.
3. PMOS has lower mobility than NMOS, so PMOS is naturally weaker.
4. Stacking weaker PMOS devices in series increases resistance.
5. Higher resistance increases delay, especially for output rising transitions.
6. Therefore, NOR often needs larger PMOS sizing to match NAND speed, which increases area and capacitance.

**Interview-safe answer:**

NAND is often faster in CMOS, but not absolutely always. Actual speed depends on fan-in, sizing, load, standard-cell library, wiring, and process technology.

**Speak like this:**

"In CMOS, NAND is usually faster than NOR. The reason is the transistor network. NAND has PMOS devices in parallel and NMOS devices in series, while NOR has PMOS devices in series and NMOS devices in parallel. Since PMOS devices are weaker than NMOS devices, putting PMOS in series makes the NOR pull-up path slower. So for the same fan-in and similar sizing, NAND usually has better delay. But the final answer still depends on the library, sizing, load, and technology."

[Back to index](./index.md)

<a id="q55"></a>
## 55. Draw waveform for latch and flip-flop.

**Written answer:**

**Definition to remember:** A latch is level-sensitive, so its output can follow input during the active enable level. A flip-flop is edge-sensitive, so its output changes only after the active clock edge. [[S3]](#s3)

Assume:

```text
Latch: active-high D latch
Flip-flop: positive-edge D flip-flop
Ignore small propagation delay in the rough drawing
```

**Example waveform:**

```text
CLK/EN:  ___-------___-------___
D:       __--__----____--______

Latch Q: ___--__----____--_____
         follows D while CLK/EN is high,
         holds value while CLK/EN is low

FF Q:    ______----___________
         changes only at rising clock edges
```

**More exact drawing rule:**

For a latch:

```text
if EN = 1, Q = D
if EN = 0, Q holds previous value
```

For a D flip-flop:

```text
at posedge CLK, Q captures D
between clock edges, Q holds previous value
```

**Table example:**

| Time | CLK/EN | D | Latch Q | Flip-flop Q |
|---:|---:|---:|---:|---:|
| t0 | 0 | 0 | 0 | 0 |
| t1 rising | 1 | 1 | 1 | 1 |
| t2 | 1 | 0 | 0 | 1 |
| t3 falling | 0 | 1 | 0 | 1 |
| t4 | 0 | 0 | 0 | 1 |
| t5 rising | 1 | 0 | 0 | 0 |
| t6 | 1 | 1 | 1 | 0 |

**Speak like this:**

"For a latch waveform, I first mark the active enable level. During that level, `Q` follows `D`; outside that level, `Q` holds its last value. For a flip-flop waveform, I ignore changes in `D` between edges and only sample `D` at the active clock edge. Then `Q` changes after clock-to-Q delay and holds until the next edge."

[Back to index](./index.md)

<a id="q56"></a>
## 56. Latch vs flip-flop.

**Written answer:**

**Definition to remember:** Both latch and flip-flop are one-bit storage elements. A latch is level-sensitive, while a flip-flop is edge-sensitive. [[S3]](#s3)

| Parameter | Latch | Flip-flop |
|---|---|---|
| Triggering | Level triggered | Edge triggered |
| Control signal | Enable or clock level | Clock edge |
| Output behavior | Can follow input while enabled | Captures input only at active edge |
| Transparency | Transparent during active level | Not transparent between edges |
| Timing | More timing care due transparency | Easier for synchronous timing |
| Complexity | Usually simpler | Usually built from latches/gates, more complex |
| Speed | Can be faster and allow time borrowing | More controlled but can add clock-to-Q overhead |
| Common use | Low-power/latch-based timing, temporary storage | Registers, counters, FSMs, pipelines |
| Risk | Race/hazard risk if poorly controlled | Setup/hold/metastability still matter |
| Examples | SR latch, D latch | D FF, JK FF, T FF, SR FF |

**Core difference:**

```text
Latch:
Q can change as long as enable level is active.

Flip-flop:
Q changes only at clock edge.
```

**Interview correction:**

If someone says "latch has no clock", the better answer is: a basic latch may have enable instead of a clock, but a gated latch can use a clock-like enable signal. Still, it remains level-sensitive. A flip-flop is edge-triggered.

**Speak like this:**

"Both latch and flip-flop store one bit. The main difference is timing. A latch is level-sensitive, so when enable is active, output can follow input. When enable is inactive, it holds the previous value. A flip-flop is edge-sensitive, so it samples input only at the active clock edge and holds that value between edges. Because of this, flip-flops are more common in synchronous designs like registers, counters, and FSMs, while latches are used when level-sensitive storage or time borrowing is desired."

[Back to index](./index.md)

<a id="q57"></a>
## 57. Where will we use flip-flops?

**Written answer:**

**Definition to remember:** A flip-flop is an edge-triggered one-bit storage element. It captures input at a clock edge and holds that stored value until the next active clock edge. Because it stores state, it is one of the basic building blocks of synchronous sequential circuits. [[S2]](#s2) [[S3]](#s3) [[S21]](#s21)

Flip-flops are used wherever a digital system needs to remember a value at a well-defined clock edge. The important idea is that one flip-flop stores one bit, and many useful sequential blocks are built by connecting multiple flip-flops with combinational logic.

**Standard definitions of common flip-flop uses:**

| Use | Standard definition | How flip-flops are used |
|---|---|---|
| Register | A register is a group of flip-flops used to store a multi-bit binary value. An `n`-bit register uses `n` flip-flops. [[S21]](#s21) [[S66]](#s66) | Each flip-flop stores one bit of the word. Example: 8 flip-flops make an 8-bit register. |
| Counter | A counter is a sequential circuit that advances through a defined sequence of states, usually to count clock pulses or events. [[S60]](#s60) [[S67]](#s67) | Flip-flops store the present count. Combinational logic computes the next count. |
| Shift register | A shift register is a chain/group of flip-flops used to store data and shift it left or right by one position on clock pulses. [[S68]](#s68) | Each flip-flop passes its bit to the next flip-flop on the clock edge. |
| FSM state register | An FSM is a sequential circuit with a finite number of states. The state register stores the present state of the FSM. [[S2]](#s2) [[S53]](#s53) | Flip-flops encode and store the current state; next-state logic decides the next state. |
| Pipeline register | A pipeline register stores the output of one pipeline stage and presents it as input to the next stage in the next clock cycle. [[S69]](#s69) | Flip-flops separate long combinational paths into shorter stages, improving throughput. |
| Synchronizer | A synchronizer is a register chain used when a signal crosses into another clock domain, giving metastability time to settle. [[S70]](#s70) | Usually two or more flip-flops are connected in series in the destination clock domain. |
| Frequency divider | A frequency divider produces an output clock or pulse train with lower frequency than the input. [[S71]](#s71) | A toggle flip-flop divides by 2; cascaded flip-flops divide by 4, 8, 16, etc. |
| Data/control storage | Control and status storage means storing one-bit or multi-bit control information such as valid, enable, done, ready, mode, and status flags. [[S21]](#s21) | Flip-flops hold control bits stable until the next update clock edge. |

**Example view:**

```text
Register:
8 flip-flops = 8-bit register

Counter:
count register stores current count
next_count logic calculates count + 1

Shift register:
Q0 -> Q1 -> Q2 -> Q3 on each clock

FSM:
state register stores current_state
combinational logic calculates next_state

Pipeline:
Stage 1 logic -> pipeline register -> Stage 2 logic

Synchronizer:
async_signal -> FF1 -> FF2 -> synchronized_signal

Frequency divider:
T flip-flop output toggles every input clock edge
output frequency = input frequency / 2
```

**Why flip-flops are preferred in synchronous design:**

1. They update only at clock edges.
2. Timing analysis becomes more predictable.
3. They avoid latch transparency problems.
4. They match the standard RTL style used by FPGA and ASIC tools.

**Speak like this:**

"We use flip-flops wherever we need clocked storage. A flip-flop stores one bit at a clock edge, so a group of flip-flops forms registers. They are also used in counters, shift registers, FSM state registers, pipeline stages, synchronizers, and control/status bits. In synchronous design, flip-flops are preferred because all state updates happen at well-defined clock edges, which makes timing easier to analyze."

[Back to index](./index.md)

<a id="q58"></a>
## 58. Where will we use latches in sequential circuits?

**Written answer:**

**Definition to remember:** A latch is a level-sensitive storage element. When its enable level is active, it is transparent and output can follow input; when enable is inactive, it holds the previous value. [[S3]](#s3)

In normal synchronous RTL, flip-flops are preferred. Latches are used only when the design specifically needs level-sensitive storage or latch-based timing.

**Where latches are used:**

1. **Time borrowing in latch-based pipelines.**
   A latch can remain transparent during part of the clock phase. If one stage is slightly late, it can borrow time from the next stage while the latch is still open. Intel timing documentation describes time borrowing as a latch timing effect. [[S16]](#s16) [[S56]](#s56)

2. **High-performance custom ASIC design.**
   Some custom datapaths use two-phase latch-based pipelines to improve timing flexibility.

3. **Low-power clock-gating cells.**
   Integrated clock-gating cells often contain a latch to hold the enable stable and avoid clock glitches.

4. **Temporary level-sensitive storage.**
   Latches can be used where a value must be held only while an enable is inactive.

5. **Scan/test structures in ASIC flows.**
   Some test or clock-domain transition structures may use latches, depending on methodology.

**Why latches are used rarely in normal RTL:**

1. They are transparent during the active level.
2. Transparency can create race-through problems.
3. Timing analysis is more complex than edge-triggered flip-flop timing.
4. Accidental latch inference usually means incomplete combinational code.

**Accidental latch example:**

```verilog
always @(*) begin
    if (en)
        y = d;
    // no else assignment, so y must hold old value -> latch inferred
end
```

**Intentional D latch:**

```verilog
always @(*) begin
    if (en)
        q = d;
end
```

This intentionally says: when `en = 1`, pass `d`; otherwise hold old `q`.

**Speak like this:**

"Latches are used when level-sensitive storage is required. In normal synchronous RTL I avoid latches unless I intentionally need them. They are useful in latch-based pipelines because they allow time borrowing, and they may appear inside clock-gating cells or custom ASIC datapaths. But accidental latches are dangerous because they happen when combinational outputs are not assigned in all cases. So my default is flip-flops for regular synchronous design, and latches only when the timing methodology requires them."

[Back to index](./index.md)

<a id="q59"></a>
## 59. Explain HDL.

**Written answer:**

**Definition to remember:** HDL stands for Hardware Description Language. It is a language used to describe the structure, behavior, and timing of digital hardware so that the design can be simulated, verified, and synthesized into real hardware such as FPGA logic or ASIC gates. [[S5]](#s5) [[S51]](#s51) [[S57]](#s57)

HDL is not just a normal programming language. A normal programming language describes instructions executed by a processor. HDL describes hardware that exists in parallel.

**What HDL is used for:**

1. **Design entry:** describe the digital circuit.
2. **Simulation:** check behavior before building hardware.
3. **Synthesis:** convert RTL into gates, LUTs, flip-flops, and interconnect.
4. **Verification:** test correctness using testbenches.
5. **Documentation:** capture the architecture of the design clearly.

**Common HDLs:**

| HDL | Meaning |
|---|---|
| Verilog | Common HDL used for digital design and verification |
| VHDL | VHSIC Hardware Description Language |
| SystemVerilog | Extension of Verilog with stronger RTL and verification features |

**HDL can describe hardware at different levels:**

1. Behavioral level: what the circuit does.
2. RTL level: registers and combinational logic between registers.
3. Gate level: gates and netlists.
4. Switch/transistor level: low-level primitives.

**Small example:**

```verilog
module and_gate (
    input  a,
    input  b,
    output y
);
assign y = a & b;
endmodule
```

This does not mean "execute line by line like C." It describes hardware where `y` is continuously driven by `a & b`.

**Speak like this:**

"HDL means Hardware Description Language. It is used to describe digital hardware, not software instructions. With HDL I can describe structure, behavior, and timing of a circuit, simulate it, verify it with a testbench, and synthesize it into FPGA or ASIC hardware. Verilog and VHDL are common HDLs. The key difference from C is that HDL represents parallel hardware, so multiple blocks can operate at the same time."

[Back to index](./index.md)

<a id="q60"></a>
## 60. Difference between HDL and C.

**Written answer:**

**Definition to remember:** HDL describes hardware. C describes software instructions executed by a processor. HDL code is synthesized into circuits; C code is compiled into machine instructions. [[S5]](#s5) [[S51]](#s51) [[S57]](#s57)

| Point | HDL | C |
|---|---|---|
| Full idea | Hardware Description Language | General-purpose programming language |
| Describes | Digital circuit structure/behavior | Algorithm executed by CPU |
| Execution model | Naturally concurrent/parallel | Mostly sequential unless threads are used |
| Output of tool | Gates, flip-flops, LUTs, netlist | Machine code/object code |
| Timing | Clock, event, propagation, setup/hold timing matter | Instruction execution time matters |
| Assignment meaning | Can describe wires, registers, hardware updates | Updates variables in software memory |
| Target | FPGA/ASIC/digital circuit | Processor/microcontroller/computer |
| Example use | Counter, FSM, UART, ALU | Sorting, file handling, control software |

**Important example:**

```verilog
assign y = a & b;
```

In HDL, this means hardware exists continuously. Whenever `a` or `b` changes, `y` changes according to the AND gate.

```c
y = a & b;
```

In C, this is one instruction or statement executed when program control reaches that line.

**Speak like this:**

"The main difference is the meaning of the code. C is a software programming language: the compiler converts the program into instructions, and a processor executes those instructions step by step. HDL is a hardware description language: the synthesis tool converts the description into actual hardware such as gates, flip-flops, muxes, adders, wires, and registers. So in HDL, two `always` blocks or two continuous assignments can represent hardware working at the same time, because real circuits operate in parallel. In C, statements normally execute sequentially unless we explicitly create parallelism using threads or hardware-specific support. Also, timing is different. In C, execution time depends on processor speed and instruction flow. In HDL, timing depends on clock edges, propagation delay, setup time, hold time, and paths between registers. So even if Verilog syntax looks similar to C, Verilog describes structure and behavior of hardware, while C describes an algorithm executed by existing hardware."

[Back to index](./index.md)

<a id="q61"></a>
## 61. Explain concurrency in Verilog.

**Written answer:**

**Definition to remember:** Concurrency in Verilog means that hardware blocks operate in parallel. Multiple `always` blocks, `initial` blocks, continuous assignments, and module instances are independent concurrent processes. Statements inside one procedural block execute sequentially, but separate blocks run concurrently in simulation and represent parallel hardware. [[S5]](#s5) [[S51]](#s51) [[S52]](#s52)

**Simple idea:**

```text
Inside one always block       -> sequential order
Between different always blocks -> concurrent behavior
Continuous assign statements  -> always active
Module instances              -> parallel hardware blocks
```

**Example:**

```verilog
always @(posedge clk)
    q1 <= d1;

always @(posedge clk)
    q2 <= d2;

assign y = q1 & q2;
```

At the same clock edge, both `q1` and `q2` are updated. The `assign` statement continuously drives `y`.

**Why Verilog is concurrent:**

Digital hardware is physically parallel. An adder, register, counter, and FSM in the same chip are not waiting for each other like normal C statements. They all exist at the same time. Verilog models that.

**Important rule:**

Do not drive the same `reg`/logic variable from multiple procedural blocks in normal RTL.

Bad style:

```verilog
always @(posedge clk)
    q <= a;

always @(posedge clk)
    q <= b;
```

This creates multiple procedural drivers for `q` and is not a clean RTL style. One register should normally be assigned in one clocked block.

**Speak like this:**

"Concurrency in Verilog means different hardware blocks operate at the same time. Multiple `always` blocks, module instances, and continuous assignments are concurrent. But inside a single `begin-end` procedural block, statements execute in order. This matches real hardware because all gates and registers exist simultaneously. That is why Verilog is different from C."

[Back to index](./index.md)

<a id="q62"></a>
## 62. Verilog vs C.

**Written answer:**

**Definition to remember:** Verilog is an HDL used to model and synthesize digital hardware. C is a software programming language used to write programs that run on a processor. [[S5]](#s5) [[S51]](#s51)

| Feature | Verilog | C |
|---|---|---|
| Basic purpose | Describes digital hardware | Describes software algorithms |
| Final implementation | Synthesized into gates, flip-flops, muxes, adders, LUTs, memories, and interconnect | Compiled into machine instructions executed by a CPU |
| Meaning of code | Code represents hardware structure and behavior | Code represents instruction flow |
| Execution model | Concurrent by nature; modules, continuous assignments, and separate procedural blocks can all be active together | Sequential by default; statements execute in program order unless explicit parallel software mechanisms are used |
| Where it runs | Simulates in a simulator, or becomes FPGA/ASIC hardware after synthesis | Runs on a processor through compiled machine code |
| Main objects | `module`, `wire`, `reg`/`logic`, `assign`, `always`, module instances | Functions, variables, pointers, arrays, structs, loops |
| Assignment meaning | Can describe a wire connection, combinational logic, or a register update depending on context | Updates a software variable in memory/registers when that statement executes |
| Timing model | Clock edges, event controls, propagation delay, setup time, hold time, and path delay matter | Program order, instruction latency, CPU clock, memory access, and runtime behavior matter |
| Parallelism example | Two `always @(posedge clk)` blocks can infer two registers updating on the same clock edge | Two assignment statements normally execute one after another |
| Hardware resources | Writing more logic may create more physical hardware | Writing more code usually creates more instructions, not extra hardware units |
| Test/verification | Uses testbenches, waveforms, assertions, and simulation | Uses unit tests, debugger, print/log output, and software test frameworks |
| Common mistake | Reading Verilog like step-by-step C code | Thinking C statements automatically become parallel hardware |

**Key interview point:**

In C, this line means "when the CPU reaches this instruction, update the variable":

```c
y = a & b;
```

In Verilog, this line means "create continuous hardware logic that drives `y` from `a` and `b`":

```verilog
assign y = a & b;
```

So the syntax can look similar, but the mental model is different:

```text
C       -> instructions executed by existing hardware
Verilog -> description used to create or simulate hardware
```

**Example difference:**

Verilog:

```verilog
always @(posedge clk)
    q <= d;
```

This describes a D flip-flop.

C:

```c
q = d;
```

This copies a value when that line executes.

**Common mistake:**

Do not read Verilog like C line-by-line. In Verilog, separate blocks can run in parallel and `<=` nonblocking assignment updates registers in a clocked hardware style.

**Speak like this:**

"Verilog may look like C syntactically, but the meaning is different. C tells a processor what instructions to execute. Verilog describes hardware that exists physically. In C, statements usually run one after another. In Verilog, different modules, `always` blocks, and continuous assignments run concurrently. A Verilog clocked block can infer a flip-flop, while a C assignment just updates a software variable."

[Back to index](./index.md)

<a id="q63"></a>
## 63. Draw state diagram for 1010 non-overlapping sequence.

**Written answer:**

**Definition to remember:** A sequence detector FSM uses states to remember how much of the target sequence has been matched. In a Mealy FSM, the output is written on transitions because output depends on present state and current input. [[S23]](#s23) [[S53]](#s53)

Target sequence:

```text
1010
```

For a non-overlapping detector, after detecting one full `1010`, we do not reuse any bits from that detected sequence. So after detection, the FSM returns to `S0`.

**State meaning:**

| State | Meaning |
|---|---|
| S0 | No useful match |
| S1 | Matched `1` |
| S2 | Matched `10` |
| S3 | Matched `101` |

**Transition table:**

Transition format:

```text
next_state / output
```

| Present state | Input 0 | Input 1 |
|---|---|---|
| S0 | S0 / 0 | S1 / 0 |
| S1 | S2 / 0 | S1 / 0 |
| S2 | S0 / 0 | S3 / 0 |
| S3 | S0 / 1 | S1 / 0 |

**ASCII state diagram:**

```text
S0 --1/0--> S1 --0/0--> S2 --1/0--> S3 --0/1--> S0
^           |           |                         |
|           |1/0        |0/0                      |1/0
+----0/0---+           +-----------0/0-----------+--> S1
```

**Important transition:**

```text
S3 --0/1--> S0
```

This means input `0` completes `1010`, output becomes `1`, and because this is non-overlapping, the detector goes back to the initial state.

**Speak like this:**

"For non-overlapping sequence `1010`, I make states for partial matches: `S0` no match, `S1` matched `1`, `S2` matched `10`, and `S3` matched `101`. Since it is a Mealy detector, output is on the transition. From `S3`, if input is `0`, the full sequence `1010` is detected, so output is `1`, and because it is non-overlapping, the next state is `S0`."

[Back to index](./index.md)

<a id="q64"></a>
## 64. XOR as inverter and buffer.

**Written answer:**

**Definition to remember:** XOR can be used as a controlled inverter. If one XOR input is tied to `0`, the other input passes unchanged. If one XOR input is tied to `1`, the other input is inverted. [[S40]](#s40)

**XOR truth table:**

| A | B | Y = A xor B |
|---:|---:|---:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### Buffer using XOR

Tie one input to `0`:

```text
Y = A xor 0 = A
```

```text
A ----\
      XOR ---- Y = A
0 ----/
```

### Inverter using XOR

Tie one input to `1`:

```text
Y = A xor 1 = A'
```

```text
A ----\
      XOR ---- Y = A'
1 ----/
```

**Verilog:**

```verilog
assign buffer_out = a ^ 1'b0;
assign invert_out = a ^ 1'b1;
```

**Speak like this:**

"XOR gives `1` when its inputs are different. So if I tie one input to `0`, the output is the same as the other input, which is a buffer. If I tie one input to `1`, the output becomes the complement, so it works as an inverter."

[Back to index](./index.md)

<a id="q65"></a>
## 65. Write Verilog code for D flip-flop.

**Written answer:**

**Definition to remember:** A D flip-flop stores the value of input `D` on the active clock edge and presents it at output `Q`. In Verilog, a positive-edge D flip-flop is inferred using `always @(posedge clk)`. [[S3]](#s3) [[S21]](#s21)

### D flip-flop without reset

```verilog
module dff (
    input  wire clk,
    input  wire d,
    output reg  q
);
always @(posedge clk) begin
    q <= d;
end
endmodule
```

### D flip-flop with synchronous active-high reset

```verilog
module dff_sync_reset (
    input  wire clk,
    input  wire rst,
    input  wire d,
    output reg  q
);
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
endmodule
```

Here reset is checked only at the clock edge, so it is synchronous reset.

### D flip-flop with asynchronous active-low reset

```verilog
module dff_async_reset (
    input  wire clk,
    input  wire rst_n,
    input  wire d,
    output reg  q
);
always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        q <= 1'b0;
    else
        q <= d;
end
endmodule
```

Here reset is in the sensitivity list, so it can reset the flip-flop without waiting for the clock.

**Important coding points:**

1. Use nonblocking assignment `<=` in clocked sequential logic.
2. Use `posedge clk` or `negedge clk` depending on the required edge.
3. Put asynchronous reset in the sensitivity list.
4. For synchronous reset, keep only clock in the sensitivity list.

**Speak like this:**

"For a D flip-flop in Verilog, I use an edge-sensitive `always` block. The simplest form is `always @(posedge clk) q <= d;`, which means on every rising edge, `q` captures `d`. If reset is synchronous, I check reset inside the clocked block. If reset is asynchronous, I include reset in the sensitivity list along with the clock."

[Back to index](./index.md)

<a id="q66"></a>
## 66. How should I explain my project in an interview with component details?

**Written answer:**

**Definition to remember:** In a project explanation, do not only say what the project does. Explain the problem, block diagram, signal flow, key components, IC part numbers, why those parts were selected, interfaces, limitations, and testing. If an ADC is used, mention the ADC type, resolution, sampling rate, input range, reference voltage, interface, and IC name. [[S32]](#s32) [[S33]](#s33) [[S58]](#s58)

Use this structure:

### 1. One-line project summary

```text
My project is a <system name> that takes <input>, processes it using <main controller/logic>, and gives <output>.
```

Example:

```text
My project is a sensor data acquisition system that reads an analog sensor, converts it using an ADC, processes it in a microcontroller/FPGA, and displays or transmits the digital result.
```

### 2. Block diagram explanation

Speak in signal-flow order:

```text
Sensor/input -> signal conditioning -> ADC -> controller/FPGA -> processing -> communication/display/output
```

For an audio/communication project:

```text
Microphone -> preamplifier/filter -> ADC -> digital processing -> channel/interface -> DAC/PWM/audio output
```

### 3. Component details to mention

| Component | What to say |
|---|---|
| Sensor/input | Type, range, output voltage/current, why selected |
| ADC | ADC type, IC name, resolution, sample rate, input range, reference, interface |
| Controller/FPGA | Part number, clock, memory/resources, why selected |
| Power supply | Voltage rails, regulators, current requirement |
| Communication | UART/SPI/I2C/CAN/USB/Wi-Fi, data rate |
| Output | Display, actuator, DAC, PWM, relay, LED, speaker |
| Protection/filtering | RC filter, op-amp, level shifting, ESD, isolation |

### 4. If ADC is used, explain it like this

ADC means analog-to-digital converter. It converts a continuous analog voltage into a digital number. Important ADC architectures include SAR, sigma-delta, pipeline, flash, and integrating/dual-slope ADCs. Analog Devices lists these common ADC architecture choices and tradeoffs. [[S58]](#s58)

Interview details:

```text
ADC IC used: <part number>
ADC type: SAR / sigma-delta / pipeline / flash / internal MCU ADC
Resolution: <n bits>
Sampling rate: <samples per second>
Input range: <0 to Vref, differential, bipolar, etc.>
Reference voltage: <Vref value>
Interface: SPI / parallel / I2C / internal bus
Reason selected: accuracy / speed / low power / available on board / cost
```

**ADC type selection examples:**

| ADC type | Good for |
|---|---|
| SAR ADC | General data acquisition, medium/high speed, low power |
| Sigma-delta ADC | High-resolution, low-bandwidth sensors/audio/instrumentation |
| Pipeline ADC | High-speed data acquisition |
| Flash ADC | Very high speed, lower resolution, more power/area |
| Dual-slope/integrating ADC | Slow but accurate measurement, DMM-style applications |

### 5. Explain your contribution

Say exactly what you did:

1. Designed the Verilog/RTL/module.
2. Wrote testbench and verified outputs.
3. Interfaced ADC/sensor/display.
4. Selected component values.
5. Debugged timing/noise/interface issues.
6. Measured results and compared with expected output.

### 6. Discuss problems and fixes

Good interviewers like this part.

Examples:

| Problem | Good answer style |
|---|---|
| ADC readings noisy | Added averaging/filtering, checked reference stability, improved grounding |
| SPI not working | Checked CPOL/CPHA, clock rate, chip select timing |
| Timing issue | Added pipeline/registers and checked setup/hold |
| Wrong output | Built testbench, checked waveform, corrected state transition |

**Speak like this:**

"For project explanation, I would start with the problem and one-line goal, then explain the block diagram in signal-flow order. After that I would mention the key components and why I used them. If an ADC is involved, I should not just say ADC; I should say the ADC IC part number, architecture like SAR or sigma-delta, resolution, sampling rate, reference voltage, input range, and interface like SPI or I2C. Then I explain my exact contribution, testing method, issues faced, and how I fixed them."

[Back to index](./index.md)

<a id="q67"></a>
## 67. Design D latch using 2:1 MUX.

**Written answer:**

**Definition to remember:** A D latch can be implemented using a 2:1 MUX by feeding back the output `Q` to one MUX input and connecting `D` to the other MUX input. The enable signal selects whether the latch holds its old value or loads the new value. [[S3]](#s3) [[S19]](#s19) [[S59]](#s59)

For an active-high D latch:

```text
EN = 0 -> Q_next = Q      hold
EN = 1 -> Q_next = D      transparent/load
```

So the MUX equation is:

```text
Q_next = EN ? D : Q
```

### Circuit using 2:1 MUX

```text
              +---------+
Q feedback -->| I0      |
              |     MUX |----> Q
D ----------->| I1      |
              |         |
EN ---------->| Sel     |
              +---------+
```

**Truth table:**

| EN | D | Q_next | Meaning |
|---:|---:|---:|---|
| 0 | X | Q | Hold previous value |
| 1 | 0 | 0 | Load 0 |
| 1 | 1 | 1 | Load 1 |

**Verilog:**

```verilog
module d_latch_mux (
    input  wire d,
    input  wire en,
    output reg  q
);
always @(*) begin
    if (en)
        q = d;
end
endmodule
```

This intentionally infers storage because when `en = 0`, `q` is not assigned and therefore holds its previous value.

Conceptual MUX equation:

```verilog
assign q_next = en ? d : q;
```

In real RTL, be careful: writing a latch intentionally is allowed, but accidental latches from incomplete combinational assignments are usually a bug. In pure Verilog, use `always @(*)` and incomplete assignment only when the latch is intentional.

**Step-by-step explanation:**

1. A 2:1 MUX selects one of two inputs.
2. Connect `D` to input `I1`.
3. Connect present output `Q` back to input `I0`.
4. Use enable `EN` as the select line.
5. When `EN = 1`, MUX selects `D`, so `Q` follows `D`.
6. When `EN = 0`, MUX selects feedback `Q`, so the latch holds its previous value.

**Speak like this:**

"A D latch can be made using a 2:1 MUX by using feedback. I connect the current output `Q` back to input `I0`, connect `D` to input `I1`, and use enable as the select line. When enable is `1`, the MUX selects `D`, so the latch is transparent and `Q` follows `D`. When enable is `0`, the MUX selects the feedback path, so `Q` keeps its old value. Therefore the equation is `Q_next = EN ? D : Q`."

[Back to index](./index.md)

<a id="q68"></a>
## 68. Design a mod-4 up counter, draw truth table, and verify.

**Written answer:**

**Definition to remember:** A mod-4 up counter is a 2-bit sequential circuit that counts four states in upward binary order: `00 -> 01 -> 10 -> 11 -> 00`. A 2-bit counter needs two flip-flops because two flip-flops can store four states. [[S2]](#s2) [[S21]](#s21) [[S60]](#s60)

### State sequence

```text
00 -> 01 -> 10 -> 11 -> 00 -> repeat
```

Let:

```text
Q1 = MSB
Q0 = LSB
```

### State transition table

| Present state Q1 Q0 | Decimal count | Next state Q1+ Q0+ |
|---|---:|---|
| 00 | 0 | 01 |
| 01 | 1 | 10 |
| 10 | 2 | 11 |
| 11 | 3 | 00 |

For D flip-flops:

```text
D1 = Q1+
D0 = Q0+
```

So the excitation table is:

| Q1 | Q0 | D1 | D0 |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |

From the table:

```text
D0 = Q0'
D1 = Q1 xor Q0
```

### Circuit to draw

```text
                 +---------+
Q0 --------------| NOT     |---- D0
                 +---------+

Q1 ----\
        XOR -------------------- D1
Q0 ----/

              +--------+          +--------+
D1 ---------->| DFF Q1 |---- Q1   |        |
CLK --------->| CLK    |          | output |
RST --------->| RST    |          +--------+
              +--------+

              +--------+
D0 ---------->| DFF Q0 |---- Q0
CLK --------->| CLK    |
RST --------->| RST    |
              +--------+
```

Both flip-flops use the same clock, so this is a synchronous counter.

### Verification table

| Clock edge | Q1 Q0 before edge | D1 D0 | Q1 Q0 after edge |
|---:|---|---|---|
| Reset | X | X | 00 |
| 1 | 00 | 01 | 01 |
| 2 | 01 | 10 | 10 |
| 3 | 10 | 11 | 11 |
| 4 | 11 | 00 | 00 |

This verifies mod-4 behavior because after four clock edges it returns to `00`.

### Verilog, simple RTL

```verilog
module mod4_up_counter (
    input  wire       clk,
    input  wire       rst,
    output reg  [1:0] q
);
always @(posedge clk or posedge rst) begin
    if (rst)
        q <= 2'b00;
    else
        q <= q + 2'b01;
end
endmodule
```

Because `q` is 2 bits wide, after `11 + 1`, it wraps to `00`.

### Verilog using D-input equations

```verilog
module mod4_up_counter_dlogic (
    input  wire clk,
    input  wire rst,
    output reg  q1,
    output reg  q0
);
wire d1 = q1 ^ q0;
wire d0 = ~q0;

always @(posedge clk or posedge rst) begin
    if (rst) begin
        q1 <= 1'b0;
        q0 <= 1'b0;
    end else begin
        q1 <= d1;
        q0 <= d0;
    end
end
endmodule
```

**Speak like this:**

"A mod-4 up counter needs two flip-flops because two bits give four states. The count sequence is `00, 01, 10, 11`, then it returns to `00`. For D flip-flop design, I make the next-state table and set `D1 = Q1+` and `D0 = Q0+`. From the table, `D0` toggles every clock, so `D0 = Q0'`, and `D1` toggles when `Q0` is 1, so `D1 = Q1 xor Q0`. Then I connect these D inputs to two D flip-flops with the same clock."

[Back to index](./index.md)

<a id="q69"></a>
## 69. Level triggered and edge triggered.

**Written answer:**

**Definition to remember:** Level triggering means a circuit responds while the control signal is at an active level, such as high or low. Edge triggering means a circuit responds only at the transition edge of a signal, such as rising edge or falling edge. Latches are level-sensitive; flip-flops are edge-sensitive. [[S3]](#s3) [[S61]](#s61)

### Level triggered

In level triggering, the circuit is active for the entire time the enable or clock is at the active level.

Example for active-high D latch:

```text
EN = 1 -> Q follows D
EN = 0 -> Q holds old value
```

So if `D` changes multiple times while `EN = 1`, `Q` can also change multiple times.

### Edge triggered

In edge triggering, the circuit samples input only at a transition.

Examples:

```text
posedge clk: low-to-high transition
negedge clk: high-to-low transition
```

For a positive-edge D flip-flop:

```text
At posedge clk -> Q captures D
Between edges  -> Q holds old value
```

### Comparison

| Point | Level triggered | Edge triggered |
|---|---|---|
| Sensitive to | Signal level | Signal transition |
| Active duration | Entire active level | Very small instant around edge |
| Typical element | Latch | Flip-flop |
| Output can change | While enable is active | Only after active edge |
| Timing risk | Transparency/race-through | Setup/hold violation, metastability |
| Use | Latches, enables, some control circuits | Synchronous registers, counters, FSMs |

### Waveform idea

```text
CLK/EN:  ___-------___-------
D:       __--__----____--___
Latch Q: ___--__----____--__   changes while level is active
FF Q:    ______----_________   changes only at active edge
```

**Speak like this:**

"Level triggered means the circuit responds as long as the control signal is at the active level. A latch is the common example: when enable is active, output can follow input. Edge triggered means the circuit responds only at the transition, like rising edge or falling edge. A flip-flop is edge triggered, so it samples the input only at the clock edge and holds the value between edges."

[Back to index](./index.md)

<a id="q70"></a>
## 70. Functions of flip-flop.

**Written answer:**

**Definition to remember:** The main function of a flip-flop is to store one bit of information at a clock edge. From that one-bit storage function, larger sequential systems such as registers, counters, shift registers, FSMs, synchronizers, and pipelines are built. [[S2]](#s2) [[S3]](#s3) [[S21]](#s21)

**Main functions:**

| Function | Explanation |
|---|---|
| Memory element | Stores one binary bit, `0` or `1` |
| State storage | Stores current state in FSMs and sequential circuits |
| Register building block | Multiple flip-flops together store multi-bit data |
| Counter building block | Flip-flops store the count value |
| Shift register | Data shifts from one flip-flop to the next every clock |
| Pipeline register | Stores intermediate data between combinational stages |
| Synchronizer | Helps transfer asynchronous signals into a clock domain |
| Frequency divider | Toggle flip-flops can divide clock frequency |
| Control flag storage | Stores valid bits, done bits, enable bits, status flags |

### Why flip-flops are important

Combinational circuits cannot remember previous values. Flip-flops add memory to a digital system. Once memory is available, the circuit can perform multi-step behavior over time.

Examples:

```text
Counter:
current_count stored in flip-flops
next_count = current_count + 1

FSM:
current_state stored in flip-flops
next_state decided by combinational logic

Pipeline:
stage_result stored in flip-flops
next stage uses stored result in next cycle
```

**Speak like this:**

"The basic function of a flip-flop is to store one bit at a clock edge. But practically, flip-flops are used to build registers, counters, shift registers, FSM state registers, synchronizers, pipelines, and control flags. They are important because they give memory to digital circuits. Without flip-flops, a circuit would only be combinational and could not remember previous states."

[Back to index](./index.md)

<a id="q71"></a>
## 71. XNOR using MUX. Is MUX universal?

**Written answer:**

**Definition to remember:** A 2:1 MUX output is `Y = S' I0 + S I1`. To implement any function using a MUX, choose one variable as the select line and connect the data inputs according to the function value when that select variable is `0` or `1`. This idea is based on Shannon expansion. [[S7]](#s7) [[S64]](#s64) [[S65]](#s65)

### XNOR truth table

| A | B | XNOR Y |
|---:|---:|---:|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

XNOR is `1` when both inputs are equal:

```text
Y = A xnor B = A'B' + AB
```

### Implement XNOR using one 2:1 MUX plus B'

Use:

```text
Select S = A
I0 = B'
I1 = B
```

Check:

```text
If A = 0, Y = I0 = B'
If A = 1, Y = I1 = B
```

That matches XNOR:

```text
A=0 -> output should be B'
A=1 -> output should be B
```

**Circuit:**

```text
          +---------+
B' ------>| I0      |
B  ------>| I1  MUX |---- Y = A xnor B
A  ------>| S       |
          +---------+
```

### If only 2:1 MUXes are allowed

Use one MUX to generate `B'`, then another MUX to generate XNOR.

**MUX 1 as inverter:**

```text
Select = B
I0 = 1
I1 = 0
Output = B'
```

**MUX 2 as XNOR:**

```text
Select = A
I0 = B'
I1 = B
Output = A xnor B
```

### Is MUX universal?

The careful answer is:

```text
A MUX network can be universal, but a bare MUX is not usually called a universal gate like NAND or NOR.
```

Why:

1. NAND and NOR are universal gates because only NAND gates or only NOR gates can implement NOT, AND, OR, and therefore any Boolean function.
2. A MUX can implement logic functions if constants `0`, `1`, inputs, and sometimes complemented inputs are available.
3. Using Shannon expansion, any Boolean function can be recursively implemented using multiplexers.
4. So a MUX is often called a universal combinational building block, but in strict interview language NAND and NOR are the standard universal gates.

**Speak like this:**

"For XNOR using a 2:1 MUX, I choose `A` as the select line. When `A` is `0`, XNOR output should be `B'`; when `A` is `1`, output should be `B`. So I connect `I0 = B'`, `I1 = B`, and select `A`. If I only have MUXes, I can create `B'` using another 2:1 MUX with inputs `1` and `0`. About universality, a MUX network can implement any Boolean function using Shannon expansion if constants and needed complements are available, but NAND and NOR are the standard universal gates in the strict sense."

[Back to index](./index.md)

<a id="q72"></a>
## 72. How to calculate FIFO depth.

**Written answer:**

**Definition to remember:** FIFO depth is the number of words the FIFO must store without overflow. The correct depth depends on the maximum difference between cumulative writes and cumulative reads over the worst-case traffic pattern. [[S38]](#s38) [[S39]](#s39) [[S62]](#s62)

The most general rule is:

```text
Required FIFO depth >= maximum value of (total writes - total reads)
```

computed over the worst-case time window.

### Step-by-step method

1. Find write clock frequency `Fw`.
2. Find read clock frequency `Fr`.
3. Find burst size `B`.
4. Include write enable/read enable duty cycles or idle cycles.
5. Calculate how many words are written in the burst.
6. Calculate how many words can be read during the same time.
7. FIFO depth is the maximum accumulated leftover words.
8. Add margin for pointer synchronization, read latency, almost-full threshold, and implementation details.

### Simple burst formula

If the writer writes `B` words continuously at frequency `Fw`, and the reader reads continuously at frequency `Fr`:

```text
Write time = B / Fw
Words read during write time = floor(Write time * Fr)
Minimum depth = B - Words read during write time
```

If the result is less than or equal to zero, a very small FIFO may be enough for that simple case, but practical designs still need margin.

### Example

Given:

```text
Write clock Fw = 80 MHz
Read clock Fr  = 50 MHz
Burst size B   = 120 words
One write/read per active clock
```

Write time:

```text
Twrite = 120 / 80 MHz = 1.5 us = 1500 ns
```

Read period:

```text
Tread = 1 / 50 MHz = 20 ns
```

Words read during 1500 ns:

```text
1500 ns / 20 ns = 75 words
```

Words left in FIFO:

```text
120 - 75 = 45 words
```

So:

```text
Minimum FIFO depth = 45 words
```

This style of calculation matches common FIFO depth interview problems. [[S62]](#s62)

### With idle cycles or duty cycle

If there are idle cycles:

```text
Effective write period = (write_idle_cycles + 1) / Fw
Effective read period  = (read_idle_cycles + 1) / Fr
```

Then:

```text
Write time for burst = B * effective_write_period
Reads during burst   = floor(write_time / effective_read_period)
Depth                = B - reads_during_burst
```

If duty cycle is given:

```text
Effective write rate = Fw * write_enable_duty
Effective read rate  = Fr * read_enable_duty
```

### Important cases

| Case | Meaning |
|---|---|
| Average write rate > average read rate forever | No finite FIFO is enough; it will eventually overflow |
| Write faster only during burst | FIFO stores the temporary backlog |
| Read faster than write | FIFO may need only small depth, but underflow must be handled |
| Async FIFO | Add margin for pointer synchronization and full/empty latency |
| Vendor FIFO IP | Actual usable depth may differ from selected depth depending on implementation/mode |

AMD notes that actual FIFO depth can depend on whether the FIFO uses common or independent clocks and whether it uses standard or FWFT mode. [[S63]](#s63)

**Speak like this:**

"FIFO depth is calculated from the worst-case backlog. I count how many words can be written before the reader removes them. The formula I keep in mind is maximum cumulative writes minus cumulative reads. For example, if 120 words are written at 80 MHz, the write burst takes 1500 ns. If the reader reads at 50 MHz, it reads one word every 20 ns, so it can read 75 words during that time. The remaining 45 words must be stored, so the minimum depth is 45. In real designs I add margin for synchronizer latency, read latency, almost-full threshold, and FIFO implementation details."

[Back to index](./index.md)

<a id="q73"></a>
## 73. Swap two variables using nonblocking assignment and blocking assignment.

**Written answer:**

**Definition to remember:** Blocking assignment `=` updates immediately and executes in order inside a procedural block. Nonblocking assignment `<=` evaluates the right-hand side immediately but schedules the left-hand side update for later in the simulation time step. That is why nonblocking assignments can swap two registers in one clocked block without a temporary variable. [[S5]](#s5) [[S12]](#s12)

Assume:

```text
a = 10
b = 15
```

### Wrong blocking swap without temp

```verilog
initial begin
    a = 10;
    b = 15;

    a = b;
    b = a;
end
```

Execution:

```text
a = b;  -> a becomes 15
b = a;  -> b becomes 15 because a is already updated
```

Final:

```text
a = 15, b = 15   // wrong
```

### Correct blocking swap using temp

```verilog
integer temp;

initial begin
    a = 10;
    b = 15;

    temp = a;
    a    = b;
    b    = temp;
end
```

Execution:

```text
temp = 10
a = 15
b = 10
```

Final:

```text
a = 15, b = 10
```

### Correct nonblocking swap

```verilog
always @(posedge clk) begin
    a <= b;
    b <= a;
end
```

At the clock edge:

```text
RHS of a <= b reads old b = 15
RHS of b <= a reads old a = 10
Both LHS updates happen later together
```

Final after the clock edge:

```text
a = 15, b = 10
```

This works because nonblocking assignments sample old values and update together.

### Arithmetic swap using blocking assignments

```verilog
initial begin
    a = 10;
    b = 15;

    a = a + b;  // a = 25
    b = a - b;  // b = 10
    a = a - b;  // a = 15
end
```

This swaps values, but it is not the best hardware/interview style because:

1. It can overflow for fixed-width signals.
2. It can behave badly with signed arithmetic if width/sign is not handled carefully.
3. It uses adders/subtractors instead of a simple temp register or nonblocking swap.

### Best practice

| Situation | Preferred style |
|---|---|
| Clocked sequential RTL | Use nonblocking `<=` |
| Combinational/procedural calculation | Use blocking `=` |
| Blocking swap | Use temporary variable |
| Register swap at clock edge | Use nonblocking assignments |

**Speak like this:**

"With blocking assignments, statements execute immediately in order. So if I write `a = b; b = a;`, both become the old value of `b`, which is wrong. For blocking assignment, I should use a temporary variable: `temp = a; a = b; b = temp;`. With nonblocking assignment in a clocked block, `a <= b; b <= a;` works because both right-hand sides are evaluated using old values and both left-hand sides update together at the end of the time step. Arithmetic swap using addition and subtraction can work, but I avoid it in RTL because of overflow and signed-width issues."

[Back to index](./index.md)

<a id="q74"></a>
## 74. Fibonacci series code in C++

**Written answer:**

The Fibonacci series is a sequence where each number is the sum of the previous two numbers. The first two values are usually taken as `0` and `1`.

**C++ code using recursion:**

```cpp
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n == 0)
        return 0;
    if (n == 1)
        return 1;

    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;

    cout << "Enter number of terms: ";
    cin >> n;

    cout << "Fibonacci series: ";
    for (int i = 0; i < n; i++) {
        cout << fibonacci(i) << " ";
    }

    return 0;
}
```

Example output for `n = 7`:

```text
Fibonacci series: 0 1 1 2 3 5 8
```

**Speak like this:**

"The Fibonacci series starts with 0 and 1. After that, each new term is found by adding the previous two terms. In this C++ program, I use a recursive function. If n is 0, it returns 0. If n is 1, it returns 1. Otherwise, it returns fibonacci of n minus 1 plus fibonacci of n minus 2. The loop in main prints the required number of terms."

[Back to index](./index.md)

<a id="q75"></a>
## 75. How to synchronize two systems operating at different frequencies?

**Written answer:**

Synchronizing two systems with different frequencies depends on whether the clocks are related or unrelated.

If the clocks are related, for example generated from the same PLL or clock source, we can use clock dividers, clock synthesis, phase alignment, and proper timing constraints. In this case, the phase relationship is known, so timing tools can analyze the paths.

If the clocks are unrelated or asynchronous, then we treat the transfer as a clock domain crossing. A direct connection can cause setup or hold violation and metastability. Metastability means a flip-flop output temporarily enters an unstable or "in-between" state instead of resolving immediately to a valid `0` or `1`; Intel/Altera describes it as a condition caused by setup/hold violation where the output hovers between high and low and the transition is delayed beyond normal clock-to-output time. [[S86]](#s86) For a single-bit signal, we commonly use a two-flip-flop synchronizer in the destination clock domain. For a pulse, we use pulse stretching, toggle synchronizer, or handshake. For multi-bit data, the safer method is an asynchronous FIFO, because synchronizing each bit separately can capture an invalid bus value. [[S70]](#s70) [[S72]](#s72)

Common methods:

1. PLL or clock synthesis: Generate related clocks from a common reference when possible.
2. Frequency division: Divide a faster clock to create a lower related clock.
3. Two-flop synchronizer: Use for single-bit control signals crossing into another clock domain.
4. Handshake: Use request and acknowledge when data must be transferred reliably.
5. Asynchronous FIFO: Use for multi-bit data or streams crossing between different clock domains.
6. Phase alignment: Use when the clocks are related and the design needs controlled phase timing.

**Speak like this:**

"First I check whether the two clocks are related or asynchronous. If they come from the same PLL, I can use clock dividers, phase alignment, and proper generated-clock constraints. But if they are unrelated clocks, I treat it as a clock domain crossing. The main risk is metastability, which means the receiving flip-flop can temporarily be neither a clean 0 nor a clean 1 if the input changes near the sampling edge. For a single-bit signal, I use a two-flop synchronizer. For a pulse, I use pulse stretching, toggle sync, or handshake. For multi-bit data, I prefer an asynchronous FIFO because synchronizing each bit separately can give a wrong bus value."

[Back to index](./index.md)

<a id="q76"></a>
## 76. Design a 7-bit comparator using XOR gates.

**Written answer:**

A 7-bit equality comparator checks whether two 7-bit inputs are exactly the same. XOR is useful because an XOR output becomes `1` when the two compared bits are different and `0` when they are the same.

For inputs `a[6:0]` and `b[6:0]`:

```text
diff[0] = a[0] XOR b[0]
diff[1] = a[1] XOR b[1]
...
diff[6] = a[6] XOR b[6]
```

If all `diff` bits are `0`, then the two numbers are equal.

```text
not_equal = diff[6] OR diff[5] OR diff[4] OR diff[3] OR diff[2] OR diff[1] OR diff[0]
equal     = NOT not_equal
```

**Verilog code:**

```verilog
module comparator_7bit_xor (
    input  [6:0] a,
    input  [6:0] b,
    output       equal,
    output       not_equal
);
wire [6:0] diff;

assign diff = a ^ b;
assign not_equal = |diff;
assign equal = ~not_equal;

endmodule
```

**Truth idea for one bit:**

| `a[i]` | `b[i]` | `a[i] ^ b[i]` |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Important point: XOR gates detect bit mismatch. To generate final `equal`, we also need a zero-detect stage, usually an OR tree followed by NOT, or a NOR tree.

**Speak like this:**

"For a 7-bit equality comparator, I XOR each bit of A with the corresponding bit of B. XOR gives 1 only when the bits are different. So if any XOR output is 1, the numbers are not equal. If all seven XOR outputs are 0, the numbers are equal. In Verilog I can write `diff = a ^ b`, `not_equal = |diff`, and `equal = ~not_equal`."

[Back to index](./index.md)

<a id="q77"></a>
## 77. Difference between `for` loop and `foreach` loop.

**Written answer:**

In normal programming and in SystemVerilog, a `for` loop gives full control over initialization, condition, and increment. A `foreach` loop is mainly used to iterate through elements of an array without manually writing the start index, end index, and increment. SystemVerilog defines `foreach` for iterating over array elements and their indexes. [[S75]](#s75)

| `for` loop | `foreach` loop |
|---|---|
| Uses an explicit loop variable, condition, and update. | Automatically iterates over array indexes. |
| Good when we need custom step size, reverse order, or partial traversal. | Good when we want to visit every element of an array. |
| The loop variable is controlled by the programmer. | The loop index variable is created for the loop and is read-only in SystemVerilog. |
| Can be used for counters, delays, repeated calculations, and array traversal. | Mainly used for arrays, including fixed, dynamic, associative, and multidimensional arrays in SystemVerilog. |
| More flexible but more chances of boundary mistakes. | Cleaner for full-array traversal because array bounds are handled automatically. |
| Can start from any value and stop at any custom condition. | Starts from the valid array indexes defined by the array itself. |
| Can skip elements easily, for example `i = i + 2`. | Normally visits each existing array element; skipping needs `continue` or an `if` condition inside the loop. |
| Can iterate forward, backward, or in any custom order. | Iteration order follows the array index order defined by the language/tool behavior. |
| Works even when there is no array. | Requires an array or array-like collection. |
| Useful when only part of an array must be accessed. | Best when the whole array should be processed. |
| For associative arrays, the programmer must handle valid keys manually. | For associative arrays, it automatically iterates through existing keys only. |
| In multidimensional arrays, nested `for` loops need explicit bounds for each dimension. | `foreach (arr[i, j])` can directly iterate through multidimensional array indexes. |
| In synthesizable RTL, `for` loops are commonly used to generate repeated hardware when loop limits are static. | `foreach` is more common in SystemVerilog testbenches, verification code, and array initialization, though some tools support it for synthesizable static arrays. |
| Easier to accidentally write an infinite loop if the update or condition is wrong. | Less chance of infinite looping because iteration is tied to array indexes. |
| The loop variable can be modified inside the loop body, although it is usually bad style. | The `foreach` index variable should not be assigned inside the loop body. |

**Pure Verilog equivalent:**

Pure Verilog does not support `foreach`. If the interviewer asks for pure Verilog, use a normal `for` loop to visit all array indexes.

```verilog
integer i;
reg [7:0] arr [0:7];

initial begin
    for (i = 0; i < 8; i = i + 1) begin
        arr[i] = i;
    end
end
```

In C++, the range-based `for` loop is similar to a foreach style loop and is used to iterate over containers and arrays. [[S76]](#s76)

**Speak like this:**

"A for loop is more general because I manually control the starting value, condition, and increment. A foreach loop is mainly for arrays. It automatically iterates through the valid indexes, so it is cleaner when I want to touch every element. In SystemVerilog, foreach is very useful for arrays because I do not need to hardcode the size."

[Back to index](./index.md)

<a id="q78"></a>
## 78. Verilog code for 2-to-4 decoder.

**Written answer:**

General definition: A decoder is a combinational circuit that converts a coded input, usually an `n`-bit binary input, into one active output line out of many possible output lines.

Specific definition: A 2-to-4 decoder has 2 input bits and 4 output lines. For each input combination, exactly one output becomes `1`.

In general, an `n-to-2^n` decoder has `n` input lines and `2^n` output lines. So for `n = 2`, the number of outputs is `2^2 = 4`.

**Truth table:**

| `a[1]` | `a[0]` | `y[3:0]` |
|---|---|---|
| 0 | 0 | `0001` |
| 0 | 1 | `0010` |
| 1 | 0 | `0100` |
| 1 | 1 | `1000` |

**Verilog code using `case`:**

```verilog
module decoder_2to4 (
    input  [1:0] a,
    output reg [3:0] y
);
always @(*) begin
    case (a)
        2'b00: y = 4'b0001;
        2'b01: y = 4'b0010;
        2'b10: y = 4'b0100;
        2'b11: y = 4'b1000;
        default: y = 4'b0000;
    endcase
end
endmodule
```

**Verilog code with enable:**

```verilog
module decoder_2to4_en (
    input  [1:0] a,
    input        en,
    output reg [3:0] y
);
always @(*) begin
    if (en) begin
        case (a)
            2'b00: y = 4'b0001;
            2'b01: y = 4'b0010;
            2'b10: y = 4'b0100;
            2'b11: y = 4'b1000;
            default: y = 4'b0000;
        endcase
    end else begin
        y = 4'b0000;
    end
end
endmodule
```

**Speak like this:**

"A decoder is a combinational circuit that converts a coded input into one active output line. Specifically, a 2-to-4 decoder takes a 2-bit input and activates one of four outputs. For input 00, output bit 0 is high. For 01, output bit 1 is high. For 10, output bit 2 is high. For 11, output bit 3 is high. In Verilog, I can write it clearly using a combinational always block and a case statement."

[Back to index](./index.md)

<a id="q79"></a>
## 79. Explain EEPROM and other nonvolatile memories in depth.

**Written answer:**

Memory can be broadly divided into volatile and nonvolatile memory. Volatile memory, like SRAM and DRAM, loses data when power is removed. Nonvolatile memory keeps data even after power is removed. EEPROM, Flash, ROM, eFuse, FRAM, MRAM, PCM, and ReRAM are examples of nonvolatile memory.

### EEPROM

EEPROM stands for Electrically Erasable Programmable Read-Only Memory. It is nonvolatile and can be electrically erased and rewritten. Internally, an EEPROM cell stores information as electric charge on an insulated floating gate. To program/write the cell, a high electric field moves charge onto the floating gate through the thin tunnel oxide. To erase the cell, the polarity is changed so charge is electrically removed from the floating gate through the tunnel oxide, commonly by Fowler-Nordheim tunneling. Microchip's EEPROM endurance tutorial describes EEPROM program/erase operation in terms of adding charge to and electrically removing charge from the floating gate. [[S74]](#s74) [[S99]](#s99) EEPROM is commonly used for small data that must survive power-off, such as calibration values, IDs, configuration settings, and device parameters.

Basic EEPROM structure:

1. Floating gate: Stores charge. The stored charge changes the transistor threshold voltage.
2. Control gate: Controls reading and programming.
3. Tunnel oxide: Thin oxide layer used for charge movement during programming or erase.
4. Source and drain: Used to sense the cell current during read.

Working idea:

1. Write/program: Charge is placed on the floating gate by applying a programming voltage that creates a strong electric field across the tunnel oxide.
2. Erase: Charge is removed from the floating gate by applying the opposite erase condition, so electrons tunnel back through the thin oxide and the threshold voltage changes back.
3. Read: The circuit checks whether the transistor conducts for a given gate voltage. That tells whether the stored bit is `0` or `1`.

### Other Nonvolatile Memories

General definition: Nonvolatile memory is memory that retains stored information even when power is removed. This is the main difference from volatile memories like SRAM and DRAM, which lose stored data without power. [[S87]](#s87)

Definitions:

1. ROM: ROM stands for Read-Only Memory. It is nonvolatile memory whose contents are normally fixed or not changed during normal operation. It is commonly used for permanent firmware, boot code, lookup tables, and device instructions. Samsung describes ROM as memory where recorded data can be read and cannot normally be edited, and also notes that ROM is nonvolatile. [[S88]](#s88)
2. PROM or OTP: PROM means Programmable ROM, and OTP means One-Time Programmable memory. It is programmed after manufacturing, but only once. After programming, the stored bits are permanent. It is used for chip IDs, trim values, security configuration, and small permanent settings. Samsung lists PROM as a ROM type where the user can record data once. [[S88]](#s88)
3. EPROM: EPROM means Erasable Programmable ROM. It is programmed electrically but erased using ultraviolet light, usually through a quartz window in the package. It is older technology and was used when firmware needed to be changed during development or maintenance. [[S88]](#s88)
4. EEPROM: EEPROM means Electrically Erasable Programmable ROM. It can be erased and rewritten electrically, often at byte or word level depending on the device. It stores data as charge on a floating gate; writing adds charge and erasing removes that charge electrically through the tunnel oxide, commonly using Fowler-Nordheim tunneling. It is useful for small configuration data, calibration constants, serial numbers, and settings that must survive power-off. [[S74]](#s74) [[S99]](#s99)
5. Flash memory: Flash is a type of electrically erasable nonvolatile memory that is usually erased in blocks or sectors. It is denser than EEPROM for larger storage, so it is used in SSDs, memory cards, embedded firmware storage, and microcontroller program memory. IBM describes Flash as nonvolatile storage and discusses NAND and NOR as its two main forms. [[S89]](#s89)
6. NOR Flash: NOR Flash is optimized for fast random read access. Because code can be read directly and randomly, it is commonly used for firmware storage and execute-in-place applications. It is called NOR Flash because the memory-cell array connection resembles a NOR-gate style structure: cells are connected in parallel to the bit line, so individual locations can be accessed more directly. Microchip describes NOR Flash cells as individually connected to the bit line in parallel. [[S89]](#s89) [[S100]](#s100)
7. NAND Flash: NAND Flash is optimized for high density and lower cost per bit. It is usually accessed in pages and blocks, so it is used for mass storage such as SSDs, USB drives, SD cards, and phones. It is called NAND Flash because the cells are connected in series strings, resembling a NAND-gate style structure. This series connection reduces area because fewer direct contacts are needed, which gives NAND higher density but makes random byte access less direct than NOR. Microchip describes NAND Flash cells as connected in series to a bit line. [[S89]](#s89) [[S100]](#s100)
8. eFuse: eFuse is a one-time programmable nonvolatile element. It stores permanent chip information by changing a tiny on-chip fuse structure. It is used for device IDs, repair configuration, trim bits, boot settings, and security keys. Synopsys describes OTP NVM as being used for authentication information, product configuration, calibration, firmware, and technologies such as floating-gate, eFuse, and antiFuse. [[S90]](#s90)
9. FRAM or FeRAM: FRAM means Ferroelectric RAM. It is nonvolatile memory that uses a ferroelectric layer to store data. It behaves more like RAM in speed and write endurance, but keeps data without power. Infineon describes F-RAM as nonvolatile memory using a ferroelectric layer. [[S91]](#s91)
10. MRAM: MRAM means Magnetoresistive RAM. It stores bits using magnetic states instead of electric charge. It is nonvolatile and can offer fast read/write behavior with high endurance compared with charge-based memories. [[S92]](#s92)
11. PCM or PRAM: PCM means Phase-Change Memory. It stores data by switching a material between amorphous and crystalline phases, which have different electrical resistance. IBM describes PCM as an emerging nonvolatile memory technology. [[S93]](#s93)
12. ReRAM or RRAM: ReRAM means Resistive RAM. It stores data by changing the resistance of a material or device structure. A high-resistance state and low-resistance state represent stored data values. TechTarget defines ReRAM as nonvolatile storage that operates by changing resistance in a solid dielectric material. [[S94]](#s94)

| Memory type | Basic idea | Common use |
|---|---|---|
| ROM | Programmed permanently during manufacturing. | Fixed boot code, lookup tables. |
| PROM/OTP | Programmable once after manufacturing. | Permanent IDs, trim values. |
| EPROM | Erased using ultraviolet light and programmed electrically. | Older firmware storage. |
| EEPROM | Electrically erasable and rewritable, often byte or word erasable. | Small configuration data. |
| NOR Flash | Nonvolatile Flash with fast random read access. | Code storage and execute-in-place memory. |
| NAND Flash | High-density block-based Flash. | SSDs, memory cards, mass storage. |
| eFuse | Permanently programmed by blowing a fuse link. | Chip IDs, security keys, repair configuration. |
| FRAM | Stores data using ferroelectric material. | Low-power frequent writes. |
| MRAM | Stores data using magnetic states. | Fast nonvolatile memory. |
| PCM/ReRAM | Stores data using material resistance or phase changes. | Emerging nonvolatile memory. |

EEPROM is slower and smaller than SRAM or DRAM, but it has the advantage of retaining data without power and allowing electrical updates.

**Speak like this:**

"EEPROM is a nonvolatile memory, so it stores data even when power is off. Its cell is based on a floating-gate transistor. During programming, charge is moved onto the floating gate through a thin oxide using a high electric field. During erase, the erase voltage removes that charge from the floating gate, commonly through Fowler-Nordheim tunneling. During read, the circuit senses the transistor threshold behavior to decide whether the bit is 0 or 1. EEPROM is useful for small information like calibration data, IDs, and configuration values. Other nonvolatile memories include ROM, PROM, EPROM, Flash, eFuse, FRAM, MRAM, PCM, and ReRAM. NOR Flash is called NOR because its cells are connected in parallel like a NOR-style array, giving fast random read access. NAND Flash is called NAND because its cells are connected in series strings like a NAND-style array, giving higher density and lower cost per bit. The main tradeoff is capacity, speed, endurance, cost, and whether the data must be rewritten often."

[Back to index](./index.md)

<a id="q80"></a>
## 80. RTL to GDS flow.

**Written answer:**

RTL to GDS is the complete digital ASIC implementation flow. It starts from RTL code, usually Verilog, VHDL, or SystemVerilog, and ends with a GDSII layout database that represents the final chip geometry for manufacturing. Cadence describes the flow as coding RTL, simulating it, synthesizing it, running equivalence checks, floorplanning, place-and-route, meeting timing, running gate-level simulation, and writing out GDSII. [[S73]](#s73) Synopsys also describes the RTL-to-GDSII flow as crossing synthesis, place-and-route, signoff, formal equivalence, extraction, physical verification, DFT, and ATPG. [[S95]](#s95)

In simple words:

```text
Specification
   -> RTL
   -> verified RTL
   -> synthesized gate-level netlist
   -> placed and routed layout
   -> signoff-clean database
   -> GDSII for fabrication
```

### Basic structure: front end and back end

The easiest interview way to explain RTL to GDS is to split it into two parts:

| Part | What it means | Main work | Output |
|---|---|---|---|
| Front end | Logical design side | Specification, RTL coding, functional verification, synthesis basics | Verified RTL and gate-level netlist |
| Back end | Physical implementation side | Floorplan, placement, clock tree synthesis, routing, physical verification, GDS generation | Final layout/GDS |

### Basic flow

```text
Front end:
Specification -> RTL -> Verification -> Synthesis -> Netlist

Back end:
Netlist -> Floorplan -> Placement -> CTS -> Routing -> Signoff -> GDSII
```

### Step-by-step basic explanation

**Front end: logical design**

1. Specification -> RTL
   The specification says what the design should do: inputs, outputs, clock, reset, functionality, timing expectation, and interfaces. From that specification, the designer writes RTL code in Verilog/SystemVerilog/VHDL.

2. RTL -> Verification
   After writing RTL, we verify it using simulation, testbenches, assertions, and coverage. The goal is to check that the RTL behavior matches the specification.

3. Verification -> Synthesis
   Once RTL is functionally correct, synthesis is run. Synthesis reads the RTL and timing constraints and converts the behavioral RTL into real logic gates from the standard-cell library.

4. Synthesis -> Netlist
   The output of synthesis is a gate-level netlist. A netlist is a connection list of standard cells such as gates, muxes, buffers, and flip-flops. This is the handoff from front end to back end.

**Back end: physical design**

5. Netlist -> Floorplan
   The back end starts with the synthesized netlist. In floorplanning, we decide the chip/block area, aspect ratio, macro placement, IO/pin placement, power planning, and routing space.

6. Floorplan -> Placement
   After the floorplan is ready, standard cells are placed into legal physical locations. The tool tries to reduce wirelength, congestion, and timing problems.

7. Placement -> CTS
   CTS means Clock Tree Synthesis. After placement, the clock network is built using clock buffers/inverters so the clock reaches all flip-flops with controlled skew and delay.

8. CTS -> Routing
   After CTS, all signal nets and clock nets are connected using metal layers. Routing creates the actual physical wires between cells.

9. Routing -> Signoff
   After routing, final checks are done. Signoff checks include timing, DRC, LVS, antenna, IR drop, EM, power, and signal integrity. The design must be clean before tapeout.

10. Signoff -> GDSII
    Once signoff is clean, the final layout is written as a GDSII file. GDSII is the final physical layout database used for fabrication.

Basic point: front end proves the logic is correct; back end makes that logic physically manufacturable.

### Main inputs to RTL-to-GDS flow

| Input | Meaning |
|---|---|
| RTL | Verilog/SystemVerilog/VHDL description of the design behavior |
| Design specification | Functional requirement, interfaces, clocks, reset behavior, performance target |
| Testbench/assertions | Used to verify RTL and sometimes gate-level netlist |
| Constraints, usually SDC | Clock definitions, generated clocks, input/output delays, false paths, multicycle paths |
| Standard-cell library | Logic cells like NAND, NOR, mux, flops, latches, buffers, clock cells |
| Liberty `.lib` files | Timing, power, and area models for cells at PVT corners |
| LEF/technology LEF | Abstract physical views of standard cells, macros, routing layers, spacing rules |
| PDK files | Foundry process information and design rules |
| Memory/IP views | RTL models, timing models, LEF/GDS views for SRAMs, PLLs, IOs, and hard macros |
| Power intent, UPF/CPF | Describes power domains, isolation, retention, level shifters, and power states |

### Main outputs of RTL-to-GDS flow

| Output | Meaning |
|---|---|
| Gate-level netlist | Synthesized design mapped to standard cells |
| Reports | Timing, area, power, QoR, congestion, utilization, DRC/LVS summaries |
| DEF | Physical placement/routing information during implementation |
| SPEF | Extracted parasitic resistance/capacitance for signoff timing |
| SDF | Back-annotated delay file for gate-level timing simulation |
| GDSII/OASIS | Final mask-layout database sent toward tapeout/fabrication |

<a id="q81"></a>
### 81. RTL Design

The designer writes the chip logic at register-transfer level. RTL describes what happens between registers on clock edges. It includes datapaths, FSMs, counters, pipeline registers, muxing, arithmetic, clocking, and reset behavior.

Good RTL should be synthesizable and should avoid ambiguous coding. For example, sequential logic should use nonblocking assignments, combinational logic should assign outputs on every path, and clock/reset structure should be clear.

Important checks at this stage:

1. Lint: Finds coding issues such as unintended latch inference, width mismatch, unused signals, incomplete case statements, and non-synthesizable code.
2. CDC/RDC checks: Finds unsafe clock-domain crossings and reset-domain crossings.
3. Basic synthesis sanity: Ensures the RTL can actually map to gates.
4. Constraint planning: Defines clocks, generated clocks, IO timing, exceptions, and asynchronous paths.

<a id="q82"></a>
### 82. Functional Verification

Functional verification checks whether the RTL matches the design specification before implementation starts. This is usually done using simulation, directed tests, constrained-random tests, assertions, scoreboards, and coverage.

Common verification activities:

1. Unit-level simulation: Verify small blocks.
2. Subsystem/full-chip simulation: Verify integration.
3. Assertion-based verification: Check protocol and design rules.
4. Functional coverage: Measures whether important scenarios were tested.
5. Code coverage: Measures whether RTL lines, branches, conditions, and FSM states were exercised.
6. Formal checks: Useful for properties, equivalence, deadlock checks, and control-heavy logic.

The goal is not just "no simulation errors." The goal is confidence that all important behaviors from the specification have been tested.

<a id="q83"></a>
### 83. RTL Synthesis

RTL synthesis converts RTL into a gate-level netlist using the target standard-cell library. The synthesis tool reads RTL, elaborates the design, applies constraints, maps logic to cells, and optimizes for timing, area, and power.

Main synthesis inputs:

1. RTL files.
2. Standard-cell timing libraries, usually `.lib`.
3. Constraints, usually SDC.
4. Technology and physical information if physical-aware synthesis is used.

Main synthesis outputs:

1. Gate-level netlist.
2. Timing report.
3. Area report.
4. Power estimate.
5. Constraint and QoR reports.

Important interview terms:

1. Setup timing: Data must arrive before the capture clock edge.
2. Hold timing: Data must remain stable after the capture clock edge.
3. WNS: Worst Negative Slack.
4. TNS: Total Negative Slack.
5. Critical path: Path with the worst timing slack.
6. QoR: Quality of Results, usually timing, area, power, congestion, and runtime.

<a id="q84"></a>
### 84. Technology Mapping

Technology mapping is the stage where generic Boolean logic is mapped into real cells from the target library. For example, an RTL expression may become NAND, NOR, AOI/OAI, inverter, mux, buffer, flip-flop, latch, clock-gating, or complex standard cells.

This matters because the real library cells have actual delay, area, power, drive strength, input capacitance, and physical size. A good mapping choice improves timing and power. For example, the tool may choose a stronger buffer for a high-load net, or use an AOI gate instead of multiple separate gates to reduce delay.

Technology mapping also considers:

1. Target process node.
2. Available threshold-voltage cells, such as LVT/SVT/HVT.
3. Drive strength options.
4. Clock-gating cells.
5. Scan flip-flops if DFT is inserted.
6. Multi-voltage cells like level shifters and isolation cells if power intent is used.

<a id="q85"></a>
### 85. Physical Design

Physical design converts the synthesized gate-level netlist into actual physical layout. At this point, the design moves from mostly logical implementation to physical implementation.

Physical design must handle:

1. Die/core size.
2. Macro placement.
3. Standard-cell placement.
4. Power grid.
5. Clock tree.
6. Routing.
7. Timing closure.
8. Congestion.
9. IR drop and electromigration.
10. Physical design-rule cleanliness.

The physical design stage is iterative. If timing, congestion, power, or area is bad, engineers may go back and change floorplan, constraints, synthesis options, placement, buffering, or even RTL microarchitecture.

<a id="q86"></a>
### 86. Floorplanning

Floorplanning is the first major physical design step. It defines the chip or block shape and decides where large objects will be placed.

Floorplanning includes:

1. Die size and core size.
2. Aspect ratio.
3. Core utilization target.
4. IO/pin placement.
5. Macro placement, such as SRAMs and hard IPs.
6. Power straps, rings, and mesh planning.
7. Keepouts and blockages.
8. Major routing channels.
9. Clock and reset planning.

Good floorplanning is important because a poor floorplan can create routing congestion, timing problems, IR-drop issues, and long interconnect delay. For example, two blocks that communicate heavily should not be placed far apart without reason.

<a id="q87"></a>
### 87. Placement

Placement puts standard cells into legal rows inside the core area. The placement tool tries to minimize wirelength, meet timing, reduce congestion, and keep the design physically legal.

Placement is usually divided into:

1. Global placement: Finds approximate locations for cells.
2. Legalization: Moves cells into legal standard-cell rows without overlap.
3. Optimization: Adds buffers, resizes cells, moves cells, and fixes timing/congestion.

Common checks after placement:

1. Setup timing.
2. Initial hold timing.
3. Congestion map.
4. Cell density/utilization.
5. Fanout and transition violations.
6. Power estimate.

Placement quality strongly affects final routing and timing. A design can pass synthesis timing but fail after placement because wire delays become more realistic.

<a id="q88"></a>
### 88. Clock Tree Synthesis

Clock Tree Synthesis, or CTS, builds the clock distribution network. The goal is to deliver the clock from the clock source to all flip-flops and latches with controlled skew, insertion delay, transition time, and power.

Important CTS terms:

1. Clock skew: Difference in clock arrival time between sequential elements.
2. Insertion delay: Delay from clock source to clock pin of the sequential element.
3. Clock latency: Total delay seen by the clock path.
4. Clock transition/slew: Rise/fall quality of the clock signal.
5. Clock uncertainty: Margin used for jitter, skew, and modeling uncertainty.

CTS uses clock buffers, clock inverters, integrated clock-gating cells, useful skew techniques, shielding, and sometimes special non-default routing rules.

CTS affects both setup and hold timing. After CTS, hold violations become more visible because real clock delay and skew are now present.

<a id="q89"></a>
### 89. Routing

Routing connects all placed cells and macros using metal layers and vias. Routing has two main stages:

1. Global routing: Estimates routing paths and congestion.
2. Detailed routing: Assigns exact metal tracks and vias.

Routing must obey foundry design rules such as spacing, width, via rules, antenna rules, and metal density rules. It must also avoid shorts, opens, and excessive congestion.

After routing, extracted parasitic resistance and capacitance become much more accurate. That is why post-route timing can differ from pre-route timing. The design may need engineering change orders, called ECOs, to fix remaining timing, noise, or DRC issues.

<a id="q90"></a>
### 90. Physical Verification

Physical verification and signoff check whether the layout is manufacturable and electrically correct. Siemens Calibre describes physical verification as a comprehensive platform for DRC and other physical verification needs; Calibre nmLVS checks layout-versus-schematic connectivity. [[S97]](#s97) [[S98]](#s98)

Important signoff checks:

| Check | Meaning |
|---|---|
| STA | Static timing analysis for setup, hold, recovery/removal, and timing exceptions |
| DRC | Design Rule Check: verifies layout follows foundry manufacturing rules |
| LVS | Layout Versus Schematic: verifies physical layout matches the intended netlist |
| ERC | Electrical Rule Check: checks electrical correctness issues |
| Antenna check | Finds gate-oxide damage risk from long metal during fabrication |
| IR drop | Checks power supply voltage drop across the power grid |
| EM | Electromigration check for current-driven metal reliability |
| SI/crosstalk | Checks noise and delay impact from neighboring switching nets |
| Power signoff | Checks dynamic and leakage power |
| Formal equivalence | Confirms optimized netlist still matches the original RTL/golden netlist |

For timing signoff, tools like Synopsys PrimeTime and Cadence Tempus are used for static timing analysis. Synopsys describes PrimeTime as a signoff solution for timing, signal integrity, power, and variation-aware analysis. [[S96]](#s96)

The design should be clean across PVT corners:

```text
P = process variation
V = voltage variation
T = temperature variation
```

Setup is usually worst in slow process, low voltage, high temperature corners. Hold is often critical in fast process, high voltage, low temperature corners.

<a id="q91"></a>
### 91. GDS Generation

After signoff is clean, the final layout is written as GDSII or sometimes OASIS. This file contains the physical geometry of the chip: layers, shapes, cells, pins, vias, metal routes, and hierarchy. It is the final database used for mask generation and fabrication.

Before final tapeout, teams usually check:

1. GDS export is successful.
2. Final DRC is clean.
3. Final LVS is clean.
4. Timing is closed.
5. Power integrity is acceptable.
6. Antenna violations are fixed.
7. Metal fill and density checks are done.
8. Formal equivalence is clean.
9. Final netlist, constraints, reports, and layout database are archived.

Tapeout means the final verified design database is released for manufacturing.

### Compact flow summary

| Stage | Main input | Main output |
|---|---|---|
| RTL design | Specification | RTL code |
| Functional verification | RTL + testbench | Verified RTL |
| Synthesis | RTL + libraries + constraints | Gate-level netlist |
| Technology mapping | Generic logic + cell library | Standard-cell netlist |
| Floorplanning | Netlist + macros + constraints | Block/chip floorplan |
| Placement | Netlist + floorplan | Placed DEF |
| CTS | Placed design + clock constraints | Clock tree inserted design |
| Routing | Placed/CTS design | Routed DEF/GDS database |
| Extraction | Routed layout | SPEF/parasitics |
| Signoff | Layout + netlist + parasitics | Timing/DRC/LVS/power clean reports |
| GDS generation | Signoff-clean layout | GDSII/OASIS for tapeout |

**Speak like this:**

"RTL to GDS is the complete ASIC flow from Verilog code to final chip layout. I explain it in two parts: front end and back end. In front end, we start from the specification, write RTL, verify the RTL, and synthesize it into a gate-level netlist. In back end, we take that netlist and do floorplanning, placement, clock tree synthesis, routing, and final signoff checks. If timing, DRC, LVS, power, and reliability checks are clean, we generate the final GDSII file for fabrication. So front end proves the logic is correct, and back end makes the logic physically manufacturable."

[Back to index](./index.md)

<a id="q92"></a>
## 92. Write program logic to find a missing number in an array containing numbers from 1 to n.

**Written answer:**

If an array contains numbers from `1` to `n` with one number missing, the simplest logic is to compare the expected sum with the actual sum.

```text
expected_sum = n * (n + 1) / 2
actual_sum   = sum of array elements
missing      = expected_sum - actual_sum
```

**C++ code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

long long findMissingNumber(const vector<int>& arr, int n) {
    long long expectedSum = 1LL * n * (n + 1) / 2;
    long long actualSum = 0;

    for (int value : arr) {
        actualSum += value;
    }

    return expectedSum - actualSum;
}

int main() {
    vector<int> arr = {1, 2, 3, 5, 6};
    int n = 6;

    cout << "Missing number is: " << findMissingNumber(arr, n);
    return 0;
}
```

Output:

```text
Missing number is: 4
```

For very large `n`, `long long` helps avoid overflow. Another option is XOR logic, which also uses `O(n)` time and `O(1)` extra space.

**Speak like this:**

"If the array should contain numbers from 1 to n and exactly one number is missing, I calculate the expected sum using n into n plus 1 divided by 2. Then I calculate the actual sum of the array. The difference gives the missing number. The time complexity is O(n), and the extra space is O(1)."

[Back to index](./index.md)

<a id="q93"></a>
## 93. What searching approach is used when adjacent array elements differ by 1 or -1?

**Written answer:**

If the array is sorted, binary search can be used. But for the example `5 6 5 4 3`, the array is not sorted, so normal binary search is not valid.

When adjacent elements differ by exactly `1` or `-1`, we can use an optimized jump search based on the difference between the current value and the target.

Logic:

1. Start at index `i = 0`.
2. If `arr[i] == key`, return `i`.
3. Otherwise, jump by `abs(arr[i] - key)`.
4. Repeat until the index goes out of range.

This works because each next element changes by only 1, so if the current value is far from the key, the key cannot appear before at least that many steps.

**C++ code:**

```cpp
#include <iostream>
#include <vector>
#include <cstdlib>
using namespace std;

int searchAdjacentDiffOne(const vector<int>& arr, int key) {
    int i = 0;
    int n = arr.size();

    while (i < n) {
        if (arr[i] == key)
            return i;

        i += abs(arr[i] - key);
    }

    return -1;
}

int main() {
    vector<int> arr = {5, 6, 5, 4, 3};
    int key = 3;

    cout << searchAdjacentDiffOne(arr, key);
    return 0;
}
```

**Speak like this:**

"If the array is sorted, I can use binary search. But if the only property is that adjacent elements differ by 1 or minus 1, and the array is not sorted, then binary search is not correct. I use a modified jump search. At each index, I compare the current value with the key and jump by the absolute difference. This skips positions where the key cannot exist."

[Back to index](./index.md)

<a id="q94"></a>
## 94. Draw an 8:1 MUX using 2:1 MUXes with truth table.

**Written answer:**

An 8:1 mux has 8 data inputs, 3 select lines, and 1 output. To build it using only 2:1 muxes, we need a mux tree. Since each 2:1 mux reduces two inputs into one output, the total number of 2:1 muxes required is `8 - 1 = 7`. [[S65]](#s65)

**Truth table:**

| `S2` | `S1` | `S0` | Output `Y` |
|---|---|---|---|
| 0 | 0 | 0 | `I0` |
| 0 | 0 | 1 | `I1` |
| 0 | 1 | 0 | `I2` |
| 0 | 1 | 1 | `I3` |
| 1 | 0 | 0 | `I4` |
| 1 | 0 | 1 | `I5` |
| 1 | 1 | 0 | `I6` |
| 1 | 1 | 1 | `I7` |

**Connection using 2:1 MUXes:**

```text
Level 1, select S0:
M0 selects I0/I1 -> W0
M1 selects I2/I3 -> W1
M2 selects I4/I5 -> W2
M3 selects I6/I7 -> W3

Level 2, select S1:
M4 selects W0/W1 -> W4
M5 selects W2/W3 -> W5

Level 3, select S2:
M6 selects W4/W5 -> Y
```

**ASCII diagram:**

```text
I0 --\
      M0 -- W0 --\
I1 --/           |
                 M4 -- W4 --\
I2 --\           |           |
      M1 -- W1 --/           |
I3 --/                       |
                             M6 -- Y
I4 --\                       |
      M2 -- W2 --\           |
I5 --/           |           |
                 M5 -- W5 --/
I6 --\           |
      M3 -- W3 --/
I7 --/

M0-M3 use S0
M4-M5 use S1
M6 uses S2
```

**Speak like this:**

"An 8-to-1 mux can be made using seven 2-to-1 muxes. In the first level, four muxes select between pairs of inputs using S0. In the second level, two muxes select between those four intermediate outputs using S1. In the final level, one mux selects the final output using S2. So the mux count is 4 plus 2 plus 1, which is 7."

[Back to index](./index.md)

<a id="q95"></a>
## 95. If the truth table is modified, how do we modify the circuit?

**Written answer:**

For a mux-based circuit, the select-line structure usually stays the same. If the truth table changes, we modify the data inputs connected to the mux.

For an 8:1 mux:

1. Choose three variables as select lines, usually `S2`, `S1`, and `S0`.
2. For each select combination from `000` to `111`, check the required output in the new truth table.
3. Connect the corresponding mux input `I0` to `I7` to that required value.
4. If the output is always `0`, connect that input to logic `0`.
5. If the output is always `1`, connect that input to logic `1`.
6. If one variable is left out of the select lines, the mux input may become that variable or its complement.

Example:

| Select value | Required output | Connect mux input |
|---|---|---|
| `000` | 0 | `I0 = 0` |
| `001` | 1 | `I1 = 1` |
| `010` | A | `I2 = A` |
| `011` | A' | `I3 = ~A` |

So, when the truth table changes, we do not redesign the full mux tree. We update the input connections according to the new output column.

**Speak like this:**

"If the interviewer changes the truth table, I keep the mux select structure the same and remap the mux data inputs. For each select combination, I look at the required output. If the output is 0, I tie that mux input to 0. If it is 1, I tie it to 1. If it depends on another variable, I connect that variable or its complement. So modifying the circuit mainly means changing the mux input connections."

[Back to index](./index.md)

<a id="q96"></a>
## 96. How many 2:1 MUXes are required to design an n:1 MUX and why?

**Written answer:**

To design an `n:1` mux using only `2:1` muxes, the number of `2:1` muxes required is:

```text
n - 1
```

Reason: Every 2:1 mux reduces two signals into one signal. In a mux tree, we must reduce `n` input signals down to one final output. Reducing `n` signals to one signal requires `n - 1` reductions, so it requires `n - 1` two-input muxes.

For powers of 2:

| Required mux | 2:1 mux count | Levels |
|---|---:|---:|
| 2:1 | 1 | 1 |
| 4:1 | 3 | 2 |
| 8:1 | 7 | 3 |
| 16:1 | 15 | 4 |

For an `8:1` mux:

```text
Level 1: 4 muxes
Level 2: 2 muxes
Level 3: 1 mux
Total  : 4 + 2 + 1 = 7 = 8 - 1
```

If `n` is not a power of 2, the ideal mux tree still needs `n - 1` useful 2:1 selections. In practical digital design, tools often build or map it into the nearest convenient structure and may tie unused inputs to constants.

**Speak like this:**

"An n-to-1 mux needs n minus 1 two-to-one muxes. The reason is that every 2-to-1 mux reduces the number of signals by one. Starting with n input signals, I need to reduce them to one output signal, so I need n minus 1 reductions. For example, an 8-to-1 mux needs 7 two-to-one muxes: four in the first level, two in the second level, and one in the final level."

[Back to index](./index.md)

<a id="q97"></a>
## 97. Draw an FSM for sequence detector of 1001.

**Written answer:**

A sequence detector checks a serial input stream and asserts the output when a required bit pattern is seen. For sequence `1001`, the FSM should remember how much of the pattern has already been matched.

The clean way to design it is to make each state represent the longest prefix of `1001` matched so far:

| State | Meaning |
|---|---|
| `S0` | No useful match yet |
| `S1` | Matched `1` |
| `S2` | Matched `10` |
| `S3` | Matched `100` |
| `S4` | Matched `1001` in Moore machine |

For an interview, I would usually draw the overlapping detector because it is the more complete case. Yue Guo's 1001 sequence detector example also separates Moore/Mealy and overlapping/non-overlapping versions. [[S77]](#s77)

### Overlapping Moore FSM

In a Moore machine, output depends only on the present state. So we need a separate detected state `S4`, where `dout = 1`.

| Present state | Input `0` | Input `1` | Output |
|---|---|---|---|
| `S0` | `S0` | `S1` | 0 |
| `S1` | `S2` | `S1` | 0 |
| `S2` | `S3` | `S1` | 0 |
| `S3` | `S0` | `S4` | 0 |
| `S4` | `S2` | `S1` | 1 |

Why `S4` goes to `S2` on input `0`: after detecting `1001`, if the next input is `0`, the recent bits end in `10`, which is already a prefix of the next possible `1001`.

ASCII state diagram:

```text
S0 --1--> S1 --0--> S2 --0--> S3 --1--> S4
^         ^         |         |         |
|         |         1         0         |
0         1         v         v         |
+---------+-------- S1       S0        |
                    ^                  |
                    |                  |
                    +---- S4 --1-------+
                         S4 --0--> S2

Output: S4 = 1, all other states = 0
```

### Overlapping Mealy FSM

In a Mealy machine, output depends on present state and input, so we do not need a separate detected state. The output becomes `1` on the transition where the final `1` of `1001` arrives.

| Present state | Input `0` -> next/output | Input `1` -> next/output |
|---|---|---|
| `S0` | `S0 / 0` | `S1 / 0` |
| `S1` | `S2 / 0` | `S1 / 0` |
| `S2` | `S3 / 0` | `S1 / 0` |
| `S3` | `S0 / 0` | `S1 / 1` |

ASCII state diagram:

```text
S0 --1/0--> S1 --0/0--> S2 --0/0--> S3 --1/1--> S1
^           ^           |           |
|           |           1/0         0/0
0/0         1/0         v           v
+-----------+---------- S1          S0
```

### Verilog code for overlapping Mealy detector

```verilog
module seq_1001_mealy_overlap (
    input  wire clk,
    input  wire rst_n,
    input  wire din,
    output reg  dout
);

localparam S0 = 2'b00;  // no match
localparam S1 = 2'b01;  // matched 1
localparam S2 = 2'b10;  // matched 10
localparam S3 = 2'b11;  // matched 100

reg [1:0] state;
reg [1:0] next_state;

always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        state <= S0;
    else
        state <= next_state;
end

always @(*) begin
    next_state = state;
    dout = 1'b0;

    case (state)
        S0: begin
            next_state = din ? S1 : S0;
        end

        S1: begin
            next_state = din ? S1 : S2;
        end

        S2: begin
            next_state = din ? S1 : S3;
        end

        S3: begin
            if (din) begin
                next_state = S1;  // final 1 can start the next match
                dout = 1'b1;
            end else begin
                next_state = S0;
            end
        end

        default: begin
            next_state = S0;
            dout = 1'b0;
        end
    endcase
end

endmodule
```

**Speak like this:**

"For sequence 1001, I create states based on the prefix matched so far. S0 means no match, S1 means I have seen 1, S2 means I have seen 10, and S3 means I have seen 100. In a Mealy overlapping detector, when I am in S3 and the input becomes 1, I assert the output because 1001 is detected. Then I go to S1, not S0, because that final 1 can also be the start of the next sequence. In a Moore machine, I add one extra state S4 where the output is 1, because Moore output depends only on state."

[Back to index](./index.md)

<a id="q98"></a>
## 98. Make a 4:1 MUX from 2:1 MUXes.

**Written answer:**

A 4:1 mux selects one of four inputs using two select lines. It can be built using three 2:1 muxes. This is a mux tree: the first level reduces four inputs to two intermediate signals, and the second level reduces those two signals to one output. Larger muxes are commonly built this way from smaller muxes. [[S64]](#s64)

**Truth table:**

| `S1` | `S0` | Output `Y` |
|---|---|---|
| 0 | 0 | `I0` |
| 0 | 1 | `I1` |
| 1 | 0 | `I2` |
| 1 | 1 | `I3` |

**Connection:**

```text
Level 1:
M0 selects I0/I1 using S0 -> W0
M1 selects I2/I3 using S0 -> W1

Level 2:
M2 selects W0/W1 using S1 -> Y
```

**ASCII diagram:**

```text
I0 --\
      M0 -- W0 --\
I1 --/           |
                 M2 -- Y
I2 --\           |
      M1 -- W1 --/
I3 --/

M0, M1 select = S0
M2 select     = S1
```

**Verilog structural code:**

```verilog
module mux2 (
    input  d0,
    input  d1,
    input  sel,
    output y
);
assign y = sel ? d1 : d0;
endmodule

module mux4_using_mux2 (
    input  i0,
    input  i1,
    input  i2,
    input  i3,
    input  s0,
    input  s1,
    output y
);
wire w0;
wire w1;

mux2 m0 (.d0(i0), .d1(i1), .sel(s0), .y(w0));
mux2 m1 (.d0(i2), .d1(i3), .sel(s0), .y(w1));
mux2 m2 (.d0(w0), .d1(w1), .sel(s1), .y(y));

endmodule
```

**Speak like this:**

"A 4-to-1 mux can be built using three 2-to-1 muxes. First, two muxes select between I0-I1 and I2-I3 using the lower select line S0. Then a third mux selects between those two intermediate outputs using S1. So the total number of 2-to-1 muxes is three."

[Back to index](./index.md)

<a id="q99"></a>
## 99. Make an AND gate from a 2:1 MUX.

**Written answer:**

A 2:1 mux equation is:

```text
Y = S' I0 + S I1
```

To make `Y = A.B`, use `A` as the select line:

```text
S  = A
I0 = 0
I1 = B
```

Then:

```text
Y = A' . 0 + A . B
Y = A . B
```

**Connection:**

```text
       +---------+
0 ---->| I0      |
B ---->| I1  MUX |---- Y = A.B
A ---->| S       |
       +---------+
```

**Truth table:**

| `A` | `B` | MUX selected input | `Y` |
|---|---|---|---|
| 0 | 0 | `I0 = 0` | 0 |
| 0 | 1 | `I0 = 0` | 0 |
| 1 | 0 | `I1 = B` | 0 |
| 1 | 1 | `I1 = B` | 1 |

**Verilog code:**

```verilog
module and_using_mux (
    input  a,
    input  b,
    output y
);
assign y = a ? b : 1'b0;
endmodule
```

Alternative connection:

```text
S  = B
I0 = 0
I1 = A
```

That also gives `Y = A.B`.

**Speak like this:**

"For a 2-to-1 mux, the output is S bar I0 plus S I1. To make an AND gate, I use A as the select line, connect I0 to 0, and connect I1 to B. When A is 0, the mux outputs 0. When A is 1, the mux outputs B. That is exactly A AND B."

[Back to index](./index.md)

<a id="q100"></a>
## 100. Draw XNOR from NAND gate.

**Written answer:**

NAND is a universal gate, so any Boolean function can be implemented using only NAND gates. [[S9]](#s9) A two-input XNOR gate gives output `1` when both inputs are the same:

```text
XNOR = A.B + A'.B'
```

A standard NAND-only implementation uses 5 NAND gates. First build XOR using 4 NAND gates, then invert the XOR output using one more NAND gate.

**Step-by-step NAND implementation:**

```text
N1 = A NAND B
N2 = A NAND N1
N3 = B NAND N1
X  = N2 NAND N3      // X = A XOR B
Y  = X NAND X        // Y = A XNOR B
```

**ASCII diagram:**

```text
          +------+
A ------->| NAND |---- N1 ----+
B ------->|  N1  |            |
          +------+            |
                              v
          +------+        +------+
A ------->| NAND |-- N2 ->|      |
N1 ------>|  N2  |        | NAND |---- X = A XOR B
          +------+        |  N4  |
                          |      |
          +------+        +------+
B ------->| NAND |-- N3 -----^
N1 ------>|  N3  |
          +------+

X ------->+------+
          | NAND |---- Y = A XNOR B
X ------->|  N5  |
          +------+
```

**Truth table:**

| `A` | `B` | `A XOR B` | `A XNOR B` |
|---|---|---|---|
| 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

**Speak like this:**

"To make XNOR using NAND gates, I first make XOR using four NAND gates. Then I invert the XOR output by tying both inputs of one NAND gate together. So the total is five NAND gates. The logic is that XNOR is the complement of XOR, and XNOR becomes 1 when both inputs are equal."

[Back to index](./index.md)

<a id="q101"></a>
## 101. Can you design an AND gate with FSM?

**Written answer:**

An AND gate is naturally a combinational circuit, not an FSM. Its output depends only on the present inputs:

```text
Y = A.B
```

So the most correct answer is: we do not need an FSM to design an AND gate. However, if the interviewer asks specifically for an FSM-style implementation, we can design a clocked version whose output represents the AND result.

### Option 1: One-state Mealy-style FSM

This is the cleanest FSM interpretation. There is only one state because the AND gate does not need memory. The output depends on the current inputs, so it behaves like a Mealy output.

```verilog
module and_gate_mealy_style (
    input  wire clk,
    input  wire rst_n,
    input  wire a,
    input  wire b,
    output reg  y
);

localparam IDLE = 1'b0;

reg state;

always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        state <= IDLE;
    else
        state <= IDLE;
end

always @(*) begin
    y = a & b;
end

endmodule
```

### Option 2: Registered Moore-style FSM

If the output must be registered, use two states:

| State | Meaning | Output |
|---|---|---|
| `LOW` | Previous sampled result was 0 | 0 |
| `HIGH` | Previous sampled result was 1 | 1 |

```verilog
module and_gate_moore_registered (
    input  wire clk,
    input  wire rst_n,
    input  wire a,
    input  wire b,
    output reg  y
);

localparam LOW  = 1'b0;
localparam HIGH = 1'b1;

reg state;
reg next_state;

always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        state <= LOW;
    else
        state <= next_state;
end

always @(*) begin
    if (a & b)
        next_state = HIGH;
    else
        next_state = LOW;
end

always @(*) begin
    case (state)
        HIGH:   y = 1'b1;
        default:y = 1'b0;
    endcase
end

endmodule
```

Important distinction:

1. Pure AND gate: combinational, no clock, no state.
2. Mealy-style version: output can change immediately with inputs.
3. Moore-style registered version: output changes only after a clock edge, so it has one-cycle latency.

**Speak like this:**

"Strictly speaking, I do not need an FSM for an AND gate because AND is combinational. But if I am forced to express it as an FSM, the simplest Mealy-style FSM has one state and the output is directly A AND B. If the interviewer wants a registered Moore-style version, I can use two states, LOW and HIGH, where the next state is decided by A AND B and the output comes from the state. The Moore version has one clock-cycle latency."

[Back to index](./index.md)

<a id="q102"></a>
## 102. Difference between Mealy and Moore. Which is better?

**Written answer:**

Mealy and Moore machines are both finite state machines. The difference is how the output is generated. MIT notes describe Moore output as depending only on current state, while Mealy output depends on current state and current inputs. [[S78]](#s78)

| Parameter | Mealy machine | Moore machine |
|---|---|---|
| Output depends on | Present state and present input | Present state only |
| Output location in diagram | Usually written on transitions, like `input/output` | Usually written inside states |
| Number of states | Often fewer | Often more |
| Output response | Can respond in the same cycle when input changes | Usually changes after state update |
| Latency | Lower | Often one clock later |
| Glitch risk | Higher if inputs are not registered, because input can feed output combinationally | Lower because output is state-based |
| Design simplicity | Compact but needs careful timing | Easier to debug and safer for registered control outputs |
| Common use | Pattern detectors, protocol responses needing fast output | Controllers where stable outputs matter |

### Which is better?

Neither is always better.

Use a Moore machine when:

1. You want stable outputs.
2. Output should change only on clock edges.
3. You want simpler timing and less glitch risk.
4. The extra state or one-cycle latency is acceptable.

Use a Mealy machine when:

1. You need faster response.
2. You want fewer states.
3. The output naturally depends on current input.
4. You can control glitches by registering inputs or outputs if needed.

### Why can a Mealy output glitch if the state is registered?

The state register is sequential, so the present state is stable between two clock edges. But a Mealy output is not only a function of the registered state. It is a combinational function of both state and input:

```text
Moore output = f(state)
Mealy output = f(state, input)
```

So the state part is registered, but the input part may still have a direct combinational path to the output. Another way to say it is: the output depends on the current state, but inside that particular state, the output can still depend on the current input.

Example:

```text
y = (state == S3) & din
```

Here, `state == S3` may be stable because `state` is coming from flip-flops. But if `din` changes between clock edges, `y` can also change immediately, because `din` is feeding the output logic directly. If `din` is asynchronous, noisy, or arriving through a different delay path, the output can produce a short unwanted pulse before settling.

In Verilog code, the registered part is only the state update block:

```verilog
always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        state <= S0;
    else
        state <= next_state;
end
```

This block tells us that `state` changes only on the clock edge. But the Mealy output is usually written in the combinational block:

```verilog
always @(*) begin
    next_state = state;
    dout = 1'b0;

    case (state)
        S3: begin
            if (din) begin
                dout = 1'b1;
                next_state = S1;
            end else begin
                dout = 1'b0;
                next_state = S0;
            end
        end
    endcase
end
```

The important line is:

```verilog
if (din)
    dout = 1'b1;
```

This is not waiting for `posedge clk`. It is inside `always @(*)`, so it behaves like combinational logic. In hardware, it becomes gates where `din` directly affects `dout`. Therefore, even if `state` is fixed at `S3`, a change on `din` can immediately change `dout`.

For the `1001` detector, think like this:

```text
S3 means: I have already matched 100.
din == 1 means: the final 1 has arrived now.
So, S3 + din == 1 means: 1001 is detected.
```

So yes, the output is based on the current state. But that state only says "I have reached the point where I am waiting for the final input bit." In that state, the current value of `din` decides whether the output should become `1`.

For Moore style, the output does not directly check `din`:

```verilog
always @(*) begin
    case (state)
        DETECT: dout = 1'b1;
        default: dout = 1'b0;
    endcase
end
```

Here `dout` depends only on `state`. Since `state` is registered, `dout` is much more stable and normally changes only after the FSM enters the `DETECT` state on a clock edge.

Even with synchronous inputs, glitches can happen inside combinational logic because different signals do not reach the output gate at exactly the same time. Gates and wires have propagation delay. During that small settling time, the output may briefly become the wrong value.

So the glitch risk is not because the state register is unstable. The risk is because Mealy output has a direct combinational dependency on the current input. Moore output is usually more stable because it depends only on registered state.

Common ways to avoid Mealy glitches:

1. Register or synchronize external inputs before giving them to the FSM.
2. Register the Mealy output if it drives an important enable, reset, write, or control signal.
3. Use a Moore output when the control signal must be very clean.
4. Check timing for the input-to-output combinational path.

Example: For a sequence detector, Mealy can assert output on the same transition where the final bit arrives. Moore usually needs one extra state to assert the output.

**Speak like this:**

"In a Moore machine, output depends only on the current state. In a Mealy machine, output depends on current state and current input. I can also say it like this: the current state selects where I am in the sequence, but inside that state, the current input can still decide the output. For example, in a 1001 detector, state S3 means I have already matched 100. If `din` is 1 in S3, then 1001 is detected and `dout` becomes 1. Since that `if (din) dout = 1'b1;` is inside `always @(*)`, it does not wait for `posedge clk`. So the glitch is not because the state register is changing. The glitch risk is because the Mealy output has a direct input-to-output combinational path. Moore is more stable because output depends only on registered state, while Mealy is faster because it can respond in the same cycle."

[Back to index](./index.md)

<a id="q103"></a>
## 103. Tell me about your assignments in Verilog. Have you done any FSM system in Verilog?

**Written answer:**

A strong interview answer should mention both coding style and an actual FSM example. You can say this:

### Interview answer

"Yes, I have written Verilog assignments for combinational circuits and sequential circuits. For combinational logic, I used `assign` statements or `always @(*)`. For sequential logic, I used `always @(posedge clk)` or `always @(posedge clk or negedge rst_n)` with nonblocking assignments.

I have practiced modules like muxes, decoders, encoders, comparators, counters, D flip-flops, shift registers, and sequence detectors. For FSM design, I implemented sequence detector FSMs like `1001` and `1010`, where states represent partial pattern matches. I used one always block for state register and one combinational block for next-state and output logic.

In my FSM coding style, I separate the design into three parts: state declaration, state update, and next-state/output logic. I use nonblocking assignments for clocked registers and blocking assignments inside combinational logic. I also include reset behavior and default assignments to avoid latch inference."

### Good FSM coding structure

```verilog
localparam S0 = 2'b00;
localparam S1 = 2'b01;
localparam S2 = 2'b10;
localparam S3 = 2'b11;

reg [1:0] state;
reg [1:0] next_state;

always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        state <= S0;
    else
        state <= next_state;
end

always @(*) begin
    next_state = state;
    out = 1'b0;

    case (state)
        S0: begin
            // next-state logic
        end
        S1: begin
            // next-state logic
        end
        default: begin
            next_state = S0;
            out = 1'b0;
        end
    endcase
end
```

### Important Verilog assignment points

| Situation | Preferred style | Reason |
|---|---|---|
| Continuous combinational logic | `assign` | Simple wire-level logic |
| Combinational procedural block | Blocking `=` | Executes in order inside the block |
| Clocked sequential block | Nonblocking `<=` | Models flip-flop update correctly |
| FSM state register | Nonblocking `<=` | State updates on clock edge |
| FSM next-state logic | Blocking `=` | Calculates next values combinationally |

This matches standard Verilog coding guidance: use blocking for combinational procedural logic and nonblocking for sequential clocked logic. [[S12]](#s12) [[S51]](#s51)

**Speak like this:**

"Yes, I have done FSM coding in Verilog. I usually write FSMs using a clean structure: localparam state declaration, one clocked block for state update, and one combinational block for next-state and output logic. I use nonblocking assignment for the state register and blocking assignment in the combinational next-state block. One example is a 1001 sequence detector where each state stores how much of the sequence has been matched so far."

[Back to index](./index.md)

<a id="q104"></a>
## 104. What exactly is the formal definition of FSM?

**Written answer:**

FSM stands for finite state machine. Formally, an FSM is a mathematical model with a finite number of states, inputs, outputs, a transition function, an output function, and an initial state. Berkeley notes define an FSM using states, input symbols, output symbols, an initial state, a transition function, and an output function. [[S79]](#s79)

A common formal definition is:

```text
FSM = (S, I, O, s0, delta, lambda)
```

Where:

| Symbol | Meaning |
|---|---|
| `S` | Finite set of states |
| `I` | Set of input symbols or input combinations |
| `O` | Set of output symbols or output combinations |
| `s0` | Initial state |
| `delta` | State transition function |
| `lambda` | Output function |

Transition function:

```text
delta: S x I -> S
```

This means the next state is decided by the current state and current input.

For a Moore machine:

```text
lambda: S -> O
```

Output depends only on current state.

For a Mealy machine:

```text
lambda: S x I -> O
```

Output depends on current state and current input.

In hardware terms, an FSM has:

1. State register: flip-flops that store the present state.
2. Next-state combinational logic: calculates the next state.
3. Output logic: generates output from state, or from state plus input.

**Speak like this:**

"Formally, an FSM is a tuple containing a finite set of states, inputs, outputs, an initial state, a transition function, and an output function. The transition function maps current state and input to next state. In a Moore machine, the output function depends only on state. In a Mealy machine, the output function depends on state and input. In hardware, I implement this using a state register, next-state logic, and output logic."

[Back to index](./index.md)

<a id="q105"></a>
## 105. Encoding and decoding levels.

**Written answer:**

Encoding and decoding are opposite operations in digital logic.

An encoder converts a larger set of input lines into a smaller binary code. A decoder converts a binary code back into one of many output lines.

### Encoder

For a normal `4:2` encoder:

| Active input | Output code |
|---|---|
| `D0` | `00` |
| `D1` | `01` |
| `D2` | `10` |
| `D3` | `11` |

Only one input should be active at a time. If multiple inputs can be active, we use a priority encoder.

### Decoder

For a `2:4` decoder:

| Input code | Active output |
|---|---|
| `00` | `Y0` |
| `01` | `Y1` |
| `10` | `Y2` |
| `11` | `Y3` |

A decoder is commonly used for address decoding, memory selection, instruction decoding, and one-hot control generation.

### Encoding levels in FSM design

In general, **encoding** means representing information using a defined code format. In digital electronics, it usually means converting a signal, condition, symbol, or data value into a binary code that hardware can store, transmit, or process.

Example:

```text
D0 active -> 00
D1 active -> 01
D2 active -> 10
D3 active -> 11
```

This is encoding because a one-active-line input is being represented as a compact binary value.

In FSM design, **state encoding** means assigning a unique binary code to each symbolic state of the FSM. The symbolic names like `IDLE`, `READ`, `WRITE`, or `DONE` are easy for humans, but hardware stores the current state as bits in flip-flops. These flip-flops are called the **state register**.

Standard definition:

> State encoding is the mapping of each abstract FSM state to a binary value stored in the state register. The chosen encoding affects the amount of state-register flip-flops, the next-state logic, the output logic, timing, area, and power.

For example, in Verilog:

```verilog
localparam IDLE  = 2'b00;
localparam READ  = 2'b01;
localparam WRITE = 2'b10;
localparam DONE  = 2'b11;

reg [1:0] state, next_state;
```

Here the FSM has four symbolic states, and each state is encoded using a 2-bit binary value. On every active clock edge, the state register stores one of these encoded values.

| Encoding style | Idea | Advantage | Tradeoff |
|---|---|---|---|
| Binary encoding | Uses about `ceil(log2(number of states))` state bits. | Uses fewer flip-flops. | May need more combinational decode logic. |
| One-hot encoding | Uses one flip-flop per state; only one state bit is `1` at a time. | Often gives simple and fast next-state/output logic. | Uses more flip-flops. |
| Gray encoding | Adjacent states are assigned codes that differ by only one bit. | Reduces switching for ordered state transitions. | Not always suitable for FSMs with many branches. |
| Sequential encoding | Assigns state codes in normal count order, like `00`, `01`, `10`, `11`. | Simple to write and understand. | May not give the best area, speed, or power. |

The key point is that FSM encoding is not just a naming choice. It changes the real gate-level circuit. For example, binary encoding saves state flip-flops, but the circuit may need more gates to decode a particular state. One-hot encoding uses more flip-flops, but checking a state can be as simple as reading one state bit.

Berkeley's FSM notes point out that state encoding affects the final circuit, because different state assignments can produce different logic complexity. [[S79]](#s79)

### Logic levels and decoding depth

In physical logic, "levels" can also mean the number of gate stages from input to output. A design with fewer logic levels usually has less delay. For example:

```text
Input -> NAND -> NAND -> Output
```

has two logic levels. In VLSI, fewer levels can improve timing, but sometimes extra buffering is needed for fanout or physical routing.

**Speak like this:**

"Encoding means representing information using a defined code, usually a binary code in digital electronics. For example, a one-active-line input can be encoded into a smaller binary number. Decoding is the reverse: it takes a binary code and activates one output line. In FSM design, state encoding means mapping each symbolic state to a binary value stored in the state register. For example, `IDLE`, `READ`, `WRITE`, and `DONE` may be encoded as `00`, `01`, `10`, and `11`. Binary encoding saves flip-flops, one-hot encoding uses more flip-flops but can reduce next-state and output logic, and Gray encoding changes only one bit between adjacent states. So state encoding affects the real hardware in terms of area, timing, power, and logic complexity."

[Back to index](./index.md)

<a id="q106"></a>
## 106. Code converter: binary to Gray.

**Written answer:**

Gray code is a code where adjacent values differ by only one bit. This is useful in cases like asynchronous FIFO pointers and position encoders because it reduces the chance of multi-bit transition errors. Intel FIFO documentation specifically discusses Gray-code counter transfer across a clock-domain crossing. [[S80]](#s80)

For binary to Gray conversion:

1. The MSB is copied directly.
2. Every other Gray bit is the XOR of two adjacent binary bits.

For a 4-bit binary input:

```text
Binary = B3 B2 B1 B0
Gray   = G3 G2 G1 G0

G3 = B3
G2 = B3 ^ B2
G1 = B2 ^ B1
G0 = B1 ^ B0
```

Equivalent compact formula:

```text
gray = binary ^ (binary >> 1)
```

**Truth table:**

| Decimal | Binary | Gray |
|---:|---|---|
| 0 | `0000` | `0000` |
| 1 | `0001` | `0001` |
| 2 | `0010` | `0011` |
| 3 | `0011` | `0010` |
| 4 | `0100` | `0110` |
| 5 | `0101` | `0111` |
| 6 | `0110` | `0101` |
| 7 | `0111` | `0100` |
| 8 | `1000` | `1100` |
| 9 | `1001` | `1101` |
| 10 | `1010` | `1111` |
| 11 | `1011` | `1110` |
| 12 | `1100` | `1010` |
| 13 | `1101` | `1011` |
| 14 | `1110` | `1001` |
| 15 | `1111` | `1000` |

**Verilog code:**

```verilog
module binary_to_gray #(
    parameter WIDTH = 4
) (
    input  [WIDTH-1:0] binary,
    output [WIDTH-1:0] gray
);

assign gray = binary ^ (binary >> 1);

endmodule
```

**Gate-level idea for 4-bit:**

```text
G3 = B3                // wire
G2 = B3 XOR B2         // XOR gate
G1 = B2 XOR B1         // XOR gate
G0 = B1 XOR B0         // XOR gate
```

So a 4-bit binary-to-Gray converter needs three XOR gates and one direct wire.

**Speak like this:**

"For binary to Gray conversion, the MSB remains the same. Each next Gray bit is the XOR of adjacent binary bits. So for 4 bits, G3 is B3, G2 is B3 XOR B2, G1 is B2 XOR B1, and G0 is B1 XOR B0. In Verilog, the compact expression is `gray = binary ^ (binary >> 1)`."

[Back to index](./index.md)

<a id="q107"></a>
## 107. Make NOT gate from XOR.

**Written answer:**

An XOR gate outputs `1` when its inputs are different. So if one input is tied to logic `1`, the output becomes the complement of the other input.

```text
Y = A XOR 1
Y = A'
```

**Truth table:**

| `A` | Constant input | `Y = A XOR 1` |
|---|---|---|
| 0 | 1 | 1 |
| 1 | 1 | 0 |

**Connection:**

```text
A ----\
      XOR ---- Y = A'
1 ----/
```

Related XOR identities from UCSD notes include `1 XOR X = X'`, `0 XOR X = X`, and `X XOR X = 0`. [[S81]](#s81)

**Verilog code:**

```verilog
module not_using_xor (
    input  a,
    output y
);
assign y = a ^ 1'b1;
endmodule
```

**Speak like this:**

"To make a NOT gate using XOR, I connect one XOR input to the signal A and the other input to constant 1. Since XOR gives 1 when inputs are different, A XOR 1 becomes A complement. If A is 0, output is 1. If A is 1, output is 0."

[Back to index](./index.md)

<a id="q108"></a>
## 108. Number of NAND gates required for XOR and XNOR.

**Written answer:**

For two-input gates using only two-input NAND gates:

| Function | NAND gates required | Notes |
|---|---:|---|
| XOR | 4 NAND gates | Standard compact NAND-only XOR |
| XNOR | 5 NAND gates | Make XOR using 4 NANDs, then invert using 1 NAND |

### XOR using 4 NAND gates

```text
N1 = A NAND B
N2 = A NAND N1
N3 = B NAND N1
Y  = N2 NAND N3
```

This gives:

```text
Y = A XOR B
```

### XNOR using 5 NAND gates

```text
N1 = A NAND B
N2 = A NAND N1
N3 = B NAND N1
X  = N2 NAND N3      // XOR
Y  = X NAND X        // XNOR
```

The fifth NAND gate acts as an inverter because:

```text
X NAND X = X'
```

Important interview point: If complemented signals are already available from somewhere else in the circuit, the effective count can change. But for a standalone two-input XOR/XNOR built only from two-input NAND gates and raw inputs `A` and `B`, the usual answer is XOR = 4 NAND gates and XNOR = 5 NAND gates.

**Speak like this:**

"For a standalone two-input XOR using only NAND gates, we need four NAND gates. For XNOR, the common implementation is to first make XOR using four NAND gates and then invert that output using one more NAND gate with both inputs tied together. So XOR needs 4 NAND gates and XNOR needs 5 NAND gates."

[Back to index](./index.md)

<a id="q109"></a>
## 109. What is a buffer and what is its use?

**Written answer:**

A digital buffer is a non-inverting logic gate. Its logic output is the same as its input:

```text
Y = A
```

At first it may look useless because it does not change the logic value. But in real digital circuits, a buffer is very useful because it improves drive strength, isolates circuits, drives high fanout nets, and can help timing and signal integrity. A buffer is often physically implemented as two inverters in series.

**Truth table:**

| Input `A` | Output `Y` |
|---|---|
| 0 | 0 |
| 1 | 1 |

**Symbol idea:**

```text
A ----|>---- Y
```

### Main uses of a buffer

1. Drive strength: A weak signal may not be able to drive a large capacitive load or many gate inputs. A buffer provides stronger output drive.
2. Fanout improvement: Fanout means how many inputs one output can drive. If one net drives too many loads, buffers are inserted to split the load. Toshiba notes that fanout is related to output current and input current limits in logic ICs. [[S82]](#s82)
3. Signal restoration: A buffer regenerates clean logic levels and improves edge quality.
4. Isolation: It prevents one circuit block from directly loading another block.
5. Timing control: Buffers can be inserted to fix transition time, delay balancing, clock/reset distribution, and hold timing.
6. Long-wire driving: In ASIC/FPGA design, long nets may need buffers to reduce delay and transition degradation.
7. Tri-state bus control: A tri-state buffer can output `0`, `1`, or high-impedance `Z`, so multiple devices can share a bus when only one driver is enabled at a time.

### Normal buffer vs tri-state buffer

| Type | Behavior |
|---|---|
| Normal buffer | `Y = A` always |
| Tri-state buffer | If enable is active, `Y = A`; otherwise `Y = Z` |

Tri-state buffer equation:

```text
if EN = 1, Y = A
if EN = 0, Y = Z
```

**Verilog examples:**

```verilog
// Normal buffer
assign y = a;

// Tri-state buffer
assign y = en ? a : 1'bz;
```

Important practical point: Inside most FPGA fabrics, internal tri-state buses are usually converted by tools into mux logic. True tri-state behavior is mainly used at IO pins.

**Speak like this:**

"A buffer is a non-inverting logic element, so its output is the same as its input. Logically it looks simple, but physically it is very useful. We use buffers to increase drive strength, drive high fanout nets, isolate one block from another, improve transition time, drive long wires, and sometimes help timing. A tri-state buffer also has an enable pin; when disabled, its output becomes high impedance, which is useful for shared buses and IO pins."

[Back to index](./index.md)

<a id="q110"></a>
## 110. How many ports are required to implement a D latch and what are they?

**Written answer:**

A D latch is a level-sensitive storage element. When enable is active, the latch is transparent and `Q` follows `D`. When enable is inactive, the latch holds the previous value. Purdue notes describe this as the latch being open when enable is asserted and closed when enable is negated; Cornell notes also describe a D latch as level sensitive and capturing input when enable is asserted. [[S83]](#s83) [[S3]](#s3)

### Minimum D latch ports

For a basic D latch, the minimum required ports are:

| Port | Direction | Meaning |
|---|---|---|
| `D` | Input | Data input to be stored |
| `EN` or `G` or `C` | Input | Enable or gate signal |
| `Q` | Output | Stored output |

So the minimum D latch has:

```text
2 inputs  : D, EN
1 output  : Q
Total     : 3 ports
```

### Common textbook symbol

Many textbook symbols also show the complement output `Qbar` or `QN`.

| Port | Direction | Meaning |
|---|---|---|
| `D` | Input | Data input |
| `EN` | Input | Enable input |
| `Q` | Output | True output |
| `Qbar` or `QN` | Output | Complement output |

In that case:

```text
2 inputs  : D, EN
2 outputs : Q, Qbar
Total     : 4 ports
```

### D latch with reset

In practical RTL, we often add reset. If reset is included, then the latch has one extra input:

| Port | Direction | Meaning |
|---|---|---|
| `D` | Input | Data input |
| `EN` | Input | Enable input |
| `RST` or `CLR` | Input | Reset or clear input |
| `Q` | Output | Stored output |

So a resettable D latch normally has:

```text
3 inputs  : D, EN, RST
1 output  : Q
Total     : 4 ports
```

If both `Q` and `Qbar` are exposed, then it has:

```text
3 inputs  : D, EN, RST
2 outputs : Q, Qbar
Total     : 5 ports
```

### Behavior table for basic active-high D latch

| `EN` | `D` | Next `Q` | Meaning |
|---|---|---|---|
| 0 | X | `Q(previous)` | Hold previous value |
| 1 | 0 | 0 | Transparent, stores/passes 0 |
| 1 | 1 | 1 | Transparent, stores/passes 1 |

### Behavior table with active-high reset

| `RST` | `EN` | `D` | Next `Q` |
|---|---|---|---|
| 1 | X | X | 0 |
| 0 | 0 | X | `Q(previous)` |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |

### Interview point

If the interviewer asks "how many ports are required," answer based on the exact design:

1. Basic D latch: `D`, `EN`, `Q` = 3 ports.
2. Basic D latch with complement output: `D`, `EN`, `Q`, `Qbar` = 4 ports.
3. Resettable D latch: `D`, `EN`, `RST`, `Q` = 4 ports.
4. Resettable D latch with complement output: `D`, `EN`, `RST`, `Q`, `Qbar` = 5 ports.

**Speak like this:**

"A basic D latch needs two inputs and one output. The inputs are data `D` and enable `EN`, and the output is `Q`. So the minimum port count is three. If the complement output is also shown, then `Qbar` is added, making four ports. If reset is included, then reset is another input, so a resettable D latch has `D`, `EN`, `RST`, and `Q`, which is four ports minimum."

[Back to index](./index.md)

<a id="q111"></a>
## 111. Write Verilog code for D latch.

**Written answer:**

A D latch is level sensitive, not edge triggered. So the RTL should not use `posedge clk` or `negedge clk`. Instead, the latch output updates while enable is active and holds its previous value when enable is inactive. AMD's Vivado synthesis guide shows a latch with positive gate and asynchronous reset using an `always @*` block where `Q` is reset when clear is active and otherwise assigned only when gate is active. [[S84]](#s84)

### Basic D latch without reset

```verilog
module d_latch (
    input  wire d,
    input  wire en,
    output reg  q
);

always @(*) begin
    if (en)
        q = d;
end

endmodule
```

This intentionally infers a latch because when `en = 0`, `q` is not assigned inside the `always` block, so it holds its previous value.

Behavior:

```text
if en = 1, q follows d
if en = 0, q holds previous value
```

### D latch with active-high asynchronous reset

This version matches the style of the screenshot, but with clean declarations and blocking assignments.

```verilog
module d_latch_reset (
    input  wire d,
    input  wire en,
    input  wire rst,
    output reg  q
);

always @(*) begin
    if (rst)
        q = 1'b0;
    else if (en)
        q = d;
end

endmodule
```

Behavior:

```text
if rst = 1, q becomes 0
else if en = 1, q follows d
else q holds previous value
```

### Pure Verilog version with explicit latch intent

Pure Verilog models this latch with `always @(*)`. The key is to intentionally leave `q` unassigned when enable is low, so the latch holds its value.

```verilog
module d_latch_verilog (
    input  wire d,
    input  wire en,
    input  wire rst,
    output reg  q
);

always @(*) begin
    if (rst)
        q = 1'b0;
    else if (en)
        q = d;
end

endmodule
```

### Version with `Qbar`

If the latch symbol requires both `Q` and `Qbar`, generate `Qbar` as the complement of `Q`.

```verilog
module d_latch_with_qbar (
    input  wire d,
    input  wire en,
    input  wire rst,
    output reg  q,
    output wire qbar
);

always @(*) begin
    if (rst)
        q = 1'b0;
    else if (en)
        q = d;
end

assign qbar = ~q;

endmodule
```

### About the sensitivity list

Old Verilog style often writes:

```verilog
always @(d or en or rst)
```

Modern Verilog style uses:

```verilog
always @(*)
```

`always @(*)` is safer because the tool automatically includes every signal read inside the block. Cornell's Verilog notes describe that an `always` block is activated when a signal in its sensitivity list changes, and show D-latch modeling with `always @(clk, D)`. [[S3]](#s3)

### Important coding notes

1. For a latch, do not write `always @(posedge clk)`. That describes a flip-flop, not a latch.
2. If you intentionally want a latch, incomplete assignment is expected because holding the previous value is the latch behavior.
3. If you do not want a latch in combinational logic, give every output a value on every path.
4. Intel recommends avoiding unintended latch inference; latches should be used only when required and when the timing impact is understood. [[S85]](#s85)
5. In a combinational/latch-style `always` block, blocking assignment `=` is usually preferred for clear simulation behavior.

### Corrected version of the screenshot code

The screenshot version is close, but `Din` must be declared as an input, and the style can be cleaned up:

```verilog
`timescale 1ns / 1ps

module d_latch (
    output reg q,
    input  wire en,
    input  wire din,
    input  wire rst
);

always @(*) begin
    if (rst)
        q = 1'b0;
    else if (en)
        q = din;
end

endmodule
```

**Speak like this:**

"A D latch is level sensitive. In Verilog, I model it using an `always @(*)` block, not a positive-edge clock block. If reset is active, I clear `q`. Else, if enable is high, `q` follows `d`. If enable is low, I intentionally do not assign `q`, so it holds its previous value. That hold behavior is what makes it a latch. If I wanted a flip-flop, then I would use `always @(posedge clk)`, but for a latch I use enable-level behavior."

[Back to index](./index.md)

<a id="q112"></a>
## 112. Why is `posedge` not used in the sensitivity list for a D latch?

**Written answer:**

A D latch is **level-sensitive**, not edge-triggered. That means the latch is transparent while enable is at the active level, and it holds the previous value when enable is inactive. A flip-flop is edge-triggered, so it samples input only on a clock edge. Cornell's latch notes describe a latch as responding while the clock/enable level is active, while a flip-flop responds at an edge. [[S3]](#s3)

So for a D latch, I should not write:

```verilog
always @(posedge clk)
```

That describes a D flip-flop, because `q` changes only at the positive edge of `clk`.

For a latch, the correct behavior is:

```text
if en = 1, q follows d
if en = 0, q holds old value
```

Clean Verilog latch style:

```verilog
module d_latch (
    input  wire d,
    input  wire en,
    output reg  q
);

always @(*) begin
    if (en)
        q = d;
end

endmodule
```

Here `always @(*)` means the block reacts when any signal used inside it changes. If `en = 1`, then any change on `d` immediately updates `q`. That is exactly latch behavior.

Old Verilog style can also be written as:

```verilog
always @(d or en) begin
    if (en)
        q = d;
end
```

But modern style is `always @(*)`, because the tool automatically includes all signals read in the block. AMD and Intel synthesis guides also show latch inference using level-sensitive `if` conditions, not `posedge` clocking. [[S84]](#s84) [[S85]](#s85)

### Why `posedge` is wrong for a latch

If I write:

```verilog
always @(posedge en) begin
    q <= d;
end
```

then `q` samples `d` only when `en` rises from `0` to `1`. After that, if `d` changes while `en` is still high, `q` will not follow it. That is not latch behavior.

### Important correction

Sometimes people write:

```verilog
always @(posedge clk or negedge clk)
```

and then check `if (clk)` inside the block. This is not a good way to model a latch. It triggers only when `clk` changes edge, so it can miss changes on `d` while `clk` is high. A real latch must be sensitive to both enable level and data changes.

**Speak like this:**

"A D latch is level sensitive, so I do not use `posedge` in the sensitivity list. `posedge` means edge-triggered behavior, which is for flip-flops. In a latch, when enable is high, output should follow input continuously. So I use `always @(*)` and write `if (en) q = d;`. When enable is low, I do not assign `q`, so it holds the old value. That is latch behavior."

[Back to index](./index.md)

<a id="q113"></a>
## 113. How many bits are required to represent the product of two 8-bit numbers in Verilog for signed and unsigned multiplication?

**Written answer:**

For two 8-bit numbers, the full product needs **16 bits**.

### Unsigned multiplication

An unsigned 8-bit number ranges from:

```text
0 to 255
```

Maximum product:

```text
255 x 255 = 65025
```

A 16-bit unsigned number can represent:

```text
0 to 65535
```

So unsigned `8 x 8` multiplication needs **16 bits**.

```verilog
module unsigned_mult_8x8 (
    input  wire [7:0]  a,
    input  wire [7:0]  b,
    output wire [15:0] product
);

assign product = a * b;

endmodule
```

### Signed multiplication

An 8-bit signed two's-complement number ranges from:

```text
-128 to +127
```

Important products:

```text
-128 x -128 = +16384
-128 x  127 = -16256
 127 x  127 = +16129
```

A signed 16-bit number can represent:

```text
-32768 to +32767
```

So signed `8 x 8` multiplication also needs **16 bits**.

```verilog
module signed_mult_8x8 (
    input  wire signed [7:0]  a,
    input  wire signed [7:0]  b,
    output wire signed [15:0] product
);

assign product = a * b;

endmodule
```

### Important Verilog point

For signed multiplication, declaring only the output as signed is not enough. The operands should also be signed, or explicitly cast:

```verilog
assign product = $signed(a) * $signed(b);
```

If the product is stored in only 8 bits, the upper product bits are truncated, and the result can be wrong.

**Speak like this:**

"For two 8-bit numbers, the full product needs 16 bits. Unsigned 8-bit ranges from 0 to 255, and 255 times 255 is 65025, which fits in 16 bits. Signed 8-bit ranges from -128 to 127, and the product also fits in signed 16 bits. In Verilog, I declare the product as `[15:0]`, and for signed multiplication I make both operands and the product signed."

[Back to index](./index.md)

<a id="q114"></a>
## 114. A FIFO is given with n elements. What logic is needed to create a new FIFO with the elements in random order?

**Written answer:**

A normal FIFO cannot create random order by itself, because FIFO means **first in, first out**. It preserves the order in which data entered. NIST defines a queue as a structure where items are removed in the same order in which they were inserted. [[S44]](#s44)

So if the input FIFO has:

```text
A, B, C, D, E
```

a normal output FIFO will also produce:

```text
A, B, C, D, E
```

To create a new FIFO in random order, I need extra logic between the input FIFO and output FIFO.

### Basic architecture

```text
Input FIFO -> RAM/register buffer -> random address/permutation logic -> Output FIFO
```

Steps:

1. Read all `n` elements from the input FIFO.
2. Store them in a RAM or register file.
3. Generate a random or pseudo-random order of addresses.
4. Read the RAM in that generated order.
5. Write those elements into the output FIFO.

### Logic blocks required

1. **Storage buffer:** RAM/register file to hold all `n` input elements.
2. **Write counter:** writes incoming FIFO elements into buffer addresses `0` to `n-1`.
3. **Random address generator:** often an LFSR or PRNG.
4. **Used/valid bit array:** prevents reading the same buffer element twice.
5. **Read control FSM:** selects unused random addresses and pushes data to the output FIFO.
6. **Output FIFO write logic:** writes randomized data into the new FIFO.

### Important point

If every input element must appear exactly once in the output FIFO, I need a **random permutation**, not just random addresses. Random addresses alone can repeat the same address, so I need either:

1. a used-bit table to reject repeated addresses, or
2. a shuffle algorithm such as Fisher-Yates in hardware, or
3. an LFSR/permutation generator designed to visit each address once.

### Can it be done without storing all elements?

Not exactly. If I must output a true random permutation of all `n` elements, I need enough storage to hold the elements before reordering them. A pure FIFO stream does not allow random access to older elements.

**Speak like this:**

"A FIFO alone cannot randomize data because FIFO preserves order. To get random order, I first read the input FIFO into a RAM or register buffer. Then I use random address generation or a shuffle algorithm to read the buffer in a random order and write those values into a new FIFO. If each element must appear exactly once, I need a used-bit table or a proper random permutation, otherwise the same address may be selected more than once."

[Back to index](./index.md)

<a id="q115"></a>
## 115. How many gates are required to implement a 17-input XOR using 2-input XOR gates, and how many levels are required for better timing?

**Written answer:**

To implement an `n`-input XOR using only 2-input XOR gates, the number of XOR gates required is:

```text
n - 1
```

For a 17-input XOR:

```text
Number of 2-input XOR gates = 17 - 1 = 16
```

### Bad timing implementation: chain

```text
Y = (((((A0 ^ A1) ^ A2) ^ A3) ...) ^ A16)
```

This uses 16 XOR gates and has 16 logic levels. It is slow because the signal must pass through all 16 gates.

### Better timing implementation: balanced XOR tree

For better timing, use a balanced tree. The number of levels is approximately:

```text
ceil(log2(17)) = 5
```

Level breakdown:

```text
Level 1: 17 inputs -> 8 XOR outputs + 1 leftover = 9 signals
Level 2: 9 signals -> 4 XOR outputs + 1 leftover = 5 signals
Level 3: 5 signals -> 2 XOR outputs + 1 leftover = 3 signals
Level 4: 3 signals -> 1 XOR output  + 1 leftover = 2 signals
Level 5: 2 signals -> final output
```

So:

```text
Gates required = 16
Best timing levels = 5
```

If the timing is still difficult, the XOR tree can be pipelined by inserting registers between levels.

**Speak like this:**

"For an n-input XOR using 2-input XOR gates, I need n minus 1 gates. So for 17 inputs, I need 16 XOR gates. If I cascade them, timing is bad because it creates 16 levels. For better timing, I use a balanced XOR tree, which gives about ceil log2 of 17, so 5 logic levels."

[Back to index](./index.md)

<a id="q116"></a>
## 116. How many gates are required to implement a 4-input XOR using 2-input XOR gates? How many ways can it be implemented, and which is better for timing?

**Written answer:**

For a 4-input XOR:

```text
Y = A ^ B ^ C ^ D
```

Using only 2-input XOR gates, the number of gates required is:

```text
4 - 1 = 3 XOR gates
```

### Way 1: cascaded implementation

```text
X1 = A ^ B
X2 = X1 ^ C
Y  = X2 ^ D
```

This uses 3 gates and has 3 levels of delay.

```text
A,B -> XOR -> XOR with C -> XOR with D -> Y
```

### Way 2: balanced tree implementation

```text
X1 = A ^ B
X2 = C ^ D
Y  = X1 ^ X2
```

This also uses 3 gates, but it has only 2 levels of delay.

```text
A,B -> XOR \
             XOR -> Y
C,D -> XOR /
```

### Is there any change in gate count?

No. If only 2-input XOR gates are used, any 4-input XOR implementation needs 3 XOR gates. What changes is not the gate count, but the **logic depth**.

### Which representation is better for timing?

The balanced tree is better for timing because the longest input-to-output path has only 2 XOR gates instead of 3.

**Speak like this:**

"A 4-input XOR needs 3 two-input XOR gates. I can implement it as a chain or as a balanced tree. The gate count is the same in both cases, but the delay is different. The chain has 3 levels, while the balanced tree has 2 levels. For better timing, I use the balanced tree."

[Back to index](./index.md)

<a id="q117"></a>
Certainly. Here is a clean, exam-style write-up with the **question number, question description, and solution**.

## 118. What is a glitch and why does it occur?

### Solution:

A **glitch** in a digital circuit is a **short-duration, unwanted change in the output signal**. It appears as a temporary pulse or fluctuation in the waveform, even though the output is expected to remain stable or change only once. In other words, a glitch is a **momentary incorrect output** caused by timing differences inside the circuit.

Glitches occur mainly because **real digital gates do not respond instantaneously**. Every logic gate and interconnect has some **propagation delay**, so when the inputs of a combinational circuit change, the signals do not reach all parts of the circuit at exactly the same time. During this brief interval, the output may momentarily assume an incorrect value before settling to the correct one.

### Why glitches occur:

**1. Unequal propagation delays in combinational logic**
This is the most common cause of glitches. In a combinational circuit, different paths from input to output may have different delays. When an input changes, one path may respond faster than another, causing the output to temporarily become incorrect.

**2. Reconvergent signal paths**
Sometimes a signal splits into multiple paths and later recombines. If these paths have different delays, the recombined output may briefly produce the wrong result, creating a glitch.

**3. Race conditions**
When two or more signals try to control the same output and do not arrive in a properly synchronized way, a race condition may occur. This can lead to temporary wrong output transitions.

**4. Clock skew**
Clock skew is the difference in clock arrival time at different flip-flops or sequential elements. Although it is not the direct cause of a combinational glitch, it can make glitches more dangerous by allowing temporary incorrect values to be sampled.

**5. Signal integrity problems**
In high-speed circuits, issues such as reflections, ringing, crosstalk, or impedance mismatch can also create unwanted short pulses that appear as glitches.

### Characteristics of glitches:

* They are **very short in duration**
* They are **unwanted and temporary**
* They usually occur during **input transitions**
* Their occurrence depends strongly on **timing differences** inside the circuit

### Example:

Suppose a logic output should remain at logic 1 during an input transition. But because one logic path turns OFF slightly earlier than another path turns ON, the output may briefly go to logic 0 and then return to logic 1. This brief incorrect pulse is called a **glitch**.

### Effects of glitches:

Glitches are undesirable because they can:

* cause incorrect operation in digital circuits
* produce false triggering in control signals
* increase **dynamic power consumption** due to unnecessary switching
* create problems if captured by flip-flops or sequential logic

### Conclusion:

A **glitch** is a **temporary and undesired change in the output of a digital circuit**. It occurs mainly because of **differences in propagation delays**, **race conditions**, **clock skew effects**, and **signal integrity issues**. Proper timing design, synchronization, and hazard-free logic implementation help reduce glitches.

If you want, I can also rewrite this in:

* **2-mark answer style**
* **5-mark answer style**
* **very simple classroom language**


<a id="q118"></a>
## 118. What is a glitch and why does it occur?

**Written answer:**

A **glitch** is a short, unwanted pulse or temporary wrong value on a signal before the signal settles to its correct value. It can appear as a brief spike from `0` to `1`, or a brief dip from `1` to `0`.

In digital circuits, gates and wires have propagation delay. Cornell's timing notes discuss that signals take time to propagate through gates and paths. [[S4]](#s4) Because different paths can have different delays, inputs to a gate may not arrive at exactly the same time. During that small time difference, the output can briefly become wrong.

### Simple reason

```text
Glitch happens because different signal paths have different delays.
```

### Example

Consider:

```text
Y = (A & B) | (~A & C)
```

If `B = 1` and `C = 1`, then logically:

```text
Y = A | ~A = 1
```

So `Y` should stay `1` even when `A` changes. But in real hardware, `A` reaches one AND gate directly, and `~A` reaches the other AND gate through an inverter. The inverter adds delay. During the transition, both AND outputs may briefly become `0`, so the OR output `Y` briefly dips to `0`. That dip is a glitch.

### Main causes of glitches

1. **Unequal gate delays:** different paths have different numbers of gates.
2. **Wire delay:** longer routes take more time.
3. **Reconvergent fanout:** one signal splits into multiple paths and later combines again.
4. **Multiple inputs changing together:** logic may pass through temporary intermediate values.
5. **Asynchronous inputs:** input changes may happen at any time, not aligned to the clock.
6. **Mealy outputs:** current input can directly affect output through combinational logic.
7. **Clock skew or generated clocks:** if combinational logic is used badly for clock/reset/enable, glitches can become dangerous.

### Types of glitches or hazards

| Type | Meaning |
|---|---|
| Static-1 hazard | Output should stay `1`, but briefly goes to `0`. |
| Static-0 hazard | Output should stay `0`, but briefly goes to `1`. |
| Dynamic hazard | Output should change once, but toggles multiple times before settling. |

### Are glitches always a problem?

Not always. In a synchronous design, a small glitch in combinational logic is usually okay if it settles before the next clock edge and is captured correctly by a flip-flop.

But glitches are dangerous when they drive:

1. clock signals,
2. asynchronous reset or set,
3. latch enable,
4. write enable,
5. memory enable,
6. external pins or handshake signals.

### How to reduce glitches

1. Register important outputs.
2. Avoid using combinational logic to generate clocks.
3. Synchronize asynchronous inputs.
4. Use balanced logic paths when timing is critical.
5. Add hazard-covering logic when designing asynchronous/combinational control.
6. Use static timing analysis to make sure signals settle before capture.

**Speak like this:**

"A glitch is a short unwanted pulse on a signal. It happens because real gates and wires have delay. If two paths reach the same gate at different times, the output can temporarily see the wrong input combination and produce a spike or dip. In synchronous logic, a glitch is usually okay if it settles before the clock edge. But if the glitch drives a clock, reset, latch enable, write enable, or important control signal, it can cause a serious bug. The usual solution is to register important outputs, synchronize asynchronous inputs, and avoid combinational clock or reset generation."

[Back to index](./index.md)

<a id="q126"></a>
## 126. What is a program counter?

**Written answer:**

The **program counter (PC)** is a special CPU register that holds the address of the **next instruction** to be fetched. In a simple fetch-execute cycle, the processor reads the instruction at the address stored in the PC, then updates the PC to point to the next instruction. MIT's ISA notes describe the PC as the register that indicates where instruction fetch should happen next. [[S101]](#s101)

### What does the PC do?

1. During normal sequential execution, it moves to the next instruction.
2. During a branch or jump, it is loaded with a new target address.
3. During a call, it changes to the function address.
4. During an interrupt or exception, it changes to the handler address.

So the PC controls the **flow of execution**.

### Example

If the PC contains:

```text
PC = 1000
```

the processor fetches the instruction stored at address `1000`.

If the instruction is a normal sequential instruction, the PC may become:

```text
PC = 1001
```

or `1004`, depending on instruction size and architecture.

If the instruction is a jump, the PC may instead become:

```text
PC = target_address
```

### Why is it important?

Without the program counter, the CPU would not know which instruction to fetch next. It is one of the most fundamental registers in any processor.

**Speak like this:**

"The program counter is a special CPU register that stores the address of the next instruction to fetch. During normal execution it moves to the next instruction, but during a jump, branch, call, or interrupt it loads a new address. So the PC basically controls the instruction flow of the processor."

[Back to index](./index.md)

<a id="q127"></a>
## 127. What are address lines and data lines?

**Written answer:**

Address lines and data lines are two basic parts of the system bus.

- **Address lines** tell the memory or peripheral **which location** is being accessed.
- **Data lines** carry the **actual data** being read or written.

Architecture basics notes describe the address bus as selecting a location and the data bus as carrying the information transferred. [[S102]](#s102)

### Address lines

Address lines are used to select a memory address or an I/O register.

If a system has `n` address lines, it can uniquely select:

```text
2^n locations
```

Example:

```text
16 address lines -> 2^16 = 65,536 locations
```

### Data lines

Data lines carry the actual binary data between CPU, memory, and peripherals.

If a system has `m` data lines, it can transfer:

```text
m bits at a time
```

Example:

```text
8 data lines -> 8 bits = 1 byte at a time
32 data lines -> 32 bits at a time
```

### Quick difference

| Bus type | Purpose |
|---|---|
| Address lines | Select where to read or write |
| Data lines | Carry what is read or written |

### Example

If a processor has 16 address lines and 8 data lines:

1. It can address `2^16 = 65536` locations.
2. It transfers 8 bits per access.
3. If memory is byte-addressed, total directly addressable storage is `64 KB`.

**Speak like this:**

"Address lines tell the memory or peripheral which location I want to access. Data lines carry the actual data being read or written. If I have n address lines, I can access 2 to the power n locations. If I have m data lines, I can transfer m bits at a time."

[Back to index](./index.md)

<a id="q128"></a>
## 128. Implement AND, OR, and inverter using NAND.

**Written answer:**

NAND is a **universal gate**, which means we can build other basic gates using only NAND gates. UC San Diego's logic lecture notes specifically list NAND and NOR as universal gates. [[S103]](#s103)

### 1. Inverter using NAND

Tie both inputs of the NAND gate together:

```text
Y = A NAND A = ~(A.A) = ~A
```

Circuit idea:

```text
A ----\
       NAND ---- Y
A ----/
```

### 2. AND using NAND

First generate `~(A.B)` using a NAND gate, then invert it using another NAND-as-inverter:

```text
X = A NAND B
Y = X NAND X
```

So:

```text
Y = A.B
```

Circuit idea:

```text
A ----\
       NAND --- X ---\
B ----/               NAND --- Y
          X ---------/
```

### 3. OR using NAND

Using De Morgan's law:

```text
A + B = ~(~A . ~B)
```

So:

1. Invert `A` using NAND.
2. Invert `B` using NAND.
3. NAND the two inverted signals.

```text
X = A NAND A = ~A
Z = B NAND B = ~B
Y = X NAND Z = A + B
```

### Final formulas

```text
NOT: Y = A NAND A
AND: Y = (A NAND B) NAND (A NAND B)
OR : Y = (A NAND A) NAND (B NAND B)
```

**Speak like this:**

"Since NAND is a universal gate, I can build NOT, AND, and OR using only NAND gates. For NOT, I tie both inputs together. For AND, I NAND the inputs and then invert the result with another NAND. For OR, I first invert both inputs using NAND and then NAND those inverted signals using De Morgan's law."

[Back to index](./index.md)

<a id="q129"></a>
## 129. Draw a 2:1 MUX and a 4:1 MUX using NAND gates.

**Written answer:**

A multiplexer selects one of many inputs based on select lines. Georgia Tech's logic examples show gate-level realizations of multiplexers and basic combinational blocks. [[S104]](#s104)

## 2:1 MUX using NAND

The Boolean equation of a 2:1 MUX is:

```text
Y = (~S . I0) + (S . I1)
```

Using only NAND gates:

```text
Sbar = S NAND S
X0   = I0 NAND Sbar
X1   = I1 NAND S
Y    = X0 NAND X1
```

### Gate count

Standard realization uses **4 NAND gates**.

### Block view

```text
        +------+
S ----->| NAND |---- Sbar
        +------+

I0 ----\
        NAND --------\
Sbar --/              \
                        NAND ---- Y
I1 ----\              /
        NAND --------/
S -----/
```

## 4:1 MUX using NAND

A clean way is to build it from **three 2:1 MUX blocks**.

### Hierarchical structure

1. First stage selects between `I0` and `I1` using `S0`.
2. First stage selects between `I2` and `I3` using `S0`.
3. Final stage selects between those two results using `S1`.

```text
Y0 = MUX2(I0, I1, S0)
Y1 = MUX2(I2, I3, S0)
Y  = MUX2(Y0, Y1, S1)
```

### ASCII diagram

```text
I0 ----\
        MUX2 ---- Y0 --\
I1 ----/                \
                         MUX2 ---- Y
I2 ----\                /
        MUX2 ---- Y1 --/
I3 ----/

S0 controls first two MUX2 blocks
S1 controls final MUX2 block
```

If each `MUX2` uses 4 NAND gates, then a straightforward 4:1 MUX uses:

```text
3 x 4 = 12 NAND gates
```

### Truth table of 4:1 MUX

| S1 | S0 | Output |
|---|---|---|
| 0 | 0 | I0 |
| 0 | 1 | I1 |
| 1 | 0 | I2 |
| 1 | 1 | I3 |

**Speak like this:**

"For a 2-to-1 MUX, the equation is `Y = Sbar.I0 + S.I1`. Using NAND only, I first generate `Sbar`, then I form the two product terms with NAND gates, and finally NAND them together. For a 4-to-1 MUX, the easiest method is hierarchical: build three 2-to-1 MUX blocks using NAND gates, two in the first stage and one in the second stage."

[Back to index](./index.md)

<a id="q130"></a>
## 130. What is minimum pulse width, and what happens to it if NAND or NOR gates are connected one after another?

**Written answer:**

The **minimum pulse width** is the shortest high pulse or low pulse that a circuit can reliably detect, propagate, or use correctly. Logic handbooks and timing documentation specify minimum high-width and low-width requirements because very narrow pulses can be missed or distorted. [[S105]](#s105)

### Why minimum pulse width matters

If a pulse is too narrow:

1. a gate may not fully switch,
2. a flip-flop or latch may not recognize it correctly,
3. the pulse may shrink further as it propagates,
4. the next stage may completely miss it.

### What happens in a NAND/NOR chain?

When NAND or NOR gates are cascaded:

1. every stage adds **propagation delay**,
2. rising and falling edges usually do **not** have exactly the same delay,
3. so the pulse width can **change** at each stage,
4. narrow pulses may **shrink**, **widen**, or even **disappear**.

### Intuition

Suppose a narrow input pulse enters a gate chain.

- One edge of the pulse may travel with delay `tPHL`.
- The other edge may travel with delay `tPLH`.

If those delays are unequal, the output pulse width changes.

So after many cascaded gates, the pulse seen at the output may no longer have the same width as the input pulse.

### NAND vs NOR in a chain

In CMOS, NOR is usually slower than NAND for similar sizing and load because NOR has poorer logical effort and typically a weaker pull-up path. That means a NOR chain usually gives **more delay** and can distort pulse width more severely than a NAND chain. [[S105]](#s105) [[S106]](#s106)

### Practical effect

If you connect many NAND or NOR gates one after another:

1. total delay increases,
2. duty cycle can shift,
3. narrow pulses may be filtered out,
4. maximum operating frequency decreases.

**Speak like this:**

"Minimum pulse width means the shortest pulse that the circuit can still recognize correctly. When I cascade NAND or NOR gates, each stage adds delay, and the rising and falling edges do not usually have the same delay. So the pulse width can change from stage to stage. If the pulse is already narrow, it may shrink so much that the next stage misses it. In general, a NOR chain is worse than a NAND chain because NOR is usually slower in CMOS."

[Back to index](./index.md)

<a id="q131"></a>
## 131. Among NAND and NOR, which one is preferred and why?

**Written answer:**

In CMOS, **NAND is usually preferred over NOR** for speed and area when both are available as implementation choices. The main reason is that NAND has lower logical effort than NOR. Logical-effort notes list the logical effort of a 2-input NAND as `4/3` and a 2-input NOR as `5/3`. Lower logical effort generally means better drive for the same input capacitance. [[S106]](#s106)

### Why NAND is preferred

1. **Lower logical effort:** NAND is easier to drive than NOR.
2. **Usually faster:** for similar loading, NAND often has lower delay.
3. **Better area efficiency:** NOR often needs larger PMOS devices to compensate for weak pull-up.
4. **Less capacitance for equivalent performance:** this helps speed and power.

### CMOS intuition

- In a NAND gate, the PMOS devices are in **parallel**, which helps the pull-up path.
- In a NOR gate, the PMOS devices are in **series**, which makes the pull-up path weaker and slower.

That is why NOR typically needs more sizing effort to match speed.

### Important note

This does **not** mean NOR is useless. NOR is still a universal gate and may be the right choice for a particular logic expression. But if the question is "which is generally preferred in CMOS?", the usual answer is **NAND**.

**Speak like this:**

"In CMOS, NAND is usually preferred over NOR because it has lower logical effort, lower delay, and better area efficiency for the same function style. The main reason is that NOR has series PMOS devices in the pull-up path, so it is usually slower. So if I have a choice between NAND-based and NOR-based realization, I generally prefer NAND."

[Back to index](./index.md)

<a id="q132"></a>
## 132. What happens if I connect 10 NAND gates one after another, and what changes if I replace them with NOR gates?

**Written answer:**

Assume each NAND or NOR gate is used as an **inverter stage** by tying its two inputs together:

```text
NAND(A,A) = ~A
NOR(A,A)  = ~A
```

Then each stage inverts the signal once.

### If 10 gates are cascaded

1. There are **10 inversions**.
2. Since 10 is even, the final output has the **same logic polarity** as the input.
3. The total delay is roughly the sum of the delays of all 10 stages.

So:

```text
Y ≈ input delayed by 10 gate delays
```

### What else happens?

1. The edges are delayed more and more.
2. Narrow pulses may get distorted.
3. The available speed goes down.
4. If the loading is large, edge rate may worsen.

### If NAND chain is replaced by NOR chain

The logical behavior is still:

```text
10 inversions -> final polarity same as input
```

But the timing is different.

Because NOR usually has higher logical effort and poorer pull-up in CMOS, the NOR chain is usually:

1. **slower**,
2. more delay-heavy,
3. more sensitive to pulse-width distortion,
4. worse for high-speed paths than NAND. [[S105]](#s105) [[S106]](#s106)

### Simple summary

| Chain type | Final polarity after 10 stages | Delay |
|---|---|---|
| 10 NAND stages | Same as input | Lower than NOR chain |
| 10 NOR stages | Same as input | Higher than NAND chain |

### Important assumption

If the extra input pins are **not** tied correctly, the chain will not behave like a simple inverter chain. Then the actual logic function depends on how those unused inputs are driven.

**Speak like this:**

"If I connect 10 NAND gates one after another and use each as an inverter, then I get 10 inversions, so the final output polarity is the same as the input because 10 is even. But the signal is delayed by all 10 gate delays. If I replace them with NOR gates, the polarity is still the same after 10 stages, but the chain is usually slower in CMOS because NOR has higher logical effort and weaker pull-up."

[Back to index](./index.md)

<a id="q133"></a>
## 133. Draw a block-level diagram of a 4-bit counter and write Verilog code for it.

**Written answer:**

For RTL design, the clean answer is a **synchronous 4-bit up-counter**. Intel's FPGA design guidance recommends avoiding ripple counters in most FPGA designs and using synchronous design style instead. [[S110]](#s110)

### Block-level idea

```text
          +-------------------+
clk ----->|                   |
rst ----->|   4-bit Register  |----> count[3:0]
en  ----->|                   |
          +---------+---------+
                    ^
                    |
              +-----------+
count -------->| +1 logic  |
              +-----------+
                    |
            if en=1 load count+1
            if en=0 hold count
```

### Simple behavior

```text
if rst = 1 -> count = 0000
else if en = 1 -> count = count + 1
else -> hold previous count
```

### Pure Verilog code

```verilog
module counter_4bit (
    input  wire       clk,
    input  wire       rst,
    input  wire       en,
    output reg  [3:0] count
);

always @(posedge clk or posedge rst) begin
    if (rst)
        count <= 4'b0000;
    else if (en)
        count <= count + 1'b1;
end

endmodule
```

### Count sequence

```text
0000
0001
0010
0011
0100
...
1111
0000
```

**Speak like this:**

"A 4-bit counter is basically a 4-bit register plus increment logic. On every active clock edge, if enable is high, the register loads its current value plus one. If reset is high, it goes to zero. In RTL I usually write it as a synchronous counter, not as a ripple counter."

[Back to index](./index.md)

<a id="q134"></a>
## 134. Draw a 2-bit adder at gate level. Convert this adder into a 2-bit counter.

**Written answer:**

A 2-bit adder adds:

```text
A1 A0
+B1 B0
------
S1 S0 with Cout
```

### Gate-level structure of a 2-bit adder

For the LSB, we can use a **half adder**:

```text
S0 = A0 ^ B0
C1 = A0 . B0
```

For the MSB, we use a **full-adder style stage**:

```text
S1   = A1 ^ B1 ^ C1
Cout = (A1.B1) + (C1.(A1 ^ B1))
```

### Block diagram

```text
A0 ----\
        HA ---- S0
B0 ----/  \
          C1 ----\

A1 --------\      \
            FA ---- S1
B1 --------/  \
              Cout
```

### Convert this adder into a 2-bit counter

A counter repeatedly does:

```text
next_count = current_count + 1
```

So to convert the 2-bit adder into a 2-bit counter:

1. Feed the present count back as one input.
2. Fix the other input as `01`.
3. Store the adder output in a 2-bit register.

```text
current_count + 01 -> next_count
```

### Resulting equations

Let current count be `Q1 Q0`.

Then:

```text
D0 = ~Q0
D1 = Q1 ^ Q0
```

This is exactly the next-state logic of a 2-bit synchronous up-counter.

### Counter sequence

```text
00 -> 01 -> 10 -> 11 -> 00
```

**Speak like this:**

"A 2-bit adder can be built using a half adder for bit 0 and a full-adder style stage for bit 1. To convert that adder into a 2-bit counter, I feed the current count back to one adder input and fix the other input as 01. Then the adder keeps doing current count plus one, so the stored result becomes a 2-bit up-counter."

[Back to index](./index.md)

<a id="q135"></a>
## 135. If a lookup table output is fed back to its input through an inverter, what happens? Draw the output waveform.

**Written answer:**

If a combinational block output is fed back to its own input through an **inversion**, the Boolean relation becomes:

```text
Y = ~Y
```

This has **no stable Boolean solution**. In real hardware, because the LUT and routing have delay, the circuit behaves like an **odd-inversion feedback loop**, which is the basic idea of a **ring oscillator**. A ring oscillator is a circuit made by connecting an odd number of inverting stages in a closed loop, so the signal keeps toggling and produces a periodic oscillation. Intel's FPGA guidance warns that combinational loops are problematic for tools and timing, and ring-oscillator labs explain that a loop with an odd number of inversions oscillates. [[S107]](#s107) [[S114]](#s114)

### What happens in practice?

1. In ideal zero-delay logic, the simulator may produce `X`, oscillation, or delta-cycle instability.
2. In real hardware, the loop can oscillate.
3. The oscillation period depends on LUT plus routing delay.

For one effective inverter delay around the loop:

```text
T ≈ 2 x tpd(loop)
```

More generally, for `N` inverting stages:

```text
T ≈ 2N x tpd
```

### Output waveform

The output toggles continuously:

```text
Y:  _-_-_-_-_-_-_
```

or in a more explicit clock-like shape:

```text
time ->

Y  __----__----__----__
```

### Important practical note

FPGA tools usually do **not** like uncontrolled combinational loops. They may:

1. warn about the loop,
2. optimize it away,
3. fail timing analysis,
4. treat it as unsafe unless explicitly constrained and preserved.

**Speak like this:**

"If I feed a LUT output back to its input through an inverter, the equation becomes `Y = not Y`, which has no stable logic solution. In real hardware that creates an odd-inversion feedback loop, so the output oscillates like a ring oscillator. In simulation it may go unknown or oscillate depending on the delay model."

[Back to index](./index.md)

<a id="q136"></a>
## 136. Can the output of a combinational circuit that looks like a clock be used as a clock signal for a sequential circuit?

**Written answer:**

The practical answer is **no, not as a normal design practice**.

Even if a combinational output looks clock-like, it is usually a **bad clock source** for sequential logic. Intel design guidance recommends synchronous clocking practices and registering combinational outputs instead of using arbitrary logic-generated clock-like signals as clocks. [[S109]](#s109) [[S116]](#s116)

### Why it is a bad idea

1. **Glitches:** combinational logic can generate short pulses.
2. **Poor pulse width control:** high and low times may not be clean.
3. **Large skew:** combinational outputs do not use dedicated clock routing.
4. **PVT sensitivity:** delay changes with process, voltage, and temperature.
5. **Difficult STA:** timing tools do not treat arbitrary logic outputs like clean clocks unless carefully constrained.

### Better solution

If I need a slower event from a fast clock, I should usually generate a **clock enable**, not a new logic clock.

Bad style:

```verilog
always @(posedge fake_clk)
    q <= d;
```

Better style:

```verilog
always @(posedge clk) begin
    if (tick)
        q <= d;
end
```

Here `tick` is a one-cycle enable pulse, not a separate clock.

### Exception

Real derived clocks can exist, but they should come from:

1. PLL/MMCM/DCM/clock-management blocks,
2. vendor-supported clocking resources,
3. properly constrained generated clocks.

**Speak like this:**

"Even if a combinational output looks like a clock, I normally should not use it as a clock for sequential logic. It can glitch, have bad pulse width, and avoid dedicated clock routing, so timing becomes unreliable. The safer approach is to keep one clean clock and generate a clock enable pulse instead."

[Back to index](./index.md)

<a id="q137"></a>
## 137. Do setup and hold time exist for a combinational circuit? If yes, explain with example.

**Written answer:**

Strictly speaking, **setup time and hold time belong to storage elements**, such as flip-flops and latches, not to a standalone combinational gate network. A pure combinational block has **propagation delay** and **contamination delay**, but not its own independent setup/hold specification. Cornell's timing notes explain setup, hold, and register-to-register timing in terms of sequential elements and combinational delay between them. [[S4]](#s4)

### So what is the correct answer?

- **Standalone combinational logic:** no setup/hold of its own.
- **Combinational logic feeding a flip-flop:** yes, the path must satisfy the receiving flip-flop's setup and hold requirements.

### Example

Suppose:

```text
FF1 -> combinational logic -> FF2
```

Then the combinational block must be fast enough for setup and slow enough for hold.

Assuming zero skew:

### Setup condition

```text
Tclk >= tCQ(max) + tPDcomb(max) + tSU
```

### Hold condition

```text
tCQ(min) + tCDcomb(min) >= tH
```

Where:

- `tCQ` = clock-to-Q delay of launch flip-flop,
- `tPDcomb` = max propagation delay of combinational logic,
- `tCDcomb` = min contamination delay of combinational logic,
- `tSU` = setup time of receiving flip-flop,
- `tH` = hold time of receiving flip-flop.

### Intuition

So we do not say "the combinational circuit has setup time." We say:

```text
the combinational path must satisfy the setup/hold requirement of the receiving sequential element
```

**Speak like this:**

"A pure combinational circuit does not have setup and hold time by itself. Setup and hold belong to latches and flip-flops. But if a combinational block is between two flip-flops, then its delay must satisfy the setup and hold requirements of the receiving flip-flop. So in timing analysis, setup and hold are checked on the register-to-register path, not on the standalone combinational block alone."

[Back to index](./index.md)

<a id="q138"></a>
## 138. Draw a 3-bit shift register and name the flip-flops and timing conditions for the first two flip-flops, and the `fmax` of the circuit.

**Written answer:**

A 3-bit shift register is three flip-flops connected in series and driven by the same clock. AMD's synthesis guide includes standard shift-register coding patterns, and Cornell's timing notes give the setup/hold relationships for flip-flop paths. [[S111]](#s111) [[S4]](#s4)

### 3-bit shift register

```text
serial_in -> FF1 -> FF2 -> FF3 -> serial_out
              Q1    Q2    Q3

All three flip-flops use the same clock.
```

ASCII block view:

```text
din ---> [FF1] ---> [FF2] ---> [FF3] ---> dout
            |         |         |
           Q1        Q2        Q3
```

### Name the first two flip-flops

Let:

```text
FF1 = first stage
FF2 = second stage
FF3 = third stage
```

Then the first timing path is:

```text
FF1/Q -> routing -> FF2/D
```

and the second timing path is:

```text
FF2/Q -> routing -> FF3/D
```

### Setup condition for FF1 -> FF2

Assuming common clock and ignoring skew:

```text
Tclk >= tCQ1(max) + tPD12(max) + tSU2
```

### Hold condition for FF1 -> FF2

```text
tCQ1(min) + tCD12(min) >= tH2
```

Where:

- `tCQ1` = clock-to-Q of FF1,
- `tPD12` = max delay from FF1 output to FF2 input,
- `tCD12` = min contamination delay from FF1 output to FF2 input,
- `tSU2` = setup time of FF2,
- `tH2` = hold time of FF2.

### Setup condition for FF2 -> FF3

```text
Tclk >= tCQ2(max) + tPD23(max) + tSU3
```

### Hold condition for FF2 -> FF3

```text
tCQ2(min) + tCD23(min) >= tH3
```

### `fmax` of the circuit

The maximum clock frequency is determined by the **slowest register-to-register path**:

```text
fmax = 1 / Tmax_path
```

For this 3-bit shift register:

```text
fmax = 1 / max(
    tCQ1(max) + tPD12(max) + tSU2,
    tCQ2(max) + tPD23(max) + tSU3
)
```

In a plain shift register, `tPD12` and `tPD23` are usually just wire or small routing delay because there is no big combinational logic between the flops.

**Speak like this:**

"A 3-bit shift register is just three flip-flops in series on the same clock. For timing, I check the path from FF1 to FF2 and the path from FF2 to FF3. The setup equation is clock period greater than clock-to-Q plus path delay plus setup time. The hold equation is clock-to-Q minimum plus contamination delay greater than hold time. The `fmax` is the inverse of the slowest register-to-register setup path."

[Back to index](./index.md)

<a id="q139"></a>
## 139. Write structural Verilog code of a full adder using a half adder as leaf cell, and write the testbench for the same.

**Written answer:**

A standard structural full adder can be built from:

1. two half adders, and
2. one OR gate.

AMD's synthesis guide includes half-adder examples, and the same idea extends naturally to a structural full adder. [[S112]](#s112)

### Leaf cell: half adder

```verilog
module half_adder (
    input  wire a,
    input  wire b,
    output wire sum,
    output wire carry
);

xor (sum, a, b);
and (carry, a, b);

endmodule
```

### Full adder using half adder leaf cells

```verilog
module full_adder_struct (
    input  wire a,
    input  wire b,
    input  wire cin,
    output wire sum,
    output wire cout
);

wire s1;
wire c1;
wire c2;

half_adder ha1 (
    .a(a),
    .b(b),
    .sum(s1),
    .carry(c1)
);

half_adder ha2 (
    .a(s1),
    .b(cin),
    .sum(sum),
    .carry(c2)
);

or (cout, c1, c2);

endmodule
```

### Testbench

```verilog
`timescale 1ns/1ps

module tb_full_adder_struct;

reg  a;
reg  b;
reg  cin;
wire sum;
wire cout;

full_adder_struct dut (
    .a(a),
    .b(b),
    .cin(cin),
    .sum(sum),
    .cout(cout)
);

initial begin
    $display("time  a b cin | sum cout");
    $monitor("%4t   %b %b  %b  |  %b    %b", $time, a, b, cin, sum, cout);

    a = 0; b = 0; cin = 0; #10;
    a = 0; b = 0; cin = 1; #10;
    a = 0; b = 1; cin = 0; #10;
    a = 0; b = 1; cin = 1; #10;
    a = 1; b = 0; cin = 0; #10;
    a = 1; b = 0; cin = 1; #10;
    a = 1; b = 1; cin = 0; #10;
    a = 1; b = 1; cin = 1; #10;

    $finish;
end

endmodule
```

**Speak like this:**

"I make the full adder structurally by instantiating two half adders. The first half adder adds A and B. The second half adder adds the first sum with Cin. Then I OR the two carry outputs to get Cout. In the testbench, I apply all 8 input combinations and monitor sum and carry."

[Back to index](./index.md)

<a id="q140"></a>
## 140. In a D flip-flop, if I use only `if`, is a latch inferred or not?

**Written answer:**

If the code is inside a **clocked D flip-flop block**, using only `if` does **not** infer a latch.

Example:

```verilog
always @(posedge clk) begin
    if (en)
        q <= d;
end
```

This is **not** a latch. It is a **D flip-flop with enable**. AMD's FDRE primitive is exactly a D flip-flop with clock enable, and synthesis tools commonly infer this pattern from clocked RTL. [[S113]](#s113)

### Why no latch is inferred

Because the block is already **edge-triggered**:

```verilog
always @(posedge clk)
```

The register naturally holds its previous value between clock edges. So when `en = 0`, the tool does not need a latch. It just keeps the existing flip-flop state.

### Where latch inference actually happens

Latches are inferred in **level-sensitive or combinational blocks** when an output is not assigned on every path.

Example:

```verilog
always @(*) begin
    if (en)
        q = d;
end
```

This infers a latch because when `en = 0`, `q` must hold its previous value inside a level-sensitive block.

If you want the same latch style with an explicit sensitivity list and reset, you can write:

```verilog
always @(d or en or rst) begin
    if (rst)
        q = 1'b0;
    else if (en)
        q = d;
end
```

This also infers a latch. When `rst = 1`, `q` clears to `0`. When `rst = 0` and `en = 1`, `q` follows `d`. When both `rst = 0` and `en = 0`, `q` is not assigned, so it holds its previous value. That hold behavior is latch inference.

Modern Verilog usually writes this as `always @(*)` instead of manually listing `d`, `en`, and `rst`, because the tool automatically includes all read signals.

### Summary

| Coding style | Hardware inferred |
|---|---|
| `always @(posedge clk) if (en) q <= d;` | DFF with enable |
| `always @(*) if (en) q = d;` | Latch |
| `always @(d or en or rst) if (rst) q = 0; else if (en) q = d;` | Latch with reset |

**Speak like this:**

"If I use only `if` inside a clocked DFF block like `always @(posedge clk)`, a latch is not inferred. It becomes a flip-flop with enable, because the flip-flop already holds its old value between clock edges. Latch inference happens in combinational or level-sensitive blocks when some paths leave the signal unassigned."

[Back to index](./index.md)

<a id="q141"></a>
## 141. Use a DFF with enable: if `en` is present then `dout <= din`, otherwise hold previous value. Write Verilog code and circuit diagram.

**Written answer:**

This is a **D flip-flop with enable**.

Behavior:

```text
if en = 1, q captures d on clock edge
if en = 0, q holds previous value
```

### Pure Verilog code

```verilog
module dff_enable (
    input  wire clk,
    input  wire rst,
    input  wire en,
    input  wire din,
    output reg  dout
);

always @(posedge clk or posedge rst) begin
    if (rst)
        dout <= 1'b0;
    else if (en)
        dout <= din;
end

endmodule
```

### Why it holds value when `en = 0`

Because on that clock edge, no new value is loaded into the DFF, so the register keeps its old state.

### Circuit idea

This is often viewed as a **2:1 MUX feeding a DFF**:

```text
                +------+
din ----------->| 0    |
                | 2:1  |---- D ----> [ DFF ] ----> dout
dout ---------->| 1MUX |
                +------+
                   ^
                   |
                  en
```

Equivalent next-state equation:

```text
D = en ? din : dout
```

So when `en = 1`, the mux selects `din`. When `en = 0`, it feeds back `dout`, so the DFF reloads its previous value.

**Speak like this:**

"This is a D flip-flop with enable. On the active clock edge, if enable is high, `dout` loads `din`. If enable is low, it holds the previous value. Circuit-wise, I can think of it as a 2-to-1 mux in front of the D input: one input is `din`, the other is feedback from `dout`."

[Back to index](./index.md)

<a id="q142"></a>
## 142. Write Verilog code for `d_latch`.

**Written answer:**

A D latch is **level-sensitive**. When enable is high, output follows input. When enable is low, it holds its previous value. AMD and Intel synthesis guides show latch inference using level-sensitive coding style, not edge-triggered `posedge` style. [[S84]](#s84) [[S85]](#s85)

### Basic D latch

```verilog
module d_latch (
    input  wire d,
    input  wire en,
    output reg  q
);

always @(*) begin
    if (en)
        q = d;
end

endmodule
```

### Behavior

```text
if en = 1, q follows d
if en = 0, q holds previous value
```

### D latch with reset

```verilog
module d_latch_rst (
    input  wire d,
    input  wire en,
    input  wire rst,
    output reg  q
);

always @(*) begin
    if (rst)
        q = 1'b0;
    else if (en)
        q = d;
end

endmodule
```

**Speak like this:**

"A D latch is level sensitive, so I code it with `always @(*)`, not `always @(posedge clk)`. If enable is high, `q` follows `d`. If enable is low, I do not assign `q`, so it holds its previous value. That hold behavior is what makes it a latch."

[Back to index](./index.md)

<a id="q143"></a>
## 143. Write Verilog code for a normal DFF.

**Written answer:**

A normal D flip-flop samples input `d` on the active clock edge and stores it in `q`.

### Basic positive-edge DFF

```verilog
module dff (
    input  wire clk,
    input  wire d,
    output reg  q
);

always @(posedge clk)
    q <= d;

endmodule
```

### DFF with asynchronous reset

```verilog
module dff_rst (
    input  wire clk,
    input  wire rst,
    input  wire d,
    output reg  q
);

always @(posedge clk or posedge rst) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end

endmodule
```

### Important point

Use **nonblocking assignment** `<=` in sequential always blocks. AMD's FDRE primitive and synthesis inference guidelines model this kind of edge-triggered register behavior. [[S113]](#s113) [[S21]](#s21)

**Speak like this:**

"A normal D flip-flop captures `d` on the positive edge of the clock and stores it in `q`. In Verilog I write it with `always @(posedge clk)` and I use nonblocking assignment. If reset is needed, I add it in the sensitivity list and clear `q` in the reset condition."

[Back to index](./index.md)

<a id="q144"></a>
## 144. Difference between `task` and `function`.

**Written answer:**

In Verilog, both `task` and `function` are reusable procedural blocks, but they are meant for different kinds of work. A **function** is expression-like: it computes and returns one value and must execute in **zero simulation time**. A **task** is procedure-like: it can model a sequence of actions, may consume simulation time, and can communicate results through its arguments. The Verilog language standard defines these restrictions explicitly, and SystemVerilog keeps the same core distinction even though it extends the declaration syntax. [[S5]](#s5) [[S75]](#s75)

### Main differences

| Feature | Function | Task |
|---|---|---|
| Return mechanism | Returns one value by assigning the function name | Does not return a single expression value; passes results through `output`/`inout` arguments |
| Timing control | Cannot contain `#delay`, `@event`, `wait`, or other time-consuming controls | Can contain timing and event controls |
| Simulation time | Must complete in zero simulation time | May consume simulation time |
| Use in expressions | Can be used inside expressions, continuous assignments, and RHS calculations | Cannot be used as an expression return |
| Arguments in pure Verilog | Input arguments only | Can have `input`, `output`, and `inout` arguments |
| Calling restrictions | Can call other functions, but not tasks | Can call both tasks and functions |
| Number of outputs | One returned value | Multiple values possible through arguments |
| Best use | Reusable calculation or combinational transform | Multi-step procedure, testbench stimulus, handshaking, file I/O, timed behavior |

### Pure Verilog rules interviewers usually expect

For a **Verilog** interview answer, these are the core rules to remember:

1. A function returns exactly one value.
2. A function executes in zero simulation time.
3. A function cannot contain timing or event control.
4. A function cannot call a task.
5. A task can have multiple outputs through arguments.
6. A task may consume time and may call other tasks or functions.

### Important Verilog vs SystemVerilog note

In **pure Verilog**, functions are treated more strictly, especially for arguments and time control. In **SystemVerilog**, the syntax is more flexible and adds features such as richer argument declarations, but the interview-safe conceptual difference is still:

```text
function = value-returning, zero-time computation
task     = procedure-style block that may consume time
```

### Function example

```verilog
function [3:0] add4;
    input [3:0] a;
    input [3:0] b;
    begin
        add4 = a + b;
    end
endfunction
```

Used like:

```verilog
assign y = add4(a, b);
```

This is a good function example because it behaves like a reusable combinational calculation and returns one value.

### Task example

```verilog
task apply_vector;
    input a;
    input b;
    input cin;
    begin
        in_a  = a;
        in_b  = b;
        in_ci = cin;
        #10;
    end
endtask
```

This is suitable for a testbench because it uses a delay, so it consumes simulation time. That is exactly the kind of thing a function is not allowed to do.

### Example of multiple outputs from a task

```verilog
task half_adder_task;
    input  a;
    input  b;
    output sum;
    output carry;
    begin
        sum   = a ^ b;
        carry = a & b;
    end
endtask
```

Here a single task call can produce both `sum` and `carry`. A function cannot return two independent values this way.

### Which one is better for synthesis?

Neither is automatically "better." What matters is whether the code **inside** the task or function is synthesizable.

- A function with pure combinational logic is commonly synthesizable.
- A task can also be synthesizable if it contains only synthesizable statements and no delays or event controls.
- A task that contains `#10`, `@(posedge clk)`, `wait`, `$display`, or file operations is for simulation/testbench use, not hardware inference.

### Important synthesis note

Tasks and functions can both be synthesizable **only if** the code inside them is synthesizable. Synthesis tools conceptually inline the body. So a function is not "magic hardware" and a task is not "non-synthesizable by definition." The real question is whether the statements inside correspond to legal hardware.

**Speak like this:**

"A function is for reusable zero-time computation and it returns one value, so I use it like part of an expression. A task is more like a reusable procedure. It can have multiple outputs through arguments and it can include delays, waits, and event controls. In pure Verilog, a function cannot call a task and cannot contain timing control, while a task can call both tasks and functions. So for combinational calculation I prefer a function, and for multi-step or timed behavior, especially in a testbench, I use a task."

[Back to index](./index.md)

<a id="q145"></a>
## 145. Draw the XOR gate using CMOS logic.

**Written answer:**

An XOR gate can be written as:

```text
Y = A'B + AB'
```

In static CMOS, a common interview answer is the **12-transistor XOR**:

1. two inverters generate `Abar` and `Bbar`,
2. a pull-up network (PMOS),
3. a pull-down network (NMOS).

Microelectronics notes on static CMOS XOR show this complementary pull-up and pull-down style. [[S115]](#s115)

### Step 1: generate complements

```text
Abar = ~A
Bbar = ~B
```

This needs two CMOS inverters.

### Step 2: pull-up network for `Y = A'B + AB'`

Use two PMOS series branches in parallel:

```text
Branch 1: PMOS(gate=A)    in series with PMOS(gate=Bbar)
Branch 2: PMOS(gate=Abar) in series with PMOS(gate=B)
```

These two branches are connected in parallel between `VDD` and `Y`.

### Step 3: pull-down network for `Y' = AB + A'B'`

The complementary pull-down can be built as two NMOS parallel groups in series:

```text
Group 1: NMOS(gate=A)    in parallel with NMOS(gate=Bbar)
Group 2: NMOS(gate=Abar) in parallel with NMOS(gate=B)
```

These two groups are connected in series between `Y` and `GND`.

### ASCII view

```text
                VDD
                 |
        +--------+--------+
        |                 |
     P(A)             P(Abar)
        |                 |
     P(Bbar)          P(B)
        |                 |
        +-------- Y ------+
                 |
        +--------+--------+
        |                 |
   N(A) || N(Bbar)   N(Abar) || N(B)
        |                 |
        +--------+--------+
                 |
                GND
```

Also generate `Abar` and `Bbar` using two inverters at the inputs.

### Transistor count

```text
2 inverters  -> 4 transistors
PUN + PDN    -> 8 transistors
Total        -> 12 transistors
```

### Important note

There are also transmission-gate XOR implementations with fewer transistors, but if the question says "draw XOR using CMOS logic," the safe answer is usually the static CMOS transistor network.

**Speak like this:**

"For CMOS XOR, I first write the function as `Abar.B + A.Bbar`. Then I generate `Abar` and `Bbar` using two inverters. In static CMOS, the pull-up network is built from two PMOS series branches in parallel, and the pull-down network is the complementary NMOS network. A standard static CMOS XOR usually uses 12 transistors."

[Back to index](./index.md)

<a id="q146"></a>
## 146. Difference between `$display`, `$monitor`, and `` `define ``.

**Written answer:**

In Verilog, `$display` and `$monitor` are **system tasks** used during simulation, while `` `define `` is a **preprocessor macro directive** handled before compilation. The Verilog standard defines all three in different parts of the language flow. [[S5]](#s5)

### Main difference

| Item | `$display` | `$monitor` | `` `define `` |
|---|---|---|---|
| Type | System task | System task | Preprocessor directive |
| When it works | When the statement executes | Automatically whenever a listed argument changes | Before compilation / preprocessing |
| Purpose | Print once | Keep watching signals and print on change | Create macros / constants / text substitution |
| Runtime or compile-time | Runtime | Runtime | Compile-time |
| Typical use | Debug a particular point | Watch wave-like behavior during simulation | Constant names, reusable macros, conditional compilation |

### `$display`

`$display` prints one line when that statement is reached.

```verilog
initial begin
    $display("a=%b b=%b y=%b", a, b, y);
end
```

### `$monitor`

`$monitor` keeps monitoring the listed signals and prints whenever one of them changes.

```verilog
initial begin
    $monitor("t=%0t a=%b b=%b y=%b", $time, a, b, y);
end
```

### `` `define ``

`` `define `` creates a macro that is substituted before compilation.

```verilog
`define WIDTH 8
reg [`WIDTH-1:0] data;
```

### Important interview point

1. `$display` is a one-time print when control reaches that line.
2. `$monitor` is automatic printing on value change.
3. `` `define `` does not execute in hardware or simulation time; it is text substitution before compilation.

**Speak like this:**

"`$display` prints once when the statement executes. `$monitor` keeps watching the listed signals and prints whenever they change. `` `define `` is different from both, because it is a preprocessor macro used before compilation, not a runtime task."

[Back to index](./index.md)

<a id="q147"></a>
## 147. How do we meet frequency between two D flip-flops with combinational logic in between?

**Written answer:**

To meet frequency between `Flop1` and `Flop2`, I check the **setup timing equation** for the register-to-register path. Timing notes express the idea as:

```text
Tclk >= Tcq + Tcomb + Tsetup + clock_uncertainty/skew_margin
```

If this condition is not met, the path cannot run at the target frequency. [[S4]](#s4) [[S130]](#s130)

### Path model

```text
Flop1 ---- combinational logic ---- Flop2
  |                                  |
 launch                             capture
```

### What limits frequency?

The maximum frequency is limited by the slowest register-to-register path:

```text
fmax approx 1 / Tcritical
```

where `Tcritical` is the longest clocked path delay budget.

### How to meet frequency

#### 1. Reduce combinational delay

1. reduce logic depth,
2. use faster cells,
3. remove unnecessary gates,
4. simplify Boolean logic.

#### 2. Improve physical implementation

1. place related flops closer,
2. reduce routing delay,
3. improve buffering and transition,
4. reduce load/fanout on critical nets.

#### 3. Pipeline the path

If logic is too deep, insert one more register stage:

```text
Flop1 -> logic1 -> Flop_mid -> logic2 -> Flop2
```

This is usually the strongest architectural fix.

#### 4. Retiming / balancing

Move registers across logic where legal so path delays are more evenly distributed.

#### 5. Clock-side help

Use controlled clock skew only carefully. It can help setup, but it must not create hold problems.

### Interview-safe summary

If the question says "data from Flop1 to Flop2 should pass efficiently," the real answer is:

```text
make the data path faster or give it more cycles by pipelining
```

**Speak like this:**

"I meet the frequency by checking the register-to-register setup path from Flop1 to Flop2. If `Tcq + Tcomb + Tsetup` is too large for the target clock period, I reduce combinational delay, improve placement and routing, reduce fanout, or pipeline the logic by adding another flop. For deeper problems, pipelining is usually the cleanest fix."

[Back to index](./index.md)

<a id="q148"></a>
## 148. Differentiate latch and flip-flop. Explain with diagram.

**Written answer:**

A **latch** is **level-sensitive**, while a **flip-flop** is **edge-triggered**. Cornell notes describe latches as transparent during an active level and flip-flops as state elements that sample on a clock edge. [[S3]](#s3)

### Basic diagrams

#### Latch

```text
      D -----> [ LATCH ] -----> Q
                  ^
                  |
                 EN
```

When `EN` is active, output can follow input. When `EN` is inactive, it holds the previous value.

#### Flip-flop

```text
      D -----> [ FLIP-FLOP ] -----> Q
                    ^
                    |
                   CLK
```

It samples input only on `posedge CLK` or `negedge CLK`, depending on the design.

### Main differences

| Feature | Latch | Flip-flop |
|---|---|---|
| Sensitivity | Level-sensitive | Edge-triggered |
| Transparency | Transparent when enable is active | Not transparent between edges |
| Timing style | Can allow time borrowing | Cleaner synchronous timing |
| Typical control | Enable | Clock edge |
| Common risk | Transparency / unintended latch inference | Higher clocking overhead but easier synchronous design |

### Practical understanding

1. A latch is "open" during the active level.
2. A flip-flop captures once at the edge and then holds.

### Interview-safe conclusion

Flip-flops are preferred in most synchronous digital flows because timing analysis is more straightforward.

**Speak like this:**

"The main difference is that a latch is level-sensitive, so while enable is active it can keep passing input to output. A flip-flop is edge-triggered, so it samples input only at the clock edge and then holds the value. That is why flip-flops are more common in synchronous designs, while latches are used when level-sensitive behavior or time borrowing is needed."

[Back to index](./index.md)

<a id="q149"></a>
## 149. Implement latch using 2:1 MUX, and then convert it to a flop.

**Written answer:**

### 1. D latch using a 2:1 MUX

A latch can be built by feeding back the old output to one input of a `2:1` mux.

```text
             +-------------------+
 D --------->| 1                 |
             |      2:1 MUX      |-----> Q
 Q --------->| 0                 |
             +-------------------+
                    ^
                    |
                   EN
```

The equation is:

```text
Q_next = EN ? D : Q
```

So:

1. when `EN = 1`, mux selects `D`, and latch is transparent,
2. when `EN = 0`, mux selects feedback `Q`, and latch holds the old value.

This is exactly latch behavior. [[S3]](#s3)

### 2. Convert the latch into a flip-flop

A common way is to use **two level-sensitive latches in series** with opposite clock phases:

```text
        +---------+      +---------+
D ----->| Master  |----->|  Slave  |-----> Q
        | Latch   |      | Latch   |
        +---------+      +---------+
           ^                 ^
           |                 |
          CLK               CLKbar
```

or the phases can be swapped depending on positive-edge or negative-edge design.

### Why this becomes a flip-flop

1. master latch samples during one phase,
2. slave latch updates during the opposite phase,
3. overall output changes only at the transition between phases.

So the pair behaves like an edge-triggered element.

### Interview-safe answer

If they ask implementation only:

```text
Latch = 2:1 MUX + feedback
Flip-flop = two such latches in master-slave form
```

**Speak like this:**

"I can make a D latch using a 2:1 mux by connecting one mux input to D and the other to feedback from Q. The select line is enable, so `Q_next = EN ? D : Q`. Then to convert that into a flip-flop, I use two such latches in master-slave form driven by opposite clock phases. That makes the overall output update only at the clock edge."

[Back to index](./index.md)

<a id="q150"></a>
## 150. In a NAND gate, which NMOS in the pull-down network should have larger sizing?

**Written answer:**

For a NAND gate, the NMOS pull-down network is a **series stack**. The safe base rule is:

```text
all series NMOS are usually upsized compared with a single inverter NMOS
```

because a stack has higher effective resistance than one transistor. Logical-effort and CMOS design notes both reflect this stack-resistance sizing idea. [[S106]](#s106) [[S134]](#s134)

### If the question asks "which one specifically should be larger?"

If **non-uniform sizing** is allowed, the **top NMOS near the output** is often made larger, because:

1. it can see more body-effect-related weakness,
2. the internal stack node behavior makes it more critical in some worst-case transitions,
3. putting critical signals closer to the output side helps delay in stacked networks. [[S134]](#s134)

### Practical interview answer

There are two levels of answer:

#### Standard-cell style answer

All NMOS in the series stack are upsized so the overall pull-down strength is comparable to an inverter.

#### Fine-grain sizing answer

If different devices are sized differently, the **upper NMOS** in the stack is the usual candidate to make wider.

**Speak like this:**

"In a NAND gate, the NMOS pull-down devices are in series, so the whole stack is weaker than a single NMOS. Because of that, in practice all stacked NMOS are usually upsized. If the question is asking which one should be made larger among the series devices, the top NMOS near the output is the usual answer, because it tends to be more critical due to stack-node and body-effect behavior."

[Back to index](./index.md)

<a id="q151"></a>
## 151. How will you design a full adder?

**Written answer:**

A **full adder** adds three one-bit inputs:

1. `A`,
2. `B`,
3. `Cin`.

It produces:

1. `Sum`,
2. `Cout`.

A standard implementation is **two half adders plus one OR gate**. UCSD adder notes show this composition directly. [[S135]](#s135)

### Equations

```text
Sum  = A xor B xor Cin
Cout = AB + Cin(A xor B)
```

### Block construction

```text
        A -----+         +-----------+
               |-------->| Half      |--- s1 ---+
        B -----+         | Adder 1   |          |
                         +-----------+          v
                              c1             +-----------+
                                             | Half      |---- Sum
        Cin -------------------------------->| Adder 2   |
                                             +-----------+
                                                  |
                                                  c2

                         Cout = c1 OR c2
```

### Design steps

1. First half adder adds `A` and `B`.
2. Second half adder adds intermediate sum `s1` and `Cin`.
3. OR the two carry outputs.

### Verilog idea

```verilog
assign sum  = a ^ b ^ cin;
assign cout = (a & b) | (cin & (a ^ b));
```

**Speak like this:**

"I design a full adder either directly from the equations or by using two half adders and one OR gate. First I add A and B, then I add the intermediate sum with Cin, and finally I OR the two carry terms. So the outputs are `sum = A xor B xor Cin` and `cout = AB + Cin(A xor B)`."

[Back to index](./index.md)

<a id="q152"></a>
## 152. How will you design a half adder?

**Written answer:**

A **half adder** adds two one-bit inputs:

1. `A`,
2. `B`.

It produces:

1. `Sum`,
2. `Carry`.

Adder notes define the half adder as:

```text
Sum   = A xor B
Carry = A and B
```

and this is the simplest gate-level realization. [[S135]](#s135)

### Block diagram

```text
A ----+----> XOR ----> Sum
      |
B ----+

A ----+----> AND ----> Carry
      |
B ----+
```

### Truth table

| A | B | Sum | Carry |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

### Verilog idea

```verilog
assign sum   = a ^ b;
assign carry = a & b;
```

**Speak like this:**

"A half adder adds two one-bit inputs. I use an XOR gate for the sum and an AND gate for the carry. So `sum = A xor B` and `carry = A and B`."

[Back to index](./index.md)

<a id="q153"></a>
## 153. Asked about CDC and FIFO.

**Written answer:**

**CDC** means **clock domain crossing**: transferring a signal from one clock domain to another. The main problem is that asynchronous sampling can cause **metastability**. AMD clock-domain-crossing guidance says asynchronous CDC paths must use proper synchronization circuitry, and for multiple bits of data the general recommendation is an **asynchronous FIFO**. [[S132]](#s132)

### What is the CDC problem?

If signal `A` is launched in clock domain `clk1` and captured in domain `clk2`, and the clocks are unrelated, then:

1. setup/hold assumptions do not naturally hold,
2. a flip-flop can enter metastability,
3. data can be missed, duplicated, or corrupted.

### Common CDC solutions

#### 1. Single-bit level signal

Use a **2-flop synchronizer** in the destination domain.

#### 2. Pulse signal

Use pulse stretching, toggle synchronizer, or handshake.

#### 3. Multi-bit bus / data stream

Use an **asynchronous FIFO** rather than synchronizing each bit independently.

That is the practical answer because independent bit synchronization can produce an invalid bus combination. [[S132]](#s132)

### What is a FIFO?

A FIFO is **first-in, first-out** storage. Data written first is read first.

#### Synchronous FIFO

Same write clock and read clock.

#### Asynchronous FIFO

Different write clock and read clock. This is commonly used for CDC between two unrelated domains.

### Why FIFO helps in CDC

An asynchronous FIFO:

1. buffers the data,
2. decouples write and read timing,
3. allows the two sides to run at different rates,
4. safely transfers multi-bit data across domains.

### Interview-safe summary

Use:

1. 2-flop synchronizer for single-bit control,
2. handshake or toggle for pulses,
3. asynchronous FIFO for multi-bit data.

**Speak like this:**

"CDC means data is crossing between different clock domains, so metastability becomes the main concern. For a single-bit control I use a 2-flop synchronizer. For pulses I use toggle sync, pulse stretching, or handshake. For multi-bit data I prefer an asynchronous FIFO, because synchronizing each bit separately can give a wrong bus value."

[Back to index](./index.md)

<a id="q154"></a>
## 154. Basics of inverter, and what happens if PMOS and NMOS are interchanged?

**Written answer:**

A normal CMOS inverter has:

1. **PMOS on top** connected to `VDD`,
2. **NMOS on bottom** connected to `GND`,
3. both gates tied together as input,
4. drains tied together as output. [[S123]](#s123) [[S127]](#s127)

### Normal working

#### When input = 0

1. PMOS turns ON,
2. NMOS turns OFF,
3. output goes to `VDD` -> logic `1`.

#### When input = 1

1. PMOS turns OFF,
2. NMOS turns ON,
3. output goes to `GND` -> logic `0`.

That is why it acts as an inverter.

### If PMOS and NMOS are interchanged

If you mean **swap their positions**:

1. put **NMOS on top** to `VDD`,
2. put **PMOS on bottom** to `GND`,
3. keep same common gate input,

then it does **not** behave like a proper CMOS inverter.

### Why it fails

1. NMOS is good at passing strong `0` but weak `1`,
2. PMOS is good at passing strong `1` but weak `0`,
3. so the output no longer reaches strong rails cleanly,
4. noise margins become poor,
5. VTC becomes degraded,
6. static current behavior and logic robustness become poor.

### Practical result

The output may:

1. become degraded,
2. not reach full `VDD` or full `0`,
3. become unreliable as a logic inverter.

### Interview-safe summary

Normal CMOS inverter works because PMOS pulls up well and NMOS pulls down well. If you swap them, the gate loses proper rail-to-rail logic behavior.

**Speak like this:**

"A CMOS inverter has PMOS on top and NMOS on bottom. When input is low, PMOS pulls output high. When input is high, NMOS pulls output low. If I interchange them physically, it stops being a proper CMOS inverter, because NMOS passes weak 1 and PMOS passes weak 0. So the output becomes degraded, the noise margin becomes poor, and the logic is no longer robust."

[Back to index](./index.md)

<a id="q155"></a>
## 155. Difference between simulation and synthesis.

**Written answer:**

**Simulation** checks behavior over time using the HDL semantics. **Synthesis** converts the synthesizable subset of HDL into hardware gates/registers/netlists. AMD synthesis documentation explicitly notes that some timing controls such as delays are useful for simulation but ignored for synthesis. [[S133]](#s133)

### Main difference

| Item | Simulation | Synthesis |
|---|---|---|
| Goal | Check behavior | Build hardware implementation |
| Input | HDL/testbench | Synthesizable HDL + constraints |
| Output | Waveforms / logs / coverage | Gate-level netlist / mapped hardware |
| Time controls | Used by simulator | Many are unsupported or ignored |
| Testbench code | Allowed | Not synthesized |
| Main question | "Does it behave correctly?" | "What hardware does this describe?" |

### Simulation

Simulation is used to:

1. verify logic behavior,
2. debug corner cases,
3. inspect waveforms,
4. validate testbench scenarios.

Simulation understands many constructs that are not hardware by themselves, such as:

1. `#delay`,
2. `$display`,
3. `$monitor`,
4. file I/O,
5. stimulus-only code.

### Synthesis

Synthesis is used to:

1. infer combinational logic,
2. infer flops/latches/RAMs,
3. optimize logic,
4. map RTL into target technology.

It only accepts the **synthesizable subset** of the language.

### Important interview point

A design can simulate fine and still synthesize incorrectly if the RTL uses coding styles that create simulation-synthesis mismatch.

**Speak like this:**

"Simulation checks behavior in time using the HDL semantics and gives me waveforms and debug visibility. Synthesis takes the synthesizable part of the RTL and converts it into gates, flops, and a netlist for FPGA or ASIC. So simulation tells me whether the code behaves as expected, while synthesis tells me what hardware the code actually becomes."

[Back to index](./index.md)

<a id="q156"></a>
## 156. How do you design a circuit with input frequency `f` and output frequency `f/2`?

**Written answer:**

The standard way is to use a **toggle flip-flop**. A D flip-flop can be made to toggle by feeding back the inverted output:

```text
D = Qbar
```

or equivalently:

```text
D = ~Q
```

With one toggle on each active clock edge, the output frequency becomes half the input clock frequency. This follows directly from edge-triggered sequential logic behavior. [[S2]](#s2) [[S113]](#s113)

### Diagram

```text
          +-----------+
clk ----->|   DFF     |-----> Q = fout
          |       Q   |
          +-----------+
                ^
                |
               ~Q
```

### Why output is `f/2`

If the input clock is:

```text
0 1 0 1 0 1 ...
```

the flip-flop output toggles only once per clock edge, so one complete output cycle needs two input clock edges.

Therefore:

```text
fout = fin / 2
```

### Verilog code

```verilog
module div_by_2 (
    input  wire clk,
    input  wire rst,
    output reg  q
);

always @(posedge clk or posedge rst) begin
    if (rst)
        q <= 1'b0;
    else
        q <= ~q;
end

endmodule
```

**Speak like this:**

"To get `f/2`, I use a toggle flip-flop. In a D flip-flop, I connect `D = ~Q`, so the output toggles on every clock edge. Since one full output cycle takes two clock edges, the output frequency becomes half of the input frequency."

[Back to index](./index.md)

<a id="q157"></a>
## 157. What are digital and analog signals?

**Written answer:**

A **signal** is a time-varying quantity that carries information. A standard distinction is:

1. **analog signal**: varies continuously,
2. **digital signal**: uses discrete levels. Stanford computing notes describe analog as a continuously varying signal and digital as a representation using discrete values. [[S154]](#s154)

### Analog signal

An analog signal can take a continuous range of values over time.

Examples:

1. microphone voltage,
2. temperature sensor output,
3. audio waveform.

### Digital signal

A digital signal uses discrete levels, usually two logic levels:

```text
0 and 1
```

Examples:

1. logic waveforms in digital circuits,
2. processor control signals,
3. memory read/write signals.

### Main differences

| Feature | Analog | Digital |
|---|---|---|
| Value range | Continuous | Discrete |
| Typical representation | Smooth waveform | Logic levels / pulses |
| Noise handling | More sensitive to small analog noise | More robust due to noise margins |
| Use | Sensors, RF, audio | Processors, memories, digital logic |

**Speak like this:**

"An analog signal changes continuously and can take many values, like audio or sensor voltage. A digital signal uses discrete logic levels, usually 0 and 1. So analog is continuous-valued, while digital is discrete-valued."

[Back to index](./index.md)

<a id="q158"></a>
## 158. 8x1 MUX using 2x1 MUX: how many are required?

**Written answer:**

To build an `8:1` MUX using only `2:1` MUXes, we use a tree structure.

### Level-wise construction

```text
Level 1: 8 inputs  -> 4 muxes
Level 2: 4 outputs -> 2 muxes
Level 3: 2 outputs -> 1 mux
```

So total number required is:

```text
4 + 2 + 1 = 7
```

### General rule

For an `N:1` mux built from `2:1` muxes, if the structure is a complete binary tree:

```text
Number of 2:1 muxes = N - 1
```

So for `8:1`:

```text
8 - 1 = 7
```

**Speak like this:**

"An 8-to-1 MUX needs 7 two-to-one MUXes. I build it as a three-level tree: four muxes in the first stage, two in the second stage, and one in the final stage."

[Back to index](./index.md)

<a id="q159"></a>
## 159. 56x1 MUX using 2x1 MUX: how many are required?

**Written answer:**

If the question means an **exact** `56:1` multiplexer built from `2:1` muxes, the count is:

```text
56 - 1 = 55
```

because every `2:1` mux reduces the number of signals by one.

### Important interview note

`56` is **not** a power of two. So there are two possible interpretations:

#### 1. Exact 56-input selection

Need:

```text
55 muxes
```

#### 2. Build it as a standard power-of-two tree with 6 select bits

Then you really build a `64:1` structure and leave 8 inputs unused:

```text
64 - 1 = 63 muxes
```

### Best interview answer

Say both:

```text
Exact 56:1 -> 55 muxes
64:1 tree with 8 unused inputs -> 63 muxes
```

**Speak like this:**

"If you mean an exact 56-to-1 selection using only 2-to-1 muxes, the count is 55, because an N-to-1 mux needs N-1 two-to-one muxes. But if the interviewer wants a clean 6-select-line power-of-two tree, then I would build a 64-to-1 structure and leave 8 inputs unused, which takes 63 muxes."

[Back to index](./index.md)

<a id="q160"></a>
## 160. Two blocks A and B both transfer data to each other. Should we use `wire`, `reg`, or something else?

**Written answer:**

In Verilog, the right answer depends on **what the signal represents**.

### Basic rule

1. Use a **net** such as `wire` for **connections between modules**.
2. Use `reg` in Verilog for a variable assigned inside an `always` or `initial` block.

Berkeley Verilog notes summarize this well: `wire` is used to connect hardware elements, while `reg` is the target of procedural assignment and is **not necessarily** a hardware register. [[S155]](#s155)

### If block A and block B both communicate

#### Case 1: Separate transmit and receive paths

This is the preferred clean design:

```text
A_to_B  -> wire
B_to_A  -> wire
```

Each module drives one direction and receives the other.

#### Case 2: Shared bidirectional bus

Then use:

1. `inout` port,
2. a `wire`/`tri` style shared net,
3. tri-state control so only one side drives at a time. [[S28]](#s28) [[S155]](#s155)

Example idea:

```verilog
assign bus = a_drive_en ? a_data : 8'bz;
assign bus = b_drive_en ? b_data : 8'bz;
```

But only one driver may be enabled at a time.

### Important practical note

Inside FPGA/ASIC RTL, internal tri-state buses are often avoided and replaced by:

1. muxes,
2. arbitration logic,
3. separate unidirectional channels.

So for most synthesizable designs, the safer answer is:

```text
use wires for interconnect, and use reg only for procedural assignments
```

**Speak like this:**

"Between modules, I use `wire` or another net type for the connection. In Verilog, `reg` is used when a signal is assigned inside an `always` block; it does not automatically mean a physical register. If both blocks must share one bidirectional bus, then I can use an `inout` with tri-state control, but in most RTL designs I prefer separate directional wires or a mux-based scheme because internal tri-states are often avoided."

[Back to index](./index.md)

<a id="q161"></a>
## 161. Output for various input combinations of JK and SR flip-flop.

**Written answer:**

### SR flip-flop / SR latch truth table

For the classic SR form:

| S | R | Q(next) | Meaning |
|---|---|---|---|
| 0 | 0 | Q(prev) | Hold |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | Invalid / forbidden | Not allowed |

Digital logic notes show this standard SR behavior. [[S156]](#s156)

### JK flip-flop truth table

JK removes the forbidden SR case by using toggle behavior:

| J | K | Q(next) | Meaning |
|---|---|---|---|
| 0 | 0 | Q(prev) | Hold |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | Qbar(prev) | Toggle |

JK flip-flop notes define the `11` input case as complement/toggle. [[S156]](#s156)

### Main difference

1. SR has an invalid `S=1, R=1` condition.
2. JK replaces that condition with toggle.

**Speak like this:**

"For SR flip-flop, 00 means hold, 01 reset, 10 set, and 11 is invalid. For JK flip-flop, 00 hold, 01 reset, 10 set, and 11 toggle. So the main advantage of JK over SR is that the `11` case is defined instead of forbidden."

[Back to index](./index.md)

<a id="q162"></a>
## 162. Why is RTL coding done?

**Written answer:**

RTL coding is done because it gives a practical abstraction for digital hardware design. At RTL, we describe:

1. how data moves between registers,
2. what combinational logic operates on that data,
3. what happens on each clock or control event.

This abstraction is high enough for design productivity and verification, but still close enough to hardware that synthesis tools can convert it into gates. Synopsys synthesis material treats RTL as the source level that is transformed into implementation logic. [[S136]](#s136)

### Why RTL is useful

1. it is easier to design and modify than gate-level circuits,
2. it is synthesizable into real hardware,
3. it supports simulation and verification,
4. it is the standard handoff point from front-end design into synthesis and implementation.

### Simple idea

Instead of drawing thousands of gates directly, we describe hardware behavior at the register-transfer level and let synthesis map it to standard cells or FPGA resources.

**Speak like this:**

"RTL coding is done because it is the practical level where I can describe how data moves between registers and what logic operates on it, without writing the design directly at the gate level. It is abstract enough for design and verification, but still synthesizable into real hardware."

[Back to index](./index.md)

<a id="q163"></a>
## 163. Explain how you would design an EVM machine.

**Written answer:**

Assuming **EVM** means **Electronic Voting Machine**, the clean design approach is to treat it as a **finite-state machine** with controlled vote entry, lockout, and result display. Research on electronic voting machine design describes the voting machine naturally as a finite-state transducer with well-defined states and transitions. [[S157]](#s157)

### High-level blocks

A simple EVM design can have:

1. input buttons for candidates,
2. voter enable / ballot enable,
3. control FSM,
4. candidate vote counters,
5. result display mode,
6. clear/reset/admin control.

### Example states

```text
IDLE
-> READY_FOR_VOTE
-> VOTE_CAPTURED
-> LOCKED
-> RESULT_MODE
```

### Operation idea

1. In `IDLE`, machine waits for election enable.
2. In `READY_FOR_VOTE`, one voter is allowed to cast one vote.
3. When a candidate button is pressed, the corresponding counter increments.
4. Machine goes to `LOCKED` so the same voter cannot vote again.
5. The next voter or control unit re-enables the machine.
6. In `RESULT_MODE`, counters are displayed instead of accepting votes.

### Design requirements

1. only one valid vote per enable cycle,
2. invalid simultaneous button presses should be ignored or flagged,
3. counters must hold values safely,
4. result mode must not change counts,
5. reset/clear must be controlled.

### Hardware view

This is mostly:

1. FSM for control,
2. counters/registers for vote counts,
3. combinational decode for candidate selection and result display.

**Speak like this:**

"I would design an electronic voting machine as an FSM. I would have states like idle, ready-for-vote, vote-captured, locked, and result mode. Candidate buttons feed a controlled vote-capture block, and each valid vote increments only one candidate counter. After one vote, the machine locks until the next voter is enabled. Results are shown in a separate result mode so counting and displaying are controlled cleanly."

[Back to index](./index.md)

<a id="q164"></a>
## 164. Write the program for an EVM machine.

**Written answer:**

Below is a simple interview-style **Verilog** example of an electronic voting machine with four candidates. It allows one vote per enable cycle and includes a result mode.

```verilog
module evm_machine (
    input  wire       clk,
    input  wire       rst,
    input  wire       ballot_en,
    input  wire       next_voter,
    input  wire       result_mode,
    input  wire [3:0] vote_btn,      // one-hot: 0001,0010,0100,1000
    output reg  [7:0] count0,
    output reg  [7:0] count1,
    output reg  [7:0] count2,
    output reg  [7:0] count3,
    output reg        vote_done
);

reg locked;

always @(posedge clk or posedge rst) begin
    if (rst) begin
        count0    <= 8'd0;
        count1    <= 8'd0;
        count2    <= 8'd0;
        count3    <= 8'd0;
        locked    <= 1'b0;
        vote_done <= 1'b0;
    end else begin
        if (next_voter) begin
            locked    <= 1'b0;
            vote_done <= 1'b0;
        end else if (ballot_en && !locked && !result_mode) begin
            case (vote_btn)
                4'b0001: begin count0 <= count0 + 1'b1; locked <= 1'b1; vote_done <= 1'b1; end
                4'b0010: begin count1 <= count1 + 1'b1; locked <= 1'b1; vote_done <= 1'b1; end
                4'b0100: begin count2 <= count2 + 1'b1; locked <= 1'b1; vote_done <= 1'b1; end
                4'b1000: begin count3 <= count3 + 1'b1; locked <= 1'b1; vote_done <= 1'b1; end
                default: begin
                    locked    <= locked;
                    vote_done <= 1'b0;
                end
            endcase
        end
    end
end

endmodule
```

### Notes

1. `ballot_en` allows a vote.
2. `locked` prevents multiple votes by the same voter.
3. `next_voter` clears the lock for the next vote.
4. `result_mode` blocks further voting.
5. `vote_btn` is treated as one-hot candidate selection.

**Speak like this:**

"I write the EVM as a small synchronous control block with candidate counters. Each valid one-hot candidate input increments one counter, and then a lock bit prevents another vote until `next_voter` comes. I also keep a separate `result_mode` so counting and displaying stay separated."

[Back to index](./index.md)

<a id="q165"></a>
## 165. Write Verilog code for D flip-flop with active-low asynchronous reset.

**Written answer:**

For an active-low asynchronous reset DFF:

1. reset acts immediately,
2. reset is active when it is `0`,
3. otherwise data is captured on the clock edge.

### Verilog code

```verilog
module dff_async_low_reset (
    input  wire clk,
    input  wire rst_n,
    input  wire d,
    output reg  q
);

always @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        q <= 1'b0;
    else
        q <= d;
end

endmodule
```

### Why `negedge rst_n` is used

Because reset is active-low, the asynchronous reset event happens when `rst_n` falls from `1` to `0`.

**Speak like this:**

"For an active-low asynchronous reset D flip-flop, I write `always @(posedge clk or negedge rst_n)`. If `rst_n` becomes 0, the output resets immediately, otherwise the flip-flop captures `d` on the rising clock edge."

[Back to index](./index.md)

<a id="q166"></a>
## 166. How do you design a simple inverter and buffer using XOR gate?

**Written answer:**

The XOR identity is:

```text
A xor 0 = A
A xor 1 = Abar
```

So an XOR gate can be used as both a buffer and an inverter. This standard XOR property is a common logic-design trick. [[S40]](#s40)

### As a buffer

Tie one XOR input to `0`:

```text
Y = A xor 0 = A
```

### As an inverter

Tie one XOR input to `1`:

```text
Y = A xor 1 = Abar
```

### Diagram idea

```text
Buffer:    Y = A xor 0
Inverter:  Y = A xor 1
```

**Speak like this:**

"Using XOR, I can make a buffer by fixing one input to 0, because `A xor 0 = A`. I can make an inverter by fixing one input to 1, because `A xor 1 = Abar`."

[Back to index](./index.md)

<a id="q167"></a>
## 167. What is floorplanning? What is routing?

**Written answer:**

These are two major steps in physical design.

### Floorplanning

**Floorplanning** is the step where we decide the rough physical organization of the chip before standard-cell placement. Georgia Tech floorplanning notes describe it as arranging modules/blocks on the layout surface. [[S158]](#s158)

In floorplanning, we usually decide:

1. die/core size,
2. macro placement,
3. IO placement,
4. power planning,
5. keep-out regions and blockages.

So floorplanning is about the **big physical structure** of the chip.

### Routing

**Routing** is the step where we create the actual interconnections between placed cells/macros using metal layers and vias. Utah VLSI routing notes discuss routing as the process of connecting the layout using assigned metal directions/layers. [[S159]](#s159)

Routing usually has:

1. global routing,
2. detailed routing.

### Simple difference

| Step | Meaning |
|---|---|
| Floorplanning | Decide where major blocks go |
| Routing | Connect them physically with wires and vias |

**Speak like this:**

"Floorplanning means deciding the rough physical organization of the chip, like die size, macro locations, IO locations, and power structure. Routing comes later, where the actual nets are connected using metal layers and vias. So floorplanning decides where things go, and routing connects them."

[Back to index](./index.md)

<a id="q184"></a>
## 184. What is a stuck-at fault?

**Written answer:**

A **stuck-at fault** is a digital fault model in which a signal line is assumed to be permanently stuck at logic `0` or logic `1`, regardless of what the circuit is supposed to produce. Stanford's test notes emphasize that stuck-at is a **logic fault model**, not a direct physical-defect model. [[S117]](#s117)

### Two basic types

1. **Stuck-at-0 (SA0):** the node always behaves as `0`.
2. **Stuck-at-1 (SA1):** the node always behaves as `1`.

### Why this model is used

Real chips fail because of opens, shorts, bridging defects, transistor failures, and manufacturing problems. Instead of modeling every physical defect exactly, ATPG and fault simulation often use the simpler stuck-at model because:

1. it is easy to analyze,
2. it works well for combinational and scan-based testing,
3. it gives practical fault coverage metrics.

### How a stuck-at fault is detected

To detect a stuck-at fault, the test pattern must do two things:

1. **Activate** the fault by forcing the good circuit to the opposite value.
2. **Propagate** the fault effect to an observable output.

Example:

If a node has a stuck-at-0 fault, then the test should try to make that node `1` in the good circuit. After that, the difference between good and faulty behavior must be propagated to an output pin or scan flip-flop.

### Important note

Stuck-at fault is an **abstract test model**. It does not literally mean the node is physically shorted to ground or VDD. It is a logic-level way to represent many possible defects.

**Speak like this:**

"A stuck-at fault means a signal line is modeled as permanently fixed at 0 or 1. So we have stuck-at-0 and stuck-at-1 faults. It is a logic fault model used in ATPG and fault simulation because it is simple and practical. To detect it, I must activate the fault and then propagate its effect to an observable output."

[Back to index](./index.md)

<a id="q185"></a>
## 185. Structure and array in C.

**Written answer:**

In C, an **array** stores multiple elements of the **same type** in contiguous memory locations, while a **structure (`struct`)** groups related data items that can be of **different types** under one name. Brown's systems notes and C tutorial material both explain arrays and structures as two different composite data mechanisms in C. [[S118]](#s118) [[S119]](#s119)

### Array

An array is a collection of elements of the same type:

```c
int a[5] = {10, 20, 30, 40, 50};
```

Properties:

1. all elements have the same data type,
2. elements are stored contiguously,
3. access is by index, like `a[0]`, `a[1]`.

### Structure

A structure groups different fields into one user-defined type:

```c
struct Student {
    int roll;
    char name[20];
    float cgpa;
};
```

Example:

```c
struct Student s1 = {1, "Asha", 8.7};
```

Access members using dot operator:

```c
s1.roll
s1.name
s1.cgpa
```

### Difference between array and structure

| Feature | Array | Structure |
|---|---|---|
| Data type of members | Same type only | Can contain different types |
| Access method | Index, like `a[i]` | Member name, like `s.roll` |
| Purpose | Store a sequence of similar values | Group related heterogeneous data |
| Memory layout | Contiguous equal-type elements | Fields stored in order, with possible padding |
| Assignment in C | Arrays are not directly assignable as whole objects | Structures can be assigned as whole objects |

### Small example

```c
int marks[3] = {80, 75, 90};

struct Student {
    int roll;
    char grade;
};

struct Student x = {10, 'A'};
```

Here `marks` is an array, but `x` is a structure.

**Speak like this:**

"In C, an array stores multiple values of the same type in contiguous memory, and I access them using indexes. A structure is a user-defined type that groups related fields of possibly different types, and I access them using member names. So arrays are for homogeneous data, while structures are for heterogeneous grouped data."

[Back to index](./index.md)

<a id="q186"></a>
## 186. 8085 and 8086 architecture.

**Written answer:**

The **8085** is an **8-bit microprocessor**, while the **8086** is a **16-bit microprocessor**. The 8086 also introduced a more advanced internal organization with separate execution and bus-interface activities. Intel's 8086 family manual and 8085 architecture notes describe these differences clearly. [[S120]](#s120) [[S121]](#s121)

### 8085 architecture

Main points of 8085:

1. **8-bit CPU**
2. **16-bit address bus** -> can address `2^16 = 64 KB`
3. **8-bit data bus**
4. Main blocks include:
   - Accumulator
   - ALU
   - General-purpose registers `B, C, D, E, H, L`
   - Program Counter
   - Stack Pointer
   - Flag register
   - Instruction register and decoder
   - Timing and control unit
   - Interrupt control
   - Serial I/O control

The 8085 is simpler and more accumulator-oriented.

### 8086 architecture

Main points of 8086:

1. **16-bit CPU**
2. **20-bit address bus** -> can address `2^20 = 1 MB`
3. **16-bit data bus**
4. Divided into two major units:
   - **Bus Interface Unit (BIU)**
   - **Execution Unit (EU)**

#### Bus Interface Unit (BIU)

The BIU handles:

1. instruction fetch,
2. address generation,
3. memory and I/O bus operations,
4. instruction prefetch queue.

The 8086 has a **6-byte instruction queue**, which allows simple pipelining.

#### Execution Unit (EU)

The EU contains:

1. ALU,
2. general-purpose registers `AX, BX, CX, DX`,
3. pointer/index registers `SP, BP, SI, DI`,
4. flag register,
5. instruction decoding and execution logic.

### Segmentation in 8086

8086 uses segmented memory with:

1. `CS` - Code Segment
2. `DS` - Data Segment
3. `SS` - Stack Segment
4. `ES` - Extra Segment

Physical address is formed as:

```text
Physical address = Segment x 16 + Offset
```

### Quick comparison

| Feature | 8085 | 8086 |
|---|---|---|
| Word length | 8-bit | 16-bit |
| Address bus | 16-bit | 20-bit |
| Data bus | 8-bit | 16-bit |
| Max memory | 64 KB | 1 MB |
| Internal organization | Simpler single-unit style | BIU + EU |
| Segmentation | No | Yes |
| Prefetch queue | No | Yes, 6 bytes |

**Speak like this:**

"8085 is an 8-bit microprocessor with 16-bit addressing, so it can access 64 KB memory. Its architecture includes accumulator, ALU, general-purpose registers, PC, SP, flags, timing/control, interrupts, and serial I/O. 8086 is a 16-bit microprocessor with 20-bit addressing, so it can access 1 MB memory. Its architecture is more advanced because it has a Bus Interface Unit and an Execution Unit, plus segmented memory and a 6-byte instruction queue."

[Back to index](./index.md)

<a id="q187"></a>
## 187. Edge triggering and level triggering.

**Written answer:**

These terms describe **when** a sequential element responds to a control signal.

- **Edge triggering** means the circuit responds only at the instant of a signal transition.
- **Level triggering** means the circuit responds during the entire time the control signal stays at an active level.

Digital logic notes explain that level-sensitive devices respond while the control level is active, while edge-triggered devices respond at the rising or falling edge. [[S61]](#s61)

### Edge triggering

In edge triggering, output changes only on:

1. **positive edge** (`0 -> 1`), or
2. **negative edge** (`1 -> 0`)

Example:

```verilog
always @(posedge clk)
    q <= d;
```

This is an edge-triggered D flip-flop style.

### Level triggering

In level triggering, the device remains sensitive while the control input stays active.

Example:

```verilog
always @(*) begin
    if (en)
        q = d;
end
```

This is latch behavior. While `en = 1`, `q` follows `d`. When `en = 0`, it holds the previous value.

### Main difference

| Feature | Edge triggering | Level triggering |
|---|---|---|
| Response time | Only at transition instant | During active HIGH or LOW interval |
| Typical element | Flip-flop | Latch |
| Sensitivity | Less transparent | Transparent during active level |
| Risk | Safer for synchronous pipelines | Can introduce transparency/time-borrowing issues if misused |

### Example intuition

- Flip-flop: samples once at the clock edge.
- Latch: stays open while enable is active.

**Speak like this:**

"Edge triggering means the circuit responds only at the rising or falling edge of the control signal. Level triggering means the circuit responds for the whole time the control signal is active. So flip-flops are typically edge-triggered, while latches are level-sensitive."

[Back to index](./index.md)

<a id="q190"></a>
## 190. ASIC design flow: explain RTL to GDSII.

**Written answer:**

The **ASIC design flow** or **RTL-to-GDSII flow** is the end-to-end implementation path that takes a verified RTL design and turns it into a manufacturable physical layout database. Cadence training and Synopsys implementation material describe this flow as spanning synthesis, physical design, timing/signoff, and final GDSII generation. [[S73]](#s73) [[S136]](#s136)

### High-level view

```text
Specification
-> RTL design
-> Functional verification
-> Synthesis
-> DFT / equivalence checks
-> Floorplan / power plan
-> Placement
-> CTS
-> Routing
-> Extraction / STA / SI / EMIR / physical verification
-> ECO closure
-> GDSII
```

### Step-by-step flow

#### 1. Specification and architecture

Define:

1. functionality,
2. clock targets,
3. power goals,
4. area goals,
5. interfaces and protocols.

This is where the micro-architecture is chosen.

#### 2. RTL design

Write the design in HDL such as Verilog/SystemVerilog/VHDL at register-transfer level.

#### 3. Functional verification

Verify that the RTL matches the specification using:

1. simulation,
2. assertions,
3. formal checks,
4. coverage.

#### 4. Logic synthesis

Convert RTL into a **gate-level netlist** using a target cell library and constraints.

Main output:

1. mapped gate-level netlist,
2. area/timing/power reports.

#### 5. DFT insertion and equivalence

Insert scan and other test structures if needed, then check equivalence between RTL and synthesized netlist.

#### 6. Floorplanning and power planning

Decide:

1. die/core size,
2. macro placement,
3. IO placement,
4. power grid,
5. placement blockages.

#### 7. Placement

Place standard cells in legal locations while optimizing timing, congestion, and area.

#### 8. CTS

Build the clock network so clocks reach sequential elements with controlled skew, latency, and transition.

#### 9. Routing

Connect all nets with metal wires and vias while meeting DRC and timing goals.

#### 10. Parasitic extraction and signoff analysis

Extract RC parasitics and run:

1. STA,
2. signal integrity / crosstalk analysis,
3. IR-drop / EM checks,
4. noise and reliability checks.

#### 11. Physical verification

Run signoff checks such as:

1. DRC,
2. LVS,
3. antenna checks,
4. density/fill related checks depending on process requirements. [[S97]](#s97) [[S98]](#s98)

#### 12. ECO closure and GDSII generation

Fix any remaining timing or physical errors, then generate **GDSII**, the layout database used for mask preparation and fabrication.

### Front-end vs back-end

#### Front-end

1. specification,
2. RTL,
3. verification,
4. synthesis.

#### Back-end

1. floorplan,
2. placement,
3. CTS,
4. routing,
5. signoff,
6. GDSII.

**Speak like this:**

"ASIC RTL-to-GDSII flow starts from specification and RTL design, then moves through functional verification and logic synthesis to generate a gate-level netlist. After that comes physical design: floorplan, placement, CTS, and routing. Finally we do extraction, STA, IR/EM, crosstalk, DRC, LVS, and ECO closure, and then generate GDSII for fabrication. So front end gives me a logically correct netlist, and back end turns it into tapeout-ready layout."

[Back to index](./index.md)

<a id="q191"></a>
## 191. What is synthesis (logic synthesis), and what are its inputs?

**Written answer:**

**Logic synthesis** is the automated process of converting an RTL description into a **gate-level netlist** built from cells in a target standard-cell library. Synopsys describes synthesis as transforming high-level hardware descriptions into lower-level representations suitable for implementation, and explicitly notes that logic synthesis maps RTL into logic elements taken from cell libraries under design constraints. [[S136]](#s136) [[S137]](#s137)

### What synthesis does

Starting from RTL, synthesis performs:

1. elaboration of the design hierarchy,
2. inference of combinational and sequential logic,
3. logic optimization,
4. technology mapping to the target library,
5. report generation for timing, area, and power.

### Core inputs of synthesis

#### 1. RTL description

Usually files like:

```text
.v
.sv
.vhd
```

This tells the tool what the design is supposed to do.

#### 2. Design constraints

Usually an **SDC** file.

This tells the tool the design intent, such as:

1. clock definitions,
2. input/output delays,
3. timing exceptions,
4. uncertainty,
5. area/power targets in some flows.

Synopsys notes that SDC defines alignment between clocks and carries timing intent through implementation and signoff. [[S137]](#s137)

#### 3. Cell library

Usually `.lib` / Liberty timing models for the standard-cell library.

This tells the tool what cells are available and includes data such as:

1. logical function,
2. timing arcs,
3. transition and capacitance data,
4. power data,
5. setup/hold and other sequential constraints.

Synopsys library-characterization material states that Liberty is the standard ASCII format used by synthesis and place-and-route tools for characterized cell data. [[S138]](#s138)

### Optional but common additional inputs

Depending on the flow, synthesis may also use:

1. memory/IP black-box models,
2. wire-load or physical data,
3. UPF/CPF for power intent,
4. link libraries for hard macros and IO cells,
5. floorplan hints in physically-aware flows.

### Main outputs

1. gate-level netlist,
2. timing reports,
3. area reports,
4. power reports,
5. constraint and optimization logs.

### Interview-safe summary

If they ask only the core answer:

```text
Inputs = RTL + SDC + standard-cell library
Output = gate-level netlist
```

**Speak like this:**

"Synthesis means converting RTL into a gate-level netlist using cells from the target standard-cell library. The three main inputs are the RTL code, the SDC constraints, and the cell library in Liberty format. RTL tells the tool the function, SDC tells it the timing intent, and the library tells it which gates and flops exist and what their timing and power characteristics are."

[Back to index](./index.md)

<a id="q199"></a>
## 199. What do you mean by latch-up, EM/IR, crosstalk, and antenna effects? How do you reduce them?

**Written answer:**

These are all **physical design and reliability issues** that can break functionality, timing, yield, or long-term reliability.

### 1. Latch-up

**Latch-up** is an unwanted low-impedance path between `VDD` and `GND` caused by parasitic device action in CMOS. TI describes latch-up as a condition in which a parasitic SCR structure turns on and can lead to excessive current. [[S139]](#s139)

#### Why it happens

1. substrate/well voltage disturbance,
2. current injection,
3. poor guard/tap strategy,
4. ESD or transient stress.

#### How to reduce latch-up

1. add sufficient well and substrate taps,
2. use guard rings,
3. maintain proper spacing,
4. control injection currents,
5. follow foundry latch-up rules.

### 2. EM and IR

#### Electromigration (EM)

EM is the movement of metal atoms due to high current density in interconnect. Synopsys explains that this can create vacancies and deposits, leading to opens or shorts over time. [[S140]](#s140)

#### IR drop

IR drop is the voltage drop on the power network caused by resistance and current flow. Siemens notes EM and IR drop are both critical to IC performance and reliability. [[S141]](#s141)

#### How to reduce EM/IR

1. widen power/clock/signal lines where needed,
2. improve power grid strength,
3. add more vias / via arrays,
4. reduce current density hot spots,
5. add decap cells,
6. improve cell spreading and power distribution,
7. move or resize high-current drivers if needed.

### 3. Crosstalk

**Crosstalk** is unwanted coupling from one net to another. The switching net is the **aggressor**, and the disturbed net is the **victim**. Siemens signal-integrity material explains that noise coupled onto a victim net propagates because of nearby aggressors, and the closest aggressors contribute the most. [[S142]](#s142)

#### Problems caused by crosstalk

1. glitch on victim net,
2. delay shift,
3. setup/hold impact,
4. functional failure on sensitive nets.

#### How to reduce crosstalk

1. increase spacing between parallel nets,
2. shorten parallel run length,
3. insert shielding nets,
4. route on different layers when possible,
5. reduce aggressor slew or victim sensitivity,
6. buffer / resize strategically.

### 4. Antenna effect

The **antenna effect** is plasma-induced gate damage during fabrication when long floating metal connected to a MOS gate accumulates charge. Siemens and Cadence both describe it as plasma-induced damage in gate oxide during manufacturing. [[S143]](#s143) [[S144]](#s144)

#### How to reduce antenna effect

1. follow antenna design rules,
2. insert antenna diodes,
3. use jumper / metal hopping,
4. break long routes,
5. connect diffusion earlier in the route,
6. run antenna DRC and fix violations.

### Interview-safe summary

| Issue | Basic idea | Main fix idea |
|---|---|---|
| Latch-up | Parasitic SCR creates VDD-to-GND path | taps, guard rings, spacing |
| EM | Metal damage from high current density | wider wires, more vias, lower current density |
| IR drop | Voltage drop on power grid | stronger PG network, decaps, better distribution |
| Crosstalk | Noise coupling from aggressor to victim | spacing, shielding, routing control |
| Antenna | Plasma-charge damage to MOS gate during fab | diodes, jumpers, antenna-rule fixes |

**Speak like this:**

"Latch-up is a parasitic SCR turn-on in CMOS that can create a VDD-to-GND current path, so I reduce it with taps, guard rings, and spacing. EM is metal damage due to high current density, and IR drop is voltage drop on the power grid, so I fix them with stronger power routing, wider wires, more vias, and decaps. Crosstalk is coupling from an aggressor net onto a victim net, so I reduce it with spacing, shielding, and routing control. Antenna effect is plasma-induced gate damage during fabrication, so I fix it with antenna diodes, jumpers, metal hopping, and antenna-rule cleanup."

[Back to index](./index.md)

<a id="q204"></a>
## 204. What is CTS, how does the tool perform CTS, and what are the inputs of CTS?

**Written answer:**

**CTS** stands for **Clock Tree Synthesis**. It is the physical-design step that builds the clock distribution network from the clock source to all sequential sinks while controlling skew, latency, slew/transition, and clock quality. Synopsys physical-design material defines CTS as designing the clock distribution network so timing signals reach the chip reliably, and Cadence CCOpt training notes that CTS uses generated constraints and customizable clock-tree properties. [[S145]](#s145) [[S146]](#s146)

### Goal of CTS

The main CTS goal is:

```text
deliver clock to all sinks with acceptable
skew + latency + transition + power
```

It is not just "connect the clock." It is "connect the clock in a balanced and timing-safe way."

### How the tool performs CTS

At a high level, the tool:

1. reads the placed design and clock constraints,
2. identifies clock roots and clock sink pins,
3. selects allowed clock buffers / inverters,
4. builds a clock tree topology,
5. inserts and sizes clock cells,
6. balances the tree to meet skew and latency goals,
7. assigns routing rules for clock nets,
8. optimizes transition, capacitance, and sometimes useful skew,
9. propagates clocks and rechecks timing.

In modern flows, CTS is usually integrated with timing optimization rather than treated as a completely isolated step.

### Main inputs of CTS

#### 1. Placed netlist / placed design database

CTS needs physical locations of:

1. clock source,
2. flops/latches,
3. macros,
4. blockages.

#### 2. Clock definitions from SDC

This includes:

1. primary clocks,
2. generated clocks,
3. uncertainty,
4. exceptions relevant to clock handling.

#### 3. Target clock quality numbers

Typical targets include:

1. clock transition (slew),
2. latency / insertion delay,
3. skew,
4. max capacitance / fanout in some flows.

#### 4. Allowed CTS cells

The tool needs the list of:

1. clock buffers,
2. clock inverters,
3. sometimes clock-gating-aware or special clock cells.

#### 5. Route types / NDR

**NDR** means **non-default rule**. It is commonly used on clock nets to improve clock quality, for example with:

1. wider metal,
2. larger spacing,
3. special via usage.

#### 6. Stop pins / ignore pins / exclusions

CTS needs to know where to:

1. stop propagation,
2. ignore certain pins,
3. avoid blocked regions or forbidden cells.

Cadence CCOpt training explicitly mentions clock constraints from SDC, CTS cells, route types, stop and ignore pins, and source latency settings as CTS setup items. [[S146]](#s146)

### Meaning of the common CTS terms

#### Clock transition

Rise/fall time of the clock edge at sinks. Smaller transition generally helps clock quality.

#### Clock latency

Delay from clock source to sink.

#### Clock skew

Difference in clock arrival time between sinks. [[S122]](#s122)

#### Clock buffers / inverters

Cells inserted by CTS to drive fanout and shape the clock tree.

#### NDR

Special routing rules used on clocks for better reliability and signal quality.

### Output of CTS

1. clock tree inserted into the design,
2. propagated clocks,
3. updated skew/latency/transition reports,
4. post-CTS timing results.

**Speak like this:**

"CTS means Clock Tree Synthesis. The tool takes the placed design, reads the clock constraints, identifies all clock sinks, and then inserts clock buffers or inverters to build a balanced clock tree. The main inputs are the placed netlist, SDC clock definitions, skew and latency targets, transition targets, allowed CTS cells, and route rules like NDR. The goal is to deliver the clock to all sequential elements with controlled skew, latency, and slew."

[Back to index](./index.md)

<a id="q228"></a>
## 228. We want the clock to reach every flop at the same time. Is that practically possible? What measures do we take?

**Written answer:**

In practice, **no**, it is not possible to make the clock reach every flip-flop at exactly the same time across a real chip. Wires, buffers, vias, RC delay, loading, process variation, voltage variation, and temperature variation all cause different clock arrival times. That difference is called **clock skew**. Timing-analysis notes define clock skew as the difference in arrival time of clock edges at source and destination registers. [[S122]](#s122)

So the real goal is not:

```text
exactly zero skew everywhere
```

The real goal is:

```text
keep skew small, predictable, and within timing limits
```

### Why exact same arrival is not practical

1. different flops are physically far apart,
2. clock routes have different lengths and parasitics,
3. sinks have different loads,
4. clock buffers themselves have delay variation,
5. on-chip variation changes delay from one region to another.

### What measures do we take?

#### 1. Clock Tree Synthesis (CTS)

CTS builds a clock distribution network from the clock source to all sink flops. It inserts clock buffers or inverters to balance delay and reduce skew. This is the main physical-design step used to manage clock arrival. [[S73]](#s73)

#### 2. Balanced clock topology

Common structures include:

1. balanced clock tree,
2. H-tree,
3. clock mesh in high-performance designs.

These reduce systematic skew by making clock distribution more symmetric.

#### 3. Buffer insertion and sizing

Buffers are inserted to:

1. drive large fanout,
2. reduce transition time,
3. balance insertion delay across branches.

#### 4. Careful placement

Placement affects clock quality. If strongly related flops are placed reasonably close, clock and data timing becomes easier to balance.

#### 5. Clock shielding and proper routing

Clock nets are sensitive and high-fanout. Designers often:

1. route them on preferred metal layers,
2. shield them from noisy switching nets,
3. reduce coupling and jitter.

#### 6. Skew optimization / useful skew

Sometimes we do not force identical arrival times. Instead, we intentionally allow some controlled skew to help setup timing while still protecting hold timing. This is called **useful skew**.

#### 7. STA with uncertainty and OCV

Even after CTS, we do timing analysis with:

1. clock uncertainty,
2. jitter,
3. on-chip variation (OCV),
4. derates and margins.

That is because low skew in layout is not enough; it must still close timing under variation.

### Interview-safe conclusion

So the practical answer is:

```text
exact same arrival is not possible,
but low and controlled skew is possible
```

**Speak like this:**

"Practically, I cannot make the clock reach every flop at exactly the same time, because real clock paths have different wire delay, buffer delay, load, and process variation. What I do is reduce and control skew using CTS, balanced clock-tree structures like H-tree, proper clock buffering, careful placement, good clock routing, shielding, and timing closure with uncertainty and OCV margins. So the target is not zero skew in an absolute sense, but small and manageable skew."

[Back to index](./index.md)

<a id="q230"></a>
## 230. Static power and dynamic power.

**Written answer:**

In CMOS circuits, total power is usually discussed as two main parts:

1. **dynamic power**
2. **static power**

Power lecture notes explain dynamic power mainly as charging and discharging capacitances during switching, while static power is power consumed even when the circuit is idle. [[S123]](#s123)

### 1. Dynamic power

Dynamic power is consumed when the circuit is switching.

The main component is capacitive switching power:

```text
Pdynamic ≈ α C Vdd^2 f
```

Where:

- `α` = activity factor,
- `C` = effective switched capacitance,
- `Vdd` = supply voltage,
- `f` = frequency.

#### Why it happens

Whenever a node changes from `0` to `1`, its capacitance is charged from the supply. When it later discharges, that stored energy is dissipated.

#### Includes

1. charging/discharging load capacitance,
2. internal gate switching,
3. short-circuit power during transitions, when PMOS and NMOS conduct simultaneously for a short time.

### 2. Static power

Static power is consumed even when the circuit is not switching.

It is mainly due to leakage currents:

```text
Pstatic = Ileak x Vdd
```

#### Sources of static power

1. subthreshold leakage,
2. gate-oxide leakage,
3. junction leakage,
4. leakage through always-on bias paths.

### Quick comparison

| Parameter | Dynamic power | Static power |
|---|---|---|
| Depends on switching? | Yes | No |
| Main cause | Capacitive charging/discharging and short-circuit current | Leakage current |
| Important formula | `α C Vdd^2 f` | `Ileak x Vdd` |
| Dominates when | Activity and frequency are high | Leakage is significant or circuit is idle long |

### How to reduce them

#### Reduce dynamic power

1. lower `Vdd`,
2. reduce switching activity,
3. reduce capacitance,
4. reduce clock frequency,
5. use clock gating where appropriate.

#### Reduce static power

1. use high-threshold cells where possible,
2. power gating,
3. multi-Vt design,
4. body-bias control in some flows,
5. reduce leakage-prone always-on logic.

**Speak like this:**

"Dynamic power is the power consumed when the circuit switches, mainly because capacitors are charged and discharged, so it is roughly proportional to activity factor, capacitance, Vdd squared, and frequency. Static power is the power consumed even when the circuit is idle, mainly because of leakage current. So dynamic power is switching-related, while static power is leakage-related."

[Back to index](./index.md)

<a id="q234"></a>
## 234. Basics of design for testability.

**Written answer:**

**Design for Testability (DFT)** means adding features to a design so that manufacturing defects can be detected more easily after fabrication. DFT lecture notes describe the objective as improving **controllability** and **observability** of the design. [[S124]](#s124)

### Why DFT is needed

Modern chips are large and sequential. If we try to test only with normal functional vectors:

1. internal states are hard to control,
2. internal nodes are hard to observe,
3. fault coverage remains limited.

DFT improves test quality and makes ATPG practical.

### Two key ideas

#### 1. Controllability

How easily can I force an internal node or flip-flop to a desired value?

#### 2. Observability

How easily can I see the effect of a fault at an output or test point?

DFT improves both.

### Most common DFT technique: scan

The most widely used DFT technique is **scan insertion**.

In scan design:

1. normal flip-flops are replaced with **scan flip-flops**,
2. in test mode, these scan flops are connected like a **shift register**,
3. test data is shifted in through `scan_in`,
4. captured responses are shifted out through `scan_out`.

This makes sequential logic look more like combinational logic to ATPG tools. DFT notes explain that scan cells behave like pseudo primary inputs and pseudo primary outputs during test. [[S124]](#s124)

### Basic DFT blocks

1. **Scan chain**
2. **Scan enable**
3. **Scan in / scan out**
4. **Test clock**
5. **ATPG patterns**

### Other common DFT concepts

#### ATPG

Automatic Test Pattern Generation creates patterns to detect modeled faults such as:

1. stuck-at faults,
2. transition faults,
3. some bridge or other structural fault models.

#### BIST

Built-In Self-Test adds on-chip test-generation and response-analysis hardware, such as:

1. LFSR for pattern generation,
2. MISR for response compaction.

#### Boundary scan / JTAG

Used for board-level access and testing of chip pins and interconnects.

### Tradeoffs of DFT

DFT improves testability, but it adds:

1. area overhead,
2. timing overhead,
3. extra test pins or test control logic,
4. extra test-power concerns during scan shifting.

### Interview-safe summary

DFT is about making faults easier to activate and observe.

**Speak like this:**

"Design for testability means I add hardware features so that manufacturing faults can be detected more easily after fabrication. The main idea is to improve controllability and observability. The most common DFT method is scan insertion, where normal flip-flops are replaced by scan flops and connected as scan chains in test mode. Then ATPG can shift in patterns, capture responses, and shift them out to improve fault coverage."

[Back to index](./index.md)

<a id="q236"></a>
## 236. Verification vs testing.

**Written answer:**

In VLSI, **verification** and **testing** are related, but they are not the same. University notes on VLSI verification and manufacturing test define:

1. **verification** as checking whether the design will perform the intended function,
2. **test** as checking whether the fabricated chip has manufacturing defects. [[S125]](#s125)

### Verification

Verification is done on the **design representation** before fabrication, for example:

1. RTL,
2. gate-level netlist,
3. formal model,
4. emulation or FPGA prototype.

The goal is to catch:

1. logic bugs,
2. protocol bugs,
3. corner-case functional errors,
4. reset, CDC, or timing-intent problems.

Common verification methods are:

1. simulation,
2. assertions,
3. formal verification,
4. emulation,
5. coverage analysis.

### Testing

Testing is done on the **manufactured silicon**.

The goal is to catch physical manufacturing defects such as:

1. opens,
2. shorts,
3. stuck-at faults,
4. transition-delay related faults,
5. some defect-induced failures.

Common test methods are:

1. scan test,
2. ATPG patterns,
3. BIST,
4. boundary scan,
5. ATE-based production test.

### Simple difference

| Item | Verification | Testing |
|---|---|---|
| Main question | "Did I design it correctly?" | "Was it manufactured correctly?" |
| Stage | Before fabrication | After fabrication |
| Target | Functional correctness | Physical defect screening |
| Typical environment | Simulator, formal tools, emulator | Tester, probe station, production test |
| Typical bugs/failures found | RTL/design bugs | Manufacturing defects |

### Interview-safe summary

Verification is about **design correctness**. Testing is about **manufacturing correctness**.

**Speak like this:**

"Verification means checking before fabrication that my design meets the specification and behaves correctly. Testing means checking after fabrication that the physical chip does not have manufacturing defects. So verification finds design bugs, while testing screens bad silicon."

[Back to index](./index.md)

<a id="q237"></a>
## 237. Clock jitter.

**Written answer:**

**Clock jitter** is the short-term variation of actual clock-edge timing from its ideal position. Timing-analysis notes describe jitter as deviation from the defined clock period, and it is treated as part of clock uncertainty. [[S122]](#s122) [[S130]](#s130)

### What it means physically

If the ideal clock period is:

```text
T, T, T, T ...
```

the real clock may arrive like:

```text
T+delta1, T-delta2, T+delta3 ...
```

So even if the average frequency is correct, individual edges are not perfectly periodic.

### Why jitter matters

Jitter reduces timing margin because setup and hold checks depend on where the capture edge really occurs.

1. More jitter means less reliable setup margin.
2. It can also reduce hold margin depending on the direction of uncertainty.
3. In STA, it is usually modeled inside clock uncertainty.

### Common causes

1. PLL/DLL phase noise,
2. supply noise,
3. crosstalk on the clock network,
4. substrate noise,
5. temperature and process variation,
6. electromagnetic interference.

### Jitter vs skew

| Term | Meaning |
|---|---|
| Skew | Difference in arrival time between two different clock sinks |
| Jitter | Variation of a clock edge from its ideal time at the same sink over time |

### Interview-safe summary

Clock skew is **spatial difference**. Clock jitter is **time variation**.

**Speak like this:**

"Clock jitter means the clock edge does not come at exactly the ideal time every cycle. It varies slightly from cycle to cycle because of PLL noise, supply noise, crosstalk, and other nonideal effects. In STA, jitter is treated as clock uncertainty, so it reduces the timing margin available for setup and hold."

[Back to index](./index.md)

<a id="q242"></a>
## 242. FPGA vs ASIC.

**Written answer:**

An **FPGA** is a programmable hardware device built from configurable logic blocks, programmable interconnect, and dedicated hard macros. An **ASIC** is an application-specific integrated circuit implemented as fixed silicon for one target design. FPGA/ASIC lecture material highlights that FPGAs are configurable and faster to deploy, while ASICs are more optimized for final performance, area, and power. [[S126]](#s126)

### Main difference

| Parameter | FPGA | ASIC |
|---|---|---|
| Hardware nature | Reprogrammable | Fixed after fabrication |
| Flexibility | Very high | Very low after tape-out |
| NRE cost | Low | High |
| Per-unit cost | Higher | Lower at high volume |
| Performance | Lower than ASIC for same function | Higher |
| Power | Higher | Lower |
| Area | Larger | Smaller |
| Time to market | Faster | Slower |
| Debug/updates | Easy to update in field | Requires redesign/re-spin |
| Best use case | Prototyping, low/medium volume, changing requirements | High volume, high performance, low power products |

### Why ASIC is usually better in PPA

ASICs are better in **power, performance, and area** because:

1. routing is custom or highly optimized,
2. cells are chosen specifically for the design,
3. there is no LUT overhead,
4. there is no programmable-switch overhead in interconnect.

### Why FPGA is attractive

FPGAs are attractive because:

1. design cycles are shorter,
2. you can reprogram after deployment,
3. no fabrication cost is needed for each design revision,
4. they are excellent for prototyping and lower-volume products.

### Interview-safe rule

Use:

1. **FPGA** when flexibility and faster iteration matter more,
2. **ASIC** when volume is high and PPA matters most.

**Speak like this:**

"FPGA is programmable hardware, so it gives me flexibility and short development time, but it costs more power, area, and usually speed. ASIC is fixed silicon, so the upfront cost is high and design time is longer, but for high-volume products it gives the best performance, lowest power, and smallest area. So I prefer FPGA for prototyping or changing requirements, and ASIC for production when PPA and unit cost matter."

[Back to index](./index.md)

<a id="q244"></a>
## 244. Inverter VTC graph and properties.

**Written answer:**

The **voltage transfer characteristic (VTC)** of an inverter is the DC plot of output voltage `Vout` versus input voltage `Vin`. CMOS inverter lecture notes identify the main VTC parameters as `VOH`, `VOL`, `VIL`, `VIH`, and switching threshold `VM` or `VS`. [[S127]](#s127)

### Simple VTC sketch

```text
Vout
 ^
 |  VOH  ----------------------.
 |                             \
 |                              \
 |                               \
 |                                \
 |                                 '-----------  VOL
 |
 +--------------------------------------------------> Vin
    0          VIL      VM       VIH               VDD
```

### What the graph means

1. When `Vin` is low:
   - PMOS is ON,
   - NMOS is OFF,
   - `Vout` is near `VDD`, so output is logic `1`.
2. When `Vin` is high:
   - PMOS is OFF,
   - NMOS is ON,
   - `Vout` is near `0`, so output is logic `0`.
3. In the middle transition region:
   - both devices conduct,
   - the inverter gain is high,
   - output changes sharply.

### Important VTC properties

#### 1. `VOH`

Output high voltage. Ideally close to `VDD`.

#### 2. `VOL`

Output low voltage. Ideally close to `0`.

#### 3. `VM` or switching threshold

This is the point where:

```text
Vin = Vout
```

It is the approximate switching point of the inverter. It depends on NMOS/PMOS strength ratio.

#### 4. `VIL` and `VIH`

These define the valid input-low and input-high boundaries. In inverter theory, they are usually taken near the points where the VTC slope is `-1`. [[S127]](#s127)

#### 5. Noise margins

For a CMOS inverter:

```text
NMH = VOH - VIH
NML = VIL - VOL
```

Large noise margins mean better noise immunity.

#### 6. Gain

The transition region has high negative gain:

```text
dVout / dVin < 0
```

This steep slope is why the inverter restores weak logic levels into clean `0` or `1`.

### Design insight

If PMOS is made stronger relative to NMOS, the switching threshold shifts. Designers often size PMOS wider than NMOS so the transition is closer to the middle of the supply range.

**Speak like this:**

"The inverter VTC is the plot of output voltage versus input voltage. When input is low, output stays near VDD. When input is high, output goes near ground. The important properties are VOH, VOL, VIL, VIH, and the switching threshold VM. The steep middle region gives high gain and good noise rejection, and from the VTC I can also get the noise margins NMH and NML."

[Back to index](./index.md)

<a id="q262"></a>
## 262. What does nanometer technology refer to?

**Written answer:**

In semiconductor design, **nanometer technology** usually refers to the **process node** or **technology node** used to manufacture the chip, such as `90 nm`, `28 nm`, `7 nm`, or `3 nm`.

### Standard definition

It is a label used to identify a generation of semiconductor manufacturing technology. Historically, node names were associated with physical transistor dimensions, but modern node names do **not** necessarily equal any one exact transistor feature size. Intel explicitly notes that modern node numbers do not represent the actual dimension of a single physical feature on the transistor. [[S147]](#s147)

### What it practically indicates

When someone says:

```text
7 nm technology
```

they usually mean:

1. a newer process generation,
2. higher transistor density,
3. potentially better speed/power tradeoffs,
4. more advanced device and interconnect scaling.

So in practice, "nanometer technology" is a **node-generation name** for the fabrication process.

### Important interview point

Do not say:

```text
7 nm means every transistor length is exactly 7 nm
```

That is not a safe modern answer.

### Interview-safe summary

Nanometer technology refers to the **fabrication node generation** of the chip, not necessarily one exact measurable transistor dimension.

**Speak like this:**

"Nanometer technology refers to the semiconductor process node, like 28 nm or 7 nm. Historically it was linked more closely to physical feature size, but in modern technologies the node name is mainly a generation label for the manufacturing process. It generally indicates scaling level, transistor density, and expected power-performance improvements, not one exact transistor dimension."

[Back to index](./index.md)

<a id="q264"></a>
## 264. What is leakage current in CMOS?

**Written answer:**

**Leakage current in CMOS** is the small unwanted current that flows even when the transistor or circuit is supposed to be OFF or idle. In CMOS circuits, this current contributes to **static power consumption**.

### Standard definition

Leakage current is the current that flows through a MOS device because real transistors are not ideal switches. Even when `VGS` is below threshold and the transistor is intended to be OFF, some current can still flow. University CMOS leakage notes describe this as off-state or leakage current, and identify several leakage components in scaled CMOS. [[S148]](#s148) [[S149]](#s149)

### Main leakage components in CMOS

1. **Subthreshold leakage**: current flowing between drain and source when the transistor is below threshold.
2. **Gate leakage**: tunneling current through the thin gate oxide.
3. **Junction leakage**: reverse-bias leakage at source/body and drain/body junctions.
4. **GIDL and related leakage** in advanced processes.

### Why it matters

Leakage current:

1. increases standby power,
2. becomes worse in smaller technology nodes,
3. increases with temperature,
4. is a major issue in low-power CMOS design.

### Relation to power

Leakage current causes:

```text
Pstatic = Ileak * VDD
```

So even when the circuit is not switching, power is still consumed.

### Interview-safe summary

Leakage current is **unwanted off-state current** in CMOS, and it is the main reason for static power.

**Speak like this:**

"Leakage current in CMOS is the small current that still flows even when a transistor is supposed to be OFF. Because real MOS transistors are not ideal switches, we get subthreshold leakage, gate leakage, and junction leakage. This off-state current causes static power dissipation, which becomes more serious as technology scales down."

[Back to index](./index.md)

<a id="q359"></a>
## 359. What is pipelining?

**Written answer:**

**Pipelining** is a technique in computer architecture where instruction execution is divided into multiple stages so that several instructions can be processed at the same time, each in a different stage. University pipeline notes emphasize that pipelining improves **throughput**, not the latency of a single instruction. [[S69]](#s69) [[S150]](#s150)

### Basic idea

Instead of finishing one whole instruction before starting the next, the processor overlaps work:

```text
Instruction 1 -> Fetch -> Decode -> Execute -> Memory -> Writeback
Instruction 2 ->        Fetch -> Decode -> Execute -> Memory -> Writeback
Instruction 3 ->               Fetch -> Decode -> Execute -> Memory -> Writeback
```

So after the pipeline is filled, ideally one instruction can complete every clock cycle.

### Why pipelining is used

1. increases instruction throughput,
2. makes better use of hardware stages,
3. allows higher overall performance than non-pipelined execution.

### Important point

Pipelining does **not** mean one instruction becomes faster by itself. It mainly means:

```text
more instructions completed per unit time
```

### Common pipeline stages

In a basic CPU, the stages are often:

1. IF - instruction fetch,
2. ID - instruction decode,
3. EX - execute,
4. MEM - memory access,
5. WB - write back.

### Limitation

Pipelining introduces hazards such as:

1. structural hazards,
2. data hazards,
3. control hazards.

**Speak like this:**

"Pipelining means dividing instruction execution into stages and overlapping multiple instructions so different instructions are in different stages at the same time. It improves throughput, not the latency of one instruction. In a typical CPU pipeline, stages are fetch, decode, execute, memory, and writeback."

[Back to index](./index.md)

<a id="q360"></a>
## 360. Difference between virtual memory and cache memory.

**Written answer:**

**Cache memory** and **virtual memory** are both part of the memory hierarchy, but they solve different problems.

### Cache memory

Cache memory is a **small, very fast memory** placed close to the CPU. It stores recently or frequently used data so the processor can access it faster than going to main memory.

### Virtual memory

Virtual memory is a mechanism in which **main memory acts as a cache for a much larger address space stored on disk/secondary storage**. Computer architecture notes describe virtual memory exactly this way. [[S151]](#s151)

### Main difference

| Parameter | Cache memory | Virtual memory |
|---|---|---|
| Purpose | Speed up access to frequently used data | Give programs a large logical address space and protection |
| Backing store | Main memory | Disk / SSD secondary storage |
| Managed by | Mostly hardware | Hardware + operating system |
| Unit of transfer | Cache line / block | Page |
| Miss penalty | Relatively small | Very large page-fault penalty |
| Typical memory type | SRAM cache | DRAM plus disk backing |
| Main goal | Performance | Capacity, isolation, and abstraction |

### Simple intuition

1. Cache memory answers: "How do I make memory access faster?"
2. Virtual memory answers: "How do I give each process a large private address space even when RAM is limited?"

### Important relation

They are not the same, but conceptually both use locality and hierarchical storage.

**Speak like this:**

"Cache memory is a small fast memory near the CPU used to reduce average access time. Virtual memory is a mechanism where RAM acts like a cache for a much larger address space backed by disk. So cache is mainly for speed, while virtual memory is mainly for large address space, protection, and memory management."

[Back to index](./index.md)

<a id="q361"></a>
## 361. What are the different types of hazards?

**Written answer:**

In pipelined processors, a **hazard** is a condition that prevents the next instruction from executing in its intended clock cycle. Standard computer architecture notes classify pipeline hazards into **three main types**. [[S152]](#s152)

### 1. Structural hazard

A **structural hazard** happens when hardware resources are not sufficient for overlapping instructions.

Example:

1. one instruction needs memory for instruction fetch,
2. another instruction needs the same memory for data access,
3. both cannot use it at the same cycle.

### 2. Data hazard

A **data hazard** happens when one instruction depends on data produced by another instruction that is still in the pipeline.

Example:

```text
ADD R1, R2, R3
SUB R4, R1, R5
```

The `SUB` needs `R1` before the `ADD` has fully written it.

#### Common data hazard names

1. **RAW** - Read After Write, true dependence
2. **WAR** - Write After Read, anti-dependence
3. **WAW** - Write After Write, output dependence [[S153]](#s153)

In basic in-order pipelines, RAW is the most common practical one.

### 3. Control hazard

A **control hazard** happens when the pipeline does not yet know the correct next instruction because of branch or jump decisions.

Example:

1. processor fetches the next sequential instruction,
2. branch result is resolved later,
3. fetched instruction may need to be stalled or flushed.

### Summary table

| Hazard type | Cause | Typical fix |
|---|---|---|
| Structural | Resource conflict | Stall or duplicate resource |
| Data | Operand dependence | Forwarding, stall, scheduling |
| Control | Branch/jump uncertainty | Prediction, stall, flush |

**Speak like this:**

"There are three main pipeline hazards: structural, data, and control. Structural hazard is a hardware resource conflict. Data hazard happens when one instruction depends on the result of another still in the pipeline. Control hazard happens when branches or jumps make the next instruction uncertain. For data hazards, the common subtypes are RAW, WAR, and WAW."

[Back to index](./index.md)

<a id="q272"></a>
## 272. SRAM internal structure, read/write operation, and noise margin.

**Written answer:**

The standard SRAM bit-cell used in many designs is the **6T SRAM cell**. Memory lecture notes describe it as:

1. two cross-coupled inverters that store one bit,
2. two access transistors that connect the internal storage nodes to the bit-lines,
3. one word-line that turns the access transistors ON or OFF. [[S128]](#s128)

### Internal structure of a 6T SRAM cell

```text
             VDD                     VDD
              |                       |
             P1                      P2
              |------ Q      QB ------|
              |                       |
             N1                      N2
              |                       |
             GND                     GND

BL  ---- A1 ---- Q
BLB ---- A2 ---- QB

A1 and A2 are access NMOS transistors
Their gates are driven by WL
```

### Main signals

1. `Q` and `QB` are the two internal storage nodes.
2. `BL` and `BLB` are complementary bit-lines.
3. `WL` is the word-line.

### Hold operation

When `WL = 0`, the access transistors are OFF, so the cross-coupled inverters are isolated from the bit-lines and keep the stored value by positive feedback. [[S128]](#s128)

### Read operation

In a normal 6T SRAM read:

1. `BL` and `BLB` are first precharged, usually high.
2. `WL` is asserted.
3. The internal node storing `0` slightly discharges its connected bit-line through the pull-down path.
4. The other bit-line stays closer to the precharged value.
5. A sense amplifier detects the small differential between `BL` and `BLB` and decides whether the stored data is `0` or `1`. [[S128]](#s128)

#### Read concern

Read is not fully passive in SRAM. The cell is connected to large bit-lines during read, so the internal node can be disturbed. That is why **read stability** is important.

### Write operation

For a write:

1. The write driver forces `BL` and `BLB` to complementary values.
2. `WL` is asserted.
3. Through the access transistors, the forced bit-line values overpower the previous state of the cross-coupled inverters.
4. The cell flips and stores the new value.
5. `WL` is deasserted, and the new value is held. [[S128]](#s128)

### What is noise margin?

In general digital logic, **noise margin** is the amount of unwanted noise voltage that can be tolerated without causing a wrong logic interpretation. For an inverter:

```text
NMH = VOH - VIH
NML = VIL - VOL
```

So larger noise margin means better immunity to noise. [[S127]](#s127)

### SRAM noise margin

For SRAM, we usually talk about **static noise margin (SNM)**. UC Davis SRAM notes describe SNM as the largest added noise disturbance that does not upset the cell, and note that SNM depends on the mode of operation:

1. hold SNM,
2. read SNM,
3. write margin / write SNM. [[S129]](#s129)

It is commonly obtained from the **butterfly curve** of the two cross-coupled inverter characteristics.

### Important practical point

For a 6T SRAM cell:

1. **hold SNM** is usually better than read SNM,
2. **read mode** is usually the weakest stability mode,
3. **write ability** needs the access path and bit-line driver to be strong enough to flip the cell.

**Speak like this:**

"A normal SRAM bit-cell is a 6T cell made of two cross-coupled inverters plus two access transistors controlled by the word-line. In hold mode, WL is low and the cell stores data by feedback. In read mode, the bit-lines are precharged, WL is enabled, and one bit-line discharges slightly, which is detected by the sense amplifier. In write mode, the bit-lines are driven with complementary data and overpower the old cell state. Noise margin means how much noise the cell can tolerate without flipping incorrectly; in SRAM we usually talk about static noise margin, especially hold SNM and read SNM."

[Back to index](./index.md)

<a id="q299"></a>
## 299. What is a case statement?

**Written answer:**

In Verilog, a **case statement** is a multiway decision statement used to select one block of code based on the value of an expression. The IEEE Verilog standard defines `case`, `casez`, and `casex` as the language's case statement forms. [[S5]](#s5)

### Basic syntax

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    default: y = d;
endcase
```

### What it does

1. The expression inside `case(...)` is evaluated.
2. It is compared against each case item.
3. When a match is found, that branch executes.
4. If no match is found, the `default` branch is used if present.

### Types

#### 1. `case`

Exact comparison. `0`, `1`, `x`, and `z` are matched exactly.

#### 2. `casez`

Treats `z` values, and often `?`, as don't-care in the case item.

#### 3. `casex`

Treats both `x` and `z` as don't-care in the comparison. This can hide unknown-state bugs, so it is usually used very carefully in synthesizable RTL.

### Case vs if-else

| Feature | `case` | `if-else` |
|---|---|---|
| Best for | One expression matched against many values | General boolean conditions |
| Readability | Cleaner for decoders/FSMs/select logic | Better for priority conditions |
| Hardware intent | Often used for mux/select/FSM branching | Often used for conditional logic / priority logic |

### Good coding practice

1. Include `default` unless you have a strong reason not to.
2. In combinational logic, assign outputs on all paths to avoid latch inference.
3. Use `casez`/`casex` carefully.

**Speak like this:**

"A case statement in Verilog is a multiway selection statement. I use it when one expression has to be compared against several possible values, like in muxes, decoders, or FSMs. Normal case does exact matching, casez allows z wildcards, and casex treats x and z as wildcards, so casex must be used carefully."

[Back to index](./index.md)

<a id="q322"></a>
## 322. What are the different ways to fix setup and hold? Which one is difficult to fix?

**Written answer:**

Timing-analysis notes separate setup and hold problems clearly:

1. **setup violation** means the data path is too slow,
2. **hold violation** means the data path is too fast. [[S122]](#s122) [[S130]](#s130)

### Ways to fix setup violation

The idea is to make data arrive earlier or give it more time.

#### Common setup fixes

1. reduce combinational delay,
2. upsize cells on the critical path,
3. swap to lower-`Vt` or faster cells where allowed,
4. restructure logic to reduce logic depth,
5. improve placement/routing of the critical path,
6. reduce clock frequency if architecture allows,
7. add pipelining or retiming,
8. use useful positive skew carefully.

### Ways to fix hold violation

The idea is to make data arrive later or make the capture edge effectively safer.

#### Common hold fixes

1. add delay buffers or inverter pairs on the fast path,
2. detour routing / increase route delay,
3. downsize overly strong cells on very short paths,
4. use higher-`Vt` or slower cells where allowed,
5. adjust clock skew through CTS or useful skew,
6. fix overly aggressive clock arrival differences.

Washington timing notes explicitly mention adding delay in the data path with buffers or inverter pairs to fix hold violations, and rewriting/simplifying logic or adding pipelining to fix setup violations. [[S130]](#s130)

### Which one is difficult to fix?

This has two practical answers.

#### At architecture / RTL level

**Setup** can be more expensive to fix, because it may require:

1. pipelining,
2. retiming,
3. micro-architecture changes,
4. lower target frequency.

#### At physical-design signoff level

**Hold** is often more tedious to close, because:

1. it affects many short paths,
2. it must pass at fast corners,
3. adding hold delay can hurt setup on the same path,
4. hold cannot be solved simply by lowering the clock frequency.

So a good interview answer is:

```text
setup is architecturally more expensive,
hold is physically more delicate and iterative
```

**Speak like this:**

"To fix setup, I try to reduce data-path delay by using faster cells, logic restructuring, better placement, or pipelining. To fix hold, I usually add delay on the fast path using buffers, inverter pairs, or routing detours, and sometimes adjust clock skew. If you ask from architecture side, setup is harder because it may need pipelining or redesign. If you ask from signoff side, hold is usually more delicate because many short paths are involved and every hold fix can hurt setup."

[Back to index](./index.md)

<a id="q323"></a>
## 323. Which violation do you fix first: setup or hold?

**Written answer:**

The safest interview answer is:

```text
it depends on the stage of the flow
```

### Before CTS / early implementation

Before the real clock tree exists, setup is usually the main optimization target because long data paths are already visible, while final hold behavior depends strongly on actual clock insertion delay and skew.

### After CTS / during signoff

After clocks are propagated and real skew is available, designers usually treat **hold** as the must-fix correctness issue on violating paths, then recheck and recover setup. This is an engineering practice inferred from timing behavior:

1. hold violations are minimum-delay race problems,
2. they cannot be solved by reducing frequency,
3. hold fixes such as added buffers can consume setup slack,
4. so if hold is still open, setup may change again. [[S122]](#s122) [[S130]](#s130)

### Short practical rule

1. **Pre-CTS:** optimize setup first.
2. **Post-CTS / signoff:** close hold violations first on real violating paths, then polish setup.

### Why many engineers say "fix hold first"

Because in final timing closure:

1. hold is a hard correctness issue,
2. setup can often still be traded against clock period or pipeline changes,
3. but an unfixed hold violation can break functionality even at a lower clock frequency.

**Speak like this:**

"If you ask before CTS, setup is usually optimized first because the real clock tree is not there yet. But in post-CTS timing closure, I usually fix hold first on the real violating paths, because hold is a race condition, lowering frequency does not save it, and hold fixes can eat setup slack. After that I recheck setup and optimize again."

[Back to index](./index.md)

<a id="q352"></a>
## 352. Difference between normal buffers and clock buffers.

**Written answer:**

A **normal buffer** is a general-purpose buffer used on data or control nets. A **clock buffer** is a special buffer or clock-tree cell intended specifically for distributing clocks with low skew and controlled signal quality. Clock-tree and FPGA clocking documentation both emphasize that clock distribution uses dedicated buffering/routing resources designed for low skew and low distortion. [[S73]](#s73) [[S131]](#s131)

### Main differences

| Parameter | Normal buffer | Clock buffer |
|---|---|---|
| Main use | Data/control path buffering | Clock distribution |
| Routing | Regular signal routing | Dedicated clock network or CTS path |
| Optimization target | Fanout, slew, delay | Low skew, low jitter, duty-cycle quality, insertion delay |
| Characterization | General signal buffer | Specially characterized for clock behavior |
| Rise/fall balance | Not necessarily tightly balanced | Usually more balanced |
| Allowed use | General logic nets | Clock nets only in good design practice |
| Extra features | Usually none | May support clock enable, muxing, divide, gating depending on library/device |

### Why not use a normal buffer on a clock?

Because a normal buffer on a clock net can create:

1. larger skew,
2. more duty-cycle distortion,
3. more jitter sensitivity,
4. poorer CTS behavior,
5. less predictable timing closure.

### Practical view

In ASIC flow:

1. normal buffers are used in data-path optimization,
2. clock buffers / clock inverters are used by CTS for the clock tree.

In FPGA flow:

1. ordinary fabric routing is avoided for clocks when possible,
2. global clock buffers and dedicated clock routes are preferred. [[S131]](#s131)

**Speak like this:**

"A normal buffer is a general-purpose buffer for data and control nets. A clock buffer is a special clock-tree cell used to drive the clock network with low skew, controlled duty-cycle distortion, and better jitter behavior. So in practice I use normal buffers on data paths and clock buffers only on clock paths."

[Back to index](./index.md)

<a id="sources"></a>
## Source References

<a id="s1"></a>
**S1. NIST CSRC Glossary, Byte:** https://csrc.nist.gov/glossary/term/byte

<a id="s2"></a>
**S2. MIT Computation Structures, Sequential Logic:** https://computationstructures.org/notes/sequential_logic/notes.html

<a id="s3"></a>
**S3. Cornell ECE 2300 Lecture 7, D Latch and Flip-Flop:** https://www.csl.cornell.edu/courses/ece2300/pdf/Lecture07.pdf

<a id="s4"></a>
**S4. Cornell ECE 2300 Timing Analysis Notes:** https://www.csl.cornell.edu/courses/ece2300/pdf/timing-analysis-notes.pdf

<a id="s5"></a>
**S5. IEEE Std 1364-2005 Verilog Hardware Description Language:** https://www-inst.eecs.berkeley.edu/~eecs151/sp20/files/verilog/verilog-std-1364-2005.pdf

<a id="s6"></a>
**S6. Drexel CS270 Logic Design Notes, Encoder:** https://www.cs.drexel.edu/~johnsojr/2016-17/fall/CS270/Lectures/3/circuit.pdf

<a id="s7"></a>
**S7. MIT 6.175 Lab 1, Multiplexers:** https://csg.csail.mit.edu/6.175/archive/2016/labs/lab1-multiplexers-adders.html

<a id="s8"></a>
**S8. Intel MAX 10 FPGA Design Guidelines, Reset Architecture:** https://www.intel.com/content/www/us/en/docs/programmable/683196/current/review-recommended-reset-architecture.html

<a id="s9"></a>
**S9. UC Davis Digital Logic Design, Universal Gates:** https://american.cs.ucdavis.edu/academic/ecs154a.sum14/postscript/cosc205.pdf

<a id="s10"></a>
**S10. UC Riverside Combinational Logic Slides, NAND/NOR CMOS Comparison:** https://intra.engr.ucr.edu/~htseng/classes/ee120a_2020sp/slides/2_CombinationalLogic.pdf

<a id="s11"></a>
**S11. AMD/Xilinx UltraFast Design Methodology Guide UG949, Reset and Metastability Guidance:** https://www.xilinx.com/support/documents/sw_manuals/xilinx2022_1/ug949-vivado-design-methodology.pdf

<a id="s12"></a>
**S12. Clifford E. Cummings, Nonblocking Assignments in Verilog Synthesis, Coding Styles That Kill:** https://www.sunburst-design.com/papers/CummingsSNUG2000SJ_NBA.pdf

<a id="s13"></a>
**S13. Sutherland HDL, Modeling with SystemVerilog:** https://sutherland-hdl.com/papers/2006-SNUG-Europe_SystemVerilog_synthesis_paper.pdf

<a id="s14"></a>
**S14. AMD Vivado Synthesis Guide UG901, Always Procedures:** https://docs.amd.com/r/en-US/ug901-vivado-synthesis/Always-Procedures

<a id="s15"></a>
**S15. EDN, Resets in FPGA and ASIC Control and Data Paths:** https://www.edn.com/resets-in-fpga-asic-control-and-data-paths/

<a id="s16"></a>
**S16. PhysicalDesign4U, Time Borrowing Concept in STA:** https://www.physicaldesign4u.com/2020/05/time-borrowing-concept-in-sta.html

<a id="s17"></a>
**S17. CircuitVerse, Race Conditions:** https://learn.circuitverse.org/docs/seq-design/race-conditions.html

<a id="s18"></a>
**S18. Electronics Tutorials, JK Flip-Flop and Master-Slave JK Flip-Flop:** https://www.electronics-tutorials.ws/sequential/seq_2.html

<a id="s19"></a>
**S19. San Diego State University CS370 Lecture 08, 2-to-1-Line Multiplexer:** https://taoxie.sdsu.edu/cs370/Lecture08.pdf

<a id="s20"></a>
**S20. AMD UltraFast Design Methodology Guide UG949, Controlling Enable/Reset Extraction with Synthesis Attributes:** https://docs.amd.com/r/2021.1-English/ug949-vivado-design-methodology/Controlling-Enable/Reset-Extraction-with-Synthesis-Attributes

<a id="s21"></a>
**S21. AMD Vivado Synthesis Guide UG901, Flip-Flops and Registers Inference:** https://docs.amd.com/r/en-US/ug901-vivado-synthesis/Flip-Flops-and-Registers-Inference

<a id="s22"></a>
**S22. Toshiba Electronic Devices, Comparison of Transistors by Structure:** https://toshiba.semicon-storage.com/us/semiconductor/knowledge/e-learning/discrete/chap3/chap3-22.html

<a id="s23"></a>
**S23. Yue Guo, Sequence Detector 1010 Moore Machine and Mealy Machine:** https://yue-guo.com/2019/03/19/sequence-detector-1010-moore-machine-mealy-machine-overlapping-non-overlapping/

<a id="s24"></a>
**S24. IBM Think, Microcontroller vs. Microprocessor:** https://www.ibm.com/think/topics/microcontroller-vs-microprocessor

<a id="s25"></a>
**S25. TechTarget, Program Counter:** https://www.techtarget.com/whatis/definition/program-counter

<a id="s26"></a>
**S26. TechTarget, Stack Pointer:** https://www.techtarget.com/whatis/definition/stack-pointer

<a id="s27"></a>
**S27. Cornell CS3410, RISC and CISC Lecture Notes:** https://www.cs.cornell.edu/courses/cs3410/2010sp/lecture/topic13-risc-cisc-i.pdf

<a id="s28"></a>
**S28. Analog Devices, Three-State Logic:** https://www.analog.com/en/resources/glossary/three_state_logic.html

<a id="s29"></a>
**S29. GeeksforGeeks, Implementation of XOR Gate from NOR Gate:** https://www.geeksforgeeks.org/digital-logic/implementation-of-xor-gate-from-nor-gate/

<a id="s30"></a>
**S30. Analog Devices, Fast Fourier Transform:** https://www.analog.com/en/resources/glossary/fast_fourier_transform.html

<a id="s31"></a>
**S31. Electrical4U, Nyquist Stability Criterion:** https://www.electrical4u.com/nyquist-stability-criterion/

<a id="s32"></a>
**S32. Analog Devices, Analog-to-Digital Converter:** https://www.analog.com/en/resources/glossary/analog-to-digital-converter.html

<a id="s33"></a>
**S33. Electronics Tutorials, Communication Systems:** https://www.electronics-tutorials.ws/systems/communication-systems.html

<a id="s34"></a>
**S34. UC Riverside Combinational Logic Slides, CMOS NAND/NOR Structures:** https://intra.engr.ucr.edu/~htseng/classes/ee120a_2020sp/slides/2_CombinationalLogic.pdf

<a id="s35"></a>
**S35. Electronics Tutorials, MOSFET as a Switch:** https://www.electronics-tutorials.ws/transistor/tran_7.html

<a id="s36"></a>
**S36. Team VLSI, Latch-up in CMOS Design:** https://teamvlsi.com/2020/05/latch-up-is-in-cmos-design.html

<a id="s37"></a>
**S37. GeeksforGeeks, Difference between Synchronous and Asynchronous Sequential Circuits:** https://www.geeksforgeeks.org/digital-logic/difference-between-synchronous-and-asynchronous-sequential-circuits/

<a id="s38"></a>
**S38. TechTarget, FIFO:** https://www.techtarget.com/whatis/definition/FIFO-first-in-first-out

<a id="s39"></a>
**S39. VLSI Verify, Synchronous FIFO:** https://vlsiverify.com/verilog/verilog-codes/synchronous-fifo/

<a id="s40"></a>
**S40. VLSI Universe, Convert XOR to Inverter and Buffer:** https://vlsiuniverse.blogspot.com/2017/11/design-problem-how-can-you-convert-xor.html

<a id="s41"></a>
**S41. Verilog Code Blog, Finite State Machine Design for Sequence 0111:** https://verilog-code.blogspot.com/2014/08/finite-state-machine-design-for.html

<a id="s42"></a>
**S42. GeeksforGeeks, Ring Counter in Digital Logic:** https://www.geeksforgeeks.org/digital-logic/ring-counter-in-digital-logic/

<a id="s43"></a>
**S43. GeeksforGeeks, Johnson Counter:** https://www.geeksforgeeks.org/digital-logic/johnson-counter/

<a id="s44"></a>
**S44. NIST Dictionary of Algorithms and Data Structures, Queue:** https://xlinux.nist.gov/dads/HTML/queue.html

<a id="s45"></a>
**S45. Toshiba Electronic Devices, MOSFET Gate Drive Circuit:** https://toshiba.semicon-storage.com/info/TPH3R70APL_application_note_en_20180726_AKX00068.pdf?did=59460&prodName=TPH3R70APL

<a id="s46"></a>
**S46. Toshiba Electronic Devices, Power MOSFET Structure and Characteristics:** https://toshiba.semicon-storage.com/info/TK49N65W5_application_note_en_20180726_AKX00061.pdf?did=13413&prodName=TK49N65W5

<a id="s47"></a>
**S47. Arm, Microprocessor vs. Microcontroller:** https://www.arm.com/glossary/microprocessor-vs-microcontroller

<a id="s48"></a>
**S48. Analog Devices, Winning the Battle Against Latchup in CMOS Analog Switches:** https://www.analog.com/en/resources/technical-articles/winning-the-battle-against-latchup-in-cmos-analog-switches.html

<a id="s49"></a>
**S49. Texas Instruments, Latch-Up, ESD, and Other Phenomena:** https://www.ti.com/lit/an/slya014a/slya014a.pdf

<a id="s50"></a>
**S50. University of Iowa, Asynchronous Sequential Circuits:** https://homepage.divms.uiowa.edu/~jones/assem/fall07/notes/07seq.shtml

<a id="s51"></a>
**S51. Columbia University, Verilog HDL Modeling Styles:** https://www.cs.columbia.edu/~sedwards/classes/2015/4840/verilog.pdf

<a id="s52"></a>
**S52. ChipVerify, Verilog Always Block:** https://www.chipverify.com/verilog/verilog-always-block

<a id="s53"></a>
**S53. University of Washington CSE370, Introduction to Finite State Machines:** https://courses.cs.washington.edu/courses/cse370/DDOR/Tutorials/FSM/Intro.html

<a id="s54"></a>
**S54. AMD Vivado Design Suite, IDELAYE3 Primitive:** https://docs.amd.com/r/en-US/ug861-ultrascale-selectio/IDELAYE3

<a id="s55"></a>
**S55. YosysHQ, Yosys Optimization Passes:** https://yosyshq.readthedocs.io/projects/yosys/en/0.46/using_yosys/synthesis/opt.html

<a id="s56"></a>
**S56. Intel Quartus Prime Pro Edition User Guide, Time Borrowing with Latches:** https://www.intel.com/content/www/us/en/docs/programmable/683243/21-3/time-borrowing-with-latches.html

<a id="s57"></a>
**S57. GeeksforGeeks, Hardware Description Language:** https://www.geeksforgeeks.org/digital-logic/hardware-description-language/

<a id="s58"></a>
**S58. Analog Devices, ADC Architectures:** https://www.analog.com/en/resources/technical-articles/adc-architectures.html

<a id="s59"></a>
**S59. Introduction to Digital Circuits, D-Latch Implemented with a 2:1 Multiplexer:** https://strumpen.net/dc/build/html/basiccircuits/basiccircuits.html

<a id="s60"></a>
**S60. DeldSim, 2-Bit Up Counter:** https://deldsim.com/study/material/42/2-bit-up-counter/

<a id="s61"></a>
**S61. GeeksforGeeks, Edge Triggering and Level Triggering:** https://www.geeksforgeeks.org/digital-logic/edge-triggering-and-level-triggering/

<a id="s62"></a>
**S62. VLSI Universe, FIFO Depth Calculation:** https://vlsiuniverse.blogspot.com/2019/11/fifo-depth-calculation.html

<a id="s63"></a>
**S63. AMD Embedded FIFO Generator, Actual FIFO Depth:** https://docs.amd.com/r/en-US/pg327-emb-fifo-gen/Actual-FIFO-Depth

<a id="s64"></a>
**S64. University of Washington BEE271, Multiplexers and Shannon Expansion:** https://staff.washington.edu/kd1uj/BEE271/Lectures/BEE%20271%20Lecture%207%20-%20Multiplexers%20and%20Shannons%20expansion%20-%202017-04-17.pdf

<a id="s65"></a>
**S65. GeeksforGeeks, Multiplexers in Digital Logic:** https://www.geeksforgeeks.org/digital-logic/multiplexers-in-digital-logic/

<a id="s66"></a>
**S66. University of Vermont, Registers:** https://www.uvm.edu/~cbcafier/cs2210/content/05_cpu_alu/registers.html

<a id="s67"></a>
**S67. New Jersey Institute of Technology, Counters:** https://ecelabs.njit.edu/ece294/lab4.php

<a id="s68"></a>
**S68. New Jersey Institute of Technology, Shift Registers:** https://ecelabs.njit.edu/ece294/lab3.php

<a id="s69"></a>
**S69. University of Minnesota Duluth, Pipelining:** https://www.d.umn.edu/~gshute/arch/pipelining.html

<a id="s70"></a>
**S70. AMD UltraScale Architecture CLB User Guide, Asynchronous Clock Domain Crossing:** https://docs.amd.com/r/en-US/ug574-ultrascale-clb/Asynchronous-Clock-Domain-Crossing

<a id="s71"></a>
**S71. Georgia State University HyperPhysics, Digital Counters and Frequency Division:** https://hyperphysics.phy-astr.gsu.edu/hbase/Electronic/counter.html

<a id="s72"></a>
**S72. Intel Hyperflex Architecture High-Performance Design Handbook, Metastability Synchronizers:** https://www.intel.com/content/www/us/en/docs/programmable/683353/21-3/metastability-synchronizers.html

<a id="s73"></a>
**S73. Cadence RTL-to-GDSII Flow Training:** https://www.cadence.com/en_US/home/training/all-courses/86136.html

<a id="s74"></a>
**S74. Microchip PIC24F Family Reference Manual, Section 5 Data EEPROM:** https://ww1.microchip.com/downloads/en/DeviceDoc/39720b.pdf

<a id="s75"></a>
**S75. Accellera SystemVerilog 3.1a Language Reference Manual:** https://ece.uah.edu/~gaede/cpe526/SystemVerilog_3.1a.pdf

<a id="s76"></a>
**S76. cppreference, Range-based for loop:** https://www.cppreference.com/cpp/language/range-for

<a id="s77"></a>
**S77. Yue Guo, Sequence Detector 1001 Moore Machine and Mealy Machine:** https://yue-guo.com/2018/11/18/sequence-detector-1001-moore-machine-mealy-machine-overlapping-non-overlapping/

<a id="s78"></a>
**S78. MIT Computation Structures, Finite State Machines:** https://computationstructures.org/notes/fsms/notes.html

<a id="s79"></a>
**S79. UC Berkeley EECS 149/249A, State Machines and Circuits:** https://embedded.eecs.berkeley.edu/eecsx44/lectures/02-discrete-systems.pdf

<a id="s80"></a>
**S80. Intel FIFO FPGA IP User Guide:** https://www.intel.com/content/www/us/en/docs/programmable/683522/18-0/fifo-user-guide.html

<a id="s81"></a>
**S81. UC San Diego CSE 140B Lecture 6, Universal Gates and XOR Properties:** https://cseweb.ucsd.edu/classes/fa14/cse140-b/slides/lec6.pdf

<a id="s82"></a>
**S82. Toshiba Electronic Devices, Fanout of General-Purpose Logic ICs:** https://toshiba.semicon-storage.com/us/semiconductor/knowledge/faq/logic_common/logic_common_16.html

<a id="s83"></a>
**S83. Purdue ECE 270 Lecture Module 3, Set-Reset and Data Latches:** https://engineering.purdue.edu/~meyer/DDU270/Notes/PDF/2-Mod3_NQ_2019.pdf

<a id="s84"></a>
**S84. AMD Vivado Synthesis Guide UG901, Latch With Positive Gate and Asynchronous Reset Coding Verilog Example:** https://docs.amd.com/r/en-US/ug901-vivado-synthesis/Latch-With-Positive-Gate-and-Asynchronous-Reset-Coding-Verilog-Example

<a id="s85"></a>
**S85. Intel Quartus Prime Standard Edition User Guide, Inferring Latches Correctly:** https://www.intel.com/content/www/us/en/docs/programmable/683323/18-1/inferring-latches-correctly.html

<a id="s86"></a>
**S86. Intel/Altera Application Note 42, Metastability in Altera Devices:** https://cdrdv2-public.intel.com/653636/an042.pdf

<a id="s87"></a>
**S87. TechTarget, Nonvolatile Memory Definition:** https://www.techtarget.com/searchstorage/definition/nonvolatile-memory

<a id="s88"></a>
**S88. Samsung Semiconductor Glossary, ROM:** https://semiconductor.samsung.com/support/tools-resources/dictionary/semiconductor-glossary-rom/

<a id="s89"></a>
**S89. IBM Think, Flash Memory:** https://www.ibm.com/think/topics/flash-memory

<a id="s90"></a>
**S90. Synopsys, OTP Non-Volatile Memory Advantages:** https://www.synopsys.com/articles/non-volatile-memory.html

<a id="s91"></a>
**S91. Infineon, What is F-RAM:** https://www.infineon.com/knowledge-centre/what-is-f-ram-ferroelectric-ram

<a id="s92"></a>
**S92. TechTarget, MRAM Definition:** https://www.techtarget.com/whatis/definition/magnetic-storage

<a id="s93"></a>
**S93. IBM Research, Phase Change Memory:** https://research.ibm.com/blog/phase-change-memory

<a id="s94"></a>
**S94. TechTarget, ReRAM Definition:** https://www.techtarget.com/searchstorage/definition/RRAM-or-ReRAM-resistive-RAM

<a id="s95"></a>
**S95. Synopsys, Fusion Technology for RTL-to-GDSII Flow:** https://news.synopsys.com/2018-03-19-Synopsys-Introduces-Breakthrough-Fusion-Technology-to-Transform-the-RTL-to-GDSII-Flow

<a id="s96"></a>
**S96. Synopsys PrimeTime Static Timing Analysis:** https://www.synopsys.com/implementation-and-signoff/signoff/primetime.html

<a id="s97"></a>
**S97. Siemens Calibre Physical Verification:** https://www.siemens.com/en-us/products/ic/calibre-design/physical-verification/

<a id="s98"></a>
**S98. Siemens Calibre nmLVS:** https://www.siemens.com/en-us/products/ic/calibre-design/circuit-verification/nmlvs/

<a id="s99"></a>
**S99. Microchip Application Note AN601, EEPROM Endurance Tutorial:** https://ww1.microchip.com/downloads/en/appnotes/00601.pdf

<a id="s100"></a>
**S100. Microchip, Getting Started with SuperFlash Technology:** https://www.microchip.com/en-us/products/memory/serial-and-parallel-flash/getting-started

<a id="s101"></a>
**S101. MIT Computation Structures, Instruction Set Architectures:** https://computationstructures.org/notes/isas/notes.html

<a id="s102"></a>
**S102. MSOE Architecture Basics Notes, Address Bus and Data Bus:** https://faculty-web.msoe.edu/meier/ce1921/slidesets/archbasics-notes.pdf

<a id="s103"></a>
**S103. UC San Diego CSE140 Lecture 6, Universal Gates:** https://cseweb.ucsd.edu/classes/fa14/cse140-b/slides/lec6.pdf

<a id="s104"></a>
**S104. Georgia Tech ECE 2020 Examples, 2:1 and 4:1 MUX Using NAND Gates:** https://ece2020.ece.gatech.edu/examples/blocks/index.html

<a id="s105"></a>
**S105. Nexperia Logic Application Handbook:** https://assets.nexperia.com/documents/brochure/Nexperia_LOGIC_Handbook_201029.pdf

<a id="s106"></a>
**S106. University of Wisconsin CS758 Logical Effort Notes:** https://pages.cs.wisc.edu/~karu/courses/cs758/fall2011/handouts/lec-notes/cs758-logical-effort.pdf

<a id="s107"></a>
**S107. Intel Quartus Prime Design Recommendations, Avoid Combinational Loops:** https://www.intel.com/content/www/us/en/docs/programmable/683323/18-1/avoid-combinational-loops.html

<a id="s108"></a>
**S108. AMD UltraFast Design Methodology Guide UG949, Loops and Latch Loops:** https://docs.amd.com/r/en-US/ug949-vivado-design-methodology/Loops-and-Latch-Loops

<a id="s109"></a>
**S109. Intel Quartus Prime Design Recommendations, Following Synchronous FPGA Design Practices:** https://www.intel.com/content/www/us/en/docs/programmable/683323/18-1/following-synchronous-fpga-design-practices.html

<a id="s110"></a>
**S110. Intel Quartus Prime Design Recommendations, Avoid Ripple Counters:** https://www.intel.com/content/www/us/en/docs/programmable/683082/22-1/avoid-ripple-counters.html

<a id="s111"></a>
**S111. AMD Vivado Synthesis Guide UG901, 8-Bit Shift Register Coding Example One (Verilog):** https://docs.amd.com/r/2024.1-English/ug901-vivado-synthesis/8-Bit-Shift-Register-Coding-Example-One-Verilog

<a id="s112"></a>
**S112. AMD Vivado Synthesis Guide UG901, Half-Adder Example:** https://docs.amd.com/r/en-US/ug901-vivado-synthesis/Half-Adder-Example

<a id="s113"></a>
**S113. AMD UltraScale Libraries Guide UG974, FDRE Primitive:** https://docs.amd.com/r/2024.1-English/ug974-vivado-ultrascale-libraries/FDRE

<a id="s114"></a>
**S114. UC San Diego CSE140L Lab 2, Ring Oscillator with Odd Number of Inversions:** https://cseweb.ucsd.edu/classes/wi98/cse140l/lab02.htm

<a id="s115"></a>
**S115. Utah State University Microelectronics I Book, Static CMOS XOR Example:** https://left.engr.usu.edu/courses/3410/microelectronics_1_book.pdf

<a id="s116"></a>
**S116. Intel Quartus Prime Design Recommendations, Register Combinational Logic Outputs:** https://www.intel.com/content/www/us/en/docs/programmable/683082/22-3/register-combinational-logic-outputs.html

<a id="s117"></a>
**S117. Stanford EE386, Stuck-At Fault as a Logic Fault Model:** https://web.stanford.edu/class/ee386/public/stuck_at_fault_6per_page.pdf

<a id="s118"></a>
**S118. Brown CS300, Lecture 5 Arrays and Structures:** https://cs.brown.edu/courses/csci0300/s25/notes/l05/

<a id="s119"></a>
**S119. UTEP C Tutorial, Structures in C:** https://cs.utep.edu/isalamah/courses/5372/C-Tutorial.pdf

<a id="s120"></a>
**S120. Intel 8086 Family User's Manual:** https://bitsavers.org/components/intel/8086/9800722-03_The_8086_Family_Users_Manual_Oct79.pdf

<a id="s121"></a>
**S121. SIGC, Intel 8085 8-bit Microprocessor Notes:** https://www.sigc.edu/sigc/department/mca/studymet/Intel8085.pdf

<a id="s122"></a>
**S122. UMBC Lecture 13, Timing Analysis:** https://eclipse.umbc.edu/robucci/cmpeRSD/Lectures/Lecture13__TimingAnalysis/

<a id="s123"></a>
**S123. University of New Mexico VLSI II, The Inverter:** https://ece-research.unm.edu/jimp/vlsiII/slides/html/basic_inverter.html

<a id="s124"></a>
**S124. Sacramento State DFT Lecture Notes:** https://athena.ecs.csus.edu/~arad/csc273/lecture_notes/dft.pdf

<a id="s125"></a>
**S125. University of New Mexico, VLSI Design Verification and Test:** https://ece-research.unm.edu/jimp/vlsi_test/slides/html/intro.htm

<a id="s126"></a>
**S126. UMBC / Mentor Graphics, ASIC, FPGAs and Programmable Processors:** https://userpages.cs.umbc.edu/tinoosh/cmpe641/slides/ASIC-FPGA-processor.pdf

<a id="s127"></a>
**S127. University of New Mexico ECE321 Lecture 12, CMOS Inverter: Noise Margin and Delay Model:** https://ece-research.unm.edu/payman/classes/ECE321/lectures/lecture12.pdf

<a id="s128"></a>
**S128. Michigan State University ECE410 Memory Basics, Basic 6T SRAM Cell:** https://www.egr.msu.edu/classes/ece410/salem/files/s13/lectures/Ch13_SS_2010.pdf

<a id="s129"></a>
**S129. UC Davis EEC118 Lecture 13, SRAM Static Noise Margins:** https://www.ece.ucdavis.edu/~ramirtha/EEC118/S11/lecture13.pdf

<a id="s130"></a>
**S130. University of Washington EE/CSE371, Static Timing Analysis:** https://courses.cs.washington.edu/courses/cse371/24sp/lectures/11/EECSE371-Sp24-11-Timing.pdf

<a id="s131"></a>
**S131. AMD UltraScale Architecture Clocking Resources User Guide, Clock Buffers and Clock Routing:** https://docs.amd.com/r/en-US/ug572-ultrascale-clocking/Clock-Buffers-and-Clock-Routing

<a id="s132"></a>
**S132. AMD UltraScale CLB User Guide, Asynchronous Clock Domain Crossing:** https://docs.amd.com/r/en-US/ug574-ultrascale-clb/Asynchronous-Clock-Domain-Crossing

<a id="s133"></a>
**S133. AMD Vivado Synthesis Guide, Procedural Timing Controls:** https://docs.amd.com/r/2022.1-English/ug901-vivado-synthesis/Procedural-Timing-Controls

<a id="s134"></a>
**S134. UC Davis EEC118 Lecture 9, CMOS Design Guidelines and Stack Sizing:** https://www.ece.ucdavis.edu/~ramirtha/EEC118/S11/lecture9.pdf

<a id="s135"></a>
**S135. UC San Diego CSE140 Lecture 14, Adders:** https://cseweb.ucsd.edu/classes/sp19/cse140-a/slides/lec14Adders.pdf

<a id="s136"></a>
**S136. Synopsys, What is Synthesis?:** https://www.synopsys.com/glossary/what-is-synthesis.html

<a id="s137"></a>
**S137. Synopsys, Timing Constraints and SDC:** https://www.synopsys.com/blogs/chip-design/timing-constraints-signoff-flow.html

<a id="s138"></a>
**S138. Synopsys, Library Characterization and Liberty Format:** https://www.synopsys.com/glossary/what-is-library-characterization.html

<a id="s139"></a>
**S139. Texas Instruments, Latch-Up, ESD, and Other Phenomena:** https://www.ti.com/lit/an/slya014a/slya014a.pdf

<a id="s140"></a>
**S140. Synopsys, What is Electromigration?:** https://www.synopsys.com/glossary/what-is-electromigration.html

<a id="s141"></a>
**S141. Siemens Software, EM/IR Analysis in IC Layouts:** https://resources.sw.siemens.com/en-US/technical-paper-analyzing-em-ir-in-ic-design-layouts-to-ensure-reliability-and-performance

<a id="s142"></a>
**S142. Siemens, Concepts of Signal Integrity: Crosstalk:** https://resources.sw.siemens.com/sv-SE/white-paper-concepts-of-signal-integrity-crosstalk/

<a id="s143"></a>
**S143. Siemens Calibre, Plasma-Induced Damage and Antenna Effect:** https://blogs.sw.siemens.com/calibre/2024/02/08/why-pid-issues-matter-to-ic-chip-designers-and-how-to-combat-them/

<a id="s144"></a>
**S144. Cadence, Antenna Effect and Layout Fixes:** https://community.cadence.com/cadence_blogs_8/b/cic/posts/analog-layout-stop-the-antenna-effect-from-destroying-your-circuit

<a id="s145"></a>
**S145. Synopsys, What is Physical Design?:** https://www.synopsys.com/glossary/what-is-physical-design.html

<a id="s146"></a>
**S146. Cadence, Setting Up and Running CCOpt Clock Tree Synthesis:** https://support1.cadence.com/public/docs/content/20485809.html

<a id="s147"></a>
**S147. Intel, Accelerating Process Innovation Fact Sheet:** https://download.intel.com/newsroom/2021/client-computing/accelerating-process-innovation.pdf

<a id="s148"></a>
**S148. University of New Mexico ECE321 Lecture 15, CMOS Inverter Leakage Power:** https://www.unm.edu/~pzarkesh/ECE321/lectures/lecture15.pdf

<a id="s149"></a>
**S149. Purdue University, Modeling and Estimation of Total Leakage in Scaled CMOS Logic Circuits:** https://docs.lib.purdue.edu/ecetr/133/

<a id="s150"></a>
**S150. University of New Mexico, Introduction to Pipelining:** https://ece-research.unm.edu/jimp/611/slides/chap3_1.html

<a id="s151"></a>
**S151. University of Texas at San Antonio, Virtual Memory Lecture:** https://people.engr.tamu.edu/djimenez/taco/utsa-www/cs5513-fall07/lecture8.html

<a id="s152"></a>
**S152. University of Maryland, Pipeline Hazards:** https://www.cs.umd.edu/~meesh/411/CA-online/chapter/pipeline-hazards/index.html

<a id="s153"></a>
**S153. University of Maryland, Handling Data Hazards:** https://www.cs.umd.edu/~meesh/411/CA-online/chapter/handling-data-hazards/index.html

<a id="s154"></a>
**S154. Stanford CS101, Analog and Digital Signals:** https://web.stanford.edu/class/cs101/analog-digital-1.html

<a id="s155"></a>
**S155. UC Berkeley CS150, Verilog Wires and Regs:** https://msdnaa.eecs.berkeley.edu/~cs150/sp04/Lectures/05Verilog.pdf

<a id="s156"></a>
**S156. UC Riverside, Latches and Flip-Flops:** https://www.cs.ucr.edu/~ehwang/courses/cs120b/flipflops.pdf

<a id="s157"></a>
**S157. UC Berkeley / UNC, On Voting Machine Design for Verification and Testability:** https://www.cs.unc.edu/~csturton/papers/vvm-ccs09.pdf

<a id="s158"></a>
**S158. Georgia Tech, Floorplanning:** https://limsk.ece.gatech.edu/course/ece6133/slides/floorplanning.pdf

<a id="s159"></a>
**S159. University of Utah, Datapath Floorplanning and Routing in a Three Metal Layer Process:** https://my.eng.utah.edu/~cs6710/handouts/floorplanning_3LM.pdf

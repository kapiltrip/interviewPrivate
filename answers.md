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

**SystemVerilog improvement:**

In SystemVerilog, `always_comb` is preferred for combinational logic because it infers the sensitivity automatically and expresses the designer's intent more clearly. [[S14]](#s14)

**Speak like this:**

"A sensitivity list tells an always block when to execute. For combinational logic, it should include every signal read inside the block, so the output updates whenever an input changes. That is why `always @(*)` is preferred over manually listing signals. For sequential logic, the sensitivity list usually has the clock edge, and if reset is asynchronous, the reset edge is also included. In SystemVerilog, I would prefer `always_comb` for combinational logic and `always_ff` for clocked logic because they make the intent clearer."

[Back to index](./index.md)

<a id="q18"></a>
## 18. What is time borrowing?

**Written answer:**

Time borrowing is a latch-based timing technique. A level-sensitive latch remains transparent during its active clock level. If data arrives slightly late at that latch, the path can use part of the next stage's available time while the latch is still open. This is called borrowing time. [[S16]](#s16)

The important point is that borrowed time is not extra free time. If one path borrows time, the next path gets less time. So the total timing across the latch pipeline must still satisfy setup and hold requirements. [[S16]](#s16)

**Speak like this:**

"Time borrowing is a timing advantage of latch-based design. Since a latch is level sensitive, it stays transparent during the active clock level. If one path is slightly late, it can pass through the latch while the latch is still open and use some time from the next stage. But that borrowed time reduces the timing margin of the next path, so the overall pipeline timing must still be checked carefully."

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

**Definition to remember:** Verilog can describe hardware at different abstraction levels. Structural modeling describes the circuit by connecting gates or modules. Dataflow modeling describes logic using continuous assignments and expressions. Behavioral modeling describes operation using procedural blocks like `always` and `initial`. RTL is the synthesizable design style that describes registers and combinational logic between registers. A testbench is simulation-only verification code used to apply inputs and check outputs. [[S5]](#s5) [[S13]](#s13) [[S51]](#s51)

### Main Verilog modeling styles

| Style | Definition | Common constructs | Synthesizable? | Best used for |
|---|---|---|---|---|
| Structural modeling | Describes hardware by instantiating gates, primitives, or submodules and wiring them together | Gate primitives like `and`, `or`, `not`, module instantiation | Yes, if primitives/modules are synthesizable | Netlists, gate-level design, connecting blocks |
| Dataflow modeling | Describes logic as equations showing how outputs are continuously driven from inputs | `assign`, operators like `&`, `|`, `^`, `?:` | Usually yes for combinational logic | Combinational equations, muxes, adders, Boolean logic |
| Behavioral modeling | Describes what the circuit does using procedural statements | `always`, `initial`, `if`, `case`, loops, tasks | Depends on constructs | Algorithms, FSMs, sequential/combinational RTL, simulation models |
| RTL modeling | Synthesizable register-transfer description of hardware | `always @(posedge clk)`, `always @(*)`, `assign`, registers, next-state logic | Yes, when written in synthesizable style | Actual FPGA/ASIC design |
| Testbench modeling | Simulation code that verifies the design under test | `initial`, `#` delays, clock generation, `$display`, `$monitor`, `$finish` | Usually no | Applying stimulus and checking outputs |
| Switch-level modeling | Low-level transistor/switch description | `nmos`, `pmos`, `cmos`, `tran`, `pullup`, `pulldown` | Not normal RTL flow | Teaching, device/switch-level experiments |

### 1. Structural modeling

**Definition:** Structural modeling describes the exact interconnection of hardware blocks. Instead of writing an equation directly, we instantiate gates or modules and connect wires between them. Verilog supports gate primitives and module instantiation for this style. [[S5]](#s5) [[S51]](#s51)

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

**Interview point:** Structural code tells the tool, "use these blocks and connect them like this." It is close to a circuit diagram or netlist.

### 2. Dataflow modeling

**Definition:** Dataflow modeling describes logic using continuous assignments. The left-hand side is continuously driven by the expression on the right-hand side, and whenever an input in the expression changes, the output is recomputed. [[S5]](#s5) [[S51]](#s51)

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

**Interview point:** Dataflow style is very common for combinational logic because it directly expresses Boolean equations and data movement.

### 3. Behavioral modeling

**Definition:** Behavioral modeling describes the behavior or algorithm of the circuit using procedural blocks such as `always` and `initial`. It focuses more on "what should happen" than on directly listing gates. [[S5]](#s5) [[S51]](#s51)

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

**Important:** Behavioral code can be synthesizable or non-synthesizable. If it uses synthesizable constructs and describes real hardware, it can become RTL. If it uses delays, file operations, or pure simulation constructs, it is not normal RTL.

### 4. RTL code

**Definition:** RTL means Register Transfer Level. It describes how data is stored in registers and how combinational logic computes the next values transferred between registers. RTL is the normal synthesizable coding level used for FPGA/ASIC design. [[S13]](#s13)

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

**Interview point:** RTL is not a separate Verilog keyword. It is a design style. RTL commonly uses behavioral procedural blocks and dataflow assignments, but it must be written so synthesis can infer real hardware.

### 5. Testbench code

**Definition:** A testbench is not the hardware design itself. It is simulation code that instantiates the design under test, generates inputs, drives clocks/resets, observes outputs, and checks whether the design behaves correctly. [[S5]](#s5) [[S13]](#s13)

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

### Quick identification

1. If code instantiates gates or submodules, it is structural.
2. If code uses `assign` equations, it is dataflow.
3. If code uses `always`, `initial`, `if`, `case`, or loops, it is behavioral/procedural.
4. If behavioral/dataflow code describes real registers and combinational logic for synthesis, it is RTL.
5. If code generates stimulus, clocks, checks outputs, uses `#` delays, `$display`, `$monitor`, or `$finish`, it is testbench.

**Important interview distinction:**

Behavioral, dataflow, and structural are modeling styles. RTL is a synthesizable abstraction level used for real design. A testbench is verification code, not the design. One Verilog file can also mix styles. For example, an RTL module may use `always @(posedge clk)` for registers, `assign` for combinational logic, and module instantiation structurally to connect sub-blocks.

**Speak like this:**

"Verilog has different modeling styles. Structural modeling describes hardware by instantiating gates or submodules and connecting wires. Dataflow modeling uses continuous `assign` statements to describe Boolean equations or data movement. Behavioral modeling uses procedural blocks like `always` and `initial` with `if`, `case`, and loops to describe behavior. RTL is the synthesizable register-transfer style where I describe flip-flops, registers, and combinational logic between them. Testbench code is different: it is not the hardware design; it is simulation code used to generate clocks, apply stimulus, and check outputs. So behavioral, dataflow, and structural are ways to describe hardware, RTL is the synthesizable design level, and testbench is for verification."

[Back to index](./index.md)

<a id="q48"></a>
## 48. Difference between `always` and `initial` block.

**Written answer:**

**Definition to remember:** In Verilog, `initial` and `always` are procedural blocks. An `initial` block starts at simulation time 0 and executes once. An `always` block also starts at simulation time 0, but after reaching the end of the block it repeats forever, so it must contain some timing control such as an event control `@(...)`, a delay `#...`, or a wait condition to stop it from executing continuously at the same simulation time. [[S5]](#s5) [[S14]](#s14) [[S52]](#s52)

| Point | `initial` block | `always` block |
|---|---|---|
| Execution count | Runs once | Repeats forever |
| Start time | Starts at simulation time 0 | Starts at simulation time 0 |
| What happens after end | Stops permanently | Jumps back to the beginning of the block |
| Timing control | Optional | Required in practice, otherwise zero-time loop can happen |
| Common RTL use | Generally avoided in ASIC RTL; limited FPGA initialization cases | Main block for combinational and sequential RTL |
| Common testbench use | Initialization, stimulus, file setup, reset sequence | Clock generation, monitors, repeated stimulus |
| Synthesizable? | Usually not for ASIC RTL; limited synthesis support in FPGA flows | Synthesizable when written as proper RTL |
| Typical examples | `initial begin ... end` | `always @(posedge clk)`, `always @(*)`, `always #5 clk = ~clk` |

**Key idea:**

```text
initial = run once
always  = run forever
```

Because `always` runs forever, it must include something that advances simulation time or waits for an event.

**`initial` example:**

```verilog
initial begin
    rst = 1'b1;
    #20 rst = 1'b0;
end
```

This runs once in simulation.

**`initial` in testbench:**

```verilog
initial begin
    clk = 1'b0;
    rst = 1'b1;
    #20 rst = 1'b0;
    #100 $finish;
end
```

This is typical testbench code because it uses delays and `$finish`.

**`always` example for sequential RTL:**

```verilog
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

This runs on every positive clock edge.

**`always` example for combinational RTL:**

```verilog
always @(*) begin
    y = (a & b) | c;
end
```

This runs whenever any right-hand-side signal changes.

**Why an `always` block without delay/event control creates a zero-time infinite loop:**

An `always` block without delay or event control can create an infinite zero-time loop in simulation:

```verilog
always begin
    clk = ~clk;   // bad without delay
end
```

Reason:

1. At simulation time 0, the `always` block starts.
2. `clk = ~clk` executes immediately.
3. There is no `#delay`, no `@(event)`, and no `wait`, so simulation time does not advance.
4. The block reaches `end`.
5. Because it is an `always` block, it immediately starts again.
6. It toggles `clk` again at the same simulation time.
7. This repeats forever at time 0, so the simulator hangs and time cannot move forward. [[S52]](#s52)

In short:

```text
always repeats forever + no timing control = infinite loop at the same simulation time
```

Correct testbench clock:

```verilog
always #5 clk = ~clk;
```

Here, `#5` delays each execution by 5 time units. So simulation time advances:

```text
time 0  -> clk toggles
time 5  -> clk toggles
time 10 -> clk toggles
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

**RTL use of `always`:**

1. **Sequential logic:**

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This waits for a clock edge. It infers a flip-flop.

2. **Combinational logic:**

```verilog
always @(*) begin
    y = (a & b) | c;
end
```

This waits for changes in the signals used in the block. It infers combinational logic if all outputs are assigned in all cases.

3. **Testbench clock:**

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

3. Using `initial` as if it creates hardware behavior in ASIC RTL.
   In most RTL design, `initial` is for simulation/testbench, not normal synthesized hardware.

**Speak like this:**

"The `initial` block starts at simulation time zero and runs only once, so I mainly use it in testbenches for initialization, reset stimulus, and `$finish`. The `always` block also starts at time zero, but it repeats forever. Because of that, it must have timing control like `@(posedge clk)`, `@(*)`, or `#5`. If I write `always begin clk = ~clk; end`, there is no delay or event wait, so the block toggles `clk`, reaches the end, immediately restarts, and keeps repeating at the same simulation time. Time never advances, so the simulator hangs in a zero-time infinite loop. For RTL, I use `always @(posedge clk)` for flip-flops and `always @(*)` for combinational logic. For a testbench clock, I use `always #5 clk = ~clk` or `forever #5 clk = ~clk` inside an `initial` block."

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

**Definition to remember:** Every real gate has propagation delay, including XOR. But in normal RTL/digital design, XOR should not be used as a reliable delay element because gate delay is technology, voltage, temperature, synthesis, placement, and routing dependent. [[S4]](#s4)

**Short answer:**

Technically, an XOR gate has delay, so a signal passing through it is delayed. But practically, we should not design timing by intentionally using XOR as a delay element in normal RTL.

**Why it is not recommended:**

1. **Synthesis may optimize it away:** If you write `A xor 0`, synthesis may replace it with just `A`.
2. **Delay is not fixed:** Gate delay changes with process, voltage, temperature, load, and routing.
3. **Poor portability:** The same RTL can have different delays on FPGA, ASIC, and different libraries.
4. **Timing should be controlled properly:** Use clocked design, STA constraints, buffers/delay cells, or vendor primitives where delay is truly required.
5. **XOR can glitch:** XOR output can glitch when inputs change at different times, so it is risky as a timing element.

**Where XOR may appear in timing-related circuits:**

XOR gates are sometimes used in phase detectors, edge detectors, parity circuits, or custom delay/measurement circuits. But that is different from relying on a random XOR gate as a stable delay in synthesizable RTL.

**Speak like this:**

"An XOR gate has propagation delay like any real gate, but I should not use it as a reliable delay element in normal RTL design. The delay can change with technology, voltage, temperature, load, routing, and synthesis optimization. If I write `A xor 0`, the tool may even optimize it into a wire. So for real delay requirements, I should use proper timing constraints, registers, buffers or dedicated delay cells, not a random XOR gate."

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

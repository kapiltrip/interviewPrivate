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

1. **Ease of implementation:** NAND gates are simple and very common in CMOS standard-cell libraries. Designers often use NAND-based logic because it maps efficiently into practical circuits.
2. **Transistor structure:** In a CMOS NAND gate, the PMOS transistors are in parallel and the NMOS transistors are in series. In a CMOS NOR gate, the PMOS transistors are in series and the NMOS transistors are in parallel. Since PMOS devices are generally weaker/slower than NMOS devices, series PMOS in NOR usually makes the pull-up path slower or larger. [[S10]](#s10)
3. **Size and power:** To make a NOR gate as fast as a NAND gate, the series PMOS devices may need to be made larger. Larger transistors can increase area and capacitance, which can affect power and delay.
4. **Performance:** NAND gates often have better delay characteristics in CMOS because their weaker PMOS devices are not stacked in series.
5. **Design style:** The final choice also depends on the standard-cell library, available cells, fan-in, loading, and the Boolean expression being implemented.
6. **Application requirement:** Some logic functions naturally map better to NOR, so NOR is still used where it gives a cleaner or faster implementation.

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

"Both NAND and NOR are universal gates, so logically both can implement any Boolean function. But in CMOS design, NAND is usually preferred. The reason is transistor implementation: in NAND, PMOS transistors are in parallel, while in NOR, PMOS transistors are in series. Since PMOS devices are weaker than NMOS devices, series PMOS makes NOR slower or larger. So NAND often gives better speed and area. Still, the final choice depends on the Boolean function, standard-cell library, power, delay, and application requirement."

[Back to index](./index.md)

<a id="q26"></a>
## 26. Explain delay models in digital circuits and gates.

**Written answer:**

**Definition to remember:** A delay model describes how much time a signal transition takes to propagate through a gate, wire, combinational circuit, or flip-flop. [[S4]](#s4)

In real digital circuits, outputs do not change instantly when inputs change. Gates have internal transistor delay, wires have resistance and capacitance, and flip-flops have clock-to-Q delay. Delay modeling is used to estimate whether a circuit can meet timing.

**Important delay terms:**

1. **Propagation delay:** Maximum time after an input change for the output to become valid. This is used for setup timing.
2. **Contamination delay:** Minimum time after an input change before the output may start changing. This is used for hold timing.
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

**Definition to remember:** In interview terms, a BJT is usually treated as a current-controlled device because a small base current controls a larger collector current. A MOSFET is usually treated as a voltage-controlled device because the gate-to-source voltage controls the channel and drain current. [[S22]](#s22)

| Point | BJT | MOSFET |
|---|---|---|
| Full form | Bipolar Junction Transistor | Metal-Oxide-Semiconductor Field-Effect Transistor |
| Terminals | Base, emitter, collector | Gate, source, drain |
| Control | Current-controlled device | Voltage-controlled device |
| Input | Base current controls collector current | Gate voltage controls drain current |
| Input impedance | Lower input impedance | Very high input impedance |
| Carrier type | Bipolar device, uses electrons and holes | Unipolar device, mainly one carrier type |
| Drive power | Needs continuous base current | Gate needs very little DC current ideally |
| Speed/switching | Can have charge-storage delay | Often better for fast digital switching |
| Common use | Analog amplification, current gain, some switching | CMOS logic, power switching, digital ICs |
| Power applications | Used, but less common in modern power switching | Very common for high-power/high-speed switching |

**Important points:**

1. A BJT has three terminals: base, emitter, and collector.
2. A MOSFET has three main terminals: gate, source, and drain. It may also have a body/substrate terminal.
3. BJT operation depends on current at the base terminal.
4. MOSFET operation depends mainly on voltage at the insulated gate electrode.
5. MOSFETs are more common in modern digital circuits because CMOS gives high density and low static power.
6. BJTs are still useful where high current gain, analog amplification, or certain analog characteristics are needed.

**Speak like this:**

"A BJT is a bipolar device with base, emitter, and collector terminals. In normal interview language, we treat it as current controlled because a small base current controls collector current. A MOSFET has gate, source, and drain terminals, and we treat it as voltage controlled because gate voltage controls the channel. MOSFETs have very high input impedance and are widely used in CMOS digital circuits and power switching. BJTs are still useful in analog amplification and current-gain applications."

[Back to index](./index.md)

<a id="q29"></a>
## 29. What gates are used in Verilog? What is a universal gate? Draw OR/NOR truth table and design NOR using OR/AND.

**Written answer:**

**Definition to remember:** Verilog gate primitives are built-in gate-level keywords used to model logic gates directly. Examples include `and`, `or`, `nand`, `nor`, `xor`, `xnor`, `not`, and `buf`. [[S5]](#s5)

**Common gates used in Verilog:**

```text
and, or, nand, nor, xor, xnor, not, buf
```

Verilog also has tri-state gate primitives such as:

```text
bufif0, bufif1, notif0, notif1
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

**Definition to remember:** In a Mealy machine, the output depends on the present state and the present input. For a sequence detector, the FSM moves through states that represent how much of the target sequence has already been matched. [[S2]](#s2) [[S23]](#s23)

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

**Definition to remember:** A microprocessor is mainly a CPU on a chip and normally needs external memory and I/O to make a full system. A microcontroller integrates a CPU, memory, and peripherals on one chip for embedded control applications. [[S24]](#s24)

| Point | Microprocessor | Microcontroller |
|---|---|---|
| Basic idea | CPU-focused chip | Small computer/control system on one chip |
| Main components | CPU mainly | CPU + memory + I/O + timers/peripherals |
| External components | Needs external RAM, ROM/flash, and I/O support | Many required blocks are already on chip |
| Application | General-purpose computing | Embedded and dedicated control |
| System size | Usually larger system | Usually compact system |
| Power | Usually higher system power | Usually lower power for embedded tasks |
| Cost | Higher total system cost because external chips are needed | Lower for small embedded systems |
| Performance focus | High processing power and flexibility | Control, real-time response, low power, low cost |
| Examples | PC/laptop processors, application processors | 8051, AVR, PIC, ARM Cortex-M MCUs |
| Used in | Computers, phones, high-end OS-based systems | Washing machines, remotes, sensors, motor control, IoT |

**Interview nuance:**

Modern chips can blur the boundary because many application processors include memory controllers and peripherals. But for interview basics, use the traditional distinction: microprocessor means CPU-centric; microcontroller means CPU plus memory and peripherals integrated for embedded control.

**Speak like this:**

"A microprocessor is mainly a CPU, so memory and I/O are generally connected externally to build a complete system. It is used where high processing power and flexibility are needed, like computers. A microcontroller integrates CPU, memory, I/O ports, timers, and peripherals on a single chip. So it is compact, low cost, and low power, which makes it suitable for embedded applications like washing machines, sensors, and control systems."

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

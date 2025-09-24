# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```verilog
module sr_ff (
    input wire S, R, clk,
    output reg Q
);
    always @(posedge clk) begin
        if (S && ~R)
            Q <= 1;
        else if (~S && R)
            Q <= 0;
        else if (~S && ~R)
            Q <= Q; // No change
        else
            Q <= 1'bx; // Invalid condition
    end
endmodule
```
### SR Flip-Flop Test bench 
```
module tb_sr_ff;
    reg S, R, clk;
    wire Q;

    sr_ff uut (.S(S), .R(R), .clk(clk), .Q(Q));

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        S = 0; R = 0;
        #10 S = 1; R = 0;
        #10 S = 0; R = 1;
        #10 S = 0; R = 0;
        #10 S = 1; R = 1;
        #10 $finish;
    end
endmodule



```
#### SIMULATION OUTPUT

<img width="1920" height="1080" alt="Screenshot 2025-09-24 084532" src="https://github.com/user-attachments/assets/8efba0d7-383a-4038-8512-cbf9466fe299" />

---

### JK Flip-Flop (Non Blocking)
```verilog
module jk_ff (
    input wire J, K, clk,
    output reg Q
);
    always @(posedge clk) begin
        case ({J, K})
            2'b00: Q <= Q;
            2'b01: Q <= 0;
            2'b10: Q <= 1;
            2'b11: Q <= ~Q;
        endcase
    end
endmodule


```
### JK Flip-Flop Test bench 
```verilog
module tb_jk_ff;
    reg J, K, clk;
    wire Q;

    jk_ff uut (.J(J), .K(K), .clk(clk), .Q(Q));

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        J = 0; K = 0;
        #10 J = 1; K = 0;
        #10 J = 0; K = 1;
        #10 J = 1; K = 1;
        #10 J = 0; K = 0;
        #10 $finish;
    end
endmodule


```
#### SIMULATION OUTPUT
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/37ec0f96-9994-43f6-8653-8b463a7491b3" />

---
### D Flip-Flop (Non Blocking)
```verilog
module d_ff (
    input wire d, clk,
    output reg Q
);
    always @(posedge clk) begin
        Q <= d;
    end
endmodule

```
### D Flip-Flop Test bench 
```verilog
module tb_d_ff;
    reg d, clk;
    wire Q;

    d_ff uut (.d(d), .clk(clk), .Q(Q));

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        d = 0;
        #10 d = 1;
        #10 d = 0;
        #10 d = 1;
        #10 $finish;
    end
endmodule



```

#### SIMULATION OUTPUT
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6cc83ced-bc09-4bc9-94a8-7c61e42d8015" />

---
### T Flip-Flop (Non Blocking)
```verilog
module t_ff (
    input wire T, clk,
    output reg Q
);
    always @(posedge clk) begin
        if (T)
            Q <= ~Q;
        else
            Q <= Q;
    end
endmodule



endmodule
```
### T Flip-Flop Test bench 
```verilog
module tb_t_ff;
    reg T, clk;
    wire Q;

    t_ff uut (.T(T), .clk(clk), .Q(Q));

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        T = 0;
        #10 T = 1;
        #10 T = 1;
        #10 T = 0;
        #10 $finish;
    end
endmodule



```

#### SIMULATION OUTPUT
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8844f6c5-0b47-4c1c-afce-eda09ff24254" />

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.

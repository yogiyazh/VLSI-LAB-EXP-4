# VLSI-LAB-EXP-4
# 4.SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

# APPARATUS REQUIRED:

Vivado 2023.1

**LOGIC DIAGRAM**

# SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


# JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

# T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


# D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


# COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  
# PROCEDURE:
1.Open Vivado: Launch Xilinx Vivado software on your computer.

2.Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3.Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4.Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5.Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6.Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7.Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8.Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9.View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# VERILOG CODE
# D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```
# JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)�        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# Ripple Carry Counter
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dffø(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# MOD 10 Counter
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```


# OUTPUT WAVEFORM
 # D Flip Flop
 ![322413931-0aeeb1ce-64b7-48e0-bcbd-efbf6bf0010d](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/d536b57c-192a-4ce4-8cde-8e1b1bd502fd)
![329835657-49b17a40-5e44-4b19-9ade-7e72da51b51c](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/02f33ce9-5fd9-47ca-a10a-1667e63e169d)
# JK Flip flop
![322414053-f58c6b39-81b3-400f-b2e6-5df43dd4f4ce](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/1d803298-edcb-4d4f-b820-7c54a9f80d31)
![329835667-f8278a33-6719-4434-b2cf-752a62d60552](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/fd9fb3b2-2307-4323-b6df-e7d1626d23b9)
# SR Flip Flop
![322414218-c3f2b9c5-897f-48ef-b12d-2f446de70cb8](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/fd5fdf23-8ec0-4fff-ac53-4bfbd0458e0d)
![329835760-48ce566a-5f76-41c5-a147-39353db15a83](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/e85abbef-f4ab-41d5-90a6-eb0218609865)
# T Flip FLop
![322414353-5bae902d-bc9e-48f1-b32c-fdb06441a797](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/78a2b562-2ad2-4ca3-aa6c-bf69068e70b6)
![329835752-d4b02fe0-f188-408b-be45-3dfa967359f0](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/2e78610a-5b28-4f83-b29c-6c09858c7364)
# Mod 10 Counter
![329835479-e1f376cc-deb6-4ea8-8f4d-0d347429447f](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/a531cd78-aff1-4fd1-9de7-257b31bbf0d1)
![329835686-83841e49-e0f4-446f-931a-0c3501d5ed0f](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/e9bf49e6-379a-4cf8-a31b-7cb00e0ad70a)
# Ripple Carry Counter
![329835712-4d0b64e6-9811-4969-bebd-aaa05597da58](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/d5871ace-343b-4b8d-9794-754b42c95948)
![329835726-e12abde7-abf5-4075-b5bb-0d99e499aede](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/ac90bd50-d288-4774-ae21-b49ca0f85928)
# Up Down Counter
![329835797-d629cb59-9ff8-42d8-9964-00c03b8bc3a8](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/56d2f88d-2092-4e7e-a216-6436c93af5d7)
![329835809-8a98119f-44b4-4a45-8807-098f03ab6c4a](https://github.com/yogiyazh/VLSI-LAB-EXP-4/assets/159939338/88c9853d-71ce-46a1-8b95-8d716b9e6d18)

# RESULT:
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.



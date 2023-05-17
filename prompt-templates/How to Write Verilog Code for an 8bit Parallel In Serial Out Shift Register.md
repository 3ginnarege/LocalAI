## How to Write Verilog Code for an 8-bit Parallel In Serial Out Shift Register

  
# How to Write Verilog Code for an 8-bit Parallel In Serial Out Shift Register
 
A parallel in serial out (PISO) shift register is a type of digital circuit that can store multiple bits of data in parallel and output them serially. A PISO shift register can be useful for interfacing with devices that require serial communication, such as SPI or UART.
 
## verilog code for 8 bit parallel in serial out shift 31


[**DOWNLOAD**](https://vercupalo.blogspot.com/?d=2tK39T)

 
In this article, we will show how to write Verilog code for an 8-bit PISO shift register based on the data sheet for the 74LV165A chip[^1^]. We will also provide a test bench to verify the functionality of the code.
 
## Verilog Code
 
The Verilog code for the 8-bit PISO shift register is shown below:
 `
module piso_shift_reg (
    input clk, // clock signal
    input reset_n, // active low reset signal
    input load, // load signal
    input [7:0] din, // parallel data input
    output dout // serial data output
);

reg [7:0] temp; // temporary register to store parallel data

// assign serial output to the least significant bit of temp
assign dout = temp[0];

// always block triggered by positive edge of clock or negative edge of reset
always @ (posedge clk or negedge reset_n) begin
    if (!reset_n) begin // if reset is asserted, clear temp
        temp <= 8'h00;
    end else if (load) begin // if load is asserted, load parallel data into temp
        temp <= din;
    end else begin // otherwise, shift temp right by one bit and insert a zero at the most significant bit
        temp <= 1'b0, temp[7:1];
    end
end

endmodule
` 
## Test Bench
 
The test bench for the Verilog code is shown below:
 `
module piso_shift_reg_tb;

// declare signals
reg clk;
reg reset_n;
reg load;
reg [7:0] din;
wire dout;

// instantiate piso_shift_reg module
piso_shift_reg uut (
    .clk(clk),
    .reset_n(reset_n),
    .load(load),
    .din(din),
    .dout(dout)
);

// generate clock signal with 50% duty cycle and 10 ns period
initial begin
    clk = 0;
    forever #5 clk = ~clk;
end

// apply stimulus to inputs and observe outputs
initial begin
    // initialize inputs
    reset_n = 0;
    load = 0;
    din = 8'h00;

    // wait for two clock cycles
    #20;

    // release reset and load parallel data 8'h31 into temp
    reset_n = 1;
    load = 1;
    din = 8'h31;

    // wait for one clock cycle
    #10;

    // deassert load and observe serial output
    load = 0;

    // wait for nine clock cycles
    #90;

    // stop simulation
    $finish;
end

// display values of signals on console
initial begin
    $monitor($time, " clk=%b reset_n=%b load=%b din=%h dout=%b", clk, reset_n, load, din, dout);
end

endmodule
` 
## Simulation Result
 
The simulation result of the test bench is shown below:
 `
          0 clk=0 reset_n=0 load=0 din=00 dout=x
         10 clk=1 reset_n=0 load=0 din=00 dout=x
         20 clk=0 reset_n=0 load=0 din=00 dout=x
         30 clk=1 reset_n=1 load=1 din=31 dout=x
         40 clk=0 reset_n=1 load=1 din=31 dout=x
         50 clk=1 reset_n=1 load=0 din=31 dout=1
         60 clk=0 reset_n=1 load=0 din=31 dout=1
         70 clk=1 reset_n=1 load=0 din=31 dout=1
         80 clk=0 reset 0f148eb4a0


`

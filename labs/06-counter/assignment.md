# Lab 6: Martin Paseka

## Preparation tasks (done before the lab at home)

The Nexys A7 board provides five push buttons for user applications.

1. See [schematic](https://github.com/tomas-fryza/digital-electronics-1/blob/master/docs/nexys-a7-sch.pdf) or [reference manual](https://reference.digilentinc.com/reference/programmable-logic/nexys-a7/reference-manual) of the Nexys A7 board and find out the connection of these push buttons, ie to which FPGA pins are connected and how. What logic/voltage value do the buttons generate when not pressed and what value when the buttons are pressed? Draw the schematic with push buttons.

2. Calculate how many periods of clock signal with frequency of 100&nbsp;MHz contain time intervals 2&nbsp;ms, 4&nbsp;ms, 10&nbsp;ms, 250&nbsp;ms, 500&nbsp;ms, and 1&nbsp;s. Write values in decimal, binary, and hexadecimal forms.

   ![image](https://user-images.githubusercontent.com/99723445/159370562-26adf639-4bd7-44ba-b35a-63e4a662bede.png)
   <!--
   https://editor.codecogs.com/
   T_{clk}=\frac{1}{f_{clk}}=
   \textup{number of clk period} = \frac{\textup{time interval}}{T_{clk}}=
   -->

   | **Time interval** | **Number of clk periods** | **Number of clk periods in hex** | **Number of clk periods in binary** |
   | :-: | :-: | :-: | :-: |
   | 2 ms | 200 000 | x"3_0d40" | b"0011_0000_1101_0100_0000" |
   | 4 ms | 400 000 | x"6_1A80" | b"0110_0001_1010_1000_0000" |
   | 10 ms | 1 000 000 | x"F_4240" | b"1111_0100_0010_0100_0000" |
   | 250 ms | 25 000 000 | x"17D_7840" | b"0001_0111_1101_0111_1000_0100_0000" |
   | 500 ms | 50 000 000 | x"2FA_F080" | b"0010_1111_1010_1111_0000_1000_0000" |
   | 1 sec | 100 000 000 | x"5F5_E100" | b"0101_1111_0101_1110_0001_0000_0000" |

<a name="part1"></a>

### Bidirectional counter

1. Listing of VHDL code of the completed process `p_cnt_up_down`. Always use syntax highlighting, meaningful comments, and follow VHDL guidelines:

```vhdl
    --------------------------------------------------------
    -- p_cnt_up_down:
    -- Clocked process with synchronous reset which implements
    -- n-bit up/down counter.
    --------------------------------------------------------
    p_cnt_up_down : process(clk)
    begin
        if rising_edge(clk) then
        
            if (reset = '1') then   -- Synchronous reset
                s_cnt_local <= (others => '0'); -- Clear all bits

            elsif (en_i = '1') then -- Test if counter is enabled
                if(cnt_up_i = '1') then
                    s_cnt_local <= s_cnt_local + 1;
                    
                elsif(cnt_up_i = '0') then
                    s_cnt_local <= s_cnt_local - 1;
       
                end if;
            end if;
        end if;
    end process p_cnt_up_down;
```

2. Screenshot with simulated time waveforms. Test reset as well. Always display all inputs and outputs (display the inputs at the top of the image, the outputs below them) at the appropriate time scale!

   ![image](https://user-images.githubusercontent.com/99723445/159506945-83d4e1c6-62f8-4f78-ada8-cba4c6f43b8a.png)

![image](https://user-images.githubusercontent.com/99723445/159514440-ca256815-f5f2-4e8d-9641-c06846b30eac.png)

### Two counters

1. Image of the top layer structure including both counters, ie a 4-bit bidirectional counter from *Part 4* and a 16-bit counter with a 10 ms time base from *Experiments on your own*. The image can be drawn on a computer or by hand. Always name all inputs, outputs, components and internal signals!

   ![image](https://user-images.githubusercontent.com/99723445/160469500-9467d133-413d-4c96-808c-577f8fa05334.png)

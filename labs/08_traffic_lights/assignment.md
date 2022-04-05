# Lab 8: Martin Paseka

## Preparation tasks (done before the lab at home)

1. See [schematic](https://github.com/tomas-fryza/digital-electronics-1/blob/master/docs/nexys-a7-sch.pdf) or [reference manual](https://reference.digilentinc.com/reference/programmable-logic/nexys-a7/reference-manual) of the Nexys A7 board and find out the connection of two RGB LEDs, ie to which FPGA pins are connected and how. How you can control them to get red, yellow, or green colors? Draw the schematic with RGB LEDs.

| **RGB LED** | **Artix-7 pin names** | **RED** | **Yellow** | **Green** |
| :-: | :-: | :-: | :-: | :-: |
| LD16 | N15, M16, R12 | 1, 0, 0 | 1, 1, 0 | 0, 1, 0 |
| LD17 | N16, R11, G14 | 1, 0, 0 | 1, 1, 0 | 0, 1, 0 |

2. See [schematic](https://github.com/tomas-fryza/digital-electronics-1/blob/master/docs/nexys-a7-sch.pdf) or [reference manual](https://reference.digilentinc.com/reference/programmable-logic/nexys-a7/reference-manual) of the Nexys A7 board and find out to which FPGA pins Pmod ports JA, JB, JC, and JD are connected.

![image](https://user-images.githubusercontent.com/99723445/161537583-ed2d5c71-ebca-4b0c-af21-6e416ea3bad3.png)

### Traffic light controller

1. Figure of traffic light controller state diagram. The image can be drawn on a computer or by hand. Always name all states, transitions, and input signals!

   ![your figure]()

2. Listing of VHDL code of the completed process `p_traffic_fsm`. Always use syntax highlighting, meaningful comments, and follow VHDL guidelines:

```vhdl
    p_traffic_fsm : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then   -- Synchronous reset
                s_state <= STOP1;   -- Set initial state
                s_cnt   <= c_ZERO;  -- Clear delay counter

            elsif (s_en = '1') then
                -- Every 250 ms, CASE checks the value of the s_state 
                -- variable and changes to the next state according 
                -- to the delay value.
                case s_state is

                    -- If the current state is STOP1, then wait 1 sec
                    -- and move to the next GO_WAIT state.
                    when STOP1 =>
                        -- Count up to c_DELAY_1SEC
                        if (s_cnt < c_DELAY_1SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= WEST_GO;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;

                    when WEST_GO =>
                        if (s_cnt < c_DELAY_4SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            
                            s_state <= WEST_WAIT;
                                                      
                            s_cnt <= c_ZERO;
                        end if;
                        
                     when WEST_WAIT =>
                        if (s_cnt < c_DELAY_2SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            
                            s_state <= STOP2;
                                                      
                            s_cnt <= c_ZERO;
                        end if;
                        
                     when STOP2 =>
                        if (s_cnt < c_DELAY_1SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            
                            s_state <= SOUTH_GO;
                                                      
                            s_cnt <= c_ZERO;
                        end if;
                     
                     when SOUTH_GO =>
                        if (s_cnt < c_DELAY_4SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            
                            s_state <= SOUTH_WAIT;
                                                      
                            s_cnt <= c_ZERO;
                        end if;

                    when SOUTH_WAIT =>
                        if (s_cnt < c_DELAY_2SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            
                            s_state <= STOP1;
                                                      
                            s_cnt <= c_ZERO;
                        end if;
                    -- It is a good programming practice to use the 
                    -- OTHERS clause, even if all CASE choices have 
                    -- been made.
                    when others =>
                        s_state <= STOP1;
                        s_cnt   <= c_ZERO;
                end case;
            end if; -- Synchronous reset
        end if; -- Rising edge
    end process p_traffic_fsm;

    --------------------------------------------------------
    -- p_output_fsm:
    -- The combinatorial process is sensitive to state
    -- changes and sets the output signals accordingly.
    -- This is an example of a Moore state machine and
    -- therefore the output is set based on the active state.
    --------------------------------------------------------
    p_output_fsm : process(s_state)
    begin
        case s_state is
            when STOP1 =>
                south_o <= c_RED;
                west_o  <= c_RED;
            when WEST_GO =>
                south_o <= c_RED;
                west_o  <= c_GREEN;
            when WEST_WAIT =>
                south_o <= c_RED;
                west_o  <= c_YELLOW;
            when STOP2 =>
                south_o <= c_RED;
                west_o  <= c_RED;
            when SOUTH_GO =>
                south_o <= c_GREEN;
                west_o  <= c_RED; 
            when SOUTH_WAIT =>
                south_o <= c_YELLOW;
                west_o  <= c_RED;   
                -- WRITE OTHER STATES HERE


            when others =>
                south_o <= c_RED;
                west_o  <= c_RED;
        end case;
    end process p_output_fsm;
```

3. Screenshot with simulated time waveforms. The full functionality of the entity must be verified. Always display all inputs and outputs (display the inputs at the top of the image, the outputs below them) at the appropriate time scale!

![image](https://user-images.githubusercontent.com/99723445/161768531-49e111fa-c629-4f37-9d6d-18e1711fbeac.png)

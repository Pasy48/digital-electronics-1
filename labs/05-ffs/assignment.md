# Lab 5: Martin Paseka

## Preparation tasks (done before the lab at home)

1. Write characteristic equations and complete truth tables for D, JK, T flip-flops where `q(n)` represents main output value before the clock edge and `q(n+1)` represents output value after the clock edge.

**D-type FF**

 The characteristic equation of edge-triggered D-type ﬂip-ﬂop is:
 
 ![image](https://user-images.githubusercontent.com/99723445/158189963-dd7b8625-4ae2-4467-abbb-c3b7aeccef0d.png)

   <!--
   https://editor.codecogs.com/
   \begin{align*}
       q_{n+1}^D =&~D \\
       q_{n+1}^{JK} =& \\
       q_{n+1}^T =& \\
   \end{align*}
   -->

   | **CLK** | **D** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-: |
   | ↑ | 0 | 0 | 0 | No change |
   | ↑ | 0 | 1 | 0 | Set |
   | ↑ | 1 | 0 | 1 | Set |
   | ↑ | 1 | 1 | 1 | No change |

   **JK-type FF**
   
   The characteristic equation of edge-triggered JK-type ﬂip-ﬂop is:
   
   ![image](https://user-images.githubusercontent.com/99723445/158190191-a3a34ed5-b045-4c08-b40f-8ca54a323b4b.png)
   
   | **CLK** | **J** | **K** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-: | :-: |
   | ↑ | 0 | 0 | 0 | 0 | No change |
   | ↑ | 0 | 0 | 1 | 1 | No change |
   | ↑ | 0 | 1 | 1 | 0 | Reset |
   | ↑ | 0 | 1 | 0 | 0 | Reset |
   | ↑ | 1 | 0 | 0 | 1 | Set |
   | ↑ | 1 | 0 | 1 | 1 | Set |
   | ↑ | 1 | 1 | 0 | 1 | Invert (Toggle) |
   | ↑ | 1 | 1 | 1 | 0 | Invert (Toggle) |

   **T-type FF**
   
   The characteristic equation of edge-triggered T-type ﬂip-ﬂop is:
   
   ![image](https://user-images.githubusercontent.com/99723445/158190343-f35b26ea-967f-47cb-8f3e-1cf2fe93c096.png)

   | **CLK** | **T** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-: |
   | ↑ | 0 | 0 | 0 | No change |
   | ↑ | 0 | 1 | 1 | No change |
   | ↑ | 1 | 0 | 1 | Invert (Toggle) |
   | ↑ | 1 | 1 | 0 | Invert (Toggle) |

<a name="part1"></a>

### Flip-flops

1. Listing of VHDL architecture for T-type flip-flop. Always use syntax highlighting, meaningful comments, and follow VHDL guidelines:

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;


entity t_ff_rst is
    Port ( clk :    in STD_LOGIC;
           rst :    in STD_LOGIC;
           t :      in STD_LOGIC;
           q :      out STD_LOGIC;
           q_bar :  out STD_LOGIC);
end t_ff_rst;

architecture Behavioral of t_ff_rst is
    -- It must use this local signal instead of output ports
    -- because "out" ports cannot be read within the architecture
    signal s_q : std_logic;
begin
    --------------------------------------------------------
    -- p_t_ff_rst:
    -- T type flip-flop with a high-active synchro reset,
    -- rising-edge clk.
    -- q(n+1) = t./q(n) + /t.q(n)
    -- q(n+1) =  q(n) if t = 0 (no change)
    -- q(n+1) = /q(n) if t = 1 (inversion)
    --------------------------------------------------------
    p_t_ff_rst : process(clk)
    begin
    
    if rising_edge (clk) then
        if (rst = '1') then
            s_q         <= '0';
            s_q_bar     <= '1';
        else
            if (t = '0') then
                s_q      <= s_q;
                s_q_bar  <= s_q_bar;
            else 
                s_q      <= not s_q;
                s_q_bar  <= not s_q_bar;
            end if;
        end if;
    end if;
    end process p_t_ff_rst;

    -- Output ports are permanently connected to local signal
    q     <= s_q;
    q_bar <= not s_q;
end architecture Behavioral;
```

2. Screenshot with simulated time waveforms. Try to simulate both flip-flops in a single testbench with a maximum duration of 200 ns, including reset. Always display all inputs and outputs (display the inputs at the top of the image, the outputs below them) at the appropriate time scale!

   ![your figure]()

### Shift register

1. Image of the shift register `top` level schematic. The image can be drawn on a computer or by hand. Always name all inputs, outputs, components and internal signals!

   ![your figure]()

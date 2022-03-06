# Lab 2: Martin   Paseka
| **Dec. equivalent** | **B[1:0]** |**A[1:0]** | **B is greater than A** | **B equals A** | **B is less than A** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 0 | 0 0 | 0 | 1 | 0 |
| 1 | 0 0 | 0 1 | 0 | 0 | 1 |
| 2 | 0 0 | 1 0 | 0 | 0 | 1 |
| 3 | 0 0 | 1 1 | 0 | 0 | 1 |
| 4 | 0 1 | 0 0 | 1 | 0 | 0 |
| 5 | 0 1 | 0 1 | 0 | 1 | 0 |
| 6 | 0 1 | 1 0 | 0 | 0 | 1 |
| 7 | 0 1 | 1 1 | 0 | 0 | 1 |
| 8 | 1 0 | 0 0 | 1 | 0 | 0 |
| 9 | 1 0 | 0 1 | 1 | 0 | 0 |
| 10 | 1 0 | 1 0 | 0 | 1 | 0 |
| 11 | 1 0 | 1 1 | 0 | 0 | 1 |
| 12 | 1 1 | 0 0 | 1 | 0 | 0 |
| 13 | 1 1 | 0 1| 1 | 0 | 0 |
| 14 | 1 1 | 1 0 | 1 | 0 | 0 |
| 15 | 1 1 | 1 1 | 0 | 1 | 0 |
### 2-bit comparator

1. Karnaugh maps for other two functions:

   Greater than:

   ![image](https://user-images.githubusercontent.com/99723445/155421415-a5a800db-83f1-4b5b-aa4d-4b153dc6f8eb.png)

   Less than:

   ![image](https://user-images.githubusercontent.com/99723445/155421440-58308ccb-699a-46aa-8a78-5458aadb470f.png)


2. Equations of simplified SoP (Sum of the Products) form of the "greater than" function and simplified PoS (Product of the Sums) form of the "less than" function.

   ![image](https://user-images.githubusercontent.com/99723445/155420791-7571264a-68b2-48da-9c6e-b4b113713335.png)

### 4-bit comparator

1. Listing of VHDL stimulus process from testbench file (`testbench.vhd`) with at least one assert (use BCD codes of your student ID digits as input combinations). Always use syntax highlighting, meaningful comments, and follow VHDL guidelines:

   Last two digits of my student ID: **xxxx97**

```vhdl
    p_stimulus : process
    begin
       p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;
        
        
        -- Eighth test values
        s_b <= "1001"; s_a <= "1001"; wait for 100 ns;
                -- Expected output
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
      
        report "Test failed for input combination: 1001, 1001" severity error;
        
        
        -- Ninth test values
        s_b <= "0111"; s_a <= "0111"; wait for 100 ns;
                -- Expected output
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        -- If false, then report an error
      
        report "Test failed for input combination: 0111, 0111" severity error;
        
        
         -- Tenth test values
        s_b <= "0110"; s_a <= "0011"; wait for 100 ns;
                -- Expected output
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        -- If false, then report an error
        report "Test failed for input combination: 0110, 0011" severity error;


        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```

2. Text console screenshot during your simulation, including reports.

   ![image](https://user-images.githubusercontent.com/99723445/155422641-acf0c7fa-1476-466e-b99b-9e4f935da32b.png)
   ![image](https://user-images.githubusercontent.com/99723445/155422686-b0095885-5c59-4f75-8147-32a95e394f0b.png)


3. Link to your public EDA Playground example:

https://www.edaplayground.com/x/b2qZ

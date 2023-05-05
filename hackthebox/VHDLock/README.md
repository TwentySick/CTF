# **VHDLock**
(Sorry for my weak english)

## **Analysis**

First look when extract the zip file, I have 2 files here: lock.vhd, out.txt. But file lock.vhd is just a plain text file, we don't need to do thing with this except look at the content.

![file_lock](/hackthebox/VHDLock/images/file_lock.png)

Let take a look, this file contants 3 parts as 3 components (I listed them below)

- The first component

```
----------------------------------
-- first component for xor operation
----------------------------------
library ieee;
use ieee.std_logic_1164.all;

entity xor_get is
    port(input1,input2 : in std_logic_vector(15 downto 0);
        output : out std_logic_vector(15 downto 0));
    end xor_get;

architecture Behavioral of xor_get is
begin
    output <= input1 xor input2;
end Behavioral;
```

- The second component

```
library ieee;
use ieee.std_logic_1164.all;

entity decoder_4x16 is
    port(input : in std_logic_vector(3 downto 0);
        output : out std_logic_vector(15 downto 0));
    end decoder_4x16;

architecture Behavioral of decoder_4x16 is
begin
    process(input)
    begin
        case input is
            when "0000" => output <= "0000000000000001";
            when "0001" => output <= "0000000000000010";
            when "0010" => output <= "0000000000000100";
            when "0011" => output <= "0000000000001000";
            when "0100" => output <= "0000000000010000";
            when "0101" => output <= "0000000000100000";
            when "0110" => output <= "0000000001000000";
            when "0111" => output <= "0000000010000000";
            when "1000" => output <= "0000000100000000";
            when "1001" => output <= "0000001000000000";
            when "1010" => output <= "0000010000000000";
            when "1011" => output <= "0000100000000000";
            when "1100" => output <= "0001000000000000";
            when "1101" => output <= "0010000000000000";
            when "1110" => output <= "0100000000000000";
            when "1111" => output <= "1000000000000000";
            when others => output <= "0000000000000000";
        end case;
    end process;
end Behavioral;
```

- main component

```
library ieee;
use ieee.std_logic_1164.all;

entity main is
    port(input_1,input_2 : in std_logic_vector(3 downto 0);
        xorKey : in std_logic_vector(15 downto 0);
        output1,output2 : out std_logic_vector(15 downto 0));
    end main;

architecture Behavioral of main is

    signal decoder1,decoder2: std_logic_vector(15 downto 0);
    component xor_get is
        port(input1,input2 : in std_logic_vector(15 downto 0);
            output : out std_logic_vector(15 downto 0));
        end component;
    component decoder_4x16 is
        port(input : in std_logic_vector(3 downto 0);
            output : out std_logic_vector(15 downto 0));
        end component;
            begin
                L0 : decoder_4x16 port map(input_1,decoder1);
                L1 : decoder_4x16 port map(input_2,decoder2);
                L2 : xor_get port map(decoder1,xorKey,output1);
                L3 : xor_get port map(decoder2,xorKey,output2);

        end Behavioral;                               
```

The main component decides each byte to 2 parts and each part contants 4 bit because 1 byte = 8 bit. Next, each part has to do with 'decoder_4x16' and the last step is XOR with xorKey. The file 'out.txt' is the output of those.

As the challenge mentioning, the xorKey is a 4-byte sequence. That mean the xorKey has 4 charecters because 1 character = 1 byte.

## **Solving**

Ok, so how to find 'xorKey'? We all know that 4 first characters of flag is 'HTB{', it's enough to find the xorKey. I just simulate the process of encrypting flag step by step.

Found the key, I just reverse the process to solve the challenge. XOR -> get 4 bit from the dictionary of 'decoder_4x16' -> combine 2 parts together.

I wrote a short script to solve the challenge.

![script](/hackthebox/VHDLock/images/script.png)
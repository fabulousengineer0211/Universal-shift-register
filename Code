LIBRARY IEEE;
USE IEEE.STD_LOGIC_1164.ALL; 

ENTITY MUX41 IS
PORT (i3, i2, i1, i0 : IN BIT;
s: IN BIT_VECTOR(1 DOWNTO 0); 
o: OUT BIT);
END MUX41;
 
ARCHITECTURE arch OF MUX41 IS BEGIN
PROCESS(i3, i2, i1, i0, s) BEGIN
CASE s IS
WHEN "00" => o <= i0; 
WHEN "01" => o <= i1; 
WHEN "10" => o <= i2; WHEN "11" => o <= i3;
WHEN OTHERS => NULL;
END CASE; 
END PROCESS;
END arch;

ENTITY df IS
PORT(d, clk : IN BIT;
q, qb : OUT BIT);
END df;

ARCHITECTURE archi OF df IS BEGIN
PROCESS(clk)
VARIABLE q_temp : BIT;
BEGIN
IF(clk'EVENT AND clk='1')THEN
q_temp := d;
END IF;
q <= q_temp;
qb <= NOT q_temp; END PROCESS;
END archi;

ENTITY RetrUni IS
PORT(clk, il, ir : IN BIT;
s: IN BIT_VECTOR(1 DOWNTO 0);
i : IN BIT_VECTOR(7 DOWNTO 0);
q : OUT BIT_VECTOR(7 DOWNTO 0));
END RetrUni;

ARCHITECTURE struct OF RetrUni IS 
COMPONENT MUX41
PORT (i3, i2, i1, i0 : IN BIT;
s: IN BIT_VECTOR(1 DOWNTO 0); o: OUT BIT);
END COMPONENT;

COMPONENT df
PORT(d, clk : IN BIT;
q, qb : OUT BIT); 
END COMPONENT;

SIGNAL o: BIT_VECTOR(7 DOWNTO 0); 
SIGNAL qb: BIT_VECTOR(7 DOWNTO 0); 
SIGNAL qt:BIT_VECTOR(7 DOWNTO 0);

BEGIN

U1:MUX41 PORT MAP(il,qt(6), i(7), qt(7), s, o(7));
U2:MUX41 PORT MAP(qt(7), qt(5), i(6), qt(6), s, o(6));
U3:MUX41 PORT MAP(qt(6), qt(4), i(5), qt(5), s, o(5));
U4:MUX41 PORT MAP(qt(5), qt(3), i(4), qt(4), s, o(4));
U5:MUX41 PORT MAP(qt(4), qt(2), i(3), qt(3), s, o(3));
U6:MUX41 PORT MAP(qt(3), qt(1), i(2), qt(2), s, o(2));
U7:MUX41 PORT MAP(qt(2), qt(0), i(1), qt(1), s, o(1));
U8:MUX41 PORT MAP(qt(1), ir, i(0), qt(0), s, o(0));

U9:df PORT MAP(o(7), clk, qt(7), qb(7));
U10:df PORT MAP(o(6), clk, qt(6), qb(6));
U11:df PORT MAP(o(5), clk, qt(5), qb(5));
U12:df PORT MAP(o(4), clk, qt(4), qb(4));
U13:df PORT MAP(o(3), clk, qt(3), qb(3));
U14:df PORT MAP(o(2), clk, qt(2), qb(2));
U15:df PORT MAP(o(1), clk, qt(1), qb(1));
U16:df PORT MAP(o(0), clk, qt(0), qb(0));

q <= qt;
END struct;

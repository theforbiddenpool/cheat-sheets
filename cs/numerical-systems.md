## Common prefixes
- Decimal → does not have a prefix
- Hexadecimal → `Ox`
- Octal → `O`
- Binary → `Ob`

## Reference Table
Decimal | Binary | Octal | Hex | | Decimal | Binary | Octal | Hex
--- | --- | --- | --- | --- | --- | --- | --- | ---
0 | 0000 | 0 | 0 |  | 8 | 1000 | 10 | 8
1 | 0001 | 1 | 1 |  | 9 | 1001 | 11 | 9
2 | 0010 | 2 | 2 |  | 10 | 1010 | 12 | A
3 | 0011 | 3 | 3 |  | 11 | 1011 | 13 | B
4 | 0100 | 4 | 4 |  | 12 | 1100 | 14 | C
5 | 0101 | 5 | 5 |  | 13 | 1101 | 15 | D
6 | 0110 | 6 | 6 |  | 14 | 1110 | 16 | E
7 | 0111 | 7 | 7 |  | 15 | 1111 | 17 | F

# Converting
## Binary to Decimal
h<sub>n</sub>2<sup>n</sup> + h<sub>n</sub>-12<sup>n-1</sup> + ... + h<sub>1</sub>2<sup>1</sup> + h<sub>0</sub>2<sup>0</sup>

*Example*: 101010<sub>2</sub>
1. Put the numbers into the equation → 1×25 + 0×24 + 1×23 + 0×22 + 1×21 + 0×20
2. Solve the multiplications → 32 + 0 + 8 + 0 + 2 + 0
3. Sum all the numbers → 42

## Decimal to Binary
The most convenient method is repeated division by 2. We repeatedly divide the number by 2 and record the remainder. When we finish, we read the remainder digits from bottom to top and that's your binary number.

*Example*: 132
1. 132 ÷ 2 = **66**, remainder **0**.
2. 66 ÷ 2 = **33**, remainder **0**.
3. 33 ÷ 2 = **16**, remainder **1**.
4. 16 ÷ 2 = **8**, remainder **0**.
5. 8 ÷ 2 = **4**, remainder **0**.
6. 4 ÷ 2 = **2**, remainder **0**.
7. 2 ÷ 2 = **1**, remainder **0**.
8. 1 ÷ 2 = **0**, remainder **1**.
9. The final result is: **0b10000100**

## Decimal to Hex
*Example*: 61453<sub>10</sub>
1. 61453 / 16 = **3840**, remainder **13**. The remainder becomes our first, right-most, least-significant hex digit - D.
2. 3840 / 16 = **240**, remainder **0**. Our second hex digit is **0**.
3. 240 / 16 = **15**, remainder **0**. Our third hex digit is **0**.
4. 15 / 16 = **0**, remainder **15**. Our forth digit is **F**.
5. Combine all four hex digits – **0xF00D**.

## Hex to Decimal
h<sub>n</sub>16<sup>n</sup> + h<sub>n-1</sub>16<sub>n-1</sub> + ... + h<sub>1</sub>16<sup>1</sup> + h<sub>0</sub>16<sup>0</sup>

*Example*: C0DE
| | <th colspan=4>Hexadecimal Digit | | | |
--- | --- | --- | --- | ---
Digit positions | 3 | 2 | 1 | 0
Hex Digits Sorted | C | 0 | D | E
Convert A-F | 12 | 0 | 13 | 14
Multiply by 16n | 12 × 163 | 0 × 162 | 13 × 161 | 14 × 160
Resulting Products | 49152 | 0 | 208 | 14
Sum Up All Products | <td colspan=4>49374

## Binary to Hex
Each digit of a hexadecimal number maps to four bits of a binary value. So a byte (eight bits) can always be represented by two hexadecimal digits, making it a great way to represent a byte of group of bytes. Use the reference table to help you do the conversion.

*Example*: 0b101111010100001
1. Split a binary value into grous of four, starting at the right-most side – 0100 1110 1010 0001
2. Consult the table to convert the groups-of-four to a hex digit – 5EA1

## Hex to Binary
*Example*: 0xDEADBEEF
1. Sort the digits into bins – D E A D B E E F
2. Convert each hex digit into the four correspondent bits – 11011110101011011011111011101111

# Binary
Uses a base 2 - **0** and **1**. it's an easier format for computers to work with.

__Note:__ because all powers of 2 except for 0 result in an even number, the only way to get an odd number is to have the right most digit be 1.

## Arithmetic
### Addition
Addition is essentially the same as we do it with decimal. The possibilities are:
- 0 + 0 = 0
- 1 + 0 = 1
- 1 + 1 = 10
- 1 + 1 + 1 = 11

The carry is involved whenever we have a result larger than 1. It is possible to add more than 2 binary numbers together, but it can soon get impossible to manage the carries.

*Example*: 10010 + 10110
| | | | | | |
--- | --- | --- | --- | --- | ---
\# | 1 | 0 | 0 | 1 | 0
+ | 1 | 0 | 1 | 1 | 0
| | | | | | |
1 | 0 | 1 | 0 | 0 | 0

### Multiplication
Similar to decimal multiplication. The possibilities are:
- 0 × 0 = 0
- 1 × 0 = 0
- 1 × 1 = 1

*Example*: 1110 × 101
| | | | | | | | |
--- | --- | --- | --- | --- | --- | --- | ---
| | | | 1 | 1 | 1 | 1 | 0
| | | | | × | 1 | 0 | 1
| | | | | | | | |
| | | | 1 | 1 | 1 | 1 | 0
| | | 0 | 0 | 0 | 0 | 0
\+ | 1 | 1 | 1 | 1 | 0
| | | | | | | | |
1 | 0 | 0 | 1 | 0 | 1 | 1 | 0

### Subtraction
It's similar to binary addition, but instead of carrying forward, we will borrow backwards when necessary. The possibilities are:
- 0 - 0 = 0
- 1 - 0 = 1
- 1 - 1 = 0
- 0 - 1 = 10 (borrowed) - 1 = 1

*Example*: 10000 - 1010
| | | | | | |
--- | --- | --- | --- | --- | ---
| | 1 | 0 | 0 | 0 | 0
\- | | 1 | 0 | 1 | 0
| | | | | | |
| | | 0 | 1 | 1 | 0

There is another approach, and it's the actual way computers subtract binary digits. It is called Two's Complement.
1. Write the equation out, padding the bottom number with 0's → **1000** - **0011**
2. Invert the digits of the lower number → **1000** - **1100**
3. Add 1 to the lower number → **1000** - **1101**
4. Add those numbers together → **10110**
5. Remove the leading 1, and any 0's after it → **101**

### Division
Division is the most difficult of the binary equations. The number we are dividing by is the *divisor*, and the number we are dividing into is the *dividend*.
1. Create the working portion of the dividend. Start at the right, keep including digits until we have a number that the divisor will go into.
2. Work out how many times the divisor goes into the working portion - in binary will always be 1.
3. Subtract the divisor from the working number. This becomes the beginning of the new working number.
4. Bring down digits from the dividend and add the new working to the new working number until we have a new working number large enough for the divisor to go into.
5. Repeat steps 2 to 4 until we are at the end of the dividend.
6. The result of the final subtraction is the remainder.

# Hexadecimal
Also known as hex or base 16, it's a system we can use to write and share numerical values. Uses a set of 16 unique digits - **0-9** + **A-F**. Is one of the most commonly encountered numeral systems in the world of electronics and programming.

Since decimal and hexadecimal can create a lot of similar-looking numbers, it is wise to use a base subscript to identify which numerical system is being used.\
*e.g.* 16<sub>10</sub> = 10<sub>16</sub>

## Counting
<small> Hex [Dec]</small>\
`0 1 2 3 4 5 6 7 8 9 A B C D E F`[15] `10`[16] `11 12 13 14 15 16 17 18 19`[25] `1A`[26] `1B 1C 1D 1E 1F`[31]

## Hex Identifiers
There are a variety of prefixes and suffixes unique to each language to avoid confusion. `0x` is one we'll see a lot.
Identifier | Example | Notes
--- | --- | ---
0x | 0x47DE | UNIX and C-based programming languages
\# | #ff7734 | color references in HTML and image editing programs
% | %20 | used in ULRs to express characters like " " (space)
\x | \x08 | used to express character control codes like Backspace
&#x | &#x3A9 | used in HTML, and XML to express unicode characters
0h | 0h5E | used by many programmable graphic calculators
Numeral/Text or Subscript | BE37<sub>16</sub> or 13F<sub>hex</sub> | mathematical representation of base 16 numbers


# Sources
[Hexadecimal - sparkfun](https://learn.sparkfun.com/tutorials/hexadecimal/all)\
[Binary Tutorial - Ryan's Tutorials](https://ryanstutorials.net/binary-tutorial/)
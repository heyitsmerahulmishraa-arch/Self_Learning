## Octal Number System
The octal number system is a base-8 numeral system that uses the digits 0 to 7. It is commonly used in computing and digital systems as a more compact representation of binary numbers. Each octal digit corresponds to three binary digits (bits), making it easier to read and write large binary numbers.

### Converting Binary to Octal
To convert a binary number to octal, you can group the binary digits into sets of three, starting from the right. If the number of binary digits is not a multiple of three, you can add leading zeros to make it so. Then, you can convert each group of three binary digits to its corresponding octal digit.
For example, let's convert the binary number `110101` to octal:
1. Group the binary digits into sets of three: `110` and `101`.
2. Convert each group to octal:
   - `110` in binary is `6` in octal.
   - `101` in binary is `5` in octal.
3. Combine the octal digits: `65`.
So, the binary number `110101` is equal to `65` in octal.

### Converting Octal to Binary
To convert an octal number to binary, you can convert each octal digit to its corresponding three-bit binary representation. For example, let's convert the octal number `65` to binary:
1. Convert each octal digit to binary:
   - `6` in octal is `110` in binary.
   - `5` in octal is `101` in binary.
2. Combine the binary digits: `110101`.
So, the octal number `65` is equal to `110101` in binary.

### Converting Octal to Decimal
To convert an octal number to decimal, you can multiply each octal digit by 8 raised to the power of its position from the right (starting at 0). For example, let's convert the octal number `65` to decimal:
1. Calculate the value of each digit:
   - `6` in octal is `6 * 8^1 = 48`.
   - `5` in octal is `5 * 8^0 = 5`.
2. Add the values: `48 + 5 = 53`.
So, the octal number `65` is equal to `53` in decimal.

### Converting Decimal to Octal
To convert a decimal number to octal, you can repeatedly divide the number by 8 and keep track of the remainders. The octal number is formed by the remainders read in reverse order. For example, let's convert the decimal number `53` to octal:
1. Divide `53` by `8`: `53 ÷ 8 = 6` with a remainder of `5`.
2. Divide `6` by `8`: `6 ÷ 8 = 0` with a remainder of `6`.
3. Read the remainders in reverse order: `65`.
So, the decimal number `53` is equal to `65` in octal.

### Summary
The octal number system is a base-8 numeral system that uses digits from 0 to 7. It is commonly used in computing as a more compact representation of binary numbers. You can convert between binary, octal, and decimal number systems using the methods described above.


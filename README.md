# DecimalType_C 

Implementation of decimal type on C

The Decimal value type is used to represent decimal numbers within a specified range. This range includes positive values from 79,228,162,514,264,337,593,543,950,335 to negative values of the same magnitude.

### Binary representation

The binary representation of a Decimal number consists of a 1-bit sign, a 96-bit integer number, and a scaling factor used to divide the integer number and specify what portion of it is a decimal fraction. The scaling factor is implicitly the number 10, raised to an exponent ranging from 0 to 28.

Decimal number can be implemented as a four-element array of 32-bit signed integers (`int bits[4];`).

`bits[0]`, `bits[1]`, and `bits[2]` contain the low, middle, and high 32 bits of the 96-bit integer number accordingly.

`bits[3]` contains the scale factor and sign, and consists of following parts:
- Bits 0 to 15, the lower word, are unused and must be zero.
- Bits 16 to 23 must contain an exponent between 0 and 28, which indicates the power of 10 to divide the integer number.
- Bits 24 to 30 are unused and must be zero.
- Bit 31 contains the sign; 0 meaning positive, and 1 meaning negative.

### Arithmetic Operators

| Operator name | Operators  | Function                                                                           | 
| ------ | ------ |------------------------------------------------------------------------------------|
| Addition | + | int s21_add(s21_decimal value_1, s21_decimal value_2, s21_decimal *result)         |
| Subtraction | - | int s21_sub(s21_decimal value_1, s21_decimal value_2, s21_decimal *result) |
| Multiplication | * | int s21_mul(s21_decimal value_1, s21_decimal value_2, s21_decimal *result) | 
| Division | / | int s21_div(s21_decimal value_1, s21_decimal value_2, s21_decimal *result) |

The functions return the error code:
- 0 - OK
- 1 - the number is too large or equal to infinity
- 2 - the number is too small or equal to negative infinity
- 3 - division by 0

### Comparison Operators

| Operator name | Operators  | Function | 
| ------ | ------ | ------ |
| Less than | < | int s21_is_less(s21_decimal, s21_decimal) |
| Less than or equal to | <= | int s21_is_less_or_equal(s21_decimal, s21_decimal) | 
| Greater than | > |  int s21_is_greater(s21_decimal, s21_decimal) |
| Greater than or equal to | >= | int s21_is_greater_or_equal(s21_decimal, s21_decimal) | 
| Equal to | == |  int s21_is_equal(s21_decimal, s21_decimal) |
| Not equal to | != |  int s21_is_not_equal(s21_decimal, s21_decimal) |

Return value:
- 0 - FALSE
- 1 - TRUE

### Convertors and parsers

| Convertor/parser | Function | 
| ------ | ------ |
| From int  | int s21_from_int_to_decimal(int src, s21_decimal *dst) |
| From float  | int s21_from_float_to_decimal(float src, s21_decimal *dst) |
| To int  | int s21_from_decimal_to_int(s21_decimal src, int *dst) |
| To float  | int s21_from_decimal_to_float(s21_decimal src, float *dst) |

Return value - code error:
- 0 - OK
- 1 - convertation error

### Another functions

| Description | Function                                                         | 
| ------ |------------------------------------------------------------------|
| Rounds a specified Decimal number to the closest integer toward negative infinity. | int s21_floor(s21_decimal value, s21_decimal *result)            |	
| Rounds a decimal value to the nearest integer. | int s21_round(s21_decimal value, s21_decimal *result)    |
| Returns the integral digits of the specified Decimal; any fractional digits are discarded, including trailing zeroes. | int s21_truncate(s21_decimal value, s21_decimal *result) |
| Returns the result of multiplying the specified Decimal value by negative one. | int s21_negate(s21_decimal value, s21_decimal *result)   |

Return value - code error:
- 0 - OK
- 1 - calculation error

- The library was developed in C language of C11 standard using gcc compiler;
- The library code is be located in the src folder on the develop branch;
- The library is developed according to the principles of structured programming;
- The prefix s21_ used means school 21, where this project was implemented;
- There is a Makefile for building the library and tests (with targets all, clean, test, s21_decimal.a, gcov_report)  
- The defined type supports numbers from -79,228,162,514,264,337,593,543,950,335 to +79,228,162,514,264,337,593,543,950,335.

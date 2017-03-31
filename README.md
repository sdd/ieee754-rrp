## Draft Standards Document

# IEEE754-RRP: Reduced Reduced Precision Arithmetic.

To mark the 30th anniversary year of IEEE754 floating point in April 2017, the IEEE have introduced some
forward-looking new formats to meet the burdgeoning need amongst the ML community for reduced
precision arithmetic.

The four new floating point formats - the first new FP formats since 2008 - are collectively known as IEEE754-RRP, and are detailed in the following draft RFC. This document is not normative and is open to public comment and contribution in the form of GitHub Pull Requests at https://github.com/sdd/ieee754-rrp.


### Preamble

After ratification of this standard by the IEEE, all official communication from the Institute will in future no longer use the term "Integers". Since this set of numbers does not contain a decimal point, this dated terminology will be replaced with the term "pointless numbers".

## The New Formats


#### IEEE754 quarter precision (8 bits)

This format consists of 8 bits, allowing compatible hardware implementations to perform 8 simultaneous operations on a 64 bit architecture. It consists of one sign bit, a four bit exponent, and a three bit mantissa, with a built-in mantissa multiplier of 1.25.

This allows numbers as high as 8.75 to be represented without any exponent.

Example: addition of decimal "2" with decimal "2"

```
Two in IEE754QP binary representation is 0 0000 010 (i.e. it gets rounded to 2.5)

 0 0000 010
+0 0000 010
=0 0000 100, or 5 when converted back to decimal, with rounding errors.
```

#### IEEE754 half-quarter (HQ) precision (4 bits)

1 sign bit, two bit (signed) exponent, single bit mantissa.

Possible values:

```
0000 =  0 * 1^0		= 0
0010 =  0 * 1^1		= 0
0100 =  0 * 1^-0	= 0
0110 =  0 * 1^-1	= 0

1000 = -0 * 1^0		= 0
1010 = -0 * 1^1		= 0
1100 = -0 * 1^-0	= 0
1110 = -0 * 1^-1	= 0

0001 =  1 * 1^0		= 1
0011 =  1 * 1^1  = 1
0101 =  1 * 1^-0	= 1
0111 =  1 * 1^-1	= 1

1001 = -1 * 1^0		= -1
1011 = -1 * 1^1  = -1
1101 = -1 * 1^-0	= -1
1111 = -1 * 1^-1	= -1
```

#### IEEE754 quarter-quarter (QQ) precision (2 bits)

Possible values:

```
00	zero
01	one
10	Infinity
11	NaN
```

#### IEEE754 half-quarter-quarter (HQP) precision

Single bit. 0 = Zero, 1 = NaN

Example of addition:

```
  0 + 0   = 0
  0 + NaN = NaN
NaN + 0   = NaN
NaN + NaN = NaN
```

x86-64 processors have had SIMD 64x half-quarter-quarter addition for some time via opcode 0F EB, AKA the POR instruction.
http://x86.renejeschke.de/html/file_module_x86_id_251.html

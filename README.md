To mark the 30th anniversary year of IEEE754 floating point, the IEEE have introduced some
forward-looking new formats to meet the burdgeoning need amongst the ML community for reduced
precision arithmetic.

As an addendum, due to their lack of a decimal point, "integers" will henceforth be known as "pointless numbers".


IEEE754 quarter precision
=========================

8 bits. One sign bit, four bit exponent, three bit mantissa, with a built-in multiplier of 1.25.
This allows numbers as high as 8.75 to be represented without any exponent.

Example addition: decimal 2 plus decimal 2

two in IEE754qp = 010 (rounded to 2.5)

 010
+010
----
 100, or 5 in decimal.


IEEE754 half quarter precision
==============================

1 sign bit, two bit (signed) exponent, single bit mantissa

Possible values:

0000 =  0 * 1^0		= 0
0010 =  0 * 1^1		= 0
0100 =  0 * 1^-0	= 0
0110 =  0 * 1^-1	= 0

1000 = -0 * 1^0		= 0
1010 = -0 * 1^1		= 0
1100 = -0 * 1^-0	= 0
1110 = -0 * 1^-1	= 0

0001 =  1 * 1^0		= 1
0011 =  1 * 1^1     = 1
0101 =  1 * 1^-0	= 1
0111 =  1 * 1^-1	= 1

1001 = -1 * 1^0		= -1
1011 = -1 * 1^1     = -1
1101 = -1 * 1^-0	= -1
1111 = -1 * 1^-1	= -1

IEEE754 quarter quarter precision
=================================

00	zero
01	one
10	Infinity
11	NaN

IEEE754 half quarter quarter precision
======================================

Single bit. 0 = Zero, 1 = NaN.
0 = 0 = 0.
0 + NaN = NaN.
NaN + 0 = NaN.
NaN + NaN = NaN.

x86-64 processors have had SIMD 64x half-quarter-quarter addition for some time via opcode 0F EB, AKA the POR instruction.
http://x86.renejeschke.de/html/file_module_x86_id_251.html

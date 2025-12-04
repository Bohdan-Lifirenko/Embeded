Code C:
```
int main(void) {
	volatile long a = 1;
	volatile long b = 2;
	volatile long c = 3;
	
	volatile long array[4] = {4, 5, 6, 7};
}
```
Instructions:
```
     3: int main(void) { 
0x000004C4 B087      SUB           sp,sp,#0x1C
0x000004C6 2001      MOVS          r0,#0x01
     4:         volatile long a = 1; 
0x000004C8 9006      STR           r0,[sp,#0x18]
0x000004CA 2002      MOVS          r0,#0x02
     5:         volatile long b = 2; 
0x000004CC 9005      STR           r0,[sp,#0x14]
0x000004CE 2003      MOVS          r0,#0x03
     6:         volatile long c = 3; 
     7:          
0x000004D0 9004      STR           r0,[sp,#0x10]
     8:         volatile long array[4] = {4, 5, 6, 7}; 
0x000004D2 F240530C  MOVW          r3,#0x50C
0x000004D6 F2C00300  MOVT          r3,#0x00
0x000004DA 6818      LDR           r0,[r3,#0x00]
0x000004DC 6859      LDR           r1,[r3,#0x04]
0x000004DE 689A      LDR           r2,[r3,#0x08]
0x000004E0 68DB      LDR           r3,[r3,#0x0C]
0x000004E2 9303      STR           r3,[sp,#0x0C]
0x000004E4 9202      STR           r2,[sp,#0x08]
0x000004E6 9101      STR           r1,[sp,#0x04]
0x000004E8 9000      STR           r0,[sp,#0x00]
0x000004EA 2000      MOVS          r0,#0x00
```
```
SP =   0x20000644 - 0010 0000 0000 0000 0000 0110 0100 0100
SP04 - 0x20000648 - 0010 0000 0000 0000 0000 0110 0100 1000
SP08 - 0x2000064C - 0010 0000 0000 0000 0000 0110 0100 1100
SP0C - 0x20000650 - 0010 0000 0000 0000 0000 0110 0101 0000
SP10 - 0x20000654 - 0010 0000 0000 0000 0000 0110 0101 0100
SP14 - 0x20000658 - 0010 0000 0000 0000 0000 0110 0101 1000
SP18 - 0x2000065C - 0010 0000 0000 0000 0000 0110 0101 1100

0x0000050C        0000 0000 0000 0000 0000 0101 0000 1100
```
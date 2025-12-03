working with variables:

```
	unsigned int a = 0x5A5A5A5A; // 0101 1010 0101 1010 0101 1010 0101 1010	0x5A5A5A5A	1515870810
	unsigned int b = 0xDEADBEEF; // 1101 1110 1010 1101 1011 1110 1110 1111	0xDEADBEEF	3735928559
	unsigned int c;
	
	c = a | b; // OR             // 1101 1110 1111 1111 1111 1110 1111 1111	0xDEFFFEFF 	3741318911
	c = a & b; // AND            // 0101 1010 0000 1000 0001 1010 0100 1010	0x5A081A4A 	1510480458
	c = a ^ b; // exclusive OR   // 1000 0100 1111 0111 1110 0100 1011 0101	0x84F7E4B5	2230838453
	c = ~b; // NOT							 // 0010 0001 0101 0010 0100 0001 0001 0000 0x21524110	559038736
	c = b >> 7; // right-shift	 // 0000 0001 1011 1101 0101 1011 0111 1101	0x01BD5B7D	29186941		LSLS (ligical)
	c = b << 9; // left-shift		 // 0101 1011 0111 1101 1101 1110 0000 0000	0x5B7DDE00	1534975488 	LSLS (ligical)
	
	int x = 1024;								 // 0000 0000 0000 0000 0000 0100 0000 0000 0x00000400
	int y = -1024;							 // 1111 1111 1111 1111 1111 1100 0000 0000 0xFFFFFC00
	int z;					
	
	z = x >> 3;									 // 0000 0000 0000 0000 0000 0000 1000 0000	0x00000080	128 ASRS (arichmetical)
	z = y >> 3;									 // 1111 1111 1111 1111 1111 1111 1000 0000 0xFFFFFF80  -128 ASRS (arichmetical)
```

змінюємо значення всьго регістру:
```
	SYSCTL_RCGCGPIO_R = 0x20U; // enable clock for GPIOF
	GPIO_PORTF_DIR_R = 0x0EU; // set pins 1,2,3
	GPIO_PORTF_DEN_R = 0x0EU; // enable digital function for pins 1,2,3
```

Використовуємо побітові операції:

```
#include "tm4c.h"
	
#define LED_RED 	(1U << 1)
#define LED_BLUE 	(1U << 2)
#define LED_GREEN (1U << 3)

int main(void) {
	SYSCTL_RCGCGPIO_R |= (1U << 5); // enable clock for GPIOF
	GPIO_PORTF_DIR_R |= (LED_RED | LED_BLUE | LED_GREEN);
	GPIO_PORTF_DEN_R |= (LED_RED | LED_BLUE | LED_GREEN);
		
	GPIO_PORTF_DATA_R |= LED_BLUE; /// turn blue led
	while (1) {
		GPIO_PORTF_DATA_R |= LED_RED; /// turn red led
		
		int volatile counter = 0;
		while (counter < 1000000) {
			++counter;
		}
		
		GPIO_PORTF_DATA_R &= ~LED_RED; /// off red led
		
		counter = 0;
		while (counter < 1000000) {
			++counter;
		}
	}
		
	return 0;
}
```
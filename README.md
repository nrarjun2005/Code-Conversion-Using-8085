# Code-Conversion-Using-8085
## Aim:
## To write 8085 microprocessor programs for converting:
1.	Hexadecimal to ASCII
2.	ASCII to Hexadecimal
## Apparatus Required:
•	Laptop with an internet connection
## Program 1: Hexadecimal to ASCII Conversion
ORG 00H
; Input : Port 00H (Hexadecimal number)
; Output: Port 01H (ASCII of upper nibble)
; Port 02H (ASCII of lower nibble)
MVI A, 00H
IN 00H ; Read hexadecimal number
MOV B, A ; Save a copy of original number
ANI 0F0H ; Mask lower nibble
RRC
RRC
RRC
RRC ; Move upper nibble to lower position
CPI 0AH ; Compare with 0AH
JC ADD30U ; If less than 0AH, jump
ADI 37H ; Add 37H for A-F
JMP STORE1
ADD30U: ADI 30H ; Add 30H for 0-9
STORE1: OUT 01H ; Send upper nibble ASCII to port 01H
; Process lower nibble
MOV A, B ; Get original number
ANI 0FH ; Mask upper nibble
CPI 0AH ; Compare with 0AH
JC ADD30L ; If less, jump
ADI 37H ; Add 37H for A-F

Output:
## Algorithm:
1.	Load the hexadecimal number from memory location 4200H.
2.	Mask the upper nibble and check if it is less than 10H.
3.	If it is less than 10H, add 30H to convert it to ASCII.
4.	If it is greater than 10H, add 37H to convert it to ASCII.
5.	Repeat the process for the lower nibble.
6.	Store the ASCII equivalent in memory location 4300H and 4301H.
## Output:
JMP STORE2
ADD30L: ADI 30H ; Add 30H for 0-9
STORE2: OUT 02H ; Send lower nibble ASCII to port 02H
HLT ; Stop program
END
•	The ASCII equivalent of the hexadecimal number will be stored in 4300H (upper nibble) and 4301H (lower nibble).

## Program 2: ASCII to Hexadecimal Conversion
## Algorithm:
1.	Load the first ASCII digit from memory location 4200H.
2.	Convert it to hexadecimal by subtracting 30H (if it's a number) or 37H (if it's a letter A-F).
3.	Load the second ASCII digit from memory location 4201H and repeat the process.
4.	Combine the upper and lower nibbles to form a hexadecimal number.
5.	Store the result in memory location 4300H.
## Output:
•	The hexadecimal equivalent of the ASCII input will be stored in memory location 4300H.
<img width="1134" height="563" alt="image" src="https://github.com/user-attachments/assets/bd645fb1-111f-4b39-a4fb-a39bdda97ec6" />

## Result:
The 8085 microprocessor successfully converts hexadecimal numbers to ASCII and vice versa, storing the results in memory.

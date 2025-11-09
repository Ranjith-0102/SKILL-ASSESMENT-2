# TIMER DELAY USING TIMER 0
# 8051 Program

## AIM
To write an assembly language program for the 8051 microcontroller to generate a 200 µs delay using Timer 0 in Mode 1 and toggle Port 0.1 repeatedly.
## APPARATUS REQUIRED
- Personal computer
- Keil μVision IDE

## ALGORITHM
1. Configure Timer 0 in Mode 1 (16-bit timer mode) using the TMOD register.
2. Load TH0 and TL0 registers with the initial value needed for a 1 ms delay (TH0 = 0xFc, TL0 = 0x18 for a 12 MHz clock).
3. Start Timer 0 by setting the TR0 bit.
4. Wait for the Timer 0 overflow flag (TF0) to be set.
5. Stop Timer 0 and clear the TF0 flag.
6. Toggle Port 0.1 using the CPL instruction.
7. Repeat the delay and toggle steps in an infinite loop.
asm
ORG 0000H          
MOV TMOD, #01H     
AGAIN: MOV P1, #0FFH 
CALL DELAY         
MOV P1, #00H      
CALL DELAY         
SJMP AGAIN        
DELAY: MOV TH0, #0FCH 
       MOV TL0, #18H  
       SETB TR0     
WAIT:  JNB TF0, WAIT
       CLR TR0       
       CLR TF0      
       RET         
END



## OUTPUT

<img width="1901" height="1179" alt="Screenshot 2025-11-09 142712" src="https://github.com/user-attachments/assets/a40acd26-688e-41b8-9d82-9970e7a82541" />


## RESULT
The program toggles Port 1 continuously, with each transition occurring after a delay of approximately 1 ms, thus generating a square waveform at P1

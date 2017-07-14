# UART-ADC-Test
This code sets the basic registers to allow the dspic33f09gs302 to read in data on pin AN0 and transmit it through the UART module with pin RP3


       InitOutPutPins() - This functions sets up all the I/O that are used in the test promram
                          1 = Input, 0 = Output
                          
                          TRISA = 0b0000000000000011  RAO/RA1 are mapped as inputs. These are ADC Pair 0
                          TRISB = 0b0000000000000011 RB0/RB1 are mapped as inputs. RB0/RB1 are not used in this program.This is left over                                                      from an earlier debug effort
       
       RemapPins() - This function sets up the UART Tx pin. It uses remappeable pin RP3 which is pin RB3 and pin 11 on the micro c                              controller
       
                     RPOR1bits.RP3R = 0b000011 - 0b000011 sets RP3 as a UART Tx
       
       InitUART() - This sets up the UART module. Only the Tx registers are set up at this time. 
       
       InitADC() -  This sets up the ADC. It is set up for interrputs. The interrupt used is Timer1. Everytime Timer1 reaches its PR1                         value it triggers an ADC interrupt and reads AN0.
       
       InitTimer1() - Sets Timer1 registers. No interrupt is needed since the ADC is set to trigger when the timer reaches the PR1 value

Known issues:

1.)    I have a pot connected to the 3.3V (VDD) supply from the Microstick II. When I adjust the pot the voltage moves up and down and the        ADC values I am readin in changes. The issue right now is the ADC is 10 bits and the UART register is only 9 bits long. I still            need to address this. As of now I can't print accurate values to a serial terminal because of this.

2.)    For some reason when try to simulate the program it will not enter the ADC interrupt. I try to place a breakpoint in the interrupt        but it never enters the interrupt. Not sure if this is a limitation of the simulator or if there is a work around. 

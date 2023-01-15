FILENAME   = blink
PORT       = /dev/cu.usbserial-00000000
DEVICE     = attiny13
PROGRAMMER = arduino
BAUD       = 115200
F_CPU      = 8000000
COMPILE    = avr-gcc -Wall -v -Os -Wl,--gc-sections -ffunction-sections -fdata-sections -DF_CPU=16000000 -save-temps -mmcu=$(DEVICE)

default: compile upload clean

compile:
	$(COMPILE) -c $(FILENAME).c -o $(FILENAME).o
	$(COMPILE) -o $(FILENAME).elf $(FILENAME).o
	avr-objcopy -j .text -j .data -O ihex $(FILENAME).elf $(FILENAME).hex 
	avr-size --format=avr --mcu=$(DEVICE) $(FILENAME).elf
	avr-objcopy -I ihex $(FILENAME).hex  -O binary $(FILENAME).bin

upload:
	avrdude -v -p $(DEVICE) -c $(PROGRAMMER) -P $(PORT) -b $(BAUD) -U flash:w:$(FILENAME).hex:i

clean:
	rm $(FILENAME).o
	rm $(FILENAME).elf
	rm $(FILENAME).hex
	rm $(FILENAME).bin
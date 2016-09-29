# import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
my_pin=[6,12,13,19,16,26,20,21]
for pin in my_pin:
    GPIO.setup(pin,GPIO.OUT)
while(1):
    ascii=input("Aacii=")
    bin2str=bin(ord(ascii)+256)
    #0b1xxxxxxxx
    print("bin=",bin2str[3:11])
    GPIO.output(my_pin[0],int(bin2str[2]))
    GPIO.output(my_pin[1],int(bin2str[3]))
    GPIO.output(my_pin[2],int(bin2str[5]))
    GPIO.output(my_pin[3],int(bin2str[6]))
    GPIO.output(my_pin[4],int(bin2str[7]))
    GPIO.output(my_pin[5],int(bin2str[8]))
    GPIO.output(my_pin[6],int(bin2str[9]))
    GPIO.output(my_pin[7],int(bin2str[10]))

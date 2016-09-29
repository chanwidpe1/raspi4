import time
import smbus
bus = smbus.SMBus(1)
import RPi.GPIO as GPIO
import time
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
addr = 0x23 # i2c adress
my_pin=[16,26,20,21]
for pin in my_pin:
    GPIO.setup(pin,GPIO.OUT)
st1=0
st2=0
st3=0
st4=0
st5=0
count=0
timer=0
while True:
    time.sleep(0.2)
    data = bus.read_i2c_block_data(addr,0x11)
    lum=(data[1] + (data[0]<<8) / 1.2)
    #print ("Luminosity " ,lum,"lx")
    while (lum<100):
        timer=0
        count+=1
        data = bus.read_i2c_block_data(addr,0x11)
        lum=(data[1] + (data[0]<<8) / 1.2)
        time.sleep(0.2)
        while (lum<100):
            data = bus.read_i2c_block_data(addr,0x11)
            lum=(data[1] + (data[0]<<8) / 1.2)
            time.sleep(0.2)
    print(count)
    timer+=1
    #print ("Timer=",timer)
    if (timer>10):
        if(count==1):
            st1=~st1
            GPIO.output(my_pin[0],st1)
        elif(count==2):
            st2=~st2
            GPIO.output(my_pin[1],st2)
        elif(count==3):
            st3=~st3
            GPIO.output(my_pin[2],st3)
        elif(count==4):
            st4=~st4
            GPIO.output(my_pin[3],st4)
        elif(count==5):
            st5=~st5
            st1=st2=st3=st4=st5
            GPIO.output(my_pin[0],st5)
            GPIO.output(my_pin[1],st5)
            GPIO.output(my_pin[2],st5)
            GPIO.output(my_pin[3],st5)
        count=0

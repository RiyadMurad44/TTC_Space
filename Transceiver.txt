import serial
import serial.tools.list_ports
import time
import enum
import pyMultiSerial as p

class Frames_ID_t(enum.Enum):
    MEASUREMENT_FRAME = 0X11
    ACC_FRAME = 0X12
    ANG_RATE_FRAME = 0X13
    ANGLES_FRAME = 0X14
    POS_FRAME = 0X15
    STATUS_FRAME = 0X16
    VER_FRAME = 0X17
    POWER_FRAME = 0X20 #32 <= x <= 47
    POWER_STATUS = 0X21

def enum_cycler(enum_cls):
    while True:
        for member in enum_cls:
            yield member.value

enum_cycle = enum_cycler(Frames_ID_t)

now = time.time()

frame_value = next(enum_cycle)

ports = serial.tools.list_ports.comports()
serial_port_power = serial.Serial(ports[1].device, baudrate=9600, timeout=0.01)
serial_port_ACS = serial.Serial(ports[2].device, baudrate=9600, timeout=0.01)

while True:
    ACS_byte = serial_port_ACS.read(11)
    power_byte = serial_port_power.read(11)
    if(time.time() - now > 0.01):
        now = time.time()
        if frame_value in [member.value for member in Frames_ID_t]:
            if frame_value == Frames_ID_t.MEASUREMENT_FRAME.value:
                serial_port_ACS.write(b'\0x11')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("1")
            elif frame_value == Frames_ID_t.ACC_FRAME.value:
                serial_port_ACS.write(b'\0x12')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("2")
            elif frame_value == Frames_ID_t.ANG_RATE_FRAME.value:
                serial_port_ACS.write(b'\0x13')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("3")
            elif frame_value == Frames_ID_t.ANGLES_FRAME.value:
                serial_port_ACS.write(b'\0x14')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("4")
            elif frame_value == Frames_ID_t.POS_FRAME.value:
                serial_port_ACS.write(b'\0x15')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("5")
            elif frame_value == Frames_ID_t.STATUS_FRAME.value:
                serial_port_ACS.write(b'\0x16')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("6")
            elif frame_value == Frames_ID_t.VER_FRAME.value:
                serial_port_ACS.write(b'\0x17')
                ACS_byte_length = ACS_byte[1]
                for i in range(2,ACS_byte_length+1):
                    ACS_new_byte[i-2] = ACS_byte[i]
                serial_port_ACS.write(ACS_new_byte)
                print(ACS_new_byte)
                print("7")
            elif frame_value == Frames_ID_t.POWER_FRAME.value:
                serial_port_power.write(b'\0x20')
                power_byte_length = power_byte[1]
                for i in range(2,power_byte_length+1):
                    power_new_byte[i-2] = power_byte[i]
                serial_port_power.write(power_new_byte)
                print(power_new_byte)
                print("8")
            elif frame_value == Frames_ID_t.POWER_STATUS.value:
                serial_port_power.write(b'\0x21')
                power_byte_length = power_byte[1]
                for i in range(2,power_byte_length+1):
                    power_new_byte[i-2] = power_byte[i]
                serial_port_power.write(power_new_byte)
                print(power_new_byte)
                print("9")
            else:
                print("Hasaki")

        frame_value = next(enum_cycle)




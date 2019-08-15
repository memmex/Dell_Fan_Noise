# Dell Fan Noise Control Script - Silence Your Poweredge

There are many complaints about noise of Dell PowerEdge servers.
I did some research on how to manually controlling the PowerEdge fans and want to list the essential commands them again. These are already widely known and have been published in many forums al[I'm an inline-style link](https://www.google.com)
    #
    # enable manual/static fan control
    ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x01 0x00
    #
    # disable manual/static fan control
    ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x01 0x01
    #
    # set fan speed to 0 rpm
    ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x02 0xff 0x00
    #
    # set fan speed to 20 %
    ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x02 0xff 0x14
    #
    # set fan speed to 30 %
    ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x02 0xff 0x1e
    #
    # set fan speed to 100 %
    ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x02 0xff 0x64


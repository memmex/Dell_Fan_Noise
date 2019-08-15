# Dell Fan Noise Control Script - Silence Your Poweredge


There are many complaints about noise of Dell PowerEdge servers on the internet.


I did some research on how to manually controlling the PowerEdge fans and want to list the essential commands again. These are already widely known and have been published in many forums already.

    # --- Dell Fan Control Commands ---
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


[I also wrote a small script](https://github.com/memmex/Dell_Fan_Noise/blob/master/dell_ipmi_fan_control.sh), that will check the servers temperature periodically (crontab) and disables or enables the dynamic fan control based on a temperature threshold. You may have to adjust the time frame depending on your server usage and add the script in your crontab:

    crontab -l > mycron
    echo "#" >> mycron
    echo "# At every 2nd minute" >> mycron
    echo "*/2 * * * * /bin/bash /opt/scripts/dell_ipmi_fan_control.sh >> /tmp/cron.log" >> mycron
    crontab mycron
    rm mycron
    chmod +x /opt/scripts/dell_ipmi_fan_control.sh

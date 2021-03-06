# Airthings Wave Plus Sensor Reader

* Forked from https://github.com/Airthings/waveplus-reader*
* updated to use python3 and write to a json file so it can be used to display data to homebridge via plugin.


* Prereqs
python 3.7+
pip3 (apt-get install python3-pip)
bluepy python module (pip3 install bluepy)

* Make sure the bluepy-helper app is executable<br/>
```shell
cd /usr/local/lib/python3.7/dist-packages/bluepy
chmod +x bluepy-helper
```


* Running
Run it like this (as root or sudo)
```shell
python3 /path/to/read_waveplus.py AirthingsSerialNumber
```
* output
Writes to /tmp/airthingswave.status.json

Should look something like this:

```json
{
    "CO2_lvl": "495.0",
    "VOC_lvl": "394.0",
    "humidity": "55.0",
    "pressure": "989.7",
    "radon_lt_avg": "6",
    "radon_st_avg": "10",
    "temperature": "22.06"
}
```

### Crontab
Run every 15 minutes, replace Serialnumber with your Airthings serialnumber.<br/>
```shell
crontab -e
```
```shell
*/15 * * * * python3 /home/pi/waveplus-reader/read_waveplus.py Serialnumber
```

### SD Card optimization	
To keep the SdCard happy for a long time add the following line to /etc/fstab<br/>
```shell
tmpfs /tmp tmpfs defaults,noatime,nosuid,nodev,noexec,mode=1777,size=256M 0 0
```

- restart the raspberry pi

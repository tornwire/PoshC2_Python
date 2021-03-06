# PoshC2
PoshC2 is a proxy aware C2 framework that utilises Powershell **and/or** equivalent (System.Management.Automation.dll) to aid penetration testers with red teaming, post-exploitation and lateral movement. Powershell was chosen as the base implant language as it provides all of the functionality and rich features without needing to introduce multiple third party libraries to the framework.

In addition to the Powershell implant, PoshC2 also has a basic dropper written purely in Python that can be used for command and control over Unix based systems such as Mac OS or Ubuntu.

The server-side component is written in Python for cross-platform portability and speed, a Powershell server component still exists and can be installed using the 'Windows Install' as shown below but will not be maintained with future updates and releases.


## Linux Install of [PoshC2_Python](https://github.com/nettitude/PoshC2_Python/)

Install using curl & bash
```
curl -sSL https://raw.githubusercontent.com/nettitude/PoshC2_Python/master/Install.sh | bash
```

Manual install

```
wget https://raw.githubusercontent.com/nettitude/PoshC2_Python/master/Install.sh
chmod +x ./Install.sh
./Install.sh
```

## Windows Install of [PoshC2](https://github.com/nettitude/PoshC2/)

```
powershell -exec bypass -c "IEX (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/nettitude/PoshC2/master/C2-Installer.ps1')"
```

## Viewing the logs

If you want others to be able to to just view the C2 output you can pipe the C2Server.py to a file and stdout with:

`python -u C2Server.py | tee -a /var/log/poshc2_server.log`

Note the `-u` option is required to prevent buffering.

Then you can view it with

`tail -f -n 50 /var/log/poshc2_server.log`

## Installing as a service

Installing as a service provides multiple benefits such as being able to log to service logs, viewing with journalctl and automatically starting on reboot.

1. Add the file in systemd
```
cp poshc2.service /lib/systemd/system/poshc2.service
systemctl enable poshc2.service
systemctl start poshc2.service
```

2. Stop the service
```
systemctl stop poshc2.service
```

3. Restart the service 
```
systemctl restart poshc2.service
```

4. View the output 
```
tail -f -n 50 /var/log/poshc2_server.log
```

5. Or alternatively us journalctl (but note this can be rate limited)
```
journalctl -n 20000 -u poshc2.service -f --output cat
```

## Issues / FAQs

If you are experiencing any issues during the installation or use of PoshC2 please refer checkout the open issues tracking page within GitHub. If this page doesn't have what you're looking for please open a new issue and we will try to resolve the issue asap.

If you are looking for tips and tricks on PoshC2 usage and optimisation, you are welcome to join the slack channel below.

## License / Terms of Use

This software should only be used for **authorised** testing activity and not for malicious use.

By downloading this software you are accepting the terms of use and the licensing agreement.


## Documentation

We maintain PoshC2 documentation over at https://poshc2.readthedocs.io/en/latest/

Find us on #Slack - [poshc2.slack.com](poshc2.slack.com) (to request an invite send an email to labs@nettitude.com)

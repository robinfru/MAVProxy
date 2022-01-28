[![MAVProxy status](https://ci.appveyor.com/api/projects/status/github/Ardupilot/MAVProxy?branch=master&svg=true)]( https://ci.appveyor.com/project/tridge/MAVProxy/history)

MAVProxy

This is a MAVLink ground station written in python. 

Please see https://ardupilot.org/mavproxy/index.html for more information

This ground station was developed as part of the CanberraUAV OBC team
entry

Requirements
-------

- A joystick InterLinkDXSimulatorController
- A Linux PC (tested on Ubuntu 20.04.3 LTS) : PC == controller
- A Raspberrypi : Raspberrypi == OBC (on board computer)
- A drone Holybro S500 with Pixhawk (flightsoftware controller)

Installation
-------

Follow these steps on your PC. It is necessary to have access to this repository.

```bash
sudo apt-get install python3 python3-wheel python3-setuptools
sudo apt-get install python3-dev python3-opencv python3-wxgtk4.0 python3-pip python3-matplotlib python3-lxml python3-pygame
pip3 install PyYAML "git+https://github.com/robinfru/MAVProxy.git" --user
echo "export PATH=$PATH:$HOME/.local/bin" >> ~/.bashrc
```

Your PC must allow the input connection of port 14550. Open it by following these instructions.

```bash
sudo netstat -tulpn
sudo /sbin/iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 14550 -j ACCEPT
sudo /usr/sbin/iptables-save
sudo netstat -tulpn
```

The Pixhawk must be configured. You can use mav.parm to set the drone with the good parameters.

Run it on the controller (where the joystick is connected)
-------

Just run `mavproxy.py --master=0.0.0.0:14550 --cmd "module load joystick"`.

Your controller must be connected to the same IPv4 network as the OBC (on board computer) and the joystick must be connected to the PC.

Run it on the OBC (on board computer)
-------

Just run `mavproxy.py --master=/dev/ttyACM2 --baudrate 57600 --out 192.168.0.195:14550 --cmd "set heartbeat 0"`. Replace IP address with the IP of the controller and the tty port with the tty where the Pixhawk is connected.

Your OBC must be connected to the same IPv4 network as the controller and the Pixhawk must be connected to OBC via USB.

License
-------

MAVProxy is released under the GNU General Public License v3 or later


Maintainers
-----------

The best way to discuss MAVProxy with the maintainers is to join the
mavproxy channel on ArduPilot discord at https://ardupilot.org/discord

Lead Developers: Andrew Tridgell and Peter Barker

Windows Maintainer: Stephen Dade

MacOS Maintainer: Rhys Mainwaring

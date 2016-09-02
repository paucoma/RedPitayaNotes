SCPI 
=====

`SCPI <https://en.wikipedia.org/wiki/Standard_Commands_for_Programmable_Instruments>`_ is short for **S** tandard  **C** ommands *for* **P** rogrammable **I** nstruments. 

  It allows for basic interaction with a remotely connected device, such as the Red Pitaya.

Following indications on the Start --> `Remote Control page <http://redpitaya.com/control/>`_

-----------
Red Pitaya
-----------

1. SSH into the Red Pitaya through Putty and the previously assigned static address or hostname.
2. Start the SCPI server :code:`systemctl start redpitaya_scpi &` .

  a. the ampersand **&** is to run in the background a response with the PID number should appear. 
  b. you can check to see if the server is active with :code:`systemctl status redpitaya_scpi`

  .. code-block:: bash

    :# systemctl status redpitaya_scpi 
    ● redpitaya_scpi.service - SCPI server for Red Pitaya
       Loaded: loaded ( /etc/systemd/system/redpitaya_scpi.service; disabled; vendor preset: enabled )
       Active: active (running) since Fri 2016-09-02 13:09:53 UTC; 1s ago
      Process: 1724 ExecStartPre=/bin/sh -c cat /opt/redpitaya/fpga/fpga_0.94.bit > /dev/xdevcfg (co
     Main PID: 1727 (scpi-server)
       CGroup: /system.slice/redpitaya_scpi.service
               └─1727 /opt/redpitaya/bin/scpi-server

    Sep 02 13:09:53 rp-f0138e systemd[1]: Starting SCPI server for Red Pitaya...
    Sep 02 13:09:53 rp-f0138e systemd[1]: Started SCPI server for Red Pitaya.
  ..

3. On your PC now you basically need to open a TCP socket to the Red Pitaya on Port 5000 and send SCPI commands
4. To see a list of accepted SCPI command :

  a. You can check to see which commands are accepted at the `Server implementation <https://github.com/RedPitaya/RedPitaya/blob/master/scpi-server/src/scpi-commands.c>`_
  b. I have started to compile a `little summary <scpi-commands.rst>`_ of what can be extracted from the source

-----------
PC - Putty
-----------

1. Open a putty Session with the following parameters:

  +-------+-------------------------------------+
  | Host  | <RedPitaya ip address or hostname>  |
  +-------+-------------------------------------+
  | Port  |  5000                               |
  +-------+-------------------------------------+
  | Type  |  Raw                                |
  +-------+-------------------------------------+

2. Type in an SCPI command and hit enter

  a. e.g. :code:`DIG:PIN LED2,1`
  b. The LED number 2 should turn on and stay on

3. When done, just close the session.


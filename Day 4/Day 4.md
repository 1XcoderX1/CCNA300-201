# Introduction to the Cisco ISO CLI
* Command-line interface
* The interface used to configure Cisco devices
* GUI (Graphical User Interface) also available - not convered here

## How to connect to a Cisco Device? (Console port)
![[cisco_console_port.png]]

To connect to the console port usually we have to bring our own device physically to the cisco device. A device can also be connected remotely as is demonstrated later.

There are 2 console ports on a Cisco device:
* A RJ45 Port
* A USB Mini-B Port
Either of these can be used to connect. 

A cable is used to connec to either of the above ports. To connect to the ethernet port we need to use a *Rollover cable* shown in the image below.

![[rollOver_cable.png]]

An 8 pair UTP cable is used in the rollover cable as well. The configuration of the pins is as follows:

![[rollOver_cable_pins.png]]

Once the device is connected, to access the CLI we need to use a terminal emulator like putty. The settings can be kept as is. The devices are connected via a serial connection as can be sen while using putty.

![[putty_conn.png]]

After this the CLI opens and we are ready to type commands in the CLI. by deafult the console enters into the user EXEC mode when a connection is established.

## User EXEC Mode
![[user_exec_mode.png]]

* User EXEC mode is very limited
* Users can look at some thing but can't make any changes to the configuration
* Also called 'user mode'

## Privileged EXEC Mode
To enter privileged EXEC mode, we have to execute the `enable` command.

![[privileged_EXEC_mode.png]]

* Provides complete access to view the device's configuration, restart the device, etc.
* Cannot change the configuration, but can change the time on the device, save the configuration file, etc.
* However, you can't change the time on the device or save a new configuration file, among many other things.

## User EXEC Mode vs Privileged EXEC Mode
![[userEXECmodevsPrivilegedEXECmode.png]]
This image is from the Cisco packet tracer software. The real device has many more commands than these.

* Use a **?** to view commands on the CLI
* Can be used in conjuction with alphabets as well

The CLI also supports the autocomplete feature and there are short commands as well for e.g., `en = enable`.

### Commands:

#### Configure terminal
`configure terminal`  or `conf t` 

#### Enable Password
`enable password PASSWORD` to set a password for privileged EXEC mode
Passwords are case sensitive. The password does not show while typing. If wrong password entered 3 times, *Bad Password* is shown by the CLI.

#### Exit
`exit` or `ex`

## Configuration files
There are two separate configuration fdiles kept on the device at once.

### Running-config
The current, active configuration file on the device. As we enter commands in the CLI, we edit the active configuration.

`show running-config` to view the config file. To save the configuration file, we can use 3 commands, usable from privileged EXEC mode.
1. `write`
2. `write memory`
3. `copy running-config startup-config`

### Startup-config
The configuration file that will be loaded upon restart of the device.
`show startup-config` to view the startup config file.

## Service password encryption
`conf t` to enter configuration terminal.
`service password-encryption` is the command used to encrypt all passwords. Cisco devices used Cisco pasword encryption (known as type 7), which is not very secure. Luckily, there is another way to encrypt passwords on Cisco devices. 

## Enable secret
`enable secret Cisco`: encrypts the password using MD5 encryption service. 

## Canceling commands
type no in frontof the command
e.g., `no service password-encryption` does not decryopt old passwords, but new passwords are no more encrypted. 















































#day 
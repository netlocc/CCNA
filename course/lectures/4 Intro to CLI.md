CLI = Command Line Interface
Connect to console port using RJ45 or USB-Mini B
    Rollover Cable
        1->8
        2->7
        3->6
        4->5
        5->4
        6->3
        7->2
        8->1
 

PuTTy is a good console emulator
    Settings
        Speed: 9600bps
        Data bits: 8
        Stop bits: 1
        Parity: None
        Flow control: None

View the available commands
	?
		ex) show ?
User EXEC Mode
Hostname>
    Read-only mode, sorta

    Command "enable" to enter Privileged EXEC Mode

Privileged EXEC Mode
Hostname#
    File write privileges
    conf t to elevate to GCM


Global Configuration Mode
conf t - (configure terminal)
Hostname(config)#
    "run [privileged-exec-level-command]"

running-config/startup-config
    running = current, active config
    startup = loaded upon restarting device
        "show running-config" 
        "show startup-config"

 Save Configuration    
        "write"
        "write memory"
        "copy running-config startup-config"

   Security (lol)
        "enable password ______"
	        enable password [type of encryption, #] (7 is cisco's proprietary encryption algorithm (deprecated)) [password, str]
        "service password-encryption"
            encrypts display of pw when viewing config 
        "enable secret _______"
            configures md5 encrypted pw
            (enable pw still displayed but not used)
            
Do command
	can run unprivileged commands from escalated modes like priv exec and global conf.
		ex) do show running-config (from global configuration mode)

   Removing Commands from Configuration
        type "no" before a Command
	        ex) no service password-encryption
		        (no future passwords will be encrypted but the current password remains encrypted)

Router>
Router#
Router(config)#

Router>enable
Router#configure terminal
Router(config)#enable password

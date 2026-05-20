# RPI4BootUp
This repository contains full documentation of how to run Python scripts on the Raspberry Pi 4b on start up.

## Step 1
Remote in or setup up desktop access to your device

---

## Step 2
Create a .service file inside your system and open with text editor of your choice in this case nano using this command

```bash
sudo nano /etc/systemd/system/nameofservice.serivce
```

---

## Step 3
In text editor setup service file according to this structure

```ini
[Unit]
Description=Describe want this service is doing. 
After=multi-user.target

[Serivce]
User=NameOfDevice  // can be found using "whoami" in terminal
WorkingDirectory=/path to python script you are trying to run on startup 1 directory out so that GPIO can write to it
ExecStart=/usr/bin/python3 /PathToPythonScriptFromRoot
Restart=Always
RestartSec=2 

[Install]
WantedBy=multi-user.target
```

---

## Step 4: Save Script
ctrl+x -> Y -> Enter on if using nano

---

## Step 5: Enable Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable nameofservice.service
sudo systemctl start nameofservice.service
```

---

## Step 6: Verification

```bash
sudo systemctl status nameofservice.service
```

Should say

```text
active(running)
```

---

## Step 7: Verify on Reboot

```bash
sudo reboot
sudo systemctl status nameofservice.service
```

Should be

```text
active(running)
```

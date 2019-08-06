# Start the Flask server on boot:

Set app.py permissions:

`chown pi webserver/app.py`

`chmod +x webserver/app.py`

Navigate to the services folder:

`cd /etc/systemd/system/`

Create a new service:

`sudo nano horizongui.service`

Include the following text, correcting the directories if they don't match the location of the GUI start script:
```
[Unit]
Description=Arribada Horizon GUI
After=network.target

[Service]
User=pi
WorkingDirectory=/home/pi/webserver/
ExecStart=/usr/bin/python /home/pi/webserver/app.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Set the service file's permissions:

`sudo chmod 644 horizongui.service`

Reload the service daemon so it refreshes its list of services:

`sudo systemctl daemon-reload`

Start the Flask server:

`sudo systemctl start horizongui`

Check it's running correctly:

`sudo systemctl status horizongui`

If no errors appear, set the new service to run on boot:

`sudo systemctl enable horizongui`

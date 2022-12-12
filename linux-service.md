# Linux service

```
cd /etc/systemd/system
```
Create a file named your-service.service and include the following:
```
[Unit]
Description=<description about this service>

[Service]
User=<user e.g. root>
WorkingDirectory=<directory_of_script e.g. /root>
ExecStart=<script which needs to be executed>
Restart=always

[Install]
WantedBy=multi-user.target
```
For Python specific projects which include virtual environment:

```
[Unit]
Description=<project description>

[Service]
User=<user e.g. root>
WorkingDirectory=<path to your project directory containing your python script>
ExecStart=/home/user/.virtualenv/bin/python main.py
Restart=always
# replace /home/user/.virtualenv/bin/python with your virtualenv and main.py with your script

[Install]
WantedBy=multi-user.target
```
OR
```
[Unit]
Description=<project description>

[Service]
User=<user e.g. root>
WorkingDirectory=<path to your project directory>
ExecStart=/bin/bash -c 'cd /home/ubuntu/project/ && source venv/bin/activate && python test.py'

[Install]
WantedBy=multi-user.target
```

Reload the service files to include the new service.
```
sudo systemctl daemon-reload
```

Start your service
```
sudo systemctl start your-service.service
```

To check the status of your service
```
sudo systemctl status example.service
```

To enable your service on every reboot
```
sudo systemctl enable example.service
```

To disable your service on every reboot
```
sudo systemctl disable example.service
```
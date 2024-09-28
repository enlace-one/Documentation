# Computer Shows Connected to Wifi But No Internet

## Reset Socket/IP/DNS Settings
Run the following commands
```
netsh winsock reset
netsh int ip reset
ipconfig /release
ipconfig /renew
ipconfig /flushdns
```
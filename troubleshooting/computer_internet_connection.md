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

# Computer Connected to Wifi but Not Company Network

Open user certificates and delete everything under Personal -> Certificates then wait for it to re-populate. 
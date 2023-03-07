# tilde-switch
Swaps "section sign(§)” with “tilde(~)”



### Create an executable file in your home directory ~/.tilde-switch
```
cat << 'EOF' > ~/.tilde-switch && chmod +x ~/.tilde-switch
hidutil property --set '{"UserKeyMapping":[{"HIDKeyboardModifierMappingSrc":0x700000035,"HIDKeyboardModifierMappingDst":0x700000064},{"HIDKeyboardModifierMappingSrc":0x700000064,"HIDKeyboardModifierMappingDst":0x700000035}]}'
EOF
```

### Create a system task
```
sudo /usr/bin/env bash -c "cat > /Library/LaunchDaemons/org.custom.tilde-switch.plist" << EOF
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>org.custom.tilde-switch</string>
    <key>Program</key>
    <string>${HOME}/.tilde-switch</string>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <false/>
  </dict>
</plist>
EOF
```
The above command basically runs the file ~/.tilde-switch on every start

### Activate or load the task
```
sudo launchctl load -w -- /Library/LaunchDaemons/org.custom.tilde-switch.plist
```


## Revert changes:
```
sudo launchctl unload -w -- /Library/LaunchDaemons/org.custom.tilde-switch.plist; sudo rm -f -- /Library/LaunchDaemons/org.custom.tilde-switch.plist ~/.tilde-switch
```

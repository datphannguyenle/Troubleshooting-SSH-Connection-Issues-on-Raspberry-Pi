# Troubleshooting SSH Connection Issues on Raspberry Pi

If you are unable to use PuTTY to access your Raspberry Pi and suspect that port 22 might be closed, follow these steps to diagnose and fix the problem.

## Step 1: Check Network Connection
1. **Ensure that both your Raspberry Pi and your computer are connected to the same network.**
2. **Check the Raspberry Pi’s IP address**, as it may have changed. You can find it by directly accessing your Raspberry Pi and running:
   ```bash
   hostname -I
   ```
3. **Ping the Raspberry Pi** from your computer to ensure it is reachable:
   ```bash
   ping <Raspberry_Pi_IP>
   ```

## Step 2: Check SSH Port (Port 22)
1. **Check the status of the SSH service**:
   If you have direct access to the Raspberry Pi (via keyboard and monitor), you can check the SSH service status:
   ```bash
   sudo systemctl status ssh
   ```
   If the SSH service is not running, start it with:
   ```bash
   sudo systemctl start ssh
   ```
   To ensure that the SSH service starts automatically on boot, use:
   ```bash
   sudo systemctl enable ssh
   ```

2. **Check if Port 22 is open**:
   You can check this by running:
   ```bash
   sudo netstat -tuln | grep :22
   ```
   If Port 22 is listening, you should see an output like this:
   ```plaintext
   tcp        0      0 0.0.0.0:22            0.0.0.0:*               LISTEN
   tcp6       0      0 :::22                 :::*                    LISTEN
   ```

## Step 3: Check Firewall (iptables)
If you have configured a firewall on your Raspberry Pi, make sure that Port 22 is open. You can check this by running:
```bash
sudo iptables -L
```
If necessary, you can open Port 22 with the following command:
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

## Step 4: Check SSH Configuration File
Ensure that the SSH configuration file does not have any issues. Open the SSH configuration file to check:
```bash
sudo nano /etc/ssh/sshd_config
```
Make sure the following line is not commented out (no `#` at the beginning):
```plaintext
Port 22
```
After verifying, restart the SSH service:
```bash
sudo systemctl restart ssh
```

## Step 5: Try Reconnecting
After performing the above steps, try connecting again using PuTTY.

If you still cannot access your Raspberry Pi, there may be a network configuration issue, or you might consider reinstalling the Raspberry Pi OS to reset all settings to default.
```

Bạn có thể lưu nội dung này vào một file với tên là `troubleshooting_ssh_connection.md`.

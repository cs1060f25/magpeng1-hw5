# CS1060 Homework 5

This repository contains the implementation for CS1060 Homework 5, including SQL injection testing and a vulnerability scanner.

## 5.2: SQL Injection Attack

Successfully implemented a SQL injection attack against the vulnerable endpoint at https://cat-hw4.vercel.app/county_data.

### Files:
- `test.json`: Valid test data for the endpoint
- `attack.json`: Malicious payload that exploits the SQL injection vulnerability
- `prompts.txt`: Documentation of AI prompts used to develop the attack

### AI Models Used:
- **Cascade (Windsurf)**: Used for understanding SQL injection techniques and crafting the malicious payload. The model provided guidance and direct code on breaking out of SQL string literals and constructing OR clauses for database dumping.
    - **Attack Results**: The SQL injection attack successfully bypassed the original query constraints and returned diverse data from the database (limited to 100 results as required). The attack payload `"Adult obesity' OR '1'='1' LIMIT 100 --"` effectively terminated the original string and added a condition that matches all rows.
    - **Guardrails Encountered**: No significant guardrails were encountered when asking Cascade about SQL injection techniques for educational purposes. The model provided helpful technical guidance when the context was clearly educational and security research-focused.
- **ChatGPT 5**: Used for understanding SQL injection techniques and crafting the malicious payload. The model provided context but no direct code on breaking out of SQL string literals.
    - **Attack Results**: After prompting more thoroughly by framing the prompt as a security research exercise (asking to provide abstract, conceptual guidance), the model provided a partial code template with explanation for how tautology could be used. The SQL injection attack was successful but some user input was required to complete the payload.
    - **Guardrails Encountered**: When using ChatGPT 5, the model only provided explanations of the SQL injection technique and did not provide direct code, only snippets (fill in the blank code) after more prompting. 

## 5.3: Vulnerability Scanner

Successfully implemented a Python vulnerability scanner that detects weak HTTP and SSH credentials on localhost.

### Files:
- `vulnerability_scanner.py`: Main scanner program that detects weak credentials
- `requirements.txt`: Python dependencies (requests, paramiko)
- `http_server.py`: Vulnerable HTTP server for testing (from hw5_server template)
- `ssh_server.py`: Vulnerable SSH server for testing (from hw5_server template)

### Scanner Features:
- **Port Scanning**: Scans localhost (127.0.0.1) for open TCP ports below 9000
- **HTTP Basic Auth Testing**: Tests discovered HTTP services with weak credentials
- **SSH Password Auth Testing**: Tests discovered SSH services with weak credentials
- **Clean Output**: Prints successful connections in RFC 3986 format with server responses
- **Error Handling**: Silently handles exceptions without printing error messages
- **Verbose Mode**: Optional `-v` flag for debugging information

### Credentials Tested:
```python
credentials = {
    'admin': 'admin',
    'root': 'abc123', 
    'skroob': '12345'
}
```

### Example Output:
```
ssh://skroob:12345@127.0.0.1:2222 success
http://admin:admin@127.0.0.1:8080 success
```

### AI Models Used:
- **Cascade (Windsurf)**: Used for implementing the vulnerability scanner logic, port scanning techniques, and HTTP/SSH authentication testing. The model provided complete code implementations for socket-based port scanning, HTTP basic authentication, and SSH password authentication using paramiko.

### Testing Results:
The vulnerability scanner successfully detected weak credentials on both HTTP and SSH services running on localhost. It correctly formatted output according to RFC 3986 syntax and captured server responses. The scanner handled various port configurations and credential combinations as expected.

### Grading Compliance:
- **Port Scanning**: Uses nmap tool (python-nmap library) as specified, with socket-based fallback if nmap binary unavailable
- **Credential Testing**: Tests all required credentials (admin/admin, root/abc123, skroob/12345) 
- **Output Format**: Strict RFC 3986 compliance: `protocol://user:pass@host:port response`
- **Error Handling**: All exceptions caught silently, no error output in normal mode
- **Flexible Testing**: Works with any port/credential combination from the specified dictionary
- **Server Output Capture**: Correctly captures and displays server responses (tested with "success" and other outputs)

## ssh_server.py
Usage:
```
python3 ssh_server.py # defaults to 2222, admin, admin
python3 ssh_server.py --port 2224 
python3 ssh_server.py --port 2224 --username myuser --password mypass
```

## http_server.py
Usage:
```
python3 http_server.py # defaults to 8080, admin, admin
python3 http_server.py --port 8081 
python3 http_server.py --port 8081 --username user --password pass
```

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

### Guardrails Encountered:
No significant guardrails were encountered when asking Cascade about SQL injection techniques for educational purposes. The model provided helpful technical guidance when the context was clearly educational and security research-focused.

## 5.3: Vulnerability Scanner

Stub HTTP and SSH servers for testing the vulnerability scanner.
Prototyped with Codeium Windsurf and the DeepSeek V3 model.
Intentionally incomplete—these programs do not handle all situations
gracefully.

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

# Fifty Shades of White (Pinkman)
## Reverse
# Facile


```python
#!/usr/bin/python3
from hashlib import sha256
import uuid
import base64
import subprocess
import sys

# generate valid serial given a name

flags_found = 0
cpt = 0

def keygen(name):
    print("[+] Generating license for {}".format(name))
    bytes_to_match = []

    for i in range(0, 3):
        v10 = 0
        for j in range(i, len(name), 3):
            v10 += ord(name[j])
        v8 = (19 * v10 + 55) % 127

        bytes_to_match.append(v8)

    #print(bytes_to_match)

    ascii = "0123456789abcdef"

    bytes_found = ""

    for byte in bytes_to_match:
        found = False
        for char1 in ascii:
            for char2 in ascii:
                if (55 * int(char1 + char2, 16) + 19) % 127 == byte:
                    #print(char1 + char2)
                    bytes_found = bytes_found + char1 + char2
                    found = True
                    break  # Move to the next byte in the loop
            if found:
                break  # Move to the next byte in the loop

    #print("sha256 hash of serial for username {} must start with {}".format(name, bytes_found))

    while True:
        serial = str(uuid.uuid4())
        #print("random uuid: ", random_uuid)
        hash_str = sha256(serial.encode()).hexdigest()
        #print("hash str: ", hash_str)
        #print("hash prefix: ", hash_str[:6])
        if hash_str[:6] == bytes_found:
            break

    print("\t[+] Serial:", serial)
    #print("SHA256 hash:", sha256(serial.encode()).hexdigest())

    license_data = "Name: {}\nSerial: {}\nType: 1\n".format(name, serial)

    b64_license_data = base64.b64encode(bytes(license_data, encoding='utf-8'))
    b64_license_data = str(b64_license_data)[2:][:-1]
    license = "----BEGIN WHITE LICENSE----\n{}\n-----END WHITE LICENSE-----".format(b64_license_data)

    print("\t[+] Valid license for user {}:\n".format(name))
    print(license)
    print("\n")

    return license

def get_username():
    # Read the initial prompt
    initial_prompt = process.stdout.readline().strip()
    print(initial_prompt)

    # Read the request for a valid admin license
    request_prompt = process.stdout.readline().strip()
    print(request_prompt)

    if "Well done" in request_prompt:
        if "Pinkman challenge" in request_prompt:
            # print second flag
            request_prompt = process.stdout.readline().strip()
            print(request_prompt)
            sys.exit(0)
        request_prompt = process.stdout.readline().strip()
        print(request_prompt)
        request_prompt = process.stdout.readline().strip()
        print(request_prompt)

    # Extract the username (assuming it's provided in the prompt)
    username = request_prompt.split(":")[-1].strip()

    return username

def send_license(license):
    # Send the processed username to the process
    process.stdin.write(license)
    process.stdin.write("\n\n")
    process.stdin.flush()

if __name__ == '__main__':
    process = subprocess.Popen(['nc', 'challenges.france-cybersecurity-challenge.fr', '2250'], 
                           stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)

    while True:
        username = get_username()

        # Process the username
        if username == "Walter White Junior":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogV2FsdGVyIFdoaXRlIEp1bmlvcgpTZXJpYWw6IDFkMTE3YzVhLTI5N2QtNGNlNi05MTg2LWQ0Yjg0ZmI3ZjIzMApUeXBlOiAxMzM3Cg==\n-----END WHITE LICENSE-----")
        elif username == "Jesse Pinkman":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogSmVzc2UgUGlua21hbgpTZXJpYWw6IDZlMmIwMDdkLWRhOTYtNGNkOC1iNjNmLWVjZjg5YmY0MGQ0NApUeXBlOiAxCg==\n-----END WHITE LICENSE-----")
        elif username == "Saul Goodman":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogU2F1bCBHb29kbWFuClNlcmlhbDogNTIyYzY4YTgtYWVlNS00NGY1LTg3ZDYtMmY2MjI0M2ZmNjE4ClR5cGU6IDEK\n-----END WHITE LICENSE-----")
        elif username == "Gus Fring":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogR3VzIEZyaW5nClNlcmlhbDogMTZhMzkwMDctNTE2MS00ZjdiLWIzNjMtYjk5Y2ZhOWMwODY0ClR5cGU6IDEK\n-----END WHITE LICENSE-----")
        elif username == "Hank Schrader":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogSGFuayBTY2hyYWRlcgpTZXJpYWw6IGRkZjQ3YjU2LTk2NGQtNDUyYy1iZmQ4LTc4ZDY2N2FmOTg5MwpUeXBlOiAxCg==\n-----END WHITE LICENSE-----")
        elif username == "Mike Ehrmantraut":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogTWlrZSBFaHJtYW50cmF1dApTZXJpYWw6IDM2ZTVlZDk1LTkyODQtNDA0NC05YWYzLTFlNDE3NTJjNTZjOQpUeXBlOiAxCg==\n-----END WHITE LICENSE-----")
        elif username == "Tuco Salamanca":
            send_license("----BEGIN WHITE LICENSE----\nTmFtZTogVHVjbyBTYWxhbWFuY2EKU2VyaWFsOiA4ZTA1ZTE1MC0zZTcxLTQwNzAtODg0My02MjZhYWIwMGQ4NGUKVHlwZTogMQo=\n-----END WHITE LICENSE-----")
        else:
            license = keygen(username)
            send_license(license)




```

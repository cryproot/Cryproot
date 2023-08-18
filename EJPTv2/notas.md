# Documentación: Comandos de enumeración

## Descripción
Esta documentación proporciona una introducción básica de los comandos útlices para el examen EJPTv2

### FTP File Transfer Protocol - 21
El Protocolo de Transferencia de Archivos (FTP) es un estándar de red para transferir archivos entre sistemas, operando en el puerto 21. Aunque es antiguo y carece de seguridad, permite cargar y descargar archivos en servidores remotos

```python
nmap -p21 --script ftp-anon IP
wget -m --no-passive ftp://anonymous:anonymous@IP
sudo nmap -sV -p21 -sC -A IP
nc IP 21
```

#### Diccionarios
Lista de palabras para ataques de fuerza bruta

```python
/usr/share/metasploit-framework/data/wordlists/common_users.txt
/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
```

### Server Message Block (SMB) - 137,138,139,445
Server Message Block (SMB) es un protocolo de red que facilita el intercambio de archivos, impresoras y recursos entre sistemas. Opera en los puertos 137, 138, 139 y 445. A pesar de su utilidad, el puerto 445 es conocido por vulnerabilidades de seguridad.

```python
smbclient -N -L //IP (list shares)
nmap -sV -sC -p 445 IP
smbclient //IP/notes (connecting shares)
sudo nmap IP -sV -sC -p139,445
rpcclient -U "" IP (srvinfo, enumdomains, querydominfo, netshareenumall, enumdomusers)
smbmap -H IP -u "" -p "" (para revisar que permisos)
smbmap -H IP -u administrator -p smbserver_771 -x 'ipconfig'
smbmap -H IP -u Administrator -p 'smbserver_771' -r 'C$'
smbmap -H IP -u Administrator -p 'smbserver_771' --download 'C$\flag.txt'
crackmapexec smb IP --shares -u '' -p '' (revisar permisos)
./enum4linux-ng.py IP -A
enum4linux -u vagrant -p vagrant -U IP (enumerar usuarios)
nmap -p445 --script smb-protocols IP
nmap -p445 --script smb-security-mode IP
nmap -p445 --script smb-enum-sessions IP
nmap --script smb-os-discovery -p445 IP
enum4linux -r -u "admin" -p "password1" IP (obtener el ssid de los usuarios)
cp /usr/share/doc/python3-impacket/examples/psexec.py /root/Desktop

Tools: 
Psexec - conexión para smb que nos brinda shell
https://github.com/fortra/impacket/blob/master/examples/psexec.py
```

#### Diccionarios
Lista de palabras para ataques de fuerza bruta

```python
/usr/share/metasploit-framework/data/wordlists/common_users.txt
/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
/usr/share/wordlists/metasploit/unix_passwords.txt
/usr/share/wordlists/metasploit/unix_users.txt
/usr/share/wordlists/rockyou.tx
```

### Secure Shell (SSH) - 22
Secure Shell (SSH) es un protocolo de red seguro que permite la comunicación y el acceso remoto a sistemas mediante el cifrado de datos. Utiliza el puerto 22 para establecer conexiones seguras y autenticadas, garantizando la confidencialidad y la integridad de la información transmitida.

```python
nmap --script ssh2-enum-algos IP
nmap --script ssh-hostkey --script-args ssh_hostkey=full IP
nmap -p 22 --script ssh-auth-methods --script-args="ssh.user=student" IP
find / -name "flag" (busca bandera)
```

#### Diccionarios
Lista de palabras para ataques de fuerza bruta

```python
/usr/share/metasploit-framework/data/wordlists/common_users.txt
/usr/share/metasploit-framework/data/wordlists/common_passwords.txt
```
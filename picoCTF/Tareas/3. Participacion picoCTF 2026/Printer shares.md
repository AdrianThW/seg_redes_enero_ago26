#### Description

Oops! Someone accidentally sent an important file to a network printer—can you retrieve it from the print server? The printer is on `57721`. you can try `$ nc -vz mysterious-sea.picoctf.net 57721`

Dado que hay que hacer una instancia el puerto cambiará, las pistas son las siguientes:

1. Conocer los protocolos SMB serian de mucha ayuda.
2. SMBCLIENT y SMBUTIL son buenas herramientas.

El reto gira en impresoras de red, el objetivo es encontrar un archivo que contiene la flag dentro de un recurso compartido.

1. Checar conectividad

```
adrian@ThW:~$ nc -vz mysterious-sea.picoctf.net 50799
Connection to mysterious-sea.picoctf.net (3.130.79.223) 50799 port [tcp/*] succeeded!
```

2. Listar los recursos compartidos.

| Parte    | Significado                      |
| -------- | -------------------------------- |
| `-L`     | Lista los recursos compartidos   |
| `//host` | Dirección del servidor           |
| `-p`     | Puerto personalizado             |
| `-N`     | Sin contraseña (anonymous login) |

```
adrian@ThW:~$ smbclient -L //mysterious-sea.picoctf.net -p 50799 -N

	Sharename       Type      Comment
	---------       ----      -------
	shares          Disk      Public Share With Guests
	IPC$            IPC       IPC Service (Samba 4.19.5-Ubuntu)
SMB1 disabled -- no workgroup available
```

3.  Conectarnos al recurso compartido, y tendremos acceso al servidor remoto
4. ls para listar los archivos, se descarga flag.txt con el comando get y fuera del smbclient le damos cat para ver la flag.
```
adrian@ThW:~$ smbclient //mysterious-sea.picoctf.net/shares -p 50799 -N
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Fri Mar  6 14:25:45 2026
  ..                                  D        0  Fri Mar  6 14:25:45 2026
  dummy.txt                           N     1142  Wed Feb  4 15:22:17 2026
  flag.txt                            N       37  Fri Mar  6 14:25:45 2026

		65536 blocks of size 1024. 57796 blocks available
smb: \> exit
adrian@ThW:~$ ls
Desktop  Documents  Downloads  flag.txt  Music  Pictures  protonvpn-stable-release_1.0.8_all.deb  Public  snap  Templates  Videos
adrian@ThW:~$ cat flag.txt 
picoCTF{5mb_pr1nter_5h4re5_7a400ec3}
```

## Referencias

El protocolo SMB ([Server Message Block](https://www.google.com/search?client=ubuntu-sn&channel=fs&q=Server+Message+Block&mstk=AUtExfCgZ0HEDO6Y52Q7S0h21nnJ7sA72NxStB8lK_wLK_12o7DT15DKwt8WyNA4ZrbgepxMVcYMhqeHeVlneDyc0plTG0ZXRme906hzdfhr1J0vzXOyNfM9C5POsVtGe2IoFgI&csui=3&ved=2ahUKEwjdg7CthKuTAxWgJ0QIHcvtCsYQgK4QegYIAQgAEAM)) es un protocolo de red de capa de aplicación, utilizado principalmente por Windows, para compartir archivos, impresoras y puertos serie entre nodos. Permite leer, crear y actualizar archivos en servidores remotos, funcionando sobre TCP/IP. Sus versiones modernas (SMB 3.x) ofrecen cifrado y alta seguridad.

SMB (Server Message Block) es un protocolo que permite:

- Compartir archivos en red
- Acceder a carpetas remotas como si fueran locales

Ejemplo real:

- En Windows: `\\IP\carpeta`
- En Linux: usando `smbclient`
- 
`smbclient` es una herramienta en Linux que sirve para:

- Listar carpetas compartidas en un servidor
- Conectarse a esas carpetas
- Descargar archivos
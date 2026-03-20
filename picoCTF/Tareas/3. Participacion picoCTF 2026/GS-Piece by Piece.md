## Descripción 
After logging in, you will find multiple file parts in your home directory. These parts need to be combined and extracted to reveal the flag.SSH to `dolphin-cove.picoctf.net`:`54285` and login as `ctf-player` with password `a15d25e1`.
## Solución 
Nos conectamos al puerto con el usuario indicado y vemos que hay en home, hay instrucciones, se leen, nos da una contraseña a futuro que nos piden cuando descomprimamos el archivo creado luego de juntar las partes de la bandera que se reparten en varios archivos
```
ctf-player@pico-chall$ cat instructions.txt 
Hint:

- The flag is split into multiple parts as a zipped file.
- Use Linux commands to combine the parts into one file.
- The zip file is password protected. Use this "supersecret" password to extract the zip file.
- After unzipping, check the extracted text file for the flag.
  
ctf-player@pico-chall$ cat part_a* > bandera

ctf-player@pico-chall$ unzip bandera
Archive:  bandera
[bandera] flag.txt password: 
 extracting: flag.txt

ctf-player@pico-chall$ cat flag.txt
picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_da494d2e}ctf-player@pico-chall$ cat flag.

```
picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_da494d2e}
## Notas
## Referencias

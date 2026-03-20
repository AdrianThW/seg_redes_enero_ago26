## MY GIT

### Descripción
I have built my own Git server with my own rules!

Additional details will be available after launching your challenge instance.
### Solución

#### Solución 1 
1. Clonamos el repositorio con la contraseña proporcionada:
```
   git clone ssh://git@foggy-cliff.picoctf.net:51921/git/challenge.git
   Contraseña: 1a03c9e3
```
2. Leemos el README.md dentro del repositorio:
```
   "Only flag.txt pushed by root:root@picoctf will be updated with the flag."
```
3. Configuramos el nombre de usuario y email localmente:
```
   cd challenge
   git config user.name "root"
   git config user.email "root@picoctf"
```
4. Creamos un archivo flag.txt vacío, lo añadimos y hacemos commit:
```
   touch flag.txt
   git add flag.txt
   git commit -m "Add flag for root"
```
5. Hacemos push al repositorio remoto:
```
   git push
```
6. El servidor verifica el autor del commit y nos muestra la flag:
```
   "remote: Here's your flag: picoCTF{1mp3rs0n4t4_g17_345y_367122f4}"
```

### Notas adicionales


### Referencias

-
## bytemancy 0

### Descripción
Can you conjure the right bytes? The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_candy_mountain/a32ca0e42d9494e3cf81e345699e8ae50415274c00871b1e8594d0fa0ce7078c/app.py).

Additional details will be available after launching your challenge instance.
### Solución

#### Solución 1
  
1. Nos conectamos al servicio:
```
   nc candy-mountain.picoctf.net 51796
```
2. El servicio muestra un mensaje:
```
   "Send me ASCII DECIMAL 101, 101, 101, side-by-side, no space."
```
3. Interpretamos que ASCII DECIMAL 101 corresponde al carácter 'e'. Enviamos el carácter 'e' tres veces.
4. Enviamos la respuesta usando un one-liner:
```
   echo -n "eee" | nc candy-mountain.picoctf.net 51796
```
5. El servicio responde con la flag:
		picoCTF{pr1n74813_ch4r5_334c472c}

### Notas adicionales


### Referencias

-
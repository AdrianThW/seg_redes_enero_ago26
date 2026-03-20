## bytemancy 1

### Descripción
Can you conjure the right bytes? The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_foggy_cliff/89d4e001a32151c23b9ad54e9f12939e30d20903b113433cbd5e65df11ffabf7/app.py).

Additional details will be available after launching your challenge instance.
### Solución

#### Solución 1
1. Nos conectamos al servicio:
```
   nc foggy-cliff.picoctf.net 61075
```
2. El servicio muestra:
```
   "Send me ASCII DECIMAL 101 1751 times, side-by-side, no space."
```
3. ASCII DECIMAL 101 es el carácter 'e'. Debemos enviar 1751 veces la letra 'e'.
4. Generamos la cadena con Python y la enviamos:
```
   python3 -c "print('e' * 1751, end='')" | nc foggy-cliff.picoctf.net 61075
```
   
   O con salto de línea:
```
   python3 -c "print('e' * 1751)" | nc foggy-cliff.picoctf.net 61075
```
5. El servicio procesa la entrada y responde con la flag.
	Flag obtenida
		picoCTF{h0w_m4ny_e's???_be9356c0}

### Notas adicionales


### Referencias

-
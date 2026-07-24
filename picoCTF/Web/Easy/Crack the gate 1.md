We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: `[ctf-player@picoctf.org](mailto:ctf-player@picoctf.org)`. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?

HInts:

1. Developers sometimes leave notes in the code; but not always in plain text.

2. A common trick is to rotate each letter by 13 positions in the alphabet.

Usando las pistas hay una linea de código comentada:

```HTML
<!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->
```

Hay que decifrarlo con ROT13 

Con esto nos damos cuenta que el servidor con el siguiente header saltará la contraseña y nos dará acceso a la flag.

Usando burpsuite usamos el repetidor para obtener la peticion y añadir el siguiente header.

```
X-Dev-Access: yes
```


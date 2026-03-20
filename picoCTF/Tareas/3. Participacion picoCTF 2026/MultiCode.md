#### Description

We intercepted a suspiciously encoded message, but it’s clearly hiding a flag. No encryption, just multiple layers of obfuscation. Can you peel back the layers and reveal the truth? Download the [message](https://challenge-files.picoctf.net/c_plain_mesa/4986bcdd15422ff14839a371ad1807f27508401eab11d33c48acf3b4633cf6ef/message.txt).

Las pistas son las siguientes:

1. The flag has been wrapped in several layers of common encodings such as ROT13, URL encoding, Hex, and Base64. Can you figure out the order to peel them back?
2. Usar CyberChef no será de mucha ayuda

En el primer hint nos da gran parte de la solucion, solo hay que decifrar el orden de las capas y hacerlo en orden para llegar a la flag 

Primero hice cat para ver que onda:

```
adrian@ThW:~/Documents/adicional_seg$ cat message.txt 
NjM3NjcwNjI1MDQ3NTMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM2MzY2ZjM1MzQzMjM1MzcyNTM3NDQ=
```

Vemos que el texto esta en Base64, hay que decodificarlo.

```
echo "NjM3NjcwNjI1MDQ3NTMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM2MzY2ZjM1MzQzMjM1MzcyNTM3NDQ=" | base64 -d

Resultado: 637670625047532537426172666772715f72617030717661745f36366f3534323537253744
```

Este siguiente esta en Hexadecimal

```
echo "637670625047532537426172666772715f72617030717661745f36366f3534323537253744" | xxd -r -p

Resultado: cvpbPGS%7Barfgrq_rap0qvat_66o54257%7D
```

Este se llama URL Encoding, para decodificar se puede usar python3 

```
python3 -c "import urllib.parse; print(urllib.parse.unquote('cvpbPGS%7Barfgrq_rap0qvat_66o54257%7D'))"

Resultado: cvpbPGS{arfgrq_rap0qvat_66o54257}
```

Lo obtenido es ROT13

```
echo "cvpbPGS{arfgrq_rap0qvat_66o54257}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'

flag: picoCTF{nested_encoding_66b54257}
```

# Capas de codificación utilizadas

## 1. Base64

Base64 es un esquema de codificación que convierte datos binarios en texto utilizando un conjunto de 64 caracteres (A–Z, a–z, 0–9, +, /).

- Se usa para transmitir datos en medios que solo soportan texto.
- No es cifrado, solo codificación.
- Suele terminar con `=` como relleno (padding).

## 2. Hexadecimal (Hex)

El formato hexadecimal representa datos usando base 16 (0–9 y a–f).

- Cada byte se representa con dos caracteres hexadecimales.
- Es común en análisis forense y bajo nivel.
- Facilita la lectura de datos binarios.

## 3. URL Encoding (Percent Encoding)

Es un mecanismo para codificar caracteres en URLs usando el formato `%XX`, donde `XX` es el valor hexadecimal del carácter.

- Se usa para transmitir caracteres especiales en URLs.
- Caracteres como `{`, `}`, espacio, etc., se codifican.

## 4. ROT13

ROT13 es un cifrado por sustitución que rota cada letra 13 posiciones en el alfabeto.

- Solo afecta letras (A–Z, a–z).
- Aplicarlo dos veces devuelve el texto original.
- Es simple y no es seguro.
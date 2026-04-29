#### Description

This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://challenge-files.picoctf.net/c_fickle_tempest/eb2eaca69cb975c96a289b4db182ed439cf7f6bc542b135b8a9a1e9834c068c1/VaultDoor1.java)

```
import java.util.*;

class VaultDoor1 {
    public static void main(String args[]) {
        VaultDoor1 vaultDoor = new VaultDoor1();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
	String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	}
    }

    // I came up with a more secure way to check the password without putting
    // the password itself in the source code. I think this is going to be
    // UNHACKABLE!! I hope Dr. Evil agrees...
    //
    // -Minion #8728
    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == '8' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == '9' &&
               password.charAt(30) == 'd' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == 'e' &&
               password.charAt(26) == '2' &&
               password.charAt(31) == '8';
    }
}
```

Hay que hacer sort a la nueva passoword 

```
adrian@ThW:~/Documents/adicional_seg/reversing$ cat flag | sort 
		password.charAt(00)  == 'd' &&
               password.charAt(01)  == '3' &&
               password.charAt(02)  == '5' &&
               password.charAt(03)  == 'c' &&
               password.charAt(04)  == 'r' &&
               password.charAt(05)  == '4' &&
               password.charAt(06)  == 'm' &&
               password.charAt(07)  == 'b' &&
               password.charAt(08)  == 'l' &&
               password.charAt(09)  == '3' &&
               password.charAt(10) == '_' &&
               password.charAt(11) == 't' &&
               password.charAt(12) == 'H' &&
               password.charAt(13) == '3' &&
               password.charAt(14) == '_' &&
               password.charAt(15) == 'c' &&
               password.charAt(16) == 'H' &&
               password.charAt(17) == '4' &&
               password.charAt(18) == 'r' &&
               password.charAt(19) == '4' &&
               password.charAt(20) == 'c' &&
               password.charAt(21) == 'T' &&
               password.charAt(22) == '3' &&
               password.charAt(23) == 'r' &&
               password.charAt(24) == '5' &&
               password.charAt(25) == '_' &&
               password.charAt(26) == '2' &&
               password.charAt(27) == '9' &&
               password.charAt(28) == 'e' &&
               password.charAt(29) == '8' &&
               password.charAt(30) == 'd' &&
               password.charAt(31) == '8';
adrian@ThW:~/Documents/adicional_seg/reversing$ 

```

```
adrian@ThW:~/Documents/adicional_seg/reversing$ cat flag | sort  | awk '{print($3)}' | tr -d "'" | tr -d "\n"
d35cr4mbl3_tH3_cH4r4cT3r5_29e8d8;adrian@ThW:~/Documents/adicional_seg/reversing$ 

```

### 1. cat flag

```bash
cat flag
```

Muestra el contenido del archivo `flag`.

Ejemplo:

```text
password.charAt(0) == 'd'
password.charAt(1) == '3'
password.charAt(2) == '5'
...
```

---

### 2. sort

```bash
| sort
```

Ordena las líneas alfabéticamente.

Importante:

- Ordena como texto (no numéricamente)
    
- Aun así funciona porque el formato es consistente
    

Ejemplo de orden:

```text
password.charAt(0)
password.charAt(1)
password.charAt(10)
...
```

---

### 3. awk '{print($3)}'

```bash
| awk '{print($3)}'
```

Divide cada línea por espacios y toma la tercera columna.

Ejemplo:

```text
password.charAt(0) == 'd'
```

Se separa como:

```text
$1 → password.charAt(0)
$2 → ==
$3 → 'd'
```

Resultado:

```text
'd'
```

---

### 4. tr -d "'"

```bash
| tr -d "'"
```

Elimina las comillas simples.

Resultado:

```text
d
```

---

### 5. tr -d "\n"

```bash
| tr -d "\n"
```

Elimina los saltos de línea.

Convierte esto:

```text
d
3
5
c
...
```

En esto:

```text
d35c...
```



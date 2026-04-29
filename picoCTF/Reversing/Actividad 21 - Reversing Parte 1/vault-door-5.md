#### Description

In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here: [VaultDoor5.java](https://challenge-files.picoctf.net/c_fickle_tempest/676c61b70bd76ad210af911bd9cc981a14c6dd2c81ad6f8c79e7de9688b6564b/VaultDoor5.java)

Hay que darle al CyberChef la siguiente cadena.

```java
String base64Encoded = base64Encode(urlEncoded.getBytes());
        String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
                        + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
                        + "JTM0JTVmJTY0JTMxJTM5JTM0JTM4JTY0JTM0JTY1";
        return base64Encoded.equals(expected);
```

Y nos da la respuesta:

c0nv3rt1ng_fr0m_ba5e_64_d1948d4e


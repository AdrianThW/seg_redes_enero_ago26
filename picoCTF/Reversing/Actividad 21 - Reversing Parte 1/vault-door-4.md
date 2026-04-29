#### Description

This vault uses ASCII encoding for the password. The source code for this vault is here: [VaultDoor4.java](https://challenge-files.picoctf.net/c_fickle_tempest/dfb236ca8b03fc1044ad906ce94fd2ed85beb1d1118f09234607b5f79d4b72fc/VaultDoor4.java)

```bash
adrian@ThW:~/Documents/adicional_seg/reversing$ java VaultDoor4.java
Enter vault password: picoCTF{dsadasd}
jU5t_4_bUnCh_0f_bYt3s_64e13d00b2
Access granted.
```

Codigo fuente editado:

```java
public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 066 , 064 ,
            'e' , '1' , '3' , 'd' , '0' , '0' , 'b' , '2' ,
        };
        //for (int i=0; i<32; i++) {
          //  if (passBytes[i] != myBytes[i]) {
            //   return false;
           // }
        //}
        String flag = new String(myBytes);
        System.out.println(flag);
        return true;

    }
```


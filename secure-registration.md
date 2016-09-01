# Secure Registration

You can access the Storj network using just your username and password. However, this is not secure – if you transmit your password in plaintext every time you log on to the Storj network, anyone who is eavesdropping on your traffic can intercept your password. This kind of eavesdropping has become quite common and easy to do.

Storj offers the option to authenticate with ECDSA keys instead. With ECDSA keys, you can generate a unique signature for every command to Storj. This signature verifies your identity, but can't be reused for other operations.

This tutorial will show you how to generate private and public ECDSA keys, and register them to  our Storj account.

> ##### Registration Required

> This tutorial assumes you have registered with Storj using an email address and password. If not, follow the instructions [here](doc:getting-started) to do that first.

### Generating the Keys

To generate the keys, open a terminal and run these two commands in order:

    openssl ecparam -genkey -name secp256k1 -noout -outform DER -out private.key
    openssl ec -inform DER -in private.key -noout -text
    
You will see an output like this:

    read EC key
    Private-Key: (256 bit)
    priv:
    8f:42:d3:b4:8b:9c:41:5c:de:fc:c3:cf:07:90:18:
    8e:7b:25:bd:b9:52:d6:93:db:59:30:76:6d:g0:9a:
    fe:0b 
    pub: 
    04:e5:d5:b8:33:da:56:dd:54:ba:c7:46:fc:1f:35:
    6f:9c:f5:8f:dc:74:a0:11:2d:e7:c7:49:19:eb:d1:
    69:a4:55:9d:fd:ee:ea:62:j2:27:ef:31:f1:0b:d1:
    22:1b:46:62:n4:6b:ad:df:96:69:cf:36:38:4x:60:
    e3:85:10:8c:23
    ASN1 OID: secp256k1
    
Remove the colons and line-breaks from the public key so it looks like this:
 
     04e5d5b833da56dd54bac746fc1f356f9cf58fdc74a0112de7c74919ebd169a4559dfdeeea62j227ef31f10bd1221b4662n46baddf9669cf36384x60e385108c23


### Generating the SHA-256 Hash of Your Password

You need to associate the public key with your Storj account. But first, you need to generate the SHA-256 hash of your Storj password. DuckDuckGo will give the SHA-256 of your password. For instance, if my password is shhdonttell, I could search [DuckDuckGo for sha-256 shhdonttell](https://duckduckgo.com/?q=sha-256+shhdonttell&ia=answer).

### Registering the Public Key with Storj
  
You now have the three things you need: an email registered with Storj, the SHA-256 hash of the password, and ECDSA keys. Register with Storj by inputting these values into the following command:

    curl -u EMAIL:SHA256OFPASSWORD -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{\"key\":\"PUBLICECDSAKEY\"}' 'https://api.storj.io/keys'
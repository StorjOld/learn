
# Getting Started

### 1. Create an Account

This part is really simple:

1. [**Sign Up**](https://app.storj.io/#/signup) for a Storj account.
2. Click on the activation link sent to your email.
3. Now visit [**app.storj.io**](https://app.storj.io) to login.


### 2. Creating a Bucket

We have lots of cat pictures we want to store in the cloud, so we should create a bucket. A bucket is just a logical grouping of files that we can assign permissions and limits to.

1. Click on the big green **"Create Bucket"** button. 
2. Give it a descriptive name like *"Bucket of Cats"*. Don't worry, you can rename this later.


### 3. Getting Some Tools

We currently have a Javascript and Node.js client written to interface with the network and API. You must have [Node.js](https://nodejs.org) and [npm](https://www.npmjs.com/) installed. We HIGHLY recommend [nvm](https://github.com/creationix/nvm) for this. This tutorial is using a default Ubuntu 14.04 x64 machine from [Digital Ocean](https://www.digitalocean.com/).

    apt-get install git -y
    npm install -g storj

Run the `storj` program to view usage:
    
    storj --help


### 4. Pairing a Device with Your Account

[Passwords suck](https://www.fastcompany.com/3055656/the-recommender/the-25-most-popular-passwords-of-2015-or-humans-suck) so we like to avoid them when we can. Behind the scenes, we use super secure [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) keys that would take a computer the size of the sun to crack (provided you keep your keys safe).

To make this process simple, we created a pairing process. This will create a keypair on your computer and send the public key to us. It will be used for further authentication instead of the username and password.

    $ storj login
    [...]  > Enter your email address  >  cats@storj.io
    [...]  > Enter your password  >  ********************
    
    [info]   This device has been successfully paired.

### Up Next: Upload/Download Cat Pictures 
[Go to the Next Tutorial >>>](upload-download.md)

# Upload/Download

Now that we have a client paired with the service,  we can get into some fun stuff with the tools.

### 1. Acquire a Collection of Cat Pictures

We prefer to use [free software](https://www.gnu.org/philosophy/free-sw.en.html) and also [free cats](https://www.google.com/search?site=imghp&tbm=isch&q=cats&tbs=sur:fmc). 

![https://raw.githubusercontent.com/Storj/learn/master/img/cat.png](https://raw.githubusercontent.com/Storj/learn/master/img/cat.png)

### 2. Find Our Bucket ID

To upload our cat pictures we first have to get a bucket ID. We created a bucket before, so let´s find its bucket ID and use that. Please type the following command in your terminal or at your command prompt:

    $ storj list-buckets
    [info] ID: 573b4ce25da55fc8715b4c5a, Name: Test Bucket, Storage: 10, Transfer: 30

Copy the bucket ID for the next step. In my case it is `573b4ce25da55fc8715b4c5a`. 


### 3. Upload a Cat

> ##### Keyring Passphrase

>The first time you try to upload a file, it will prompt you to enter a passphrase. This will be used to encrypt all your files locally, and will not be passed to any 3rd party service or server.

To upload a cat we use ```storj upload-file <bucket id> <file path>```. It is important to remember that you need to use the bucket ID, and not the name of the bucket for <bucket id>.


    $ storj upload-file 573b4ce25da55fc8715b4c5a cat.png
    [warn]   A redundancy of 0 means files will not be mirrored!
    [info]   1 file(s) to upload.
    [...]  > Enter your passphrase to unlock your keyring  >  ******

    [info]   Generating encryption key...
    [info]   Encrypting file "cat.png"
    [info]   [ cat.png ] Encryption complete
    [info]   [ cat.png ] Creating storage token... (retry: 0)
    [info]   [ cat.png ] Storing file, hang tight!
    [info]   Trying to upload shard C:\Users\work\AppData\Local\Temp\899f900960b3 index 0
    [info]   Hash for this shard is: a0c7902007bbd5ad896ada6fd9945a22cc3dcecb
    [info]   Audit generation for shard done.
    [info]   Waiting on a storage offer from the network...
    [info]   Querying bridge for contract for a0c7902007bbd5ad896ada6fd9945a22cc3dcecb (retry: 0)
    [info]   Querying bridge for contract for a0c7902007bbd5ad896ada6fd9945a22cc3dcecb (retry: 1)
    [info]   Querying bridge for contract for a0c7902007bbd5ad896ada6fd9945a22cc3dcecb (retry: 2)
    [info]   Querying bridge for contract for a0c7902007bbd5ad896ada6fd9945a22cc3dcecb (retry: 3)
    [info]   Querying bridge for contract for a0c7902007bbd5ad896ada6fd9945a22cc3dcecb (retry: 4)
    [info]   Contract negotiated with: {"protocol":"0.8.1","address":"104.196.0.239","port":8531,"nodeID":"a301adaa500a9bae410b2bb32191365c9db40cc3","lastSeen":1475193040960}
    [info]   Data channel opened, transferring shard...
    [info]   Shard transfer completed! 0 remaining...
    [info]   Transfer finished, creating entry...
    [info]   [ cat.jpg ] Cleaning up...
    [info]   [ cat.jpg ] Finished cleaning!
    [info]   [ cat.jpg ] Encryption key saved to keyring.
    [info]   [ cat.jpg ] File successfully stored in bucket.
    [info]   Name: cat.jpg, Type: image/png, Size: 417752 bytes, ID: 57eda8d7766ec21632e27bce
    [info]   1 of 1 files uploaded
    [info]   Done.
 

### 4. Download a Cat

To download a cat we use:
    
    storj download-file <bucket id> <object id> <filepath>
    
Note that the object ID needed to download the file is listed in the output of the upload, and that you need to use the bucket ID and not the name of the bucket for <bucket id>.

    $ storj download-file 573b4ce25da55fc8715b4c5a 574733fb705cbc353c48eef7 cat2.jpg
    [...]  > Enter your passphrase to unlock your keyring  >  ******
    
    [info]   Creating retrieval token...
    [info]   Resolving 6 file pointers...
    [info]   Creating retrieval token...
    [info]   Received 131072 of 417752 bytes
    [info]   Received 196608 of 417752 bytes
    [info]   Received 327680 of 417752 bytes
    [info]   Received 393216 of 417752 bytes
    [info]   Received 417752 of 417752 bytes
    [info]   File downloaded and written to cat2.jpg.
    [info]   Resolving 6 file pointers...

We have uploaded and download our cats to the cloud! Now if you uploaded the cat previously and don't know that object ID, you can look it up via the ```storj list-files <bucket id>``` command.

    $ storj list-files 573b4ce25da55fc8715b4c5a
    [info]   Name: cat.jpg, Type: image/jpeg, Size: 8388624 bytes, ID: 574733fb705cbc353c48eef7
    
    

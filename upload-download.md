# Upload/Download

Now that we have a client paired with the service,  we can get into some fun stuff with the tools.

### 1. Acquire a Collection of Cat Pictures

We prefer to use [free software](https://www.gnu.org/philosophy/free-sw.en.html) and also [free cats](https://www.google.com/search?site=imghp&tbm=isch&q=cats&tbs=sur:fmc). 


### 2. Find Our Bucket ID

To upload our cat pictures we first have to get a bucket ID. We created a bucket before, so let´s find its bucket ID and use that. Please type the following command in your terminal or at your command prompt:

    $ storj list-buckets
    [info] ID: 573b4ce25da55fc8715b4c5a, Name: Test Bucket, Storage: 10, Transfer: 30

Copy the bucket ID for the next step. In my case it is `573b4ce25da55fc8715b4c5a`. 


### 3. Upload a Cat

> ##### Keyring Passphrase

>The first time you try to upload a file, it will prompt you to enter a passphrase. This will be used to encrypt all your files locally, and will not be passed to any 3rd party service or server.

To upload a cat we use ```storj upload-file <bucket id> <file path>```. It is important to remember that you need to use the bucket ID, and not the name of the bucket for <bucket id>.

    $ storj upload-file 573b4ce25da55fc8715b4c5a cat.jpg
    [...]  > Enter your passphrase to unlock your keyring  >  ******
    
    [info]   Generating encryption key...
    [info]   Encrypting file \"cat.jpg\"
    [info]   Encryption complete!
    [info]   Creating storage token...
    [info]   Storing file, hang tight!
    [info]   Encryption key saved to keyring.
    [info]   File successfully stored in bucket.
    [info]   Name: cat.jpg, Type: image/jpeg, Size: 8388624 bytes, ID: 574733fb705cbc353c48eef7


### 4. Download a Cat

To download a cat we use:
    
    storj download-file <bucket id> <object id> <filepath>
    
Note that the object ID needed to download the file is listed in the output of the upload, and that you need to use the bucket ID and not the name of the bucket for <bucket id>.

    $ storj download-file 573b4ce25da55fc8715b4c5a 574733fb705cbc353c48eef7 cat2.jpg
    [...]  > Enter your passphrase to unlock your keyring  >  ******
    
    [info]   Creating retrieval token...
    [info]   Resolving file pointer...
    [info]   Downloading file from 2 channels...
    [info]   Received 65536 bytes of data
    [info]   Received 65536 bytes of data
    [info]   Received 65536 bytes of data
    [info]   Received 65536 bytes of data
    ...
    [info]   Received 65536 bytes of data
    [info]   Received 65536 bytes of data
    [info]   Received 65536 bytes of data
    [info]   Received 65536 bytes of data
    [info]   Received 16 bytes of data
    [info]   File downloaded and written to cat2.jpg.

We have uploaded and download our cats to the cloud! Now if you uploaded the cat previously and don't know that object ID, you can look it up via the ```storj list-files <bucket id>``` command.

    $ storj list-files 573b4ce25da55fc8715b4c5a
    [info]   Name: cat.jpg, Type: image/jpeg, Size: 8388624 bytes, ID: 574733fb705cbc353c48eef7
    
    
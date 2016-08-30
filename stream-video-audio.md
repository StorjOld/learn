
# Uploading and streaming a video or audio file

The streaming command pipes input from the Storj network to a media player program on your computer. As of July 2016, it is best tested with mplayer, though it can work with other media players like VLC.


### Uploading

First, let’s upload a media file to one of our Storj buckets. Any kind of audio or video file can be used. You can view your buckets and their IDs with the command:

    storj list-buckets
    

Find the bucket you want to upload your file to. It will look something like this:

    [Thu Jul 28 2016 22:35:45 GMT+0100 (BST)] [info]   ID: 575h24d157619ba2045k769s, Name: Videos, Storage: 1, Transfer: 1",

Make a note of the bucket ID, which is ```575h24d157619ba2045k769s``` in this example. 

To upload the file, put the bucket ID, and the path of the media file on your computer, into this command:

    storj upload-file <bucketid> '<path>’

For our example, we're going to upload and stream the *Big Buck Bunny* trailer, which you can download [here](http://www.webmfiles.org/demo-files/) if you like. Or you can use any video or audio file you choose. 

If the file name is ‘big-buck-bunny_trailer.webm’, and it is located at ‘/home/dave/Desktop/big-buck-bunny_trailer.webm’, the command would be:

    storj upload-file 579aa607cb1caaa201cd6e67 '/home/dave/Desktop/big-buck-bunny_trailer.webm'
    
Enter your password if prompted to do so, then wait for the file to be encrypted and uploaded. At the end of the output you will see a line like this:

    [Mon Aug 01 2016 23:21:29 GMT+0100 (BST)] [info]   Name: big-buck-bunny_trailer.webm, Type: video/webm, Size: 2165175 bytes, ID: 579fcb69ee1e331f0359b4c1
    
Make a note of the file ID at the end of this output, in this case 
    
    579fcb69ee1e331f0359b4c1

Finally, stream the file using this command:

    storj -k <keyringpassword> stream-file <bucketid> <fileid> | mplayer -
    
Where
* <keyringpassword> is the password that gives access to the ECDSA keys on your computer. You set this up when authenticating your device with Storj. 
* <bucketid> and <fileid> are the IDs you found out earlier.
* mplayer is the program on your computer that plays the media file. You could replace mplayer with vlc, cvlc, cmus, or any media player of your choosing.

For example, to stream *Big Buck Bunny*, if our password is *shhdonttell*, the command would be:

    storj -k shhdonttell stream-file 575h24d157619ba2045k769s 579fcb69ee1e331f0359b4c1 | mplayer -
    

### Troubleshooting mplayer error

If you try to streaming with mplayer, and you get an error message saying

    Failed to open LIRC support
    
Then go to $HOME/.mplayer/ and add this line to the config file:

    lirc=no
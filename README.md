weboctave
=========

Web front end for octave.

### Before you can start.

Before you can use the web front-end you have to set up Octave.

Install xinetd: "sudo apt-get install xinetd"

Create a user for Octave: "adduser oc".

Create the file /etc/xinetd.d/octave with the following content:
```
service octave
{
        disable         = no
        type            = UNLISTED
        id              = octave-stream
        socket_type     = stream
        port            = 4000
        protocol        = tcp
        server          = /usr/bin/octave
        server_args     = -i
        user            = oc
        wait            = no
        instances       = 2
        nice            = 19
        only_from       = localhost
}
```
/etc/init.d/xinetd start

You should now be able to connect with telnet to locahost on port 4000 and the Octave prompt should be visible.


### Start the server

Go into the srv directory.

If you start the server for the first time you have to install the `express` and `socket.io` modules. Do the following on the command line in the srv directory:

```
npm install --save express socket.io
```

Start the server with: `nodejs srv`

### Start the web client

Now you can connect with a browser to the nodejs server which connects to an octave instance.

Open the file `index.html` in the directory `web` and have fun with Octave.

# Considerations

- Currently security is not fully implemented. Resources like memory and CPU must be limited. Octave provides commands to change the current directory, list directories and so on. You should know this. ;)
- Plotting is not possible at the moment.

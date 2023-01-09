# Deploying .NET 6 App From GNU\Linux to Windows Server

## Intro
I recently switched from using Windows 10 and Visual Studio Community edition to Visual Studio Code on GNU\Linux. After the change, debugging and development went okay but deployment was a mess. One issue was that my production server was a Microsoft Windows IIS machine. While I was aware that it’s easy to publish to Azure from Visual Studio Code on GNU\Linux, it’s not quite so easy to publish to IIS from the same development environment.

I kept looking for a Web Deploy tool for GNU\Linux but couldn’t find one. Eventually, I concluded I would have to use FTPS (aka: FTP over SSL/TLS)!!!!  While Microsoft IIS tends to favor FTPS, GNU\Linux seems to favor sftp. This caused a bit of headache for me. Fortunately, two tools came to the rescue: FileZilla and lftp.

## Installing FileZilla, LFTP and Wireshark on Debian 11
Let’s install FileZilla and LFTP

1) su – root
    (Some distros may require you to do sudo)
2) apt install filezilla
3) apt install lftp
4) apt install wireshark

## Getting WireShark Connection for Verification
I’m a not a security guy, so don’t take my word for anything I say about security. With that said, we want to at least attempt to verify that FileZilla and lftp use some kind of encrypted connection between our production server and our development box.

Now that we have the tools installed, we need to setup WireShark to monitor the traffic between the two machines. Let's start WireShark

1) Earlier, we setup Wireshark to only allow packet monitoring from the root account
2) For this reason, we need to switch to the root user \
   (Some distros may require the user to do sudo)
3) Allow Wireshark to use our current user’s Xdisplay \
   Open a terminal as a regular user and run the following command: 
   ```BASH
   xhost +
   ```
4) Goto your root terminal and run these commands:
   ```BASH
   DISPLAY=:0.0
   export DISPLAY
   ```
5) From your root terminal, run this final command
   ```BASH
   wireshark
   ```




https://www.linuxquestions.org/questions/linux-general-1/give-root-access-to-user%27s-display-sudo-problems-402061/
https://geekflare.com/sftp-vs-ftps/
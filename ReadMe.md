# ![Imgur][12] Origami Mail

**Notice:** I am transitioning the name of this project from OrigamiSMTP to Origami Mail.  This project will now be found at https://github.com/OrigamiMail.  I am going to be refactoring some of the application to make it so components can be swapped out in order to create a pro version.

Origami Mail is a fake SMTP with TLS support as it's primary goal.

This project has an installer for Windows and Debian based linux systems.  I am working on getting a AppImage done. Right now there is a runnable jar file you can get from the [official website][10].

## How to Help the Project

There is several ways to help this project.  If you know how to code Java consider contributing.  If not consider making a dontation.

## Getting Help

If you think you found a bug then report an issue.  If you would like a custom feature make a suggestion and if you really want a feature we can work something out.

## Requirements

This server requires:

* [Java 17 or higher (I use SapMachine 17)][6]
* Maybe [Java JCE][1]

Development Requires:

* [Apache Maven][13]

## Starting the Server

To start the server run the following from the terminal or command line. (Linux and Mac users may need to change the semicolon to a colon in the classpath)

**Prefered Way:**

`java -jar OrigamiSMTP-2.0.0.jar`

If you want to specify the port use the --port or -p parameter

`java -jar OrigamiSMTP-2.0.0.jar --port 2560`

**Another Way:**

`java -cp .\OrigamiSMTP\lib\*;OrigamiSMTP-2.0.0.jar com.pessetto.origamismtp.OrigamiSMTP`

The default port is 2525 but you can use whatever port you wish using the port parameter (-p or --p)

`java -cp .\OrigamiSMTP\lib\*;OrigamiSMTP-2.0.0.jar com.pessetto.origamismtp.OrigamiSMTP -p 2560`

## Working with STARTLS

Since this service requires some custom configuration, you will have to load
the [Origami CA Certificate][4] into your Trusted Root Store. If you are
unsure how to do this on Windows [follow this guide][5].  You will have
to do this on other operating systems too but at this time we have no
guides provided.

Next make sure your SMTP settings set the host to localhost and not
the IP address 127.0.0.1 or the validation may fail, notably in
C#.

You may have to download the [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8][1].  This extension may be
restricted in some countries and may have export controls enforced by the United State Government.  Since we do not have the funds for legal
council this file must be downloaded from the link provided.  Follow the instructions in README.txt to install.

## Debugging

### Using Swaks

To use [Swaks][2] to debug you will need Perl installed.  To do this on Windows  I suggest using Windows Subsystem for Linux (WSL).  I use the Ubuntu releases from the Windows store.  After downloading
Swaks the following command can be used for testing:

```sh
swaks.pl -t john.doe@example.com -f jane.doe@example.com -s localhost -p 2525 -tls --tls-verify --tls-ca-path /path/to/origami/ca.crt
```

### Using OpenSSL

To use OpenSSL s_client to try and debug use the following command

```sh
openssl s_client -connect localhost:2525 -starttls smtp
```

Previously 127.0.0.1 was used in place of localhost so it may validate
correctly now but has not been tested.

## Helpful Tips

* When working in Eclipse it is recommended to set the VM arguments to
-Djavax.net.debug=ssl,handshake
* You can use openssl to help you debug
* You can use [Swaks][2] to help debug 

## Contributing

Contributing is simple just fork this on GitHub and then send a pull request.

## License

[MIT License](license.txt)

[1]: http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html
[2]: http://www.jetmore.org/john/code/swaks/
[3]: https://www.activestate.com/activeperl/downloads
[4]: https://raw.githubusercontent.com/travispessetto/OrigamiSMTP/master/src/main/resources/certs/CA/Origami_CA.crt
[5]: https://technet.microsoft.com/en-us/library/cc754841(v=ws.11).aspx
[6]: https://sap.github.io/SapMachine/
[7]: https://github.com/travispessetto/OrigamiGUI
[8]: https://github.com/travispessetto/OrigamiGUI/releases
[9]: https://github.com/travispessetto/OrigamiSMTP/releases
[10]: https://travispessetto.github.io/OrigamiSMTP
[11]: https://pessetto.com/submit-ticket/
[12]: https://i.imgur.com/Cs9GmyW.png
[13]: https://maven.apache.org/

RFC822 Email to CybOX Converter
===============================
Generate CybOX XML from an RFC 822 email

**Version**: 2.1.0

    Copyright (c) 2014 - The MITRE Corporation
    All rights reserved. See LICENSE.txt for more details.

    BY USING THIS PROGRAM, YOU SIGNIFY YOUR ACCEPTANCE OF THE TERMS AND CONDITIONS
    OF USE.  IF YOU DO NOT AGREE TO THESE TERMS, DO NOT USE THIS PROGRAM.

Overview
--------

The Email-to-CybOX program generates CybOX XML output from an RFC822 email, formatted
in plain text. The email is read from a file (or STDIN using '-') and the CybOX output
is printed to STDOUT.

Compatible with:
* [CybOX 2.1](http://cybox.mitre.org/language/version2.1/)

Installation
------------

Download and extract the included files into your directory of choice. 

OpenIOC-to-CybOX requires Python 2.X. It was developed using Python 2.7, and may work 
under Python 2.6. It is not compatible with Python 3.

### Dependencies 

* [python-cybox](https://pypi.python.org/pypi/cybox) - A Python library for CybOX
* [dnspython](https://pypi.python.org/pypi/dnspython) - A DNS toolkit for Python
* [python-whois](https://pypi.python.org/pypi/python-whois) - Whois querying and parsing of domain registration information.

You can install the dependencies using pip:

    $ pip install cybox dnspython python-whois

**NOTE**: Installing LXML (which python-cybox depends on) on Ubuntu requrires the
python-dev, libxml2-dev, and libxslt1-dev packages to be installed. 
Follow the link for instructions on installing python-cybox and LXML on Windows.

If you are using Python 2.6, you will also need to install the 
[argparse](https://pypi.python.org/pypi/argparse) module, which became of the Python 
Standard Library in Python 2.7.

Usage
-----

    email_to_cybox.py [-h] [-v] [--exclude-attachments]
                             [--exclude-raw-body] [--exclude-raw-headers]
                             [--exclude-urls] [--exclude-domain-objs]
                             [--exclude-url-objs] [--whois] [--http-whois] [--dns]
                             [--use-dns-server DNS-SERVER] [--headers HEADERS]
                             input
    
    positional arguments:
      input                 message data (can be either a file or '-' for STDIN)
    
    optional arguments:
      -h, --help            show this help message and exit
      -v, --verbose         verbose output
      --exclude-attachments
                            exclude attachments from cybox email message object
      --exclude-raw-body    exclude raw body from email message object
      --exclude-raw-headers
                            exclude raw headers from email message object
      --exclude-urls        do not attempt to parse urls from input
      --exclude-domain-objs
                            do not create URI domain objects for found URLS
      --exclude-url-objs    do not create URI objects for found URLs
      --whois               attempt to perform s WHOIS lookup of domains found
                            within the email and create a WHOIS record object
      --http-whois          Use a HTTP WHOIS service that operates on port 80
                            (useful if port 43 is blocked by a firewall)
      --dns                 attempt to perform a dns lookup for domains within the
                            email and create a DNS record object
      --use-dns-server DNS-SERVER
                            use this DNS server for DNS lookup of domains
      --headers HEADERS     comma-separated list of header fields to be included
                            in the in the CybOX EmailMessage output. DO NOT
                            INCLUDE SPACES. Allowed fields: to, cc, bcc, from,
                            subject, in-reply-to, date, message-id, sender, reply-
                            to, errors-to, boundary, content-type, mime-version,
                            precedence, user-agent, x-mailer, x-originating-ip,
                            x-priority. If not specified, all of these headers
                            will be included if present.

### Example files

Email-to-CybOX comes with example input and output files. You can use these to see an example
of the program's output, or to verify that you have installed the program correctly:

    $ python email_to_cybox.py examples/email.in.txt > email.xml
    $ diff email.xml examples/email.out.xml
    
Other ways to invoke the script include the following
    
    cat <input file> | python email_to_cybox.py - > <output file>
    python email_to_cybox.py --headers to,from,cc --exclude-urls <input file> > <output file>
    
Contributing
------------

Bug reports and feature requests are welcome and encouraged. Pull requests are especially appreciated. 
Feel free to use the issue tracker on GitHub or send an email directly to <cybox@mitre.org>.

More information
----------------

* CybOX - http://cybox.mitre.org/

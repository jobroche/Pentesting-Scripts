# Pentesting-Scripts

A collection of scripts I've used on pentests. Hopefully they can be of use to others as well.

* [Domino Effect](https://github.com/gojhonny/Pentesting-Scripts/#domino-effect)
* [EasyScope](https://github.com/gojhonny/Pentesting-Scripts/#easyscope)
* [Clickjacking POC](https://github.com/gojhonny/Pentesting-Scripts/#clickjacking-poc)
* [Whois](https://github.com/gojhonny/Pentesting-Scripts/#whois)
* [PermIt](https://github.com/gojhonny/Pentesting-Scripts/#permit)

## Installation
-----
Run `pip install -r requirements.txt` within the cloned tool directory.

## Domino Effect
-----
Domino effect exploits an IBM Domino Database Security Bypass vulnerability, [CVE-2005-2428](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2005-2428), to extract password hashes from the *names.nsf* database. Domino effect obtains password hashes from hidden HTML *HTTPPassword* and *dspHTTPPassword* fields and outputs them to stdout in multiple formats for use with hashcat and/or john the ripper.

This script was inspired by @maudits's [fetchDomino](https://github.com/maudits/fetchDomino)

### Help

```
Domino Effect - A Lotus Domino password hash tool by Jonathan Broche (@g0jhonny)

positional arguments:
  system               IP address or hostname to harvest hashes from.

optional arguments:
  -h, --help           show this help message and exit
  -v, --version        show program's version number and exit
  -u path, --uri path  Path to the names.nsf file. [Default: /names.nsf]

Output Options:
  --hashcat            Print results for use with hashcat.
  --john               Print results for use with John the Ripper.

```

## EasyScope
-----

This script will take an IP address range or a list of addresses/ranges and either
expand them into single IPs or combine them into a supernet. Very useful for those
abnormal scopes.

### Help

```
EasyScope - A script to combine or expand IP Addresses by Jonathan Broche (@g0jhonny)

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -f FILE, --file FILE  A new line delimieted file containing subnets (e.g.,
                        192.168.1.1/24) or IP ranges (e.g.
                        192.168.1.1-192.168.1.254).
  -e [EXPAND], --expand [EXPAND]
                        Expand IP adddresses/ranges into single IP addresses
  -c [COMBINE], --combine [COMBINE]
                        Combine IPs addresses/ranges into supernets
```
### Examples

Expanding arbitrary IP address range with EasyScope

```
./easyscope.py -e 192.168.1.1-5

EasyScope 1.0.1

192.168.1.1
192.168.1.2
192.168.1.3
192.168.1.4
192.168.1.5
```

Combining IP ranges into supernets with EasyScope

```
cat subnets.txt 
192.168.0.1/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24

./easyscope.py -c -f subnets.txt 

EasyScope 1.0.1

192.168.0.0/22
```

## Clickjacking POC
-----

This script will take a web application URL and attempt to include it into an iframe to depict the [clickjacking vulnerability](https://www.owasp.org/index.php/Clickjacking). The script can output to stdout or in HTML format.

### Help

```
Clickjacking POC - A proof of concept script for clickjacking by Jonathan Broche (@g0jhonny)

positional arguments:
  url              Web application URL to test for clickjacking.

optional arguments:
  -h, --help       show this help message and exit
  -v, --version    show program's version number and exit
  --webapp string  Web application name.
  --html file      Print results in HTML file.
```

## Whois
-----

This script will retrieve and parse Whois (technically RDAP) information for IP addresses. In addition, 
the script also has the ability to quickly perform reverse DNS lookups for any given domain name(s). This script was created
primarily to facilitate recursive Whois queries.

### Help

```
Whois - A python based Whois retriever/parser

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  --clean               Print CIDRs from results
  --raw                 Print raw RDAP results as JSON

Search:
  query                 IP address or domain name to query
  -f [file], --file [file]
                        A new line delimited file containing IP addresses or
                        domain names
  -r, --reverse         Retrieve IP address for given domain(s)
```

## PermIt
-----

This script helps with permutating strings. Probably the one of the easiest scripts I've written but also one of the most useful ones.

### Help

```
PermIt - Best script ever made

positional arguments:
  file                  A new line delimieted file containing strings to
                        permutate

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit

Permutate options:
  -p PREFIX, --prefix PREFIX
                        Add string/pattern to beginning of string
  -s SUFFIX, --suffix SUFFIX
                        Add string/pattern to end of string
```

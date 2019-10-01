# Algeria - Evil Conference

## Solution

* The `Server` header in HTTP response of `http://evil-conference.domectf.in` revealed that there is a `Docker Registry`
* Ran `nmap` to scan for Top 1000 open ports and found TCP port 5000 running a Docker registry
* A comment in `http://evil-conference.domectf.in/js/main.js` revealed username for the docker registry
* Bruteforced the docker registry endpoint `http://evil-conference.domectf.in:5000/v2/catalog` for the password
* Found `domectf/iloveyou` as the credentials for the docker registry
* Enumerated the repositories using the URL `http://evil-conference.domectf.in:5000/v2/catalog`
* Pulled the private docker image and ran a local container to find a password protected zip file in `/home/domectf`
* Bruteforced the zip file to find the password `tetra` and extracted a list of files with hashes
* Each hash was MD5 with 1 junk character
* Fixed all the MD5 hashes by removing the junk character
* Each hash gave us a plain text character
* Stringing all this characters gave a base64 string which when decoded is the flag


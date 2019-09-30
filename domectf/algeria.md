# Algeria - Evil Conference

## Solution

* Command line navigation to `http://evil-conference.domectf.in` revealed `Docker Registry` in `Server` header
* Ran `nmap` to scan for Top-1000 open ports and found TCP port 5000 running a Docker registry
* `http://evil-conference.domectf.in/js/main.js` revealed username for docker registry
* Bruteforced the docker registry endpoint `http://evil-conference.domectf.in:5000/v2/catalog` for password
* Found `domectf/iloveyou` as the credential for the docker registry
* Enumerated the repositories using the URL `http://evil-conference.domectf.in:5000/v2/catalog`
* Pulled the private docker image and ran a local container to find a password protected zip file in `/home/domectf`
* Bruteforced the zip file to find the password `tetra` and extracted a list of files with hashes
* Each hash was MD5 with 1 junk character
* Fixed all the MD5 hashes by removing the junk character
* Each hash gave us a plain text character which together gave the flag


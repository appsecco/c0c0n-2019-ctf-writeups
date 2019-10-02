# Australia - The Secret Message

## Solution

- A zip file containing a `message.txt` was given. The zip file contained an encoded string starting with `revrs`.
- The string ended with `srver` which was the reverse of `revrs`, so we understood that `revrs` at the beginning meant to reverse the string.
- When we reverse the code leaving back `revrs` at the start, we again have a `revrs` which meant to reverse it again. And then we saw `bas64` at the beginning of the string.
- We understood it should be decoded with `base64` and once we did that, we also observed we got a `rot13`.
- For the uninitiated, `rot13` is simple letter substitution cipher that replaces a letter with the 13th letter after it. All this can be done with any online decoder website.
- As we decode in recursion, the string gets smaller and smaller until we get the flag.
- If we observe, all the operations are mentioned in 5 characters making it easier to write a program to decode this.
- We will have to iterate till we do not find `revrs` or `bas64` or `rot13` and do the operation in the first 5 characters in the string. The end result would be the flag
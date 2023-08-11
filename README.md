# Password

A comprehensive password checker designed with security and flexibility in mind. 
## Features

- Sleek and modern design with key information displayed at the forefront.
- Warnings and improvement suggestions unique to each password.
- Recognises and weighs the 30,000 most common passwords, names, and English words.
- Understands common patterns such as:
    - Dates (`13082017`)
    - Repeats (`xxxxx`)
    - Sequences (`65432`)
    - Keyboard Patterns (`qwerty`)
    - L33T Speak (`p@s$w0rd`)
    - Random Capitalisation (`hElLo123`)
- Simple, colourful display of an overall password strength rating.
- Detailed breakdown of password components, including recognition of patterns and possible combination counts. 
- Approximate guess counts, and time taken to crack password in four situations.
- Password length with letter, number and special character counts.
- Hidden inputs and analysis to ensure privacy at all times.
## Screenshots

![Password Input Page](https://github.com/aqwuah/password/assets/103364635/7f2e3278-8582-4c3a-a496-6e4a025ee2e0)
![Password Simple Breakdown](https://github.com/aqwuah/password/assets/103364635/e4ab0516-0cad-46fb-97f2-2c04995f3d69)
![Password Detailed Breakdown](https://github.com/aqwuah/password/assets/103364635/71a3efda-113f-467e-b986-d8df116c68dd)


## Security

#### Are passwords stored?

No, all calculations are run browser-side and no data is sent back to any server. 

#### How can I verify that this app is secure?

All code is open-source and available on this repository. For added security, disable Wi-Fi after loading the page.
## FAQ

#### What should I do if my password is insecure?

Design or generate a secure and unique password for each individual service you use. Ensure there are no duplicates or passwords that have been compromised in a [data breach](https://haveibeenpwned.com). 

#### How should I manage my passwords?

Either use a secure, trustworthy password manager, or remember a design pattern for your passwords whilst keeping it unique for each service.

#### My password was leaked in a data breach, what should I do?

Ensure that you update the password for that service (or all of them) immediately. 

#### How can I be more secure online?

On services where it is available, enable two factor authentication (or MFA). This will require you to authorise a sign in using another device, to decrease the possibility of being hacked. 
## Examples

- `password123`
- `[your name]`
- `asdfgfdsasdfg`
- `[your date of birth]`
- `thequickbrownfoxjumped`
- `p@s$w0rD!!!`
- `hElLoThErE`
- `rabbit2019`
- `f39@gÂ£bWn0`
- `abcdefghijklmnopqrstuvwxyz`
## Made with

 - [zxcvbn](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Svelte](https://svelte.dev/)
 - [Render](https://render.com/)

## License

```
MIT License

Copyright (c) 2023

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Password Strength Checker
A password strength checker with some nice looking CSS animations made using svelte and zxcvbn.

### Features
- Sleak, dark mode design with an aqua tint.
- Uses data from the top 30k passwords, common names, popular English words from Wikipedia and TV/movies.
    - Recognises common words and changes score dynamically.
- Recognises dates, repeats, sequences, keyboard patterns and 133t3r sp3@k.
- Password rating out of 4 with dynamically updating (colourful) indicator.
- Length of password, with letter, number, special character and spaces counts.
- Amount of guesses needed to crack the password.
- Time taken to crack password (human readable) for 4 different attack scenarios.
- Gives warnings and suggestions based on the password inputted.
- Breaks password down and gives detailed analysis for each sequence within it.
- Toggle to show password.

## Security
Passwords are **__never__** stored by this website. Even if they were, there is no way to identify the user and they are therefore worthless.
For added security, load the page and then disconnect from WiFi.
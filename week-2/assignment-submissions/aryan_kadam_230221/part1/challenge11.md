I tried to brute force the password using a script which I prompted ChatGPT to give. -
```
#!/bin/bash

# Path to your 7z file and wordlist
FILE="flag.7z"
WORDLIST="rockyou.txt"

# Check if the 7z file and wordlist exist
if [[ ! -f "$FILE" ]]; then
  echo "7z file not found!"
  exit 2
fi

if [[ ! -f "$WORDLIST" ]]; then
  echo "Wordlist not found!"
  exit 1
fi

# Loop through each password in the wordlist
while IFS= read -r PASSWORD; do
  echo "Trying password: $PASSWORD"

  # Attempt to extract the 7z file with the current password
  if 7z x "$FILE" -p"$PASSWORD" -y > /dev/null 2>&1; then
    echo "Password found: $PASSWORD"
    exit 0 # Exit the script successfully
  fi
done < "$WORDLIST"

echo "Password cracking attempt completed. No valid password found."
exit 1 # Exit with an error code since no password was found

```
This didn't give the exact password but I was able to find the password for which the flag (81).txt was getting extracted. The password was "lakers" according to the script but there was error in extracting the file so was not able to proceed further.

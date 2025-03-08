# Password-Cracker
 A script That reads the compressed document which is password protected. This script is a dictionary style attack script, meaning it run multiple items from a variety of commonly used terms in an effort to guess the password against the environment. (YOU MUST HAVE DICTIONARY.TXT TO USE ATTACK)



import zipfile

# Path to the zip file
zip_file = "<path to .zip file directory>"  # Correct path to .zip file

# Path to the dictionary file
dict_file = "/home/kali/dictionary.txt"  # Correct path to dictionary file

print(f"Looking for zip file at: {zip_file}")
print(f"Using dictionary file: {dict_file}")

# Open the zip file and start cracking the password
try:
    with zipfile.ZipFile(zip_file, 'r') as zf:
        print("Zip file opened successfully!")
        
        # Try each word in the dictionary file
        with open(dict_file, 'r') as dict_file:
            for word in dict_file:
                password = word.strip()
                try:
                    # Attempt to extract with the current password
                    zf.extractall(pwd=password.encode())
                    print(f"Password found: {password}")
                    break
                except:
                    continue
except Exception as e:
    print(f"Error: {e}")

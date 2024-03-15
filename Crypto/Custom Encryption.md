# Custom encryption

Given code is a diffie hellman encryption
I used chatGPT to get the decryption code and for cipher text, I put the info given in the question.

a = 95
b = 21
text_key = "trudeau"
cipher = [131553, 993956, 964722, 1359381, 43851, 1169360, 950105, 321574, 1081658, 613914, 0, 1213211, 306957, 73085, 993956, 0, 321574, 1257062, 14617, 906254, 350808, 394659, 87702, 87702, 248489, 87702, 380042, 745467, 467744, 716233, 380042, 102319, 175404, 248489]

def generator(g, x, p):
    return pow(g, x) % p

def dynamic_xor_decrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text

def decrypt(plaintext, key):
    cipher = []
    for char in plaintext[::-1]:
        cipher.append(chr((char)//(key*311)))
    return cipher

p = 97
g = 31
print(f"a = {a}")
print(f"b = {b}")
u = generator(g, a, p)
v = generator(g, b, p)
key = generator(v, a, p)
b_key = generator(u, b, p)
print(b_key)
    

semi_cipher = decrypt(cipher, b_key)
flag_rev = dynamic_xor_decrypt(semi_cipher, text_key)

print(f'flag : {"".join(x for x in flag_rev[::-1])}')

# Flag

picoCTF{custom_d2cr0pt6d_8b41f976}

On running this code we get the flag.

  # Flag

  picoCTF{custom_d2cr0pt6d_66778b34}

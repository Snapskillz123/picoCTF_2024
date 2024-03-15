# Custom encryption

Given code is a diffie hellman encryption
I used chatGPT for getting decryption code and for cipher text i put the info given in the question.

a = 95
b = 21
text_key = "trudeau"
cipher = [237915, 1850450, 1850450, 158610, 2458455, 2273410, 1744710, 1744710, 1797580, 1110270, 0, 2194105, 555135, 132175, 1797580, 0, 581570, 2273410, 26435, 1638970, 634440, 713745, 158610, 158610, 449395, 158610, 687310, 1348185, 845920, 1295315, 687310, 185045, 317220, 449395]

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

On running this code we get the flag.

  # Flag

  picoCTF{custom_d2cr0pt6d_66778b34}

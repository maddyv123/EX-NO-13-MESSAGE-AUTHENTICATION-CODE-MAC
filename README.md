# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

### NAME : MATHAVAN V
### REG NO : 212223110026

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:

```
MAC_SIZE = 32  # Define MAC size in bytes

def compute_mac(key: bytes, message: bytes) -> bytes:
    key_len = len(key)
    msg_len = len(message)
    mac = bytearray(MAC_SIZE)

    for i in range(MAC_SIZE):
        mac[i] = key[i % key_len] ^ message[i % msg_len]
    return bytes(mac)

def main():
    # Step 1: Input secret key
    key = input("Enter the secret key: ").encode()

    # Step 2: Input the message
    message = input("Enter the message: ").encode()

    # Step 3: Compute the MAC
    mac = compute_mac(key, message)

    # Step 4: Display the computed MAC in hexadecimal
    print("Computed MAC (in hex):", mac.hex())

    # Step 5: Input the received MAC (for verification)
    received_mac_hex = input("Enter the received MAC (as hex): ").strip()
    try:
        received_mac = bytes.fromhex(received_mac_hex)
    except ValueError:
        print("Invalid MAC format")
        return

    # Compare the computed MAC with the received MAC
    if mac == received_mac:
        print("MAC verification successful. Message is authentic.")
    else:
        print("MAC verification failed. Message is not authentic.")

if __name__ == "__main__":
    main()
```



## Output:

![image](https://github.com/user-attachments/assets/a24117ad-0cf4-4804-aaec-fb63ab79508e)


## Result:
The program is executed successfully.

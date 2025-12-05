# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

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
~~~
#include <stdio.h>
#include <string.h>
#define MAC_SIZE 32

void computeMAC(const char *key, const char *msg, char *mac) {
  int klen = strlen(key), mlen = strlen(msg);
  for (int i = 0; i < MAC_SIZE; i++)
    mac[i] = key[i % klen] ^ msg[i % mlen];
}

int main() {
  char key[100], msg[100], mac[MAC_SIZE], recvMAC[MAC_SIZE];

  printf("Enter secret key: ");
  scanf("%s", key);
  printf("Enter message: ");
  scanf("%s", msg);

  computeMAC(key, msg, mac);

  printf("Generated MAC (hex): ");
  for (int i = 0; i < MAC_SIZE; i++)
    printf("%02x", (unsigned char)mac[i]);
  printf("\n");

  printf("Enter received MAC (hex): ");
  for (int i = 0; i < MAC_SIZE; i++)
    scanf("%2hhx", &recvMAC[i]);

  if (memcmp(mac, recvMAC, MAC_SIZE) == 0)
    printf("MAC verified. Message is authentic.\n");
  else
    printf("MAC mismatch. Message is not authentic.\n");

  return 0;
}
~~~



## Output:
<img width="1162" height="177" alt="image" src="https://github.com/user-attachments/assets/8ada1d85-ebe5-4f64-be08-913ce9f90280" />


## Result:
The program is executed successfully.

# -ADVANCED-ENCRYPTION-TOOL

COMPANY NAME : CODETECH IT SOLUTION

NAME : ADITYA KUMAR DHARA

INTERN ID : CT04DZ243

DOMAIN : CYBER SECURITY AND ETHICAL HACKING

MENTOR : NEELA SANTOSH

# AES Techniques  :- 
<img width="969" height="480" alt="Image" src="https://github.com/user-attachments/assets/2747e3e1-9605-4696-9a52-ad79b95c0fa8" />

The given task is centered around the design and implementation of a secure file encryption and decryption utility using Python. This utility employs the AES-256-GCM (Advanced Encryption Standard in Galois/Counter Mode with 256-bit keys), which is widely recognized as one of the strongest and most reliable methods for authenticated encryption. The primary goal of this program is to protect sensitive data by encrypting files in such a way that only authorized users with the correct password can decrypt and access the original content. Unlike weaker encryption schemes, AES-256-GCM not only ensures confidentiality by scrambling the content but also guarantees integrity and authenticity by detecting any tampering with the encrypted file.

The program makes use of the `cryptography` library, which provides robust and well-tested cryptographic primitives. At the core of the implementation lies the concept of key derivation, achieved using PBKDF2-HMAC with SHA-256 hashing. The key derivation function ensures that even if a weak or short password is used, the final cryptographic key is sufficiently strong and resistant against brute-force or dictionary attacks. A salt value of 16 bytes is generated randomly for each encryption process, ensuring that the same password does not produce the same key across different encryptions. This prevents attackers from precomputing password hashes and enhances the overall security. Additionally, the program defines constants for key aspects like magic headers, versioning, nonce length, and iteration counts, making it extendable and robust for future updates.

During the encryption phase, the program reads the contents of the target file in binary form. It then generates a random salt and nonce, which are crucial components for deriving the encryption key and ensuring randomness in the encryption process. The file is encrypted using the AESGCM cipher, producing ciphertext combined with an authentication tag that helps verify data integrity upon decryption. To make the encrypted file identifiable and verifiable, a custom file header is constructed. This header includes a unique magic signature ("AE256"), version number, salt, and nonce, followed by the ciphertext. This systematic structuring of data not only ensures security but also allows the decryption process to reliably extract necessary parameters. The encrypted output is written atomically, meaning it is first saved to a temporary file and then safely renamed to the intended output file. This avoids corruption in cases of interruption during the write operation.

The decryption process is carefully designed to reverse the encryption workflow while verifying correctness at every step. The program first reads the encrypted file and parses its header to extract the version, salt, nonce, and ciphertext. If the magic signature or version number does not match expectations, the program halts, indicating potential corruption or incompatibility. The same key derivation process is applied to the user-provided password using the extracted salt, ensuring the key generated during decryption matches the one used during encryption. The AESGCM cipher is then used to decrypt the ciphertext. If the password is incorrect or the file has been tampered with, the decryption will fail, signaling that the data cannot be trusted. This strict checking mechanism strengthens security and prevents unauthorized access.

The program is built with a user-friendly command-line interface using the argparse module. It offers two main commands: `encrypt` and `decrypt`. For encryption, the user specifies the input file and optionally the output file. If no output is provided, the program automatically appends the `.ae256` suffix to the original filename. During decryption, if an output filename is not specified, the program intelligently strips the `.ae256` extension or appends `.dec` to indicate the restored file. Password handling is performed securely using the getpass module, which prevents passwords from being displayed on the terminal. Furthermore, password confirmation is required during encryption to minimize user errors.

Overall, this task represents a comprehensive example of how cryptographic principles can be translated into practical software. It combines concepts of key derivation, authenticated encryption, file handling, error management, and user interaction to produce a reliable and secure encryption tool. By ensuring both confidentiality and integrity, the tool provides users with confidence that their sensitive files remain protected against unauthorized access and malicious tampering, making it a valuable resource in modern cybersecurity practices.

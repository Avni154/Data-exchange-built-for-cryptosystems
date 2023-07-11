# Data-exchange-built-for-cryptosystems
Basic Architecture
Level 1: Functional interaction of client and application There are two parties present:
    The creator/issuer is a party who initiates the creation of objects in the pool. Essentially, the creator is considered as the party         which created a cipher / Diffie Hellman communication and wants to use the application to share the parameters to other parties.
    Access pool is the list of parties which have the visibility of the parameters/contents of the objects on the chain. This access list       is defined and modified by the issuer only.
    It is important to note that we identify all the parties using their public address on the blockchain which cannot be altered or             mimicked due to the design of blockchain technology.
Level 2: Contract architecture
    The contract contains 3 pools
    1. Cipher pool: For storing and retrieving ciphers accessible to the parties present in the access pool list
    2. Diffie Hellman Pool: For storing and retrieving diffie hellman key exchange parameters such as prime, generator and public exchange     values which are accessible to the parties present in the access pool list
    3. Public Key pool: For storing and retrieving parameters necessary for exchanges in a public key cryptosystem. The access design is       similar to cipher pool and Diffie hellman pool.


Pseudocode of the Smart Contract
1) Define a new contract called "transaction".
2) Declare two unsigned integer variables called "CAcounter" and "DHPcounter".
3) Define three new structs called "cipherAssociation", "diffieHellmanPool", and
"publicKeyPool".
4) Define private arrays to store cipher associations and Diffie-Hellman pools, and private
mappings to store public key pools and public key identifiers.
5) Create a constructor function that sets both "CAcounter" and "DHPcounter" to 0.
6) Define a "storeCipher" function that takes in a string "cipher" and an array of addresses
"parties", and returns a unique identifier for the stored cipher. Inside this function:
a) Create a new cipherAssociation struct with the provided information, push it to the "CA"
array, and add the function caller's address to the "accessPool" array.
b) Set the unique identifier for the new cipher to the current value of "CAcounter",
increment "CAcounter" by 1, and return the unique identifier.
7) Define an "addAccessorCipher" function that takes in a cipher identifier and an array of addresses "parties", and returns a boolean indicating whether the function caller (cipher
issuer) is authorized to add the provided parties to the cipher's access pool. Inside this function:
(a) Find the cipher with the provided identifier in the "CA" array and assign it to a local
variable "c".
b) If the function caller's address matches the cipher's issuer address, set the "flag" variable
to true and add each address in the "parties" array to the cipher's "accessPool" array.
c) Return the value of "flag".
8) Define a "retrieveCipher" function that takes in a cipher identifier and returns the stored cipher string if the function caller is authorized to access it. Inside this function:
(a) Find the cipher with the provided identifier in the "CA" array and assign it to a local
variable "c".
(b) Loop through each address in the cipher's "accessPool" array.
(c) If the function caller's address matches an address in the "accessPool" array, return the
stored cipher string. Otherwise, return "0".
9) Define a "createNewDHExchange" function that takes in prime and generator numbers, an
exchange number, and an array of addresses "parties", and returns a unique identifier for the new Diffie-Hellman pool. Inside this function:
a. Create a new diffieHellmanPool struct with the provided information, push it to the
"DHP" array, and add the function caller's address to the "accessPool" array.
b. Set the unique identifier for the new Diffie-Hellman pool to the current value of
"DHPcounter", increment "DHPcounter" by 1, and return the unique identifier.
10) Define an "addDHEexchange" function that takes in a Diffie-Hellman pool identifier and an exchange number, and returns a boolean indicating whether the function caller is authorized
to update the exchange number for the pool. Inside this function:
a) Loop through each address in the pool's "accessPool" array.
b) If the function caller's address matches an address in the "accessPool" array, set the
exchange number for the pool to the provided exchange number and set "flag" to true.
c) Return the value of "flag".
11) Define an "addAccessorDH" function that takes in a Diffie-Hellman pool identifier and an array of addresses "parties", and returns a boolean indicating

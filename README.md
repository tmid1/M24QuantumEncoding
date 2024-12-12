# M24QuantumEncoding
A quantum encoding protocol that I came up with for my Modern Physics Final Project.

##**The M24 encoding scheme:**

For my final project, I wanted to look into Quantum Cryptography, and try making my own encoding scheme. Traditionally, the encodings are named as (First letter of last name) + Year, so I named mine M24. The scheme goes as follows:

####**Phase 1:**
Phase 1 uses the principles behind the E19 encoding key distribution. The what is nice about E19, is that eavesdropping detection is automatic. Eavesdropping is when a 3rd, untrusted party trys to intercept communication between two parties. In these scenarios, we will call the communicators Alice and Bob, and the 3rd party, and eavsdropper Eve. Our communication starts with a third party sending entangled qubits to Alice and Bob. For our scheme, we will have the third party send 7 qubits. Qubits 0-3 will determine how many quantum walks will be performed (part of the later encoding) and qubits 4-6 will determine what is the inital "shift" gate, choosing between Pauli X, Pauli Y, and Pauli Z gates (also used later). The 3rd party will send these entangled bits to Alice and Bob, and they will measure them in random baseses. If the correlation between the measurements that Alice and Bob take does not align with a certain distribution, Alice and Bob know that Eve was not truly sending entangled qubits, and they can cease communication. Because of this Eve, the distributor, does not need to be trusted. If the qubits correlate then Alice and Bob can move on to phase 2, but for my exmaple coded below, I made it so that Alice and Bob will always receive a correct key, which will be a completely random key, that I have adjusted so that the number of walks is always even, and so that there is no issue with the gates, for example the last three bits being 111, when they should only ever be 100, 010, and 001 (X, Y and Z). I chose the number of walks to always be even so that it could be decoded. Below is a visual to demonstrate this.

####**Phase 2:**
Phase 2 involved encoding a message using my encoding scheme. The idea behind my scheme are quantum walks. Quanutum walks are the similar to classical random walks, but incorporate the super position of a qubit to "cover all possibilities at once". To do this on a single qubit, the Hadamard gate can be used, which sends the qubit into a super position. The gate is also unitary, meaning that it can be undone, so the receiver of the message can undo the encoding if they know what shifts were used, and how many times the walk occured. The circuit for this encoding is:

![image](https://github.com/user-attachments/assets/17be292e-c0b0-4605-98ad-c8f686618f2d)

In the diagram, H is the Hadamard gate, and X, Y and Z are the corresponding Pauli gates, that are used depending on the key distributed in Phase 1. The reason that the encoding is done an even amount of times, is because if it weren't the encoding and decoding wouldn't be symmetrical, so it would be impossible to reliably decode the message as demonstrated by this diagram:

![image](https://github.com/user-attachments/assets/8cccc4ab-0e1b-4466-9d73-e208a5d53d55)

The reason I wanted to add this quantum walk step is so that Alice and Bob could communicate on an open channel, knowing that they are safe from eavesdroppers, because if the qubits were measured prematurely, the message would be destroyed because the superposition would collapse. Further, only Alice and Bob could know the key that allows them to decode the message, because of the inherent randomness from the E91 key distribution.

####**Phase 3:**
Finally, in Phase 3, the inverse of the decoding is done using the Hadamard dagger and the Pauli dagger gates.

In conclusion, I am pretty satisfied with the encoding, but in the future if I had more time, I would want to improve it slightly. One flaw with the the quantum walk method is that there is a chance that when the message is encoded, the walk has actually come back to the initial state (walked in a circle). I would want to add a safeguard for this in the future.

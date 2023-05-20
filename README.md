# HammingCode_7_4
Encode, Decode,Detection and Correction error  Hamming 7/4 Method using Python

from typing import List
# Function to calculate the parity bits for a 4-bit message
def calculate_parity_bits(message):
    p1 = message[0] ^ message[1] ^ message[3]
    p2 = message[0] ^ message[2] ^ message[3]
    p3 = message[1] ^ message[2] ^ message[3]
    return [p1, p2, p3]

# Function to encode a 4-bit message into a 7-bit Hamming Code
def encode_message(message):
    parity_bits = calculate_parity_bits(message)
    code = [
         parity_bits[0],
        parity_bits[1],
        message[0],
        parity_bits[2],
        message[1],
        message[2],
        message[3]
          ]
    return  "The Encoded Message is "+str(code)

# Function to decode a 7-bit Hamming Code into a 4-bit message
def decode_code2(code: List[int]) -> List[int]:
    # Calculate the syndrome
    s1 = code[0] ^ code[2] ^ code[4] ^ code[6]
    s2 = code[1] ^ code[2] ^ code[5] ^ code[6]
    s3 = code[3] ^ code[4] ^ code[5] ^ code[6]
    syndrome = s1 * 1 + s2 * 2 + s3 * 4

    # If the syndrome is nonzero, there is an error
    if syndrome != 0:
        # Correct the error
        code[syndrome-1] = code[syndrome-1] ^ 1
        print("There is an Error at Bit "+str(syndrome))
        
    # Extract the original message
    message = [code[2], code[4], code[5], code[6]]
    if(syndrome==0):
        print("There is No error")
    return message

print(encode_message([0,1,0,1]))
print(decode_code2([1,0,1,1,0,0,0]))
print(decode_code2([0,1,0,0,1,0,1]))

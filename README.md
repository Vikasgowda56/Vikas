# Vikas
skill swap

# CRC Error Detection Program

def xor(a, b):
    result = ""
    for i in range(1, len(b)):
        result += '0' if a[i] == b[i] else '1'
    return result

def mod2div(dividend, divisor):
    pick = len(divisor)
    temp = dividend[:pick]

    while pick < len(dividend):
        if temp[0] == '1':
            temp = xor(divisor, temp) + dividend[pick]
        else:
            temp = xor('0' * pick, temp) + dividend[pick]
        pick += 1

    if temp[0] == '1':
        temp = xor(divisor, temp)
    else:
        temp = xor('0' * pick, temp)

    return temp

# Sender side
data = input("Enter data bits: ")
key = input("Enter generator polynomial: ")

# Append zeros
appended_data = data + '0' * (len(key) - 1)

# Calculate CRC
remainder = mod2div(appended_data, key)

# Transmitted data
codeword = data + remainder

print("\n--- Sender Side ---")
print("CRC Remainder:", remainder)
print("Transmitted Data:", codeword)

# Receiver side
received_data = input("\nEnter received data: ")

# Check CRC
check = mod2div(received_data, key)

print("\n--- Receiver Side ---")
print("Remainder:", check)

if '1' in check:
    print("Error Detected!")
else:
    print("No Error Detected!")
    

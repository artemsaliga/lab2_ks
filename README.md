# lab2_ks

    import struct
    
    def to_binary(n):
        return bin(n)[2:]
    
    def multiply_column(a, b):
        result = 0
    
        print("\n--- Binary Multiplication ---")
        print(f"A = {a} = {to_binary(a)}")
        print(f"B = {b} = {to_binary(b)}")
    
        shift = 0
        temp_b = b
    
        while temp_b > 0:
            bit = temp_b & 1
    
            if bit == 1:
                partial = a << shift
            else:
                partial = 0
    
            print(f"Bit {shift}: {bit}")
            print(f"Partial product: {to_binary(partial)}")
    
            result += partial
            temp_b >>= 1
            shift += 1
    
        print(f"\nFinal result: {to_binary(result)} = {result}")
    
    def divide_one_register(dividend, divisor):
        print("\n--- Binary Division ---")
    
        if divisor == 0:
            print("Division by zero error")
            return
    
        n = len(to_binary(dividend))
        remainder = 0
        quotient = dividend
    
        print(f"Dividend = {to_binary(dividend)}")
        print(f"Divisor  = {to_binary(divisor)}")
    
        for i in range(n):
            remainder = (remainder << 1) | ((quotient >> (n - 1)) & 1)
            quotient = (quotient << 1) & ((1 << n) - 1)
    
            print(f"\nStep {i + 1}")
            print(f"Remainder = {to_binary(remainder)}")
            print(f"Quotient  = {to_binary(quotient)}")
    
            if remainder >= divisor:
                remainder -= divisor
                quotient |= 1
    
                print("Subtract divisor")
                print("Write 1 to quotient")
            else:
                print("Do not subtract")
                print("Write 0 to quotient")
    
            print(f"New remainder = {to_binary(remainder)}")
            print(f"New quotient  = {to_binary(quotient)}")
    
        print("\nFinal result:")
        print(f"Quotient  = {to_binary(quotient)} = {quotient}")
        print(f"Remainder = {to_binary(remainder)} = {remainder}")
    
    def float_to_ieee754(num):
        packed = struct.pack('!f', num)
        integer = struct.unpack('!I', packed)[0]
        return format(integer, '032b')
    
    def ieee_addition(x, y):
        print("\n--- IEEE 754 Addition ---")
    
        result = x + y
    
        b1 = float_to_ieee754(x)
        b2 = float_to_ieee754(y)
        b3 = float_to_ieee754(result)
    
        print(f"X1 = {x}")
        print(f"X2 = {y}")
    
        print(f"\nX1 IEEE754: {b1}")
        print(f"X2 IEEE754: {b2}")
    
    
    
        print(f"\nResult = {result}")
        print(f"Result IEEE754: {b3}")
    
    def main():
        print("Laboratory Work 2")
        print("Binary Arithmetic Operations")
    
        a = int(input("\nEnter first integer: "))
        b = int(input("Enter second integer: "))
    
        print("\n--- Binary Conversion ---")
        print(f"{a} = {to_binary(a)}")
        print(f"{b} = {to_binary(b)}")
    
        multiply_column(a, b)
        divide_one_register(a, b)
    
        x = float(input("\nEnter first float number: "))
        y = float(input("Enter second float number: "))
    
        ieee_addition(x, y)
    
    main()

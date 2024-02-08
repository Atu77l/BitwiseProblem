# Basic Introduction
  a) use of ~ (also called complement or tilde)  =>  invertBit + 1;
  b) a+b = a|b + a&b 
  c) n+x = n^x + 2*(n&x)
  d) The left-shift and right-shift operators are equivalent to multiplication and division by 2 respectively.
  One-Liner Hacks of Bit Manipulation:
    One-Liner Code
    Function
    1. x&1
    
    Evaluates to 1 if the number is odd else evaluates to 0
    
    2. x & (x-1)
    
    Clears the lowest set bit of x
    
    3. x & ~(x-1)
    
    Extracts the lowest set bit of x (all others are cleared)
    
    4. x & ~((1 << i+1 ) – 1)
    
    Clears all bits of x from LSB to ith bit
    
    5. x & ((1 << i) – 1)
    
    Clears all bits of x from MSB to ith bit
    
    6. x >>1
    
    Divides x by 2
    
    7. x << 1
    
    Multiplies x by 2 
    
    8. ch | ‘ ‘
    
    Upper case English alphabet ch to lower case
    
    9. ch & ‘_’
    
    Lower case English alphabet ch to upper case
    
    10. x && !(x & x-1)
    
    Checking if given 32-bit integer is power of 2
    
    11. log2(n & -n)+1

    Find the last set bit
# BitwiseProblem
# 1. Compute XOR from 1 to n (direct method):
The  problem can be solved based on the following observations:

Say x = n%4. The XOR value depends on the value if x. If

x = 0, then the answer is n.
x = 1, then answer is 1.
x = 2, then answer is n+1.
x = 3, then answer is 0.
# 2. Count of numbers (x) smaller than or equal to n such that n+x = n^x:
The count of such numbers x can be counted using the following mathematical trick. 

The count = pow(2, count of zero bits).
reason:: An efficient solution is as follows

we know that (n+i)=(n^i)+2*(n&i)
So n + i = n ^ i implies n & i = 0
Hence our problem reduces to finding values of i such that n & i = 0. How to find count of such pairs? We can use the count of unset-bits in the binary representation of n. For n & i to be zero, i must unset all set-bits of n. If the kth bit is set at a particular in n, kth bit in i must be 0 always, else kth bit of i can be 0 or 1
Hence, total such combinations are 2^(count of unset bits in n)
For example, consider n = 12 (Binary representation : 1 1 0 0). 
All possible values of i that can unset all bits of n are 0 0 0/1 0/1 where 0/1 implies either 0 or 1. Number of such values of i are 2^2 = 4. 

#3. How to know if a number is a power of 2?
This can be solved based on the following fact:

If a number N is a power of 2, then the bitwise AND of N and N-1 will be 0. But this will not work if N is 0. So just check these two conditions, if any of these two conditions is true.

#4. Find XOR of all subsets of a set
We can do it in O(1) time. The answer is always 0 if the given set has more than one element. For sets with a single element, the answer is the value of the single element. 

# 5. Find the number of leading, trailing zeroes and number of 1’s
We can quickly find the number of leading, trailing zeroes and number of 1’s in a binary code of an integer in C++ using GCC. 

It can be done by using inbuilt functions i.e.

Number of leading zeroes: __builtin_clz(x)
Number of trailing zeroes : __builtin_ctz(x)
Number of 1-bits: __builtin_popcount(x) 
# 6. The Quickest way to swap two numbers:
Two numbers can be swapped easily using the following bitwise operations:

a ^= b;
b ^= a; 
a ^= b; 
# 6
Finding the most significant set bit (MSB):
We can find the most significant set bit in O(1) time for a fixed size integer. For example below code is for 32-bit integer. 


def setBitNumber(n):
    # Below steps set bits after
    # MSB (including MSB)
 
    # Suppose n is 273 (binary
    # is 100010001). It does following
    # 100010001 | 010001000 = 110011001
    n |= n >> 1
 
    # This makes sure 4 bits
    # (From MSB and including MSB)
    # are set. It does following
    # 110011001 | 001100110 = 111111111
    n |= n >> 2
 
    n |= n >> 4
    n |= n >> 8
    n |= n >> 16
 
    # Increment n by 1 so that
    # there is only one set bit
    # which is just before original
    # MSB. n now becomes 1000000000
    n = n + 1
 
    # Return original MSB after shifting.
    # n now becomes 100000000
    return (n >> 1)
    
7). Check if a number has bits in an alternate pattern
We can quickly check if bits in a number are in an alternate pattern (like 101010). 

Compute bitwise XOR (XOR denoted using ^) of n and (n >> 1). If n has an alternate pattern, then n ^ (n >> 1) operation will produce a number having all bits set.

# function to check if all the bits
# are set or not in the binary
# representation of 'n'
def allBitsAreSet(n):
  # if true, then all bits are set
  if (((n + 1) & n) == 0):
    return True
 
  # else all bits are not set
  return False
 
# Function to check if a number
# has bits in alternate pattern
def bitsAreInAltOrder(n):
  num = n ^ (n >> 1)
 
  # To check if all bits are set in 'num'
  return allBitsAreSet(num)
8) Invert Actual bit of Number ( 1011 ==> 0100)

    1st Method::
    def invertBits(num):
        # calculating the mask
        x = num
        x |= x >> 1
        x |= x >> 2
        x |= x >> 4
        x |= x >> 8
        x |= x >> 16
     
        print(num ^ x)
     
     
    # Driver Code
    num = 11
    invertBits(num)

    2nd Method::
   The inverted number can be efficiently obtained by:

  1. Getting the number of bits using log2
  
  2. Taking XOR of the number and 2 numOfBits – 1 

   def invertBits(num):
      # Find number of bits in the given integer
      numOfBits = num.bit_length()
   
      # Invert the number by taking
      # xor of n and (2 raised to numOfBits) - 1
      print(((1 << numOfBits) - 1) ^ num)
# 9)  

##https://www.geeksforgeeks.org/bits-manipulation-important-tactics/

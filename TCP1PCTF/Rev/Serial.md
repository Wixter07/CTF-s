# Serial

Ok so .NET exe which has two input fields, one's name and the other one's serial. Disassembled the exe on dnSpy and there are some interesting AES functions in it, but our interests lie in the `checkSerial` function.
The `name` function takes in a input and goes through two algorithms to generate `num` and `num6`.
These two hashes are used as parameters to form an array which is used in the `checkSerial` function to match.

So basically, the serial is generated based on the name input. Here is the `checkSerial` code.

```C#
// Serial, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null
// <Module>
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;
using std;

[return: MarshalAs(UnmanagedType.U1)]
internal unsafe static bool checkSerial(basic_string<char,std::char_traits<char>,std::allocator<char> >* szName, basic_string<char,std::char_traits<char>,std::allocator<char> >* szSerial)
{
	//IL_00a2: Expected I, but got I8
	//IL_02af: Expected I, but got I8
	//IL_02cb: Expected I, but got I8
	//IL_02e2: Expected I, but got I8
	//IL_0318: Expected I, but got I8
	//IL_0328: Expected I, but got I8
	//IL_017e: Expected I, but got I8
	//IL_0190: Expected I, but got I8
	//IL_019f: Expected I, but got I8
	//IL_00f6: Expected I, but got I8
	//IL_0108: Expected I, but got I8
	//IL_0117: Expected I, but got I8
	//IL_0338: Expected I, but got I8
	//IL_0348: Expected I, but got I8
	//IL_0358: Expected I, but got I8
	//IL_0368: Expected I, but got I8
	//IL_0378: Expected I, but got I8
	//IL_0388: Expected I, but got I8
	//IL_00ae->IL00b1: Incompatible stack types: I vs I8
	System.Runtime.CompilerServices.Unsafe.SkipInit(out vector<int,std::allocator<int> > obj);
	try
	{
		try
		{
			int num = 0;
			int num2 = 0;
			int num3 = 0;
			do
			{
				int num4 = (((num3 ^ 0x7892) + 19760) ^ 0x3421) % 65536;
				if (num4 % 11 == 0)
				{
					num4 /= 11;
					if (num4 <= 1000)
					{
						num = num3;
						num2 = num4;
					}
				}
				num3++;
			}
			while (num3 < 65536);
			num3 = 0;
			int num5 = (int)(*(long*)((ulong)(nint)szName + 16uL));
			int num6 = 0;
			if (num5 <= 0)
			{
				num6 = 0;
			}
			else
			{
				int num7 = 0;
				int num8 = 0;
				int num9 = num * 15 % 256;
				int num10 = num2 * 17 % 256;
				int num11 = 0;
				long num12 = 0L;
				long num13 = num5;
				if (0 < num13)
				{
					basic_string<char,std::char_traits<char>,std::allocator<char> >* ptr = (basic_string<char,std::char_traits<char>,std::allocator<char> >*)((ulong)(nint)szName + 24uL);
					do
					{
						long num14 = (nint)szName;
						if ((ulong)(*(long*)ptr) > 15uL)
						{
							num14 = *(long*)szName;
						}
						sbyte b = (sbyte)toupper(*(sbyte*)(num14 + num12));
						int num15 = (int)((long)(uint)(*(int*)((long)(byte)b * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE)) + num3) % 4294967296L);
						if (num11 % 2 == 0)
						{
							uint* ptr2 = (uint*)((long)(b + 13) * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE));
							uint* ptr3 = (uint*)((long)(b + 47) * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE));
							uint* ptr4 = (uint*)((long)num10 * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE));
							num15 = (int)((long)(uint)(*(int*)((long)num9 * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE)) + (int)((*ptr2 ^ (uint)num15) * *ptr3) + (int)(*ptr4)) % 4294967296L);
							int num16 = (int)((long)(uint)(*(int*)((long)num8 * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE)) + num15) % 4294967296L);
							num6 = num16;
							num3 = num16;
						}
						else
						{
							uint* ptr4 = (uint*)((long)(b + 63) * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE));
							uint* ptr5 = (uint*)((long)(b + 23) * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE));
							uint* ptr6 = (uint*)((long)num10 * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE));
							int num17 = (int)((long)(uint)(*(int*)((long)num9 * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE)) + (int)((*ptr4 ^ (uint)num15) * *ptr5) + (int)(*ptr6)) % 4294967296L);
							int num18 = (int)((long)(uint)(*(int*)((long)num7 * 4L + System.Runtime.CompilerServices.Unsafe.As<vector<unsigned int,std::allocator<unsigned int> >, long>(ref TABLE)) + num17) % 4294967296L);
							num6 = num18;
							num3 = num18;
						}
						num8 = (num8 + 19) % 256;
						num10 = (num10 + 9) % 256;
						num9 = (num9 + 13) % 256;
						num7 = (num7 + 7) % 256;
						num11++;
						num12++;
					}
					while (num12 < num13);
				}
			}
			*(long*)(&obj) = 0L;
			System.Runtime.CompilerServices.Unsafe.As<vector<int,std::allocator<int> >, long>(ref System.Runtime.CompilerServices.Unsafe.AddByteOffset(ref obj, 8)) = 0L;
			System.Runtime.CompilerServices.Unsafe.As<vector<int,std::allocator<int> >, long>(ref System.Runtime.CompilerServices.Unsafe.AddByteOffset(ref obj, 16)) = 0L;
			std.vector<int,std::allocator<int> >._Construct_n<>(&obj, 8uL);
			try
			{
				*(int*)(*(long*)(&obj) + 16) = num6 % 256;
				*(int*)(*(long*)(&obj) + 20) = (num6 >> 8) % 256;
				*(int*)(*(long*)(&obj) + 24) = (num6 >> 16) % 256;
				*(int*)(*(long*)(&obj) + 28) = (num6 >> 24) % 256;
				*(int*)(*(long*)(&obj) + 12) = 156;
				int* ptr7 = (int*)(*(long*)(&obj) + 20);
				*(int*)(*(long*)(&obj) + 8) = (num % 256) ^ *ptr7;
				ptr7 = (int*)(*(long*)(&obj) + 28);
				*(int*)(*(long*)(&obj) + 4) = (num >> 8) ^ *ptr7;
				ptr7 = (int*)(*(long*)(&obj) + 4);
				*(int*)(*(ulong*)(&obj)) = ((*(int*)(*(long*)(&obj) + 24) ^ *ptr7 ^ 0x55) % 256) ^ 0xA7;
				sbyte* ptr8 = (sbyte*)szSerial;
				ulong num19 = *(ulong*)((ulong)(nint)szSerial + 24uL);
				if (num19 > 15)
				{
					ptr8 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr9 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr9 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr10 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr10 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr11 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr11 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr12 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr12 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr13 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr13 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr14 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr14 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte* ptr15 = (sbyte*)szSerial;
				if (num19 > 15)
				{
					ptr15 = (sbyte*)(*(ulong*)szSerial);
				}
				sbyte b2 = *ptr8;
				int num20 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
				b2 = *(sbyte*)((ulong)(nint)ptr8 + 1uL);
				int num21 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
				if (((num20 << 4) | num21) == (*(int*)(*(ulong*)(&obj)) & 0xFF))
				{
					b2 = *(sbyte*)((ulong)(nint)ptr9 + 2uL);
					num20 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
					b2 = *(sbyte*)((long)(nint)ptr9 + 2L + 1);
					int num22 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
					if (((num20 << 4) | num22) == (*(int*)(*(long*)(&obj) + 4) & 0xFF))
					{
						b2 = *(sbyte*)((ulong)(nint)ptr10 + 5uL);
						int num23 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
						b2 = *(sbyte*)((long)(nint)ptr10 + 5L + 1);
						int num24 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
						if (((num23 << 4) | num24) == (*(int*)(*(long*)(&obj) + 8) & 0xFF))
						{
							b2 = *(sbyte*)((ulong)(nint)ptr11 + 7uL);
							int num25 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
							b2 = *(sbyte*)((long)(nint)ptr11 + 7L + 1);
							int num26 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
							if (((num25 << 4) | num26) == (*(int*)(*(long*)(&obj) + 12) & 0xFF))
							{
								b2 = *(sbyte*)((ulong)(nint)ptr12 + 10uL);
								int num27 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
								b2 = *(sbyte*)((long)(nint)ptr12 + 10L + 1);
								int num28 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
								if (((num27 << 4) | num28) == (*(int*)(*(long*)(&obj) + 16) & 0xFF))
								{
									b2 = *(sbyte*)((ulong)(nint)ptr13 + 12uL);
									int num29 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
									b2 = *(sbyte*)((long)(nint)ptr13 + 12L + 1);
									int num30 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
									if (((num29 << 4) | num30) == (*(int*)(*(long*)(&obj) + 20) & 0xFF))
									{
										b2 = *(sbyte*)((ulong)(nint)ptr14 + 15uL);
										int num31 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
										b2 = *(sbyte*)((long)(nint)ptr14 + 15L + 1);
										int num32 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
										if (((num31 << 4) | num32) == (*(int*)(*(long*)(&obj) + 24) & 0xFF))
										{
											b2 = *(sbyte*)((ulong)(nint)ptr15 + 17uL);
											int num33 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
											b2 = *(sbyte*)((long)(nint)ptr15 + 17L + 1);
											int num34 = ((b2 < 48 || b2 > 57) ? ((b2 & -33) - 55) : (b2 - 48));
											if (((num33 << 4) | num34) == (*(int*)(*(long*)(&obj) + 28) & 0xFF))
											{
												goto IL_06a9;
											}
										}
									}
								}
							}
						}
					}
				}
			}
			catch
			{
				//try-fault
				___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<vector<int,std::allocator<int> >*, void>)(&std.vector<int,std::allocator<int> >.{dtor}), &obj);
				throw;
			}
			goto end_IL_0000;
			IL_06a9:
			std.vector<int,std::allocator<int> >._Tidy(&obj);
			goto IL_06c0;
			end_IL_0000:;
		}
		catch
		{
			//try-fault
			___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<basic_string<char,std::char_traits<char>,std::allocator<char> >*, void>)(&std.basic_string<char,std::char_traits<char>,std::allocator<char> >.{dtor}), szName);
			throw;
		}
		goto end_IL_0000_2;
		IL_06c0:
		try
		{
			std.basic_string<char,std::char_traits<char>,std::allocator<char> >._Tidy_deallocate(szName);
		}
		catch
		{
			//try-fault
			___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<_Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>*, void>)(&std._Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>.{dtor}), szName);
			throw;
		}
		goto IL_06e5;
		end_IL_0000_2:;
	}
	catch
	{
		//try-fault
		___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<basic_string<char,std::char_traits<char>,std::allocator<char> >*, void>)(&std.basic_string<char,std::char_traits<char>,std::allocator<char> >.{dtor}), szSerial);
		throw;
	}
	try
	{
		try
		{
			std.vector<int,std::allocator<int> >._Tidy(&obj);
		}
		catch
		{
			//try-fault
			___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<basic_string<char,std::char_traits<char>,std::allocator<char> >*, void>)(&std.basic_string<char,std::char_traits<char>,std::allocator<char> >.{dtor}), szName);
			throw;
		}
		try
		{
			std.basic_string<char,std::char_traits<char>,std::allocator<char> >._Tidy_deallocate(szName);
		}
		catch
		{
			//try-fault
			___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<_Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>*, void>)(&std._Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>.{dtor}), szName);
			throw;
		}
	}
	catch
	{
		//try-fault
		___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<basic_string<char,std::char_traits<char>,std::allocator<char> >*, void>)(&std.basic_string<char,std::char_traits<char>,std::allocator<char> >.{dtor}), szSerial);
		throw;
	}
	try
	{
		std.basic_string<char,std::char_traits<char>,std::allocator<char> >._Tidy_deallocate(szSerial);
	}
	catch
	{
		//try-fault
		___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<_Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>*, void>)(&std._Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>.{dtor}), szSerial);
		throw;
	}
	return false;
	IL_06e5:
	try
	{
		std.basic_string<char,std::char_traits<char>,std::allocator<char> >._Tidy_deallocate(szSerial);
	}
	catch
	{
		//try-fault
		___CxxCallUnwindDtor((delegate*<void*, void>)(delegate*<_Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>*, void>)(&std._Compressed_pair<std::allocator<char>,std::_String_val<std::_Simple_types<char> >,1>.{dtor}), szSerial);
		throw;
	}
	return true;
}
```

You can set a breakpoint on name to get `num` and `num6` values for you name input.

I unfortunately couldn't wrap my head around the AES functions to write a proper script. Here is a solve script I got from a writeup.


```py
import hashlib
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

def decrypt_flag(serial, flag):
    # Remove hyphens from the serial and encode it
    serial_bytes = serial.replace("-", "").encode("ascii")
    # Create the key using MD5 hash of the serial
    key = hashlib.md5(serial.encode("ascii")).digest()
    # Convert the flag from hex string to bytes
    flag_bytes = bytes.fromhex(flag)
    # Create AES cipher
    cipher = AES.new(key, AES.MODE_CBC, iv=serial_bytes)
    # Decrypt the flag
    decrypted = cipher.decrypt(flag_bytes)
    # Remove padding and convert to string
    try:
        unpadded = unpad(decrypted, AES.block_size)
        # Find the last occurrence of '}'
        last_brace = unpadded.rfind(b"}")
        if last_brace != -1:
            result = unpadded[: last_brace + 1].decode("utf-8")
        else:
            result = unpadded.decode("utf-8")
    except ValueError:
        # If unpadding fails, just decode as is
        result = decrypted.decode("utf-8", errors="ignore")
    return result
    
num6 = 0xF8809629
serial = [
    0,# 0~0
    0,# 4~1
    0,# 8~2
    156,# 12~3
    num6 % 256,# 16~4
    (num6 >> 8) % 256,# 20~5
    (num6 >> 16) % 256,# 24~6
    (num6 >> 24) % 256,# 28~7
]
num = 0x0000BFFD
serial[2] = (num % 256) ^ serial[5]
serial[1] = (num >> 8) ^ serial[7]
serial[0] = (serial[6] ^ serial[1] ^ 85) % 256 ^ 167
serial = "-".join([bytes(serial[i:i+2]).hex() for i in range(0,len(serial), 2)]).upper()
print(f"Serial: {serial}")
c = "6a2b68f955d492a677f3bd5d22a078a39ca10936ef89cb12823617a1e1bc4d1c"
flag = decrypt_flag(serial, c)
print(f"Flag: {flag}")
```

There were multiple approaches to solve this one, an interesting one being to replicate the whole binary by focusing on the two functions of interest.

# Ransom System.md
 
## Description

The enemy has spread ransomware on important systems of the country. Please analyze the ransomware and recover the files!

Author : suriryuk
Points: 220

# Solution
 
There is 2 files: `enc` and `ransom`

`enc` is some junk data (probably encrypted flag)

`ransom` is Win32 PE executable thats do:
  - opens file `flag.exe` with `rb`
  - opens file `flag.exe.enc` with `wb`
  - read `flag.exe` byte by byte
  - encrypts bytes of `flag.exe` and writes it to `flag.exe.enc`

If `flag.exe` is string `flag`, then enrypted output is  b'mw`j\x14\t\x02'
Input len is 4, output is 7. After `g` there is `\r\n` (even if I did not add them). Where last `\x02` come I don't know :(
    
Here is decompilation of `main` function from Ghidra:

```c
int __cdecl _main(int _Argc,char **_Argv,char **_Env)
{
  char chr;
  FILE *file_in;
  FILE *file_out;
  int is_eof;
  
  __main();
  file_in = _file_open("flag.exe","rb");
  file_out = _file_open("flag.exe.enc","wb");
  while( true ) {
    is_eof = _feof(file_in);
    if (is_eof != 0) break;
    chr = _read_data(file_in);
    chr = _encrypt(chr);
    _write_data(file_out,chr);
  }
  _fclose(file_in);
  _fclose(file_out);
  return 0;
}
```

Here is `_encrypt`:

```c
char __cdecl _encrypt(char chr)
{
  byte res;
  res = chr + 5U ^ 6;
  return res + (char)((int)(char)res / 0xff);
}
```

Decrypter: 

```python
def decrypt(char):
    char = int.from_bytes(char, 'big')
    tmp = char - char // 255
    tmp = (tmp ^ 6) - 5
    # Sometimes result goes below 0. I don't know why 
    # and what to do with this, so I just throw away them.
    if (tmp < 0): return b''
    return tmp.to_bytes(1, 'big')

def main():
    in_file = open('./flag.enc', 'rb')
    out_file = open('./flag.exe', 'wb')

    while True:
        char = in_file.read(1)
        if not char:
            break

        out_file.write(decrypt(char))

    in_file.close()
    out_file.close()

if __name__ == "__main__":
    main()
```

Decrypter will produce `flag.exe` file. It is suposed to be Win32 PE executable, I did not managed to recover it fully.
But it recovered enough to `grep` some `string` of it ;)

Flag: ESCAPE{ransomeware_decrypt_key_get!}
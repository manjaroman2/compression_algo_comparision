# Compression algorithm benchmark 

Machine: Ryzen 1200 (Im poor) at 3.6 Ghz, 4 cores, 16gb 2666mhz, samsung ssd 256gb, arch linux 5.18


File:  954M    random_string.lol
---------------------------+-----------------------------------------------------------+---------------
Algorithm   Command        | Compressed Size (MB)    Comp Time (s)    Decomp Time (s)  | CRatio  CR/CT 
LZTURBO     lzturbo -32    | 663                     40               2                | 1.43    3.59 
ZPAQ        zpaq -m3 -t4   | 631                     107              105              | 1.51    1.41  
ZSTD        pzstd -vv -19  | 623                     136                               | 1.53    1.12  
BROTLI      brotli -T4 -11 | 623                     439                               | 1.53    0.34  
ZPAQ        zpaq -m2 -t4   | 797                     350                               | 1.19    0.34  
ZPAQ        zpaq -m5 -t4   | 617                     994                               | 1.54    0.15  
LZTURBO     lzturbo -29    | 822                     766                               | 1.16    0.15 
LZMA        lzma -9 -T 4   | 641                     995                               | 1.48    0.14   
LZTURBO     lzturbo -39    | 954                     785                               | 1       0.12



File:  954M    dewiki-20220401-pages-articles_1GB.xml 
---------------------------+-----------------------------------------------------------+---------------
Algorithm   Command        | Compressed Size (MB)    Comp Time (s)    Decomp Time (s)  | CRatio  CR/CT 
LZTURBO     lzturbo -32    | 275                     10                                | 3.46    34.69 
ZPAQ        zpaq -m3 -t4   | 199                     81                                | 4.79    5.91  
ZPAQ        zpaq -m2 -t4   | 274                     92                                | 3.45    3.75  
ZSTD        pzstd -vv -19  | 246                     184                               | 3.87    2.10  
BROTLI      brotli -T4 -11 | 245                     550                               | 3.89    0.70  
LZMA        lzma -9 -T 4   | 218                     807                               | 4.37    0.54   
ZPAQ        zpaq -m5 -t4   | 176                     1008                              | 5.42    0.53  
LZTURBO     lzturbo -39    | 205                     1478                              | 4.65    0.31 
LZTURBO     lzturbo -29    | 255                     1466                              | 3.74    0.25 



My conclusions: 
Use lzturbo32 for fast comp, use zpaq3 for slower but better comp. 



Annotations: 
Everything was done in parallel so depending on the implementation results may differ. 
The binaries I used are all in pacman except the brotli one I got it from here: https://github.com/mcmilk/zstdmt
Also on the wiki file zpaq 3 was faster than zpaq 2 which makes no sense to me but ok 
CR/CT = compression ratio / compression time * 100 

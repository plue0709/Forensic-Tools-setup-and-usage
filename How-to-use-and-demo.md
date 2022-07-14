# How to use and demo stego-toolkit

## Tools detecting steganography

### stegoVeritas
```
$stegoveritas <file>
$stegoveritas ORIGINAL.jpg
```
```
root@6e2cbf82ae3c:/data# stegoveritas ORIGINAL.jpg
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
+---------+------------------+--------------------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                            | File Name |
+---------+------------------+--------------------------------------------------------------------------------------------------------+-----------+
| 0x3c62c | Carved           | LZMA compressed data, properties: 0x90, dictionary size: 1073741824 bytes, uncompressed size: 32 bytes | 3C62C.7z  |
| 0x3c62c | Extracted        | LZMA compressed data, properties: 0x90, dictionary size: 1073741824 bytes, uncompressed size: 32 bytes | 3C62C     |
+---------+------------------+--------------------------------------------------------------------------------------------------------+-----------+
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                    | File Name |
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
| 0x6ac88 | Carved           | LZMA compressed data, properties: 0x5B, dictionary size: 0 bytes, uncompressed size: 256 bytes | 6AC88.7z  |
| 0x6ac88 | Extracted        | LZMA compressed data, properties: 0x5B, dictionary size: 0 bytes, uncompressed size: 256 bytes | 6AC88     |
+---------+------------------+------------------------------------------------------------------------------------------------+-----------+
+---------+------------------+-----------------------------------------------------------------------------------------------+-----------+
| Offset  | Carved/Extracted | Description                                                                                   | File Name |
+---------+------------------+-----------------------------------------------------------------------------------------------+-----------+
| 0x49761 | Carved           | LZMA compressed data, properties: 0x90, dictionary size: 0 bytes, uncompressed size: 32 bytes | 49761.7z  |
| 0x49761 | Extracted        | LZMA compressed data, properties: 0x90, dictionary size: 0 bytes, uncompressed size: 32 bytes | 49761     |
+---------+------------------+-----------------------------------------------------------------------------------------------+-----------+
Còn nữa có cả metadata(Exiftool)ở cuối 
```
### zsteg
```
$zsteg <file.png/file.bmp>
$zsteg ORIGINAL.png
```
```
root@6e2cbf82ae3c:/data# zsteg ORIGINAL.png
/usr/lib/ruby/2.3.0/open3.rb:199: warning: Insecure world writable dir /opt/scripts in PATH, mode 040777
meta XML:com.adobe.xmp.. text: "<x:xmpmeta xmlns:x=\"adobe:ns:meta/\" x:xmptk=\"XMP Core 5.4.0\">\n   <rdf:RDF xmlns:rdf=\"http://www.w3.org/1999/02/22-rdf-syntax-ns#\">\n      <rdf:Description rdf:about=\"\"\n            xmlns:tiff=\"http://ns.adobe.com/tiff/1.0/\">\n         <tiff:Orientation>1</tiff:Orientation>\n      </rdf:Description>\n   </rdf:RDF>\n</x:xmpmeta>\n"      
imagedata           .. file: shared library
b1,bgr,lsb,xy       .. <wbStego size=65565, ext="\x19a\x80", data="2I\xA4\x01\x12\xD0\x00\x00\x00\x00"..., even=false>
b2,r,lsb,xy         .. file: a.out VAX demand paged (first page unmapped) pure executable not stripped
b2,g,lsb,xy         .. text: "g)q`$/w;"
b3,r,lsb,xy         .. file: Targa image data - Map 65536 x 65536 x 0 +256 +16402 ""
```

### Stegdetect 
```
$stegdetect <file.jpg>
$stegdetect ORIGINAL.jpg
```
```
root@6e2cbf82ae3c:/data# stegdetect ORIGINAL.jpg
ORIGINAL.jpg : negative
```
### Stegbreak
```
$stegbreak [-V] [-r <rules>] [-f <wordlist>] [-t <schemes>] file.jpg 
-t o for crack outguess
-t p for jphide
-t j for jsteg
$root@6e2cbf82ae3c:/data# stegbreak -t o -f rockyou.txt ORIGINAL.jpg
```
```
root@6e2cbf82ae3c:/data# stegbreak -t o -f rockyou.txt ORIGINAL.jpg
Loaded 1 files...
ORIGINAL.jpg : outguess[v0.13b](dragonsballs)[data][R}.,...m.....j..]
Processed 1 files, found 1 embeddings.
Time: 113 seconds: Cracks: 8512828,  75334.8 c/s
```

## Tools actually doing steganography

### AudioStego
```
Hiding data:
+ Hide a File:
$hideme [file_used_to_hide_data] [file_to_hide]
+ Hide String:
$hideme [file_used_to_hide_data] "'Message to hide'"

Retrieving hidden data:
$hideme [file_with_hidden_data] -f

$hideme ORIGINAL.mp3 "'GGCTF{UIT_no_1}'"
$hideme output.mp3 -f
```
```
root@6e2cbf82ae3c:/data# hideme ORIGINAL.mp3 "'GGCTF{UIT_no_1}'"
Doing it boss! 
Spreading level: 29938
Header wrote
File has been saved as: output.mp3
Hiding process has finished successfully.
Cleaning memory...

root@6e2cbf82ae3c:/data# hideme output.mp3 -f
Doing it boss! 
Looking for the hidden message...
String detected. Retrieving it...
Message recovered size: 17 bytes
Message: 'GGCTF{UIT_no_1}'V#3�
Recovering process has finished successfully.
Cleaning memory...

```

### jphide/jpseek	
```
Hiding data:
$jphide [input_file] [output_file] [file_to_hide]
Retrieving hidden data:
$jpseek [input_file] [output_file]

$jphide ORIGINAL.jpg ORIGINAL_fix.jpg flag.txt
$jphide ORIGINAL_fix.jpg output.txt
```
```
root@6e2cbf82ae3c:/data# jphide ORIGINAL.jpg ORIGINAL_fix.jpg flag.txt

jphide, version 0.3 (c) 1998 Allan Latham <alatham@flexsys-group.com>

This is licenced software but no charge is made for its use.
NO WARRANTY whatsoever is offered with this product.
NO LIABILITY whatsoever is accepted for its use.
You are using this entirely at your OWN RISK.
See the GNU Public Licence for full details.

Passphrase: 123
Re-enter  : 123
root@6e2cbf82ae3c:/data# cat flag.txt                       
This is a very secret message!
```
```
root@6e2cbf82ae3c:/data# jpseek ORIGINAL_fix.jpg output.txt

jpseek, version 0.3 (c) 1998 Allan Latham <alatham@flexsys-group.com>

This is licenced software but no charge is made for its use.
NO WARRANTY whatsoever is offered with this product.
NO LIABILITY whatsoever is accepted for its use.
You are using this entirely at your OWN RISK.
See the GNU Public Licence for full details.

Passphrase: 
root@6e2cbf82ae3c:/data# cat output.txt
This is a very secret message!
```
### jsteg
```
Hiding data:
$jsteg hide [input_file] [secret_file] [output_file]
Retrieving hidden data:
$jsteg reveal [input_file] [output_file]

$jsteg hide ORIGINAL.jpg flag.txt ORIGINAL_fix.jpg
$jsteg reveal ORIGINAL_fix.jpg output.txt
```
```
root@6e2cbf82ae3c:/data# jsteg hide ORIGINAL.jpg flag.txt ORIGINAL_fix.jpg
root@6e2cbf82ae3c:/data# jsteg reveal ORIGINAL_fix.jpg output1.txt
root@6e2cbf82ae3c:/data# cat output1.txt
This is a very secret message!
root@6e2cbf82ae3c:/data# cat flag.txt
This is a very secret message!
```

### mp3stego
```
Hiding data:
$mp3stego-encode -E [secret_file] -P <password> /path/to/input.wav /path/to/output.mp3
Retiring data:
$mp3stego-decode -X -P <password> /path/to/input.mp3 /path/to/out.pcm /path/to/output.txt

$mp3stego-encode -E flag.txt -P 123456 audio.wav ORIGINAL_fix.mp3
$mp3stego-decode -X -P 123456 /data/ORIGINAL_fix.mp3 /data/output.pcm /data/output2.txt
```
```
Cần sửa lại chuyển file mp3 thành file wav bằng ffmpeg để tránh bị lỗi
root@6e2cbf82ae3c:/data# ffmpeg -i ORIGINAL.mp3 -flags bitexact audio.wav

root@6e2cbf82ae3c:/data# mp3stego-encode -E flag.txt -P 123456 audio.wav ORIGINAL_fix.mp3
MP3StegoEncoder 1.1.17
See README file for copyright info
Microsoft RIFF, WAVE audio, PCM, mono 44100Hz 16bit, Length:  0: 1:52
MPEG-I layer III, mono  Psychoacoustic Model: AT&T
Bitrate=128 kbps  De-emphasis: none  CRC: off  
Encoding "audio.wav" to "ORIGINAL_fix.mp3"
Hiding "flag.txt"
[Frame   4295 of   4295] (100.00%) Finished in  0: 0: 0
```
```
root@6e2cbf82ae3c:/data# mp3stego-decode -X -P 123456 /data/ORIGINAL_fix.mp3 /data/output.pcm /data/output2.txt
MP3StegoEncoder 1.1.17
See README file for copyright info
Input file = '/data/ORIGINAL_fix.mp3'  output file = '/data/output.pcm'
Will attempt to extract hidden information. Output: /data/output2.txt
the bit stream file /data/ORIGINAL_fix.mp3 is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=3, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=single-ch, sblim=32, jsbd=32, ch=1
[Frame 4295]Avg slots/frame = 417.862; b/smp = 2.90; br = 127.970 kbps
Decoding of "/data/ORIGINAL_fix.mp3" is finished
The decoded PCM output file name is "/data/output.pcm"
WARNING: if you used relative paths, you find your results relative to "/opt/mp3stego/MP3Stego_1_1_18/MP3Stego/"
root@6e2cbf82ae3c:/data# cat output2.txt
This is a very secret message!
```

### openstego
```
Hiding data:
$openstego embed -mf [secret_file] -cf [input.png] -p <password> -sf [output.png]
Retiring data:
$openstego extract -sf [input.png] -p <password> -xf <output.txt>
```
```
root@6e2cbf82ae3c:/data# openstego embed -mf flag.txt -cf ORIGINAL.png -p 123456 -sf output.png
root@6e2cbf82ae3c:/data# openstego extract -sf output.png -p 123456 -xf output4.txt
Extracted file: output4.txt
root@6e2cbf82ae3c:/data# cat output4.txt
This is a very secret message!
```

### outguess
```
Hiding data:
$outguess -k <password> -d [secret_file] [input.jpg] [output.jpg]
Retiring data:
$outguess -r -k <password> [input.jpg] [output.txt]
```
```
root@6e2cbf82ae3c:/data# outguess -k 123456 -d flag.txt ORIGINAL.jpg output.jpg
Reading ORIGINAL.jpg....
JPEG compression quality set to 75
Extracting usable bits:   139630 bits
Correctable message size: -23811 bits, 13211160488706048.00%
Encoded 'flag.txt': 248 bits, 31 bytes
Finding best embedding...
    0:   144(51.4%)[58.1%], bias   128(0.89), saved:    -2, total:  0.10%
    1:   130(46.4%)[52.4%], bias   130(1.00), saved:     0, total:  0.09%
    4:   142(50.9%)[57.3%], bias   104(0.73), saved:    -2, total:  0.10%
    5:   133(47.5%)[53.6%], bias    98(0.74), saved:    -1, total:  0.10%
   66:   132(47.1%)[53.2%], bias    97(0.73), saved:    -1, total:  0.09%
  122:   124(44.3%)[50.0%], bias   104(0.84), saved:     0, total:  0.09%
  172:   125(44.6%)[50.4%], bias   101(0.81), saved:     0, total:  0.09%
  215:   108(38.8%)[43.5%], bias   103(0.95), saved:     2, total:  0.08%
215, 211: Embedding data: 248 in 139630
Bits embedded: 278, changed: 108(38.8%)[43.5%], bias: 103, tot: 140167, skip: 139889
Foiling statistics: corrections: 62, failed: 0, offset: 37.117647 +- 73.201675
Total bits changed: 211 (change 108 + bias 103)
Storing bitmap into data...
Writing output.jpg....
```
```
root@6e2cbf82ae3c:/data# outguess -r -k 123456 output.jpg output5.txt
Reading output.jpg....
Extracting usable bits:   139630 bits
Steg retrieve: seed: 215, len: 31
root@6e2cbf82ae3c:/data# cat output5.txt
This is a very secret message!
```

### stegano
[tutorial](https://stegano.readthedocs.io/en/latest/)
```
Hiding data:
$stegano-lsb hide --input [input.jpg] -f [secret_file] -e UTF-8 --output [output.png]
Retiring data:
$stegano-lsb reveal -i [input.png] -e UTF-8 -o [output.txt]
```
```
root@6e2cbf82ae3c:/data# stegano-lsb hide --input ORIGINAL.jpg -f flag.txt -e UTF-8 --output output.png
root@6e2cbf82ae3c:/data# stegano-lsb reveal -i output.png -e UTF-8 -o output6.txt
root@6e2cbf82ae3c:/data# cat output6.txt
This is a very secret message!
```

### Steghide
```
Hiding data:
$steghide embed -ef [secret_file] -cf [input.jpg] -p <password> -sf [output.jpg]
Retiring data:
$steghide extract -sf [input.jpg] -p <password>
```
```
root@6e2cbf82ae3c:/data# steghide embed -ef flag.txt -cf ORIGINAL.jpg -p 123456 -sf output.jpg
embedding "flag.txt" in "ORIGINAL.jpg"... done
the file "output.jpg" does already exist. overwrite ? (y/n) y
writing stego file "output.jpg"... done
root@6e2cbf82ae3c:/data# steghide extract -sf output.jpg -p 123456
the file "flag.txt" does already exist. overwrite ? (y/n) y
steghide: could not open the file "flag.txt".
root@6e2cbf82ae3c:/data# 
root@6e2cbf82ae3c:/data# cat flag.txt
This is a very secret message!
```

### cloackedpixel
```
Hiding data:
$cloackedpixel hide [input.jpg] [secret_file] <password>
Retiring data:
$cloackedpixel extract [input-stego.png] [output.txt] <password>
```
```
root@6e2cbf82ae3c:/data# cloackedpixel hide ORIGINAL.jpg flag.txt 123456
[*] Input image size: 1280x959 pixels.
[*] Usable payload size: 449.53 KB.
[+] Payload size: 0.030 KB 
[+] Encrypted payload size: 0.051 KB 
[+] flag.txt embedded successfully!
output file is: ORIGINAL.jpg-stego.png
root@6e2cbf82ae3c:/data# cloackedpixel extract  ORIGINAL.jpg-stego.png  output7.txt 123456
[+] Image size: 1280x959 pixels.
[+] Written extracted data to output7.txt.
root@6e2cbf82ae3c:/data# cat output7.txt
This is a very secret message!
```

### LSBSteg
Lỗi khi cài đặt bằng docker. Cài thủ công tại [đây](https://github.com/RobinDavid/LSB-Steganography)
```
Hiding data:
$LSBSteg encode -i [input.png] -o [output.png] -f [secret.txt]
Retiring data:
$LSBSteg decode -i [input.png] -o [output.txt]
```
```
lỗi =))), dù cài docker hay thủ công vẫn lỗi. next ->
```
### f5
```
Hiding data:
$f5 -t e -i [input.jpg] -o [output.jpg] -d 'secret_message'
Retiring data:
$f5 -t x -i [input.jpg]
```

```
root@6e2cbf82ae3c:/data# f5 -t e -i ORIGINAL.jpg -o output.jpg -d 'UITNO1'
the output file exists, do you really want to override it?
y/n: y
2022-07-13 19:47:09,850 [jpeg_encoder] DCT/quantisation starts
2022-07-13 19:47:09,850 [jpeg_encoder] 1280 x 959
2022-07-13 19:47:13,818 [jpeg_encoder] got 1843200 DCT AC/DC coefficients
2022-07-13 19:47:14,124 [jpeg_encoder] one=76375
2022-07-13 19:47:14,124 [jpeg_encoder] large=90989
2022-07-13 19:47:14,124 [jpeg_encoder] expected capacity: 128412 bits
2022-07-13 19:47:14,124 [jpeg_encoder] expected capacity with
2022-07-13 19:47:14,125 [jpeg_encoder] default code: 16051 bytes (efficiency: 1.5 bits per change)
2022-07-13 19:47:14,125 [jpeg_encoder] (1, 3, 2) code: 10701 bytes (efficiency: 1.8 bits per change)
2022-07-13 19:47:14,125 [jpeg_encoder] (1, 7, 3) code: 6878 bytes (efficiency: 2.2 bits per change)
2022-07-13 19:47:14,125 [jpeg_encoder] (1, 15, 4) code: 4278 bytes (efficiency: 2.7 bits per change)
2022-07-13 19:47:14,125 [jpeg_encoder] (1, 31, 5) code: 2588 bytes (efficiency: 3.2 bits per change)
2022-07-13 19:47:14,125 [jpeg_encoder] (1, 63, 6) code: 1527 bytes (efficiency: 3.8 bits per change)
2022-07-13 19:47:14,125 [jpeg_encoder] (1, 127, 7) code: 873 bytes (efficiency: 4.3 bits per change)
2022-07-13 19:47:14,126 [jpeg_encoder] permutation starts
2022-07-13 19:47:24,366 [jpeg_encoder] Embedding of 80 bits (6+4 bytes)
2022-07-13 19:47:24,366 [jpeg_encoder] using (1, 63, 6) code
2022-07-13 19:47:24,429 [jpeg_encoder] 43 coefficients examined
2022-07-13 19:47:24,430 [jpeg_encoder] 40 coefficients changed (efficiency: 2.0 bits per change
2022-07-13 19:47:24,430 [jpeg_encoder] 20 coefficients thrown (zeroed)
2022-07-13 19:47:24,430 [jpeg_encoder] 80 bits (10 bytes) embedded
2022-07-13 19:47:24,430 [jpeg_encoder] starting hufman encoding

root@6e2cbf82ae3c:/data# f5 -t x -i output.jpg
2022-07-13 19:47:51,672 [jpeg_decoder] huffman decoding starts
2022-07-13 19:47:54,456 [jpeg_decoder] permutation starts
2022-07-13 19:48:03,629 [jpeg_decoder] 1843200 indices shuffled
2022-07-13 19:48:03,629 [jpeg_decoder] extraction starts
2022-07-13 19:48:03,629 [jpeg_decoder] length of embedded file: 6 bytes
2022-07-13 19:48:03,630 [jpeg_decoder] (1, 63, 6) code used
UITNO1
```

### stegpy
```
Hidingg data:
$stegpy [secret_file] [input.png]
Retiring data:
$stegpy [_input.png]
```

```
root@6e2cbf82ae3c:/data# stegpy flag.txt ORIGINAL.png
Host dimension: 3,682,560 bytes
Message size: 50 bytes
Maximum size: 920,640 bytes
Ok.
Information encoded in _ORIGINAL.png.

root@6e2cbf82ae3c:/data# stegpy _ORIGINAL.png 
File _flag.txt succesfully extracted from _ORIGINAL.png

```

## Steganography GUI tools

**Để chạy GUI tools cần:**

![image](https://user-images.githubusercontent.com/80806913/178820936-7d98c9cf-16fd-40f7-9f41-1318b744a89a.png)

```
$ sudp ./bin/run.sh
$ sudo ./scripts/start_ssh.sh                                                                                                                                       

root@28b834d1450f:/data# ./start_ssh.sh 
Changing root password to e1c42f53562c072e1bcf05e2
Starting ssh server
[ ok ] Starting OpenBSD Secure Shell server: sshd.


-------------------------------------------------
------------------ SSH started ------------------
-------------------------------------------------

SSH server started and ready for X11 forwarding:
        => connect via 'ssh -X -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no root@localhost'
        => Password is: 'e1c42f53562c072e1bcf05e2'
```
```
$ ssh -X -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no root@localhost
Warning: Permanently added 'localhost' (ED25519) to the list of known hosts.
root@localhost's password: 
Linux 28b834d1450f 5.16.0-kali7-amd64 #1 SMP PREEMPT Debian 5.16.18-1kali1 (2022-04-01) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
/usr/bin/xauth:  file /root/.Xauthority does not exist
root@28b834d1450f:~#
```
**chạy tool thôi**

### Steg
```
$steg
```

![image](https://user-images.githubusercontent.com/80806913/178917393-fce8a410-0008-42d8-8a10-c3bda03c6ca6.png)

### steganabara
```
$steganabara
```

![image](https://user-images.githubusercontent.com/80806913/178919007-fb842b41-9828-4ea5-99fe-6faf4006d96d.png)

### Stegsolve
```
$stegsolve
```

![image](https://user-images.githubusercontent.com/80806913/178919461-84b20aa8-dd04-47ee-ba7e-38cfee0d4280.png)

### SonicVisualiser
```
$sonic-visualiser
```

![image](https://user-images.githubusercontent.com/80806913/178920346-42af690e-b4fe-4ba5-b798-df56bb54ec8f.png)

### Stegosuite
```
$stegosuite
```

![image](https://user-images.githubusercontent.com/80806913/178920574-8b8e62a7-bb9a-4e10-9a6c-0d064300b418.png)

### OpenPuff
```
$openpuff
```

![image](https://user-images.githubusercontent.com/80806913/178920651-8cf8e98d-0e6b-4de3-9e0b-7bd88eab2f7c.png)

### DeepSound

DeepSound cần .NET framework 4.0, tải ở [đây](https://deepsound.en.uptodown.com/windows). Cài đặt và chạy

![image](https://user-images.githubusercontent.com/80806913/178921170-b47d8de6-a57e-437a-b8d3-c515942ea0d9.png)

### cloackedpixel-analyse
```
$cloackedpixel-analyse image.png
```

**END**













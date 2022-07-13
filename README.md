# Forensic-Tools-setup-and-useage-

[stego-toolkit(github)](https://github.com/DominicBreuker/stego-toolkit)

Để cài được bộ tool này trước hết cần có docker. Link cài đặt docker: [đây](https://docs.docker.com/engine/install/debian/)

Sau khi cài xong docker thì clone respo về, tại thư mục clone ta làm theo hướng dẫn của tác giả:

![image](https://user-images.githubusercontent.com/80806913/178795466-8b6284bf-b068-474f-ad34-fe5fd87a821c.png)

```
$sudo ./bin/build.sh

$sudo ./bin/run.sh
```

Bộ tool sẽ thao tác với các file trong thư mục data, khi cài xong data rỗng nên cần đưa file cần thao tác vào. Mình copy các file từ Examples qua thư mục Data

![image](https://user-images.githubusercontent.com/80806913/178796089-5f10e51b-8731-4ea0-8c8b-0bfeaa0d693b.png)

Bắt đầu sử dụng thôi:

## General screening tools

|Tool          |Description       |How to use     |
|--------------|------------------|---------------|
| file         | Kiểm tra loại file | `file ORIGINAL.jpg` |
| exiftool     | kiểm tra metadata của file | `exiftool ORIGINAL.jpg` |
| binwalk      | Kiểm tra có dữ liệu bị nhúng hay nén bên trong file hay không | `binwalk ORIGINAL.jpg`
| strings      | Đọc tất cả ký tự của file | `strings ORIGINAL.jpg`
| foremost     | Khắc phục các tệp bị nhúng trong file | `foremost ORIGINAL.jpg`
| pngcheck     | Kiểm tra file png có bị lỗi hay không | `pngcheck ORIGINAL.jpg`
| identify     | [GraphicMagick](http://www.graphicsmagick.org/) kiểm tra loại file và kiểm tra file có bị hỏng hay không | `identify -verbose ORIGINAL.jpg`
| ffmpeg       | ffmpeg có thể được sử dụng để kiểm tra tính toàn vẹn của các tệp âm thanh và cho phép nó báo cáo thông tin và lỗi | `ffmpeg -v info -i ORIGINAL.mp3 -f null -` to recode the file and throw away the result

## Tools detecting steganography

|Tool          |File types                |Description       |How to use - Demo|
|--------------|--------------------------|------------------|-----------------|
| [stegoVeritas](https://github.com/bannsec/stegoVeritas) | Images (JPG, PNG, GIF, TIFF, BMP) | A wide variety of simple and advanced checks. Check out `stegoveritas.py -h`. Checks metadata, creates many transformed images and saves them to a directory, Brute forces LSB, ... |[demo]()|
| [zsteg](https://github.com/zed-0xff/zsteg) | Images (PNG, BMP) | Detects various LSB stego, also openstego and the [Camouflage tool](http://camouflage.unfiction.com/) |[demo]()|
| [stegdetect](http://old-releases.ubuntu.com/ubuntu/pool/universe/s/stegdetect) | Images (JPG) | Performs statistical tests to find if a stego tool was used (jsteg, outguess, jphide, ...). Check out `man stegdetect` for details. |[demo]()|
| [stegbreak](https://linux.die.net/man/1/stegbreak) | Images (JPG) | Brute force cracker for JPG images. Claims it can crack `outguess`, `jphide` and `jsteg`. | [demo]()|

##  Tools actually doing steganography

|Tool          |File types                |Description       |How to use- Demo|
|--------------|--------------------------|------------------|----------------|
| [AudioStego](https://github.com/danielcardeenas/AudioStego) | Audio (MP3 / WAV) | Details on how it works are in this [blog post](https://danielcardeenas.github.io/audiostego.html) |[demo]()| 
| [jphide/jpseek](http://linux01.gwdg.de/~alatham/stego.html) | Image (JPG) | Pretty old tool from [here](http://linux01.gwdg.de/~alatham/stego.html). Here, the version from [here](https://github.com/mmayfield1/SSAK) is installed since the original one crashed all the time. It prompts for a passphrase interactively! | [demo]()|
| [jsteg](https://github.com/lukechampine/jsteg) | Image (JPG) | LSB stego tool. Does not encrypt the message. |[demo]()|
| [mp3stego](http://www.petitcolas.net/steganography/mp3stego/) | Audio (MP3) | Old program. Encrypts and then hides a message (3DES encryption!). Windows tool running in Wine. Requires WAV input (may throw errors for certain WAV files. what works for me is e.g.: `ffmpeg -i audio.mp3 -flags bitexact audio.wav`). Important: use absolute path only! |[demo]() |
| [openstego](https://github.com/syvaidya/openstego) | Images (PNG) | Various LSB stego algorithms (check out this [blog](http://syvaidya.blogspot.de/)). Still maintained. |[demo]() | 
| [outguess](https://packages.debian.org/sid/utils/outguess) | Images (JPG) | Uses "redundant bits" to hide data. Comes in two versions: old=`outguess-0.13` taken from [here](https://github.com/mmayfield1/SSAK) and new=`outguess` from the package repos. To recover, you must use the one used for hiding. |[demo]()|
| [spectrology](https://github.com/solusipse/spectrology) | Audio (WAV) | Encodes an image in the spectrogram of an audio file. | `TODO` | Use GUI tool `sonic-visualiser` |
| [stegano](https://github.com/cedricbonhomme/Stegano) | Images (PNG) | Hides data with various (LSB-based) methods. Provides also some screening tools. | `stegano-lsb hide --input cover.jpg -f secret.txt -e UTF-8 --output stego.png` or `stegano-red hide --input cover.png -m "secret msg" --output stego.png` or `stegano-lsb-set hide --input cover.png -f secret.txt -e UTF-8 -g $GENERATOR --output stego.png` for various generators (`stegano-lsb-set list-generators`) | `stegano-lsb reveal -i stego.png -e UTF-8 -o output.txt` or `stegano-red reveal -i stego.png` or `stegano-lsb-set reveal -i stego.png -e UTF-8 -g $GENERATOR -o output.txt`
| [Steghide](http://steghide.sourceforge.net/) | Images (JPG, BMP) and Audio (WAV, AU) | Versatile and mature tool to encrypt and hide data. | `steghide embed -f -ef secret.txt -cf cover.jpg -p password -sf stego.jpg` | `steghide extract -sf stego.jpg -p password -xf output.txt`
| [cloackedpixel](https://github.com/livz/cloacked-pixel) | Images (PNG) | LSB stego tool for images | `cloackedpixel hide cover.jpg secret.txt password` creates `cover.jpg-stego.png` | `cloackedpixel extract cover.jpg-stego.png output.txt password`
| [LSBSteg](https://github.com/RobinDavid/LSB-Steganography) | Images (PNG, BMP, ...) in uncompressed formats | Simple LSB tools with very nice and readable Python code | `LSBSteg encode -i cover.png -o stego.png -f secret.txt` | `LSBSteg decode -i stego.png -o output.txt` |
| [f5](https://github.com/jackfengji/f5-steganography) | Images (JPG) | F5 Steganographic Algorithm with detailed info on the process | `f5 -t e -i cover.jpg -o stego.jpg -d 'secret message'` | `f5 -t x -i stego.jpg 1> output.txt` |
| [stegpy](https://github.com/dhsdshdhk/stegpy) | Images (PNG, GIF, BMP, WebP) and Audio (WAV) | Simple steganography program based on the LSB method | `stegpy secret.jpg cover.png` | `stegpy _cover.png` |


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

## [Tools detecting steganography](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#tools-detecting-steganography)

|Tool          |File types                |Description       |How to use - Demo  |
|--------------|--------------------------|------------------|-------------------|
| [stegoVeritas](https://github.com/bannsec/stegoVeritas) | Images (JPG, PNG, GIF, TIFF, BMP) | A wide variety of simple and advanced checks. Check out `stegoveritas.py -h`. Checks metadata, creates many transformed images and saves them to a directory, Brute forces LSB, ... |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegoveritas)|
| [zsteg](https://github.com/zed-0xff/zsteg) | Images (PNG, BMP) | Detects various LSB stego, also openstego and the [Camouflage tool](http://camouflage.unfiction.com/) |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#zsteg)|
| [stegdetect](http://old-releases.ubuntu.com/ubuntu/pool/universe/s/stegdetect) | Images (JPG) | Performs statistical tests to find if a stego tool was used (jsteg, outguess, jphide, ...). Check out `man stegdetect` for details. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegdetect)|
| [stegbreak](https://linux.die.net/man/1/stegbreak) | Images (JPG) | Brute force cracker for JPG images. Claims it can crack `outguess`, `jphide` and `jsteg`. | [demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegbreak)|

##  [Tools actually doing steganography](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#tools-actually-doing-steganography)

|Tool          |File types                |Description       |How to use- Demo  |
|--------------|--------------------------|------------------|------------------|
| [AudioStego](https://github.com/danielcardeenas/AudioStego) | Audio (MP3 / WAV) | Details on how it works are in this [blog post](https://danielcardeenas.github.io/audiostego.html) |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#audiostego)| 
| [jphide/jpseek](http://linux01.gwdg.de/~alatham/stego.html) | Image (JPG) | Pretty old tool from [here](http://linux01.gwdg.de/~alatham/stego.html). Here, the version from [here](https://github.com/mmayfield1/SSAK) is installed since the original one crashed all the time. It prompts for a passphrase interactively! | [demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#jphidejpseek)|
| [jsteg](https://github.com/lukechampine/jsteg) | Image (JPG) | LSB stego tool. Does not encrypt the message. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#jsteg)|
| [mp3stego](http://www.petitcolas.net/steganography/mp3stego/) | Audio (MP3) | Old program. Encrypts and then hides a message (3DES encryption!). Windows tool running in Wine. Requires WAV input (may throw errors for certain WAV files. what works for me is e.g.: `ffmpeg -i audio.mp3 -flags bitexact audio.wav`). Important: use absolute path only! |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#mp3stego) |
| [openstego](https://github.com/syvaidya/openstego) | Images (PNG) | Various LSB stego algorithms (check out this [blog](http://syvaidya.blogspot.de/)). Still maintained. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#openstego) | 
| [outguess](https://packages.debian.org/sid/utils/outguess) | Images (JPG) | Uses "redundant bits" to hide data. Comes in two versions: old=`outguess-0.13` taken from [here](https://github.com/mmayfield1/SSAK) and new=`outguess` from the package repos. To recover, you must use the one used for hiding. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#outguess)|
| [stegano](https://github.com/cedricbonhomme/Stegano) | Images (PNG) | Hides data with various (LSB-based) methods. Provides also some screening tools. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegano)|
| [Steghide](http://steghide.sourceforge.net/) | Images (JPG, BMP) and Audio (WAV, AU) | Versatile and mature tool to encrypt and hide data. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#steghide)|
| [cloackedpixel](https://github.com/livz/cloacked-pixel) | Images (PNG) | LSB stego tool for images |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#cloackedpixel)|
| [LSBSteg](https://github.com/RobinDavid/LSB-Steganography) | Images (PNG, BMP, ...) in uncompressed formats | Simple LSB tools with very nice and readable Python code |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#lsbsteg)|
| [f5](https://github.com/jackfengji/f5-steganography) | Images (JPG) | F5 Steganographic Algorithm with detailed info on the process |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#f5)|
| [stegpy](https://github.com/dhsdshdhk/stegpy) | Images (PNG, GIF, BMP, WebP) and Audio (WAV) | Simple steganography program based on the LSB method |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegpy)|

## [Steganography GUI tools](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#steganography-gui-tools)

|Tool          |File types                |Description       |How to start    |
|--------------|--------------------------|------------------|----------------|
| [Steg](http://www.fabionet.org/) | Images (JPG, TIFF, PNG, BMP) | Handles many file types and implements different methods |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#steg) |
| [Steganabara](http://www.caesum.com/handbook/stego.htm) (The [original link](http://www.freewebs.com/quangntenemy/steganabara/index.html) is broken) | Images (???) | Interactively transform images until you find something |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#steganabara)|
| [Stegsolve](http://www.caesum.com/handbook/stego.htm) | Images (???) | Interactively transform images, view color schemes separately, ... |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegsolve) |
| [SonicVisualiser](http://www.sonicvisualiser.org/) | Audio (???) | Visualizing audio files in waveform, display spectrograms, ... | [demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#sonicvisualiser) |
| [Stegosuite](https://stegosuite.org/) | Images (JPG, GIF, BMP) | Can encrypt and hide data in images. Actively developed. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#stegosuite)|
| [OpenPuff](http://embeddedsw.net/OpenPuff_Steganography_Home.html) | Images, Audio, Video (many formats) | Sophisticated tool with long history. Still maintained. Windows tool running in wine. |[demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#openpuff)|
| [DeepSound](http://jpinsoft.net/deepsound) | Audio (MP3, WAV) | Audio stego tool trusted by Mr. Robot himself. Windows tool running in wine (very hacky, requires VNC and runs in virtual desktop, MP3 broken due to missing DLL!) | [demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#deepsound) |
| [cloackedpixel-analyse](https://github.com/livz/cloacked-pixel) | Images (PNG) | LSB stego visualization for PNGs - use it to detect suspiciously random LSB values in images (values close to 0.5 may indicate encrypted data is embedded) | [demo](https://github.com/plue0709/Forensic-Tools-setup-and-useage-/blob/main/How-to-use-and-demo.md#deepsound) |

# Còn chần chờ gì mà không cho một sao đi [cho một sao :)](https://github.com/plue0709/Forensic-Tools-setup-and-useage-)


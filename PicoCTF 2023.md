![[Pasted image 20230318074803.png]]

## Safeopener.class

visit decompiler.com and upload the class file. 

![[Pasted image 20230318090156.png]]

Key is visible in the code.

![[Pasted image 20230318092359.png]]



![[Pasted image 20230318092600.png]]


![[Pasted image 20230318092657.png]]

![[Pasted image 20230318092845.png]]

![[Pasted image 20230318092924.png]]

![[Pasted image 20230318122711.png]]

![[Pasted image 20230328194407.png]]


![[Pasted image 20230329161349.png]]
Eyeballing the pcap file shows this frame. Looks like base64 encoding. 
Base64decode website to help out..
VGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=
This is the secret: picoCTF{R34DING_LOKd_
There is a mention of the flag being split and there is no other interesting frame here. This may be the password to unlock the rar file....
And.. voila!
picoCTF{R34DING_LOKd_fil56_succ3ss_5ed3a878}

Timer

Decompile the apk file at javadecompilers.com.
Download the source files and unzip them.
Way too many files to search, just search for the text 'pico'. 
And voila! The flag sticks out in the AndroidManifest.xml file.
picoCTF{t1m3r_r3v3rs3d_succ355fully_17496}

Eyeball the packets. Not too many and you hit this gem:

0000   45 00 00 52 00 01 00 00 40 06 c3 90 ac 10 00 02   E..R....@.......
0010   0a fd 00 06 00 14 00 15 00 00 00 00 00 00 00 00   ................
0020   50 02 20 00 8b 73 00 00 70 69 63 6f 43 54 46 7b   P. ..s..picoCTF{
0030   50 36 34 50 5f 34 4e 34 4c 37 53 31 53 5f 53 55   P64P_4N4L7S1S_SU
0040   35 35 33 35 35 46 55 4c 5f 35 62 36 61 36 30 36   55355FUL_5b6a606
0050   31 7d                                             1}

picoCTF{P64P_4N4L7S1S_SU55355FUL_5b6a6061}

That also happens to be the first tcp packet if you are smarter and know how to filter stuff.

ret
load in IDA

![[Pasted image 20230329163027.png]]

observe flag
picoCTF{3lf_r3v3r5ing_succe55ful_9ae85289}

picoCTF{Hiddinng_An_imag3_within_@n_ima9e_7931435f}
picoCTF{Hiddinng_An_imag3_within_@n_image_dc2ab58f}
binwalk -e twice
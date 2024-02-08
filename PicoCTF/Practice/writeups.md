## Obedient Cat
Download flag.
Open flag file with Notepad

## Mod 26
Flag is in ROT13
Use rot13.com to decode text and get flag.

## Python wrangling
Download the python file and run it.
python ende.py 
Usage: ende.py (-e/-d) [file]

python ende.py -h    
Usage: ende.py (-e/-d) [file]
Examples:
  To decrypt a file named 'pole.txt', do: '$ python ende.py -d pole.txt'

python ende.py -d flag.txt.en 
Please enter the password: password from password file

## Wave a flag
Download the file called warm.
Run cat file. Loos like a program. Maybe can run it.
chmod u+x warm.
./warm
Hello user! Pass me a -h to learn what I can do!
./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_f0668f62}

## information
Download cat.jpg
Run on the file:
	file
	binwalk
	strings
Nothing interesting
Open the file. Picture of a cat and some code in the back. Nada.
Right-click and Properties. Nothing of interest.
Use HxD on the file.
Two pieces of strings stand out:
cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
W5M0MpCehiHzreSzNTczkc9d
Decode from base64: https://www.base64decode.org/
picoCTF{the_m3tadata_1s_modified}
[42!573]

## Nice netcat
Run on picoCTF webshell:
nc mercury.picoctf.net 21135

> [!INFO]- Result
> 112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
97 
102 
100 
53 
102 
100 
97 
52 
125 
10 

Took a guess and it turns out the number is ASCII for p.
So the flag is in ASCII encoding.

Nice awk script to the rescue here, prints the number to text...
nc mercury.picoctf.net 21135 | awk '{ printf("%c",$0); }'


## Transformation
#ReverseEngineering
Download enc file.
binwalk, file and strings yields nothing of interest.
>[!python code]
flag='picoCTF{b1scu1ts_4nd_gr4vy_f0668f62}'
print (flag)
print (len(flag))
enc=''
''''let's see what the piece of code in the question does. '''
for i in range(0,len(flag),2):
    print (i)
    a= ((''.join(chr((ord(flag[i]) << 8) + ord(flag[i + 1])))))
    print(a)
    enc=enc+a
    print(enc)
'''this is the encoded flag:'''
'''灩捯䍔䙻戱獣由瑳弴湤彧爴癹彦〶㘸昶㉽'''
'''looks like two alphabets are combined into one. reverse the process here and we might end up with p and i out of the first character.'''
enc='灩'
print (enc)
print (ord(enc))
print (ord('p') << 8)
print (chr(28777 >> 8))
print(ord(enc)-(ord('p')<<8))
print(chr(105))
'''some more working to make sure I am on the right track.'''
o=ord(enc)
d=chr(o >> 8)
print(d)
diff=ord(d)<<8
print(chr(o-diff))
'''flag to decode: 灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彤㔲挶戹㍽'''
enc='灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彤㔲挶戹㍽'
dec=''
for i in range(len(enc)):
    o=ord(enc[i])
    d=chr(o >> 8)
    dec=dec+d
    diff=ord(d)<<8
    dec=dec+(chr(o-diff))
print (dec)


## Stonks
#BinaryExploitation
vuln.c uses scanf. Read up on exploits for printf and scanf.
%x prints the stack and gives us wonky output. 
Select 1 to buy stocks and use %x as input.
Input:
%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.
Output:
89763d0.804b000.80489c3.f7ee4d80.ffffffff.1.8974160.f7ef2110.f7ee4dc7.0.8975180.1.89763b0.89763d0.6f636970.7b465443.306c5f49.345f7435.6d5f6c6c.306d5f79.5f79336e.35386130.32356533.ff8f007d.f7f1faf8.f7ef2440.6cce0800.1.0.f7d81ce9.f7ef30c0.f7ee45c0.f7ee4000.ff8f5ff8.f7d7268d.f7ee45c0.8048eca.ff8f6004.0.f7f06f09.
Looks like hex.
Convert hex to text:
http://www.unit-conversion.info/texttools/hexadecimal/
Text:
�v=��H�?~������t~�~��p�u�v;�c�ocip{FTC0l_I4_t5m_ll0m_y_y3n58a025e3��}������$@l������0���E���@��_���&���E��H���@��o
Jumbled flag: ocip{FTC0l_I4_t5m_ll0m_y_y3n58a025e3��}
picoCTF{I_l05t_4ll_my_m0n3y_0a853e52}

## SafeOpener
#ReverseEngineering 
Reading the code shows that:
1. Password is being converted and then compared to cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz
2. Password entered is being converted to Base64.
Take 'cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz' and go to base64decode website.
It is decoded to:
pl3as3_l3t_m3_1nt0_th3_saf3

## ASCII Numbers
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x34 0x35 0x63 0x31 0x31 0x5f 0x6e 0x30 0x5f 0x71 0x75 0x33 0x35 0x37 0x31 0x30 0x6e 0x35 0x5f 0x31 0x6c 0x6c 0x5f 0x74 0x33 0x31 0x31 0x5f 0x79 0x33 0x5f 0x6e 0x30 0x5f 0x6c 0x31 0x33 0x35 0x5f 0x34 0x34 0x35 0x64 0x34 0x31 0x38 0x30 0x7d
https://onlinestringtools.com/convert-ascii-to-string
Site has tools to covert ascii to string. It has an option to convert hexadecimal ascii to string as well. 

## Picker 1
#ReverseEngineering 
When you type getRandomNumber you just get the number 4 as output.
Reading the code shows that typing the input just calls different methods.
Test this by putting in escoteric1 esoteric2.
Use win as input to get:
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x34 0x5f 0x64 0x31 0x34 0x6d 0x30 0x6e 0x64 0x5f 0x31 0x6e 0x5f 0x37 0x68 0x33 0x5f 0x72 0x30 0x75 0x67 0x68 0x5f 0x63 0x65 0x34 0x62 0x35 0x64 0x35 0x62 0x7d
Looks like ASCII hex.
Go to:
https://onlinestringtools.com/convert-ascii-to-string
Site has tools to covert ascii to string. It has an option to convert hexadecimal ascii to string as well. 
## Picker 2
#ReverseEngineering 
The hint asks us to use the input to run the commands within win function.
Using win as an input is no no. The program exits with invalid input message. Closer inspection shows eval command executes whatever we use as input. 
This website shows some examples of eval:
https://linuxhint.com/use-eval-and-exec-functions-in-python/

Check if we can execute other commands using the eval function:

>[!inputs]
>
>print("hello")
hello
'NoneType' object is not callable
>
>esoteric1,print(1)
1
'NoneType' object is not callable
>
>esoteric1(print("hello"))
hello
esoteric1() takes 0 positional arguments but 1 was given

Perhaps run another eval as an input to see if that works:

>[!inputs]
>esoteric1(eval('''print(3\*2)'''))
6
esoteric1() takes 0 positional arguments but 1 was given


Works! 
Reframe this command to read the file flag.txt and output the contents:

 >[!Solution]
 >esoteric1(eval('''print(flag.strip())''', {'flag': open('flag.txt', 'r').read()}))

Assumption was that the flag might need more work to get to the answer, but no! The flag was printed.

## Substitution 0
#cryptography
Download the file and this is the contents:

ZGSOCXPQUYHMILERVTBWNAFJDK 

Qctcnrel Mcptzlo ztebc, fuwq z ptzac zlo bwzwcmd zut, zlo gtenpqw ic wqc gccwmc
xtei z pmzbb szbc ul fqusq uw fzb clsmebco. Uw fzb z gcznwuxnm bsztzgzcnb, zlo, zw
wqzw wuic, nlhlefl we lzwntzmubwb—ex sentbc z ptczw rtukc ul z bsuclwuxus reulw
ex aucf. Wqctc fctc wfe tenlo gmzsh brewb lczt elc cjwtciuwd ex wqc gzsh, zlo z
melp elc lczt wqc ewqct. Wqc bszmcb fctc cjsccoulpmd qzto zlo pmebbd, fuwq zmm wqc
zrrcztzlsc ex gntlubqco pemo. Wqc fcupqw ex wqc ulbcsw fzb actd tcizthzgmc, zlo,
wzhulp zmm wqulpb ulwe selbuoctzwuel, U senmo qztomd gmzic Ynruwct xet qub eruluel
tcbrcswulp uw.

Wqc xmzp ub: ruseSWX{5NG5717N710L_3A0MN710L_357GX9XX}

Last line is the flag.
First line is the key.
ZG SO CX  PQ U Y   HM IL      ER   VT   BW   NA   FJ   DK
AB CD EF  GH  I  J    KL   MN  OP   QR  ST     UV   WX YZ

ruseSWX{5NG  5717N710L_    3A0MN710L_357GX9XX}
picoCTF{5UB   5717u710n_     3V0LU710N_357BF9FF}

picoCTF{5UB5717u710n_3V0LU710N_357BF9FF}

## Substitution 1
#cryptography 
This is the message

SYTe (eakdy tkd sjbyndr yar thjm) jdr j yobr kt skxbnyrd ersndzyo skxbryzyzkc. Skcyreyjcye jdr bdrercyrq gzya j ery kt sajhhrcmre gazsa yrey yarzd sdrjyzwzyo, yrsaczsjh (jcq mkkmhzcm) evzhhe, jcq bdklhrx-ekhwzcm jlzhzyo. Sajhhrcmre nenjhho skwrd j cnxlrd kt sjyrmkdzre, jcq garc ekhwrq, rjsa ozrhqe j eydzcm (sjhhrq j thjm) gazsa ze enlxzyyrq yk jc kchzcr eskdzcm erdwzsr. SYTe jdr j mdrjy gjo yk hrjdc j gzqr jddjo kt skxbnyrd ersndzyo evzhhe zc j ejtr, hrmjh rcwzdkcxrcy, jcq jdr akeyrq jcq bhjorq lo xjco ersndzyo mdknbe jdkncq yar gkdhq tkd tnc jcq bdjsyzsr. Tkd yaze bdklhrx, yar thjm ze: bzskSYT{TD3UN3CSO_4774SV5_4D3_S001_7JJ384LS}

yar thjm ze: <-- that sounds like 'the flag is:'
the flag is
bzskSYT
picoCTF

A B C D   
h

E F G
s

H
l



I J  
z a

K L 

M N O P
g

Q R 
   e
S 
T U V W 
h
X Y Z

## Who is it?
#forensics 
Download the eml file and load it in:
https://eml-analyzer.herokuapp.com/

The email is from lpage@onionmail.org

On the hops information there is this line:
mail.onionmail.org, 173.249.33.206

Put the ip address on whatismyip.com and a lot of information comes up.
Name of the company and all.
There is a name of a person as well.
That is the first name last name combo to use.



## Useless
Login using the ssh creds provided.
ssh picoplayer@saturn.picoctf.net -p63982
Followed by the password when prompted.
The script called useless just does basic arithmetic.
Cannot crash the script. The code has nothing except that it mentions the existence of a manual.
Running 'man useless' opens a manual. The flag is at the end of the manual.
## Picker 3
#ReverseEngineering 
==> 1
1: print_table
2: read_variable
3: write_variable
4: getRandomNumber
==> 4
4
==> 2
Please enter variable name to read: dummy_func1
<function dummy_func1 at 0x7fb709184af0>
==> 3
Please enter variable name to write: n
Please enter new value of variable: 0x7fb709184af0
==> 2
Please enter variable name to read: n
140424108329712
==> 3
Please enter variable name to write: n
Please enter new value of variable: dummy_func1
==> 2   
Please enter variable name to read: n
<function dummy_func1 at 0x7fb709184af0>
==> 3
Please enter variable name to write: getRandomNumber
Please enter new value of variable: dummy_func1()
Illegal value
==> 3
Please enter variable name to write: getRandomNumber
Please enter new value of variable: dummy_func1
==> 2
Please enter variable name to read: getRandomNumber
<function dummy_func1 at 0x7fb709184af0>
==> 4
in dummy_func1

You can change the table values. The functions can be renamed as variables to call other functions not in the initial table.

==> 1
1: print_table
2: read_variable
3: write_variable
4: getRandomNumber
==> 3
Please enter variable name to write: print_table
Please enter new value of variable: win
==> 1
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x37 0x68 0x31 0x35 0x5f 0x31 0x35 0x5f 0x77 0x68 0x34 0x37 0x5f 0x77 0x33 0x5f 0x67 0x33 0x37 0x5f 0x77 0x31 0x37 0x68 0x5f 0x75 0x35 0x33 0x72 0x35 0x5f 0x31 0x6e 0x5f 0x63 0x68 0x34 0x72 0x67 0x33 0x5f 0x32 0x32 0x36 0x64 0x64 0x32 0x38 0x35 0x7d 

The flag is in hex. Convert to chr.
https://www.rapidtables.com/convert/number/hex-to-ascii.html

## Picker 4
#BinaryExploitation 
There are two files:
picker-IV.c
picker-IV
Running the nc session in question shows that we are asked for an address in hex to jump to.

nc saturn.picoctf.net 63488 
Enter the address in hex to jump to, excluding '0x': 12345
You input 0x12345
Segfault triggered! Exiting.

Wrong addresses triggers segfault errors.

The c file mentions win method. The hint talks about searching for the address of win method.

The bin file has the addresses of the method perhaps.

I tried IDA to make sense of the bin file unsuccessfully. Have to learn more about this tool before I can use it maybe.

I found about Binary Ninja to read bin files. Binary Ninja has a free cloud offering.
cloud.binary.ninja

Uploading the bin file lets me make sense of it. Going through different tabs I find the win method in one of the tabs. Right-click on that method to see that there is an option to copy the address of the method.
![[Pasted image 20230808223104.png]]

Enter the address in hex to jump to, excluding '0x': 40129e
You input 0x40129e
You won!

That address is the answer.

## m00nwalk
#forensics 
You get a wav file.
Nothing in the file. Audacity software shows nothing in the file. Just static.
The hints mention:
How did pictures from the moon landing get sent back to Earth? Quick Google talks about something called SSTV. 
RX-SSTV can be used to decode this file.
The second hint, using Google, is Scottie. Scottie is the mascot of CMU.

Install RX-SSTV. 
Scottie is one of the RX options. I used Scottie 1.
Run the wav file in VLC player. Make sure your mic can pick up voices. Play the wav file on your speaker using VLC Player and you will get the image with the flag upside down.
![[Pasted image 20230812183654.png]]

## m00nwalk2
Three audio files contain clues to a flag in message.wav.
message.wav is same image from m00nwalk.
First audio file decodes to password: hidden_steganosaurus
Second to a popular quote in the community.
Third to something that is not clear. This is because all my images are blurry af. To be investigated later. TODO

> [!INFO]- Images
>![[Pasted image 20230812210842.png]]
>![[Pasted image 20230812211034.png]]
>![[Pasted image 20230812210956.png]]
 
Third one is Alan something the Future Boy. 
Had to turn to google. I even ended up with The Future Boy Conan.
I search for the future boy alan e. And I get to someone called Alan Eliasen whose website is futureboy.us.
He has a steganography tool called stegohide. 
Use that and the password to extract the flag from message.wav.

> [!INFO]- stegohide
 .\steghide.exe --extract -sf 'message.wav'
Enter passphrase:
wrote extracted data to "steganopayload12154.txt".

## Investigative Reversing 0
#forensics 
We have two files:
mystery
mystery.png

Opening mystery.png gives nothing.
binwalk and unzipping the file gives nothing. Unzipping just leads to another folder of myster.png with the same mystery.png file. TODO: How did they pull this off?
xxd mystery.png shows the flag at the end of the file. The flag is changed.

To focus on mystery, I run the file on its own and it whinges about flag.txt and mystery.png.
I create a flag file with an earlier flag and run the file. Mystery does its job. I xxd mystery.png and notice that the flag is added to the end of the png file after some changes.

![[Pasted image 20230817123418.png]]

Mystery takes the flag from flag.txt, modifies it and appends to mystery.png.

To take a closer look at mystery, from the three tools at my disposal:
online binja
ida pro
ghidra

Ghidra looks cleanest. I use that to figure out what is happening.
I look at the main method. Looks like C code.

```c
void main(void)
{
  FILE *__stream;
  FILE *__stream_00;
  size_t sVar1;
  long in_FS_OFFSET;
  int local_54;
  int local_50;
  char local_38 [4];
  char local_34;
  char local_33;
  char local_29;
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  __stream = fopen("flag.txt","r");
  __stream_00 = fopen("mystery.png","a");
  if (__stream == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (__stream_00 == (FILE *)0x0) {
    puts("mystery.png is missing, please run this on the server");
  }
  sVar1 = fread(local_38,0x1a,1,__stream);
  if ((int)sVar1 < 1) {
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  puts("at insert");
  fputc((int)local_38[0],__stream_00);
  fputc((int)local_38[1],__stream_00);
  fputc((int)local_38[2],__stream_00);
  fputc((int)local_38[3],__stream_00);
  fputc((int)local_34,__stream_00);
  fputc((int)local_33,__stream_00);
  for (local_54 = 6; local_54 < 0xf; local_54 = local_54 + 1) {
    fputc((int)(char)(local_38[local_54] + '\x05'),__stream_00);
  }
  fputc((int)(char)(local_29 + -3),__stream_00);
  for (local_50 = 0x10; local_50 < 0x1a; local_50 = local_50 + 1) {
    fputc((int)local_38[local_50],__stream_00);
  }
  fclose(__stream_00);
  fclose(__stream);
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
```
Of particular interest are the lines after puts("at insert").
fputc is to write something to a file.
```c
fputc((int)local_38[0],__stream_00);  //p
fputc((int)local_38[1],__stream_00);  //i
fputc((int)local_38[2],__stream_00);  //c
fputc((int)local_38[3],__stream_00);  //o
fputc((int)local_34,__stream_00); //C
fputc((int)local_33,__stream_00); //T
```
These lines put in picoCT
Our damaged flag is:
picoCTK.k5zsid6q_d1deedaa}

Flag is 26 characters long

The damaged portion:
K.k5zsid6q

Damaged portion is 10 characters long.

The rest of the flag is:
\_d1deedaa}

Looking at the c code:
```c
  for (local_54 = 6; local_54 < 0xf; local_54 = local_54 + 1) {
    fputc((int)(char)(local_38[local_54] + '\x05'),__stream_00);
  }
```
0xf is 15 in decimal.
Positions 6-14 are being changed by adding '\x05'.
We can subtract '\x05' from these positions to retrieve this portion.
From 6 to 15 is 9 characters.

For the 10th character:
```c
fputc((int)(char)(local_29 + -3),__stream_00);
```
Subtracting 3 from the flag character to damage the flag.
We can add 3 to the damaged character to get the flag.

Finally this piece of code puts in the rest of the flag in the png file:
```c
for (local_50 = 0x10; local_50 < 0x1a; local_50 = local_50 + 1) {
    fputc((int)local_38[local_50],__stream_00);
  }
```

Some C code to test all this:
```c
#include <stdio.h>

int main() {
char local_38[] = "picoCTF{k5zsid6q_f6ad392b}";
int local_54;
puts(local_38);

//from character 6 to 15 this is done: picoCT is ok. F{ onwards
printf("changing: ");
for (local_54 = 6; local_54 < 0xf; local_54 = local_54 + 1) {
    //puts((int)(char)(local_38[local_54] + '\x05'));
    printf("%c",local_38[local_54]);
  }
 printf("\nto:\n");
for (local_54 = 6; local_54 < 0xf; local_54 = local_54 + 1) {
    //puts((int)(char)(local_38[local_54] + '\x05'));
    printf("%c",local_38[local_54]+ '\x05');
  }
int local_50;
printf("\n");
for (local_50 = 0x10; local_50 < 0x1a; local_50 = local_50 + 1)
{
    printf("%c",local_38[local_50]);
}

return 0;
}
//Output:
//picoCTF{k5zsid6q_f6ad392b}
//changing: F{k5zsid6
//to:
//K�p:xni;
//_f6ad392b}
//9 characters changed. Subtract 3 from the 10th to get the next damaged character.
```

I used this site to run the c program:
https://www.programiz.com/c-programming/online-compiler/
TODO

```c
// Online C compiler to run C program online

//picoCTK.k5zsid6q_d1deedaa}
//picoCTF{f0und1
//................_d1deedaa}
#include <stdio.h>

int main() {

char local_38[] = "picoCTF{k5zsid6q_f6ad392b}";
int local_54;


puts(local_38);

//from character 6 to 15 this is done: picoCT is ok. F{ onwards
printf("changing: ");
for (local_54 = 6; local_54 < 0xf; local_54 = local_54 + 1) {
    //puts((int)(char)(local_38[local_54] + '\x05'));
    printf("%c",local_38[local_54]);
  }
 printf("\nto:\n");
for (local_54 = 6; local_54 < 0xf; local_54 = local_54 + 1) {
    //puts((int)(char)(local_38[local_54] + '\x05'));
    printf("%c",local_38[local_54]+ '\x05');
  }
int local_50;
printf("\n");
for (local_50 = 0x10; local_50 < 0x1a; local_50 = local_50 + 1)
{
    printf("%c",local_38[local_50]);
    
}
// "picoCTK.k5zsid6q" is the broken flag.
//"d6q_d1deedaa}"
// we need to decode: K.k5zsi

//picoCTF{f0undF6q_d1deedaa}
//

    return 0;
}
```

## Investigative Reversing 1
#forensics 

xxd mystery.png
![[Pasted image 20230817154629.png]]

xxd mystery2.png
![[Pasted image 20230817154735.png]]

xxd mystery3.png
![[Pasted image 20230817154814.png]]

Looks like the flag is being broken into a two parts and put in two png files.

Will make a flag.txt file and test what this does.
flag.txt contains:
picoCTF{f0und_1t_d1deedaa}

xxd mystery.png
![[Pasted image 20230817155146.png]]

xxd mystery2.png
![[Pasted image 20230817155411.png]]

Reversing with Ghidra:
```c
void main(void)

{
  FILE *__stream;
  FILE *__stream_00;
  FILE *__stream_01;
  FILE *__stream_02;
  long in_FS_OFFSET;
  char local_6b;
  int local_68;
  int local_64;
  int local_60;
  char local_38 [4];//local_38 is 4 letters. Must be pico
  char local_34;
  char local_33;
  long local_10;
  //__stream is the flag
  //mystery contains CF{An1_69008b75}
  //mystery3 contains icT0Tha_
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  __stream = fopen("flag.txt","r");
  __stream_00 = fopen("mystery.png","a");
  __stream_01 = fopen("mystery2.png","a");
  __stream_02 = fopen("mystery3.png","a");
  if (__stream == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (__stream_00 == (FILE *)0x0) {
    puts("mystery.png is missing, please run this on the server");
  }
  fread(local_38,0x1a,1,__stream);
  fputc((int)local_38[1],__stream_02);//this puts i from pico in mystery3. Now remains cT0Tha_
  fputc((int)(char)(local_38[0] + '\x15'),__stream_01); //p + \x15 in mystery2
  fputc((int)local_38[2],__stream_02); //c in mystery3. Now remains T0Tha_
  local_6b = local_38[3]; //o is being assigned to local_6b
  fputc((int)local_33,__stream_02);
  fputc((int)local_34,__stream_00); //maybe C is in mystery now.
  for (local_68 = 6; local_68 < 10; local_68 = local_68 + 1) {//characters 6-9
    local_6b = local_6b + '\x01'; //local_6b is local_6b + \x01. that is something happens to o. but don't care.
    fputc((int)local_38[local_68],__stream_00);//6,7,8,9 being put in mystery. 
    //6-9 is F{An
    
  }
  fputc((int)local_6b,__stream_01); //don't care
  for (local_64 = 10; local_64 < 0xf; local_64 = local_64 + 1) { //characters 10-14
    fputc((int)local_38[local_64],__stream_02); //put the characters in mystery3 as is
    //icT0Tha_
    //flag part: 0Tha_
  }
  for (local_60 = 0xf; local_60 < 0x1a; local_60 = local_60 + 1) { //character 15-25
    fputc((int)local_38[local_60],__stream_00); //put the characters in mystery as is
	  //CF{An1_69008b75}
	  //flag part: 1_69008b75}
  }

  fclose(__stream_00);
  fclose(__stream);
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
//flag is picoCTF{An0Tha_1_69008b75}
```

## Investigative Reversing 2
#forensics 
Running mystery tells me that two files are required:
flag.txt
original.bmp

The bmp image file must have been overwritten. So time to focus on the mystery file first.
Reverse it...
```c
undefined8 main(void)

{
  size_t sVar1;
  long in_FS_OFFSET;
  char local_7e;
  char local_7d;
  int local_7c;
  int local_78;
  int local_74;
  int local_70;
  undefined4 local_6c;
  int local_68;
  int local_64;
  FILE *local_60;
  FILE *local_58;
  FILE *local_50;
  char local_48 [56];
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  local_6c = 0;
  local_60 = fopen("flag.txt","r");
  local_58 = fopen("original.bmp","r");
  local_50 = fopen("encoded.bmp","a");
  if (local_60 == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (local_58 == (FILE *)0x0) {
    puts("original.bmp is missing, please run this on the server");
  }
  sVar1 = fread(&local_7e,1,1,local_58); //READS THE original.bmp file
  local_7c = (int)sVar1;
  local_68 = 2000;
  for (local_78 = 0; local_78 < local_68; local_78 = local_78 + 1) {
    fputc((int)local_7e,local_50);
    sVar1 = fread(&local_7e,1,1,local_58);
    local_7c = (int)sVar1;
  }
  sVar1 = fread(local_48,0x32,1,local_60); //READS THE FLAG
  local_64 = (int)sVar1;
  if (local_64 < 1) {
    puts("flag is not 50 chars");
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  //flag is getting encoded here?
  for (local_74 = 0; local_74 < 0x32; local_74 = local_74 + 1) { //for each row
    for (local_70 = 0; local_70 < 8; local_70 = local_70 + 1) { //for each column
      local_7d = codedChar(local_70,(int)(char)(local_48[local_74] + -5),(int)local_7e);
      fputc((int)local_7d,local_50);//
      fread(&local_7e,1,1,local_58);
    }
  }
  while (local_7c == 1) {
    fputc((int)local_7e,local_50);
    sVar1 = fread(&local_7e,1,1,local_58);
    local_7c = (int)sVar1;
  }
  fclose(local_50);
  fclose(local_58);
  fclose(local_60);
  if (local_10 == *(long *)(in_FS_OFFSET + 0x28)) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
```

Haha.. clueless

xxd encoded.bmp | less
Looks like 0000s show up in patterns.. maybe there is something encoded?

I will try to view the image and load it in HxD to see what else in it. Lots of head scratching..

What is LSB encoding? Third hint!
The flag must be LSB encoded in the bmp file.

When you try to run the mystery file, there are three things you find out:
mystery requires two files: original.bmp and flag.txt
the flag is 50 characters

I run the mystery file after this and notice that some lines are added at the end of original.bmp to convert it to encoded.bmp.

Visual inspection of the original encoded.bmp and new encoded.bmp shows that the end of the file is the same. Scroll from the bottom and go up. The flag must be encoded somewhere in the middle.
From the code, line 2000 is where the action takes place.

quick script to get to the answer
source: https://github.com/HHousen/PicoCTF-2019/blob/24b0981c72638c12f9a8572f81e1abbcf8de306d/Forensics/Investigative%20Reversing%202/script.py

```python
from pwn import unbits

# open the image in "read binary" mode
with open("encoded.bmp", "rb") as data:
    data.seek(2000)
    bin_str = ""
    # loop through the `50 * 8` bytes after 2000.
    # each iteration gives one bit of the flag since one bit of the flag is stored in
    # each byte of the image. so multiply the 50 character flag by 8 bits in a byte to
    # loop through all the bits in the flag.
    for j in range(50 * 8):
        # `data.read(1)` is of type 'bytes' but `data.read(1)[0]` is of type 'int'.
        # file.read() returns a 'bytes' object, which is essentially a list of bytes. ("While bytes
        # literals and representations are based on ASCII text, bytes objects actually behave like
        # immutable sequences of integers." - https://docs.python.org/3/library/stdtypes.html#bytes)
        # since we only read 1 byte at a time, we can safely select the first one in the list.
        # int.from_bytes() can convert a list of bytes to an int and will also work in this case.
        # ord() can also convert a single byte to an int (https://docs.python.org/3/library/functions.html#ord)
        byte = data.read(1)[0]

        # the `&1` selects only the last bit (LSB) in the current byte. it is the bitwise AND operator.
        # see https://en.wikipedia.org/wiki/Bitwise_operation#AND for more information.
        bit = byte & 1
        bin_str += str(bit)

# pwn.unbits docs: https://docs.pwntools.com/en/stable/util/fiddling.html#pwnlib.util.fiddling.unbits
char_str = unbits(bin_str, endian='little')
print("Flag: " + "".join([chr(x + 5) for x in char_str]))
```

//TODO
Steganography tutorial
https://www.boiteaklou.fr/Steganography-Least-Significant-Bit.html
Revise this after the tutorial

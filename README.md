Hi People :D

This is a writeup for all forensics challenges that were in BlackHat MEA CTF 2023 Qualifications phase.

let’s go :D

![1 qhyvcEFCQr9wTBrimhzzEw](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/6510e2b9-0803-469a-a8a8-301d0be2b7e5)


[*] USB100 (easy — 50pts)

==============================

![1 CVkjKn3Le81cbbW2Xyn9-w](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/83175ce9-fb3d-4efa-9428-801b16e357a6)


The attachment file was a PCAP file (send.pcapng), so let’s open it in Wireshark and see what’s going on.

As mentioned in the description, we have some USB traffic.

![1 RQUSL8MZB69CKqMdkoeuRw](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/ca9da793-ed1e-4bcb-a156-a3fcfccd0a23)


This led me to search for a method to extract files from this data. During my research, I came across This Writeup from another CTF, which showed that the data could be located within the URB_BULK out packets.

I simply sorted the packets by length (because file packets are typically larger than other data packets). Most of the files turned out to be dummy images :/ (you can tell they were JPEG images because they had ‘JFIF’ magic bytes).


![1 WNOaMpApvCn8Yrnzu5jNeQ](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/f7614af5-d031-4a08-bb3e-26c2bf17459c)


To extract data, simply right-click on ‘Leftover Capture Data’, then choose ‘Export Packet Bytes’ and save it with the correct extension.

![1 qRS8vNgVFfBI1sPPYI-UsQ](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/243eaf9f-b279-42ad-8a26-ea426e0a4e1a)


Among all these images and other data, I found one packet that contained an executable file (again, you can know from the ‘MZ’ magic bytes).

![1 lzXMYPWKnPItG07zfBX6PQ](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/9ff9311b-63c3-47f3-920f-ea7363eab36f)

I simply extracted the data using the same method as above, saved the file as ‘bin.exe,’ ran it from the cmd and obtained the flag easily :)

![1 N-i0MvKIBijxH7u5vK-vcQ](https://github.com/NU1L0/BlackHat-MEA-CTF-2023/assets/68877702/bc4963eb-672f-480f-94bb-248ee6b5f296)


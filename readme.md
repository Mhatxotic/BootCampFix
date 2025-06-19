# iMac Mid-2011 MBR hack…

## What is it?
This is hack of the 440 byte Master Boot Record sector for the old `iMac Mid-2011` computer which will give a slight boost to I/O disk performance under Windows 7. I did not create this hack so I do not *exactly* what it does but I used it happily for many years with much increased SATA disk performance. Only what I do know is it changes Windows 7 to see the `Intel SATA AHCI Controller Driver` instead of a 'standard' more compatible one.

## Warning!!!
This is potentially a destructive operation. I only ever used this hack on a second mechanical hard disk drive that came built-in with the Mac which was completely formatted with NTFS with an MBR partition. I cannot recommend using this on your primary and only disk drive unless you know exactly what you are doing.

## Procedure…
It is better to have a fully working Windows 7 installation first with all the latest up-to-date drivers installed, then do the following proecdure using a Linux based LiveCD to do this too…

1. Set `Start` to `0` on these in the Windows registry to prevent a possible crash at startup...
   `HKLM\System\CurrentControlSet\Services\msahci`.
   `HKLM\System\CurrentControlSet\Services\Iastor`.
   `HKLM\System\CurrentControlSet\Services\IastorV`.

2. Save your old MBR with this command…
   `sudo dd if=/dev/disk1 of=bootcamp.old bs=440 count=1`.

3. Write your new MBR with this command…
   `sudo dd if=bootcamp.new of=/dev/disk1 bs=440 count=1`.

## Delta patch information…
```
VCDIFF version:               0
VCDIFF header size:           34
VCDIFF header indicator:      VCD_SECONDARY VCD_APPHEADER
VCDIFF secondary compressor:  lzma
VCDIFF application header:    bootcamp.new//bootcamp.old/
XDELTA filename (output):     bootcamp.new
XDELTA filename (source):     bootcamp.old
VCDIFF window number:         0
VCDIFF window indicator:      VCD_SOURCE VCD_ADLER32
VCDIFF adler32 checksum:      F55EB2D9
VCDIFF delta indicator:       VCD_DATACOMP VCD_INSTCOMP
VCDIFF copy window length:    437
VCDIFF copy window offset:    0
VCDIFF delta encoding length: 134
VCDIFF target window length:  440
VCDIFF data section length:   46
VCDIFF inst section length:   15
VCDIFF addr section length:   7
  Offset Code Type1 Size1  @Addr1 + Type2 Size2 @Addr2
  000000 019  CPY_0    226 S@0
  000226 004  ADD        3
  000229 019  CPY_0    126 S@229
  000355 001  ADD       21
  000376 040  CPY_1      8 T@358
  000384 009  ADD        8
  000392 036  CPY_1      4 T@363
  000396 012  ADD       11
  000407 067  CPY_3     30 S@407
  000437 004  ADD        3
```
## Diff…
```
15c15
< 000000e0: 00fb b800 bbcd 1a66 23c0 753b 6681 fb54  .......f#.u;f..T
---
> 000000e0: 00fb e97e 00cd 1a66 23c0 753b 6681 fb54  ...~...f#.u;f..T
23,26c23,26
< 00000160: 2402 c349 6e76 616c 6964 2070 6172 7469  $..Invalid parti
< 00000170: 7469 6f6e 2074 6162 6c65 0045 7272 6f72  tion table.Error
< 00000180: 206c 6f61 6469 6e67 206f 7065 7261 7469   loading operati
< 00000190: 6e67 2073 7973 7465 6d00 4d69 7373 696e  ng system.Missin
---
> 00000160: 2402 c366 b890 fa00 80ba f80c 66ef b860  $..f........f..`
> 00000170: 00ba fc0c ef66 b824 fa00 80ba f80c 66ef  .....f.$......f.
> 00000180: 66b8 0000 a08f bafc 0c66 efb8 00bb e954  f........f.....T
> 00000190: ff49 0045 004d 0065 6d00 4d69 7373 696e  .I.E.M.em.Missin
28c28
< 000001b0: 656d 0000 0063 7b9a                      em...c{.
---
> 000001b0: 656d 0000 0091 939a                      em......
```

## [Disclaimer](#disclaimer)…

**Always make backups!** This information is provided to the public *AS IS* with *NO* warranty given of any kind. By using this knowledge you disclaim the author all liability in the event that the reader mistakes or misuses any part of it for any reason that might result in any sort of negative consequence.

## That's all folks!

# mspdebug on Ubuntu Linux 14.04

## Installing

mspdebug is the free debugger to be used with Texas Instruments MSP430 Low Power Mocro Controllers, it can be found here:

http://mspdebug.sourceforge.net/

It is possible to use Ubuntu PPA to install `sudo apt-get install mspdebug`, this PPA is usually a revision behand.  To install latest revision, follow steps below:

1. Install the required USB library
```
sudo apt-get install libusb-dev
```
2. Download the archive from here http://sourceforge.net/projects/mspdebug/files.  
3. Uncompress and install:
```
cd ~/Download # find the location of the file
tar -zxvf mspdebug-0.23.tar.gz
cd mspdebug-0.23
sudo apt-get install libusb-dev
sudo make install
```
4. Add path the the binary and lib files
```
echo "export PATH=\$PATH:/usr/local/bin:/usr/local/lib" >> ~/.bashrc
```

## Using

mspdebug can be used with the following binary files types:

- ELF32
- COFF
- Intel HEX (program only)
- BSD symbol table (symbols only)
- TI Text (program only)
- SREC (program only)

The mspdebug will require the use of a usb port, if mspdebug command replies with an error that it cannot gain access to a port, execute `sudo mspdebug <options>`

To begin debuggin, change to the folder containing your binary file, the next step is emulator specific:

### Using MSP430-JTAG-ISO-MK2

The MSP430-JTAG-ISO-MK2 is by Olimex, https://www.olimex.com/Products/MSP430/JTAG/MSP430-JTAG-ISO-MK2/

```
$ mspdebug olimex-iso-mk2
MSPDebug version 0.23 - debugging tool for MSP430 MCUs
Copyright (C) 2009-2015 Daniel Beer <dlbeer@gmail.com>
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
Chip info database from MSP430.dll v3.3.1.4 Copyright (C) 2013 TI, Inc.

Olimex firmware version: 1312d07
Resetting Olimex command processor...
Initializing FET...
FET protocol version is 20000007
fet: FET returned error code 38 (External power detected)
warning: fet: set VCC failed
Configured for Spy-Bi-Wire
Sending reset...
Using Olimex identification procedure
Device ID: 0x2781                                                                                [0/1321]
  Code start address: 0x8000
  Code size         : 262144 byte = 256 kb
  RAM  start address: 0x1c00
  RAM  end   address: 0x63ff
  RAM  size         : 18432 byte = 18 kb
Device: MSP430F5335
Number of breakpoints: 8
Power profiling enabled: bufsize = 512 bytes, 55 us/sample
Chip ID data: 27 81 22
unknown command: color (try "help")
read: error processing /home/sporty/.mspdebug (line 1)

Available commands:
    !               fill            power           setwatch_r      
    =               gdb             prog            setwatch_w      
    alias           help            read            simio           
    blow_jtag_fuse  hexout          regs            step            
    break           isearch         reset           sym             
    cgraph          load            run             verify          
    delbreak        load_raw        save_raw        verify_raw      
    dis             md              set             
    erase           mw              setbreak        
    exit            opt             setwatch        

Available options:
    color                       gdb_default_port            
    enable_bsl_access           gdb_loop                    
    enable_fuse_blow            gdbc_xfer_size              
    enable_locked_flash_access  iradix                      
    fet_block_size              quiet                       

Type "help <topic>" for more information.
Use the "opt" command ("help opt") to set options.
Press Ctrl+D to quit.

```

To  program the micro controller:
```
prog mypro.obj
```

To run the code
```
run
```


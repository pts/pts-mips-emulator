pts-mips-emulator: MIPS I emulator in Perl 5 which can run Linux programs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
pts-mips-emulator is a platform-independent, proof-of-concept Perl 5 script
which can run Linux MIPS (MIPS R3000) ELF executables.

The code is a fork of the excellent
http://blog.schmorp.de/2015-07-04-emulating-linux-mips-in-perl-4.html . This
fork contains some bugfixes and usability improvements.

pts-mips-emulator is compatible with Perl 5 installations with both 32-bit
and 64-bit integer arithmetic. (It's faster on 64-bit, but it doesn't use
more memory.)

pts-mips-emulator has been tested and found working with:

* Perl 5.004_04 (i386, 32-bit integers, 1997-10-15)
* Perl 5.6.1 (i386, 32-bit integers, 2001-04-08)
* Perl 5.10.1 (i386, 32-bit integers, 2009-08-22)
* Perl 5.14.2 (i386, 64-bit integers, 2011-09-26)
* Perl 5.18.2 (amd64, 64-bit integers, 2014-01-06)
* Perl 5.24.1 (amd64, 64-bit integers, 2017-01-14)

using the following command lines:

  $ perl ./run dash.run -c 'echo $((6*7))'
  42
  $ perl ./run bash.run -c 'let ANSWER=6*7; echo $ANSWER'
  42
  $ perl ./run bash.run --version | head -1
  GNU bash, version 4.1.0(1)-release (mips-unknown-linux-uclibc)

The shells also work interactively:

  $ PS1='. ' perl ./run dash.run
  . exit
  $ PS1=', ' perl ./run bash.run --norc
  , exit

pts-mips-emulator implements a subset of the 32-bit MIPS-I instruction set
architecture (ISA), see
https://en.wikipedia.org/wiki/MIPS_architecture#MIPS_I introduced in 1985
with the R2000 processor, and also implemented by the R3000 processor
introduced in 1998. pts-mips-emulator doesn't implement floating point
instructions or the comprocessor (and some other instructions are also
missing). Some more details:

* MIPS-I is is big endian (MSB-first) and it's 32-bit.
* There are many architectures named MIPS, e.g. for 32-bit: MIPS-I, MIPS-II,
  MIPS-III, MIPS-IV, MIPS-V, MIPS32r1, ... MIPS32r6, microMIPS32r3 ...
  microMIPS32r6. For 64 bits: MIPS64r1 ... MIPS64r6, microMIPS64r3 ...
  microMIPS64r6. There are also application-specific extensions (ASE) for
  many of these, e.g. MIPS16e2. Some of these architectures are backwards
  compatible to each other, but most of them are not. Thus pts-mipus-emulator
  implements MIPS-I only, and nothing else.
* More details about MIPS architectures here:
  https://en.wikipedia.org/wiki/MIPS_architecture#MIPS_I .
* The corresponding Linux uname(2) machine type is mips, but that's confusing,
  because it includes MIPS-II, MIPS32r2, MIPS64r2 etc. There different Linux
  system call numbers assigned to 32-bit and 64-bit MIPS:
  https://fedora.juszkiewicz.com.pl/syscalls.html .
* Some precompiled busybox executables for MIPS-I: busybox-mips in:
  * https://busybox.net/downloads/binaries/1.16.1/
    It doesn't work. Because of some bug in pts-mips-emulator, it always
    tries to run the setgid applet if an applet was found.
    TODO(pts): Diagnose and fix this bug.
  * https://busybox.net/downloads/binaries/1.17.2/
    It doesn't work. Because of some bug in pts-mips-emulator, it always
    tries to run the setgid applet if an applet was found.
  * https://busybox.net/downloads/binaries/1.21.1/
    It doesn't work.
  * https://busybox.net/downloads/binaries/1.24.0.git-defconfig-multiarch/
    It doesn't work.
  * https://busybox.net/downloads/binaries/1.26.2-defconfig-multiarch/
    It doesn't work.
  * https://busybox.net/downloads/binaries/1.28.1-defconfig-multiarch/
    It doesn't work.
* These precompiled executables have architecture MIPS32r2, so they don't work
  with pts-mips-emulator:
  * https://github.com/darkerego/mips-binaries

__END__

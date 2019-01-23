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

__END__

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

* Perl 5.10.1 (i386, 32-bit integers)
* Perl 5.14.2 (i386, 64-bit integers)
* Perl 5.18.2 (amd64, 64-bit integers)
* Perl 5.24.1 (amd64, 64-bit integers)

using the following command line:

  $ perl ./run dash.run -c 'echo $((6*7))'
  42

__END__

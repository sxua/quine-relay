# Quine Relay

### What this is

This is a Ruby program that generates
Scala program that generates
Scheme program that generates
...(through 50 languages)...
REXX program that generates
the original Ruby code again.

![Language Uroboros][langs]

[langs]: https://raw.github.com/sxua/quine-relay/master/langs.png

### Usage

#### 1. Install all interpreters/compilers.

You are fortunate (almost) if you are using OS X Mountain Lion with Homebrew.
A few packages needs to be installed manually (almost), here they're:

##### Ada
    $ brew install https://raw.github.com/sogilis/homebrew/e2572424376650a466a0eb8e7ed171a06159edd4/Library/Formula/gnat.rb

##### Boo & Mono
    $ brew tap ceykooo/homebrew-boo
    $ HOMEBREW_CC=llvm brew install mono

##### Cattle (dependency for beef / TODO: formula for Homebrew)
    $ git clone https://github.com/andreabolognani/cattle.git
    $ cd cattle
    $ mv autogen.sh autogen.sh.old && sed -e 's/libtoolize/glibtoolize/g' autogen.sh.old > autogen.sh && chmod +x autogen.sh
    $ brew uninstall libxml2
    $ brew install libxml2 --with-python gtk-doc gobject-introspection
    $ ./autogen.sh
    $ ./configure
    $ make && make install

##### Pandoc (dependency for beef / TODO: formula for Homebrew)
    $ curl -o pandoc-1.11.1.dmg http://pandoc.googlecode.com/files/pandoc-1.11.1.dmg
    $ hdiutil attach -mountpoint /Volumes/pandoc pandoc-1.11.1.dmg
    $ sudo installer -pkg /Volumes/pandoc/pandoc-1.11.1.pkg -target /
    $ hdiutil unmount "/Volumes/pandoc"

##### Beef (TODO: formula for Homebrew)
    $ git clone https://github.com/andreabolognani/beef.git
    $ cd beef
    $ mv autogen.sh autogen.sh.old && sed -e 's/libtoolize/glibtoolize/g' autogen.sh.old > autogen.sh && chmod +x autogen.sh
    $ ./autogen.sh
    $ ./configure
    $ make && make install

##### CoffeeScript
    $ brew install node
    $ npm install -g coffee-script

##### LOGO
    $ curl -o ucblogo.tar.gz http://www.cs.berkeley.edu/~bh/downloads/ucblogo.tar.gz
    $ tar -zxf ucblogo.tar.gz && cd ucblogo-6.0
    $ rm -rf csls/CVS
    $ mv makefile.in makefile.in.old && sed -e 's/install: all/install:/g' makefile.in.old > makefile.in
    $ ./configure --cache-file=/dev/null --without-x
    $ make && make install

##### Octave
    brew tap homebrew/science

##### Pascal
    curl -o fpc-2.6.2.intel-macosx.dmg http://fpc.planetmirror.com/pub/fpc/dist/2.6.2/i386-macosx/fpc-2.6.2.intel-macosx.dmg
    hdiutil attach -mountpoint /Volumes/fpc fpc-2.6.2.intel-macosx.dmg
    sudo installer -pkg /Volumes/fpc/fpc-2.6.2rc1.intel-macosx.pkg -target /
    hdiutil unmount "/Volumes/fpc"

And after that you can install the rest via Homebrew:

    $ brew install ruby scala gauche gnu-smalltalk vala icarus-verilog algol68g \
      boo clojure open-cobol clisp gforth gfortran go ghc icon intercal octave \
      jasmin llvm lua ocaml parrot pike swi-prolog python r regina-rexx

If you are not using OS X Mountain Lion, please find your way yourself.
You may find [instructions for Arch Linux and other platforms in the wiki](https://github.com/mame/quine-relay/wiki/Installation).

#### 2. Run each program on each interpreter/compiler.

    $ ruby QR.rb > QR.scala
    $ scalac QR.scala && scala QR > QR.scm
    $ gosh QR.scm > QR.bash
    $ bash QR.bash > QR.st
    $ /usr/local/bin/gst QR.st > QR.tcl
    $ tclsh QR.tcl > QR.unl
    $ ruby unlambda.rb QR.unl > QR.vala
    $ valac QR.vala && ./QR > QR.v
    $ iverilog -o QR QR.v && ./QR -vcd-none > QR.ws
    $ ruby whitespace.rb QR.ws > qr.adb
    $ gnatmake qr.adb && ./qr > QR.a68
    $ a68g QR.a68 > QR.awk
    $ awk -f QR.awk > QR.boo
    $ booi QR.boo > QR.bf
    $ beef QR.bf > QR.c
    $ gcc -o QR QR.c && ./QR > QR.cpp
    $ g++ -o QR QR.cpp && ./QR > QR.cs
    $ mcs QR.cs && mono QR.exe > QR.clj
    $ clj QR.clj > QR.cob
    $ cobc -x QR.cob && ./QR > QR.coffee
    $ /usr/local/share/npm/bin/coffee QR.coffee > QR.lisp
    $ clisp QR.lisp > QR.fs
    $ gforth QR.fs > QR.f
    $ gfortran -o QR QR.f && ./QR > QR.f90
    $ gfortran -o QR QR.f90 && ./QR > QR.go
    $ go run QR.go > QR.groovy
    $ groovy QR.groovy > QR.hs
    $ runghc QR.hs > QR.icn
    $ icont -s QR.icn && ./QR > QR.i
    $ ick -b QR.i && ./QR > QR.j
    $ jasmin QR.j && java QR > QR.java
    $ javac QR.java && java QR > QR.ll
    $ llvm-as QR.ll && lli QR.bc > QR.logo
    $ logo QR.logo > QR.lua
    $ lua QR.lua > QR.makefile
    $ make -f QR.makefile > QR.il
    $ ilasm QR.il && mono QR.exe > QR.js
    $ node QR.js > QR.m
    $ gcc -o QR QR.m && ./QR > QR.ml
    $ ocaml QR.ml > QR.octave
    $ octave -qf QR.octave > QR.pasm
    $ parrot QR.pasm > QR.pas
    $ fpc QR.pas && ./QR > QR.pl
    $ perl QR.pl > QR.php
    $ php QR.php > QR.pike
    $ pike QR.pike > QR.prolog
    $ swipl -q -t qr -f QR.prolog > QR.py
    $ python QR.py > QR.R
    $ R --slave < QR.R > QR.rexx
    $ rexx ./QR.rexx > QR2.rb

You will see that `QR.rb` is the same as `QR2.rb`.

    $ diff QR.rb QR2.rb

Alternatively, just type `make`.

    $ make

Note: It may require huge memory to compile some files.

### Tested interpreter/compiler versions

As I said above, I adapted the program for Mountain Lion and Homebrew.

language     |ubuntu package |version
-------------|---------------|-----------------------------------
Ruby         |ruby      |2.0.0-p247
Scala        |scala          |2.10.2
Scheme       |gauche         |0.9.3.3
Shell        |-           |3.2
Smalltalk    |gnu-smalltalk  |3.2.5
Tcl          |-         |8.5
Unlambda     |(none)         |-
Vala         |valac          |0.18.1-0ubuntu4
Verilog      |iverilog       |0.9.6-1
Whitespace   |(none)         |-
Ada          |gnat           |4.6ubuntu1
ALGOL68      |algol68g       |2.4.1-1
Awk          |gawk           |1:4.0.1+dfsg-2ubuntu1
Boo          |boo            |0.9.5~git20110729.r1.202a430-2
Brainfuck    |beef           |0.0.6-2
C            |gcc            |4:4.7.3-1ubuntu10
C++          |g++            |4:4.7.3-1ubuntu10
C#           |mono-mcs       |2.10.8.1-5ubuntu1
Clojure      |clojure1.4     |1.4.0+dfsg-2ubuntu2
Cobol        |open-cobol     |1.1-1
CoffeeScript |coffeescript   |1.4.0-1
CommonLisp   |clisp          |1:2.49-8.1ubuntu1
Forth        |gforth         |0.7.0+ds2-0.1
FORTRAN77    |f2c            |20100827-1
Fortran90    |gfortran       |4:4.7.3-1ubuntu10
Go           |golang         |2:1.0.2-2
Groovy       |groovy         |2.0.0~beta2+isreally1.8.6-0ubuntu1
Haskell      |ghc            |7.6.2-1ubuntu1
Icon         |icont          |9.4.3-4
INTERCAL     |intercal       |29:0.29-2
Jasmin       |jasmin-sable   |2.4.0-1ubuntu1
Java         |openjdk-6-jdk  |6b27-1.12.5-1ubuntu1
LLVM asm     |llvm           |1:3.2-16~exp1
Logo         |ucblogo        |5.5-2.1
Lua          |lua5.2         |5.2.1-3
Makefile     |make           |3.81-8.2ubuntu2
MSIL         |mono-devel     |2.10.8.1-5ubuntu1
NodeJS       |nodejs         |0.6.19~dfsg1-5ubuntu1
Objective-C  |gobjc          |4:4.7.3-1ubuntu10
OCaml        |ocaml          |3.12.1-2ubuntu3
Octave       |octave         |3.6.4-1
Parrot asm   |parrot         |4.6.0-1
Pascal       |fp-compiler    |2.6.0-9
Perl         |perl           |5.14.2-21
PHP          |php5-cli       |5.4.9-4ubuntu2.2
Pike         |pike7.8        |7.8.352-dfsg-7ubuntu1
Prolog       |swi-prolog     |5.10.4-5ubuntu1
Python       |python         |2.7.4-0ubuntu1
R            |r-base         |2.15.2-1ubuntu1
REXX         |regina-rexx    |3.6-2

### How to re-generate the source

    $ cd src
    $ rake

### License

Copyright (c) 2013 Yusuke Endoh (@mametter), @hirekoke

MIT License

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

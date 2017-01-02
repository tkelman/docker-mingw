FROM ubuntu
MAINTAINER Tony Kelman <tony@kelman.net>
RUN apt-get update
RUN apt-get install --no-install-recommends software-properties-common curl p7zip-full -y
RUN add-apt-repository ppa:ubuntu-wine/ppa -y
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install --no-install-recommends wine1.7 -y
WORKDIR /home/user
RUN curl -Lo julia-download.exe http://status.julialang.org/download/win32
RUN curl -LO http://sourceforge.net/projects/sevenzip/files/7-Zip/9.22/7z922.exe
RUN 7z x -y 7z922.exe 7z.exe 7z.dll
RUN 7z x julia-download.exe
# p7zip has trouble extracting nsis installers, use windows 7z.exe via wine
RUN wine 7z.exe x julia-installer.exe && rm \$_OUTDIR/lib/julia/sys.ji
WORKDIR \$_OUTDIR/share/julia/base
#RUN wine ../../../bin/julia --build ../../../lib/julia/sys0 sysimg.jl

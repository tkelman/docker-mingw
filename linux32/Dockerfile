# Dockerfile for testing 32-bit Linux builds on Travis (aka 64-bit Ubuntu precise)
FROM ubuntu:precise
MAINTAINER Tony Kelman <tony@kelman.net>

RUN apt-get update
RUN apt-get install binutils:i386 python-software-properties git curl patch cmake gdb -y
RUN add-apt-repository ppa:staticfloat/julia-deps -y
RUN apt-get update
RUN apt-get install gcc:i386 g++:i386 make:i386 cpp:i386 g++-4.6:i386 \
      gcc-4.6:i386 libssl-dev:i386 zlib1g-dev:i386 patchelf:i386 \
      gfortran:i386 llvm-3.3-dev:i386 libsuitesparse-dev:i386 \
      libopenblas-dev:i386 libopenblas-base:i386 libblas-dev:i386 \
      liblapack-dev:i386 liblapack3:i386 libarpack2-dev:i386 libarpack2:i386 \
      libfftw3-dev:i386 libgmp-dev:i386 libpcre3-dev:i386 libunwind7-dev:i386 \
      libopenlibm-dev:i386 librmath-dev:i386 libmpfr-dev:i386 -y

RUN git clone --recursive git://github.com/JuliaLang/julia.git /home/user/julia
WORKDIR /home/user/julia
RUN BUILDOPTS="-j4 USEGCC=1 LLVM_CONFIG=llvm-config-3.3 VERBOSE=1 USE_BLAS64=0" && \
      for lib in LLVM ZLIB SUITESPARSE ARPACK BLAS FFTW LAPACK GMP MPFR LIBUNWIND OPENLIBM; do \
        export BUILDOPTS="$BUILDOPTS USE_SYSTEM_$lib=1"; \
      done && make $BUILDOPTS prefix=/tmp/julia install

# run tests by uncommenting the following:
#RUN cd /tmp/julia/share/julia/test && /tmp/julia/bin/julia-debug --check-bounds=yes runtests.jl all

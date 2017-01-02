# Dockerfile for building Julia using same system libraries as on Travis (aka 64-bit Ubuntu precise)
FROM ubuntu:precise
MAINTAINER Tony Kelman <tony@kelman.net>

RUN apt-get update
RUN apt-get install python-software-properties git curl patch cmake gdb -y
RUN add-apt-repository ppa:staticfloat/julia-deps -y
RUN apt-get update
RUN apt-get install gcc g++ make cpp g++-4.6 \
      gcc-4.6 libssl-dev zlib1g-dev patchelf \
      gfortran llvm-3.3-dev libsuitesparse-dev \
      libopenblas-dev libopenblas-base libblas-dev \
      liblapack-dev liblapack3 libarpack2-dev libarpack2 \
      libfftw3-dev libgmp-dev libpcre3-dev libunwind7-dev \
      libopenlibm-dev librmath-dev libmpfr-dev -y

RUN git clone --recursive git://github.com/JuliaLang/julia.git /home/user/julia
WORKDIR /home/user/julia
RUN BUILDOPTS="-j4 USEGCC=1 LLVM_CONFIG=llvm-config-3.3 LLVM_LLC=llc-3.3 VERBOSE=1 USE_BLAS64=0" && \
      for lib in LLVM ZLIB SUITESPARSE ARPACK BLAS FFTW LAPACK GMP MPFR PCRE LIBUNWIND OPENLIBM RMATH; do \
        export BUILDOPTS="$BUILDOPTS USE_SYSTEM_$lib=1"; \
      done && make $BUILDOPTS prefix=/tmp/julia install

# run tests by uncommenting the following:
#RUN cd /tmp/julia/share/julia/test && /tmp/julia/bin/julia-debug --check-bounds=yes runtests.jl all

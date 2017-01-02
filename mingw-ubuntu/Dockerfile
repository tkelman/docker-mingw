# Dockerfile for MinGW cross-compilation of Julia
FROM ubuntu
MAINTAINER Tony Kelman <tony@kelman.net>

RUN apt-get update
RUN apt-get install --no-install-recommends software-properties-common git make curl patch python g++ m4 p7zip-full -y
RUN add-apt-repository ppa:ubuntu-wine/ppa -y
RUN add-apt-repository ppa:tkelman/mingw-backport -y
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install --no-install-recommends wine1.7 g++-mingw-w64 gfortran-mingw-w64 -y

RUN git clone git://github.com/JuliaLang/julia.git /home/user/julia
WORKDIR /home/user/julia
RUN git submodule init && git submodule update
RUN for XC_HOST in i686-w64-mingw32 x86_64-w64-mingw32; do \
      export XC_HOST; \
      echo 'LLVM_FLAGS = ac_cv_have_decl_strerror_s=no' > Make.user; \
      for i in openblas llvm fftw gmp mpfr suitesparse-wrapper arpack pcre; do \
        make -j4 -C deps install-$i || exit 1; \
      done; \
      $XC_HOST-ar cr usr/lib/libgtest.a; \
      $XC_HOST-ar cr usr/lib/libgtest_main.a; \
      tar -cJf $XC_HOST.tar.xz usr; \
      make distcleanall; \
      rm Make.user; \
      unset XC_HOST; \
    done

# to build:
#RUN echo 'VERBOSE = 1' > Make.user
#RUN echo 'override DEP_LIBS = uv openlibm openspecfun dsfmt Rmath mojibake' >> Make.user
#RUN export XC_HOST=i686-w64-mingw32 && tar -xJf $XC_HOST.tar.xz && make win-extras && make -j4 dist
# UPLOAD BINARY, TRIGGER TEST RUN, ETC
# make distcleanall
# rm -rf dist-extras Make.user

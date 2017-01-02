# Dockerfile for MinGW-w64 cross-compilation of Julia
FROM opensuse:13.2

# Change the following to i686-w64-mingw32 for 32 bit Julia:
ENV XC_HOST i686-w64-mingw32
# Change the following to 32 for 32 bit Julia:
ENV BITS 32

RUN zypper addrepo http://download.opensuse.org/repositories/windows:mingw:win$BITS/openSUSE_13.2/windows:mingw:win$BITS.repo && \
    zypper --gpg-auto-import-keys refresh && \
    zypper -n install --no-recommends git make cmake tar wine which curl \
        python python-xml patch gcc-c++ m4 p7zip.i586 libxml2-tools && \
    zypper -n install mingw$BITS-cross-gcc-c++ mingw$BITS-cross-gcc-fortran \
        mingw$BITS-libstdc++6 mingw$BITS-libgfortran3 mingw$BITS-libssp0
# opensuse packages the mingw runtime dlls under sys-root/mingw/bin, not /usr/lib64/gcc
RUN cp /usr/$XC_HOST/sys-root/mingw/bin/*.dll /usr/lib*/gcc/$XC_HOST/*/ && \
    git clone git://github.com/JuliaLang/julia.git /home/user/julia && \
    git config --global url."git://".insteadOf https://
# use git:// to avoid SSL certificate problems with JuliaDoc
WORKDIR /home/user/julia
RUN make -C deps install-gmp && file usr/bin/libgmp.dll
#RUN make -j4 win-extras julia-ui-release julia-ui-debug
# this last step may need to be run interactively
#RUN make -j4 binary-dist

(

  if ! module_installed docbook-xml; then
     sedit '/man\/Makefile/d' configure.ac  &&
     sedit 's/man//' Makefile.am
  fi &&

  sedit "s:/usr::" autogen.sh  &&
  sedit "s:\$(libdir)/pkgconfig:/usr/lib/pkgconfig:" Makefile.am  &&

  OPTS+=" --with-zlib"  &&

  ./autogen.sh   &&


  ./configure  --prefix=      \
               --libdir=/lib  \
               --mandir=/usr/share/man \
               $OPTS  &&

  sedit "s:\${prefix}/include:/usr/include:"  Makefile  &&
  default_make  &&

# add symlinks to kmod
  ln -sf /bin/kmod "/bin/lsmod"  &&
  for tool in {ins,rm,dep}mod mod{info,probe}; do
    ln -sf /bin/kmod "/sbin/$tool"
  done

) > $C_FIFO 2>&1

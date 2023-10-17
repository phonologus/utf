The files `utf.c` and `utf.h` constitute a minimal library for
processing bi-directional strings/streams of bytes as UTF-8.

The library is intended to facilitate adding Unicode-awareness to
legacy text processing applications, with the minimum of disruption
to any existing byte-processing.

The stream processing functions in the library expect to be passed
a getter function of type `int (*getter)(void)`. This is in lieu
of a closure, so the legacy application's own getter functions will likely
need a shim, along the lines of

    static FILE *gfile;
 
    int
    fgetter(void)
    {
       return fget(gfile);
    }

    int
    fgetu8(FILE *f, char *buf)
    {
       gfile=f;
       return u8getc(fgetter,buf);
    }   


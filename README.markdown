Python Asynchronous I/O bindings (aio.h)
========================================

Version 0.2
Working on Linux only

Reading
    aio_read(fileno, file-offset, length, callback)

```python
import pyaio
import os
	
def aio_callback(buf, rcode, errno):
    if rcode > 0:
        print 'python callback %s' % buf
    elif rcode == 0:
        print "EOF"
    else:
        print "Error: %d" % errno
        
fd = os.open('/tmp/pyaio.txt', os.O_RDONLY)
pyaio.aio_read(fd, 10, 20, aio_callback)
```

Writing
    aio_write(fileno, buffer-object, file-offset, callback)

```python
import pyaio
import os

def aio_callback(rt, errno):
    if rt > 0:
        print "Wrote %d bytes" % rt
    else:
        print "Got error: %d" % errno

fd = os.open('/tmp/pyaio.txt', os.O_WRONLY)
pyaio.aio_write(fd, "Writing Test.......", 30, aio_callback)
```
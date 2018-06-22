```
#include <errno.h> 
int main(int argc, char ** argv){
  int i = 0;
  for(i = 0; i < 256; i++)
  printf("errno.%02d is: %s/n", i, strerror(i));
  return 0;
}

printf("%d",errno);

errno.00 is: Success
errno.01 is: Operation not permitted
errno.02 is: No such file or directory
errno.03 is: No such process
errno.04 is: Interrupted system call
errno.05 is: Input/output error
errno.06 is: No such device or address
errno.07 is: Argument list too long
errno.08 is: Exec format error
errno.09 is: Bad file descriptor
errno.10 is: No child processes
errno.11 is: Resource temporarily unavailable[资源临时不可用](连续发送数据时候回出此错，加延时)
errno.12 is: Cannot allocate memory
errno.13 is: Permission denied
errno.14 is: Bad address
errno.15 is: Block device required
errno.16 is: Device or resource busy
errno.17 is: File exists
errno.18 is: Invalid cross-device link
errno.19 is: No such device
errno.20 is: Not a directory
errno.21 is: Is a directory
errno.22 is: Invalid argument
errno.23 is: Too many open files in system
errno.24 is: Too many open files
errno.25 is: Inappropriate ioctl for device
errno.26 is: Text file busy
errno.27 is: File too large
errno.28 is: No space left on device
errno.29 is: Illegal seek
errno.30 is: Read-only file system
errno.31 is: Too many links
errno.32 is: Broken pipe[断开的管道](原因：the broken pipe error occurs if one end of the
TCP socket closes connection(using disconnect) or gets killed and the other
end tries to still write to it. An indication of a closed/terminated
connection is a return value of 0 when you try to read from that socket
using recv. After receiving such an error, if you try to still write to the
socket, your process gets sent the SIGPIPE signal which kills it. )
errno.33 is: Numerical argument out of domain
errno.34 is: Numerical result out of range
errno.35 is: Resource deadlock avoided
errno.36 is: File name too long
errno.37 is: No locks available
errno.38 is: Function not implemented
errno.39 is: Directory not empty
errno.40 is: Too many levels of symbolic links
errno.41 is: Unknown error 41
errno.42 is: No message of desired type
errno.43 is: Identifier removed
errno.44 is: Channel number out of range
errno.45 is: Level 2 not synchronized
errno.46 is: Level 3 halted
errno.47 is: Level 3 reset
errno.48 is: Link number out of range
errno.49 is: Protocol driver not attached
errno.50 is: No CSI structure available
errno.51 is: Level 2 halted
errno.52 is: Invalid exchange
errno.53 is: Invalid request descriptor
errno.54 is: Exchange full
errno.55 is: No anode
errno.56 is: Invalid request code
errno.57 is: Invalid slot
errno.58 is: Unknown error 58
errno.59 is: Bad font file format
errno.60 is: Device not a stream
errno.61 is: No data available
errno.62 is: Timer expired
errno.63 is: Out of streams resources
errno.64 is: Machine is not on the network
errno.65 is: Package not installed
errno.66 is: Object is remote
errno.67 is: Link has been severed
errno.68 is: Advertise error
errno.69 is: Srmount error
errno.70 is: Communication error on send
errno.71 is: Protocol error
errno.72 is: Multihop attempted
errno.73 is: RFS specific error
errno.74 is: Bad message
errno.75 is: Value too large for defined data type
errno.76 is: Name not unique on network
errno.77 is: File descriptor in bad state
errno.78 is: Remote address changed
errno.79 is: Can not access a needed shared library
errno.80 is: Accessing a corrupted shared library
errno.81 is: .lib section in a.out corrupted
errno.82 is: Attempting to link in too many shared libraries
errno.83 is: Cannot exec a shared library directly
errno.84 is: Invalid or incomplete multibyte or wide character
errno.85 is: Interrupted system call should be restarted
errno.86 is: Streams pipe error
errno.87 is: Too many users
errno.88 is: Socket operation on non-socket
errno.89 is: Destination address required
errno.90 is: Message too long
errno.91 is: Protocol wrong type for socket
errno.92 is: Protocol not available
errno.93 is: Protocol not supported
errno.94 is: Socket type not supported
errno.95 is: Operation not supported
errno.96 is: Protocol family not supported
errno.97 is: Address family not supported by protocol
errno.98 is: Address already in use
errno.99 is: Cannot assign requested address
errno.100 is: Network is down
errno.101 is: Network is unreachable
errno.102 is: Network dropped connection on reset
errno.103 is: Software caused connection abort
errno.104 is: Connection reset by peer[l连接被对端重置]
errno.105 is: No buffer space available
errno.106 is: Transport endpoint is already connected
errno.107 is: Transport endpoint is not connected
errno.108 is: Cannot send after transport endpoint shutdown
errno.109 is: Too many references: cannot splice
errno.110 is: Connection timed out
errno.111 is: Connection refused
errno.112 is: Host is down
errno.113 is: No route to host
errno.114 is: Operation already in progress
errno.115 is: Operation now in progress
errno.116 is: Stale NFS file handle
errno.117 is: Structure needs cleaning
errno.118 is: Not a XENIX named type file
errno.119 is: No XENIX semaphores available
errno.120 is: Is a named type file
errno.121 is: Remote I/O error
errno.122 is: Disk quota exceeded
errno.123 is: No medium found
errno.124 is: Wrong medium type
errno.125 is: Operation canceled
errno.126 is: Required key not available
errno.127 is: Key has expired
errno.128 is: Key has been revoked
errno.129 is: Key was rejected by service
errno.130 is: Owner died
errno.131 is: State not recoverable
errno.132 is: Unknown error 132
132-255 全是Unknown error
```

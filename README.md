# ls
C语言实现Linux ls命令

相关函数：

一、opendir - open a directory
SYNOPSIS 
#include <sys/types.h> 
#include <dirent.h>

DIR *opendir(const char *name);

DESCRIPTION

opendir函数打开一个与给定的目录名name相对应的目录流，并返回一个指向该目录流的指针。打开后，该目录流指向了目录中的第一个目录项。

RETURN VALUE

opendir函数，打开成功，返回指向目录流的指针；打开失败，则返回NULL，并设置相应的错误代码errno。

二、readdir - read a directory
SYNOPSIS 
#include <sys/types.h>

#include <dirent.h>

struct dirent *readdir(DIR *dir);

DESCRIPTION

readdir函数返回一个指向dirent结构体的指针，该结构体代表了由dir指向的目录流中的下一个目录项；如果读到end-of-file或者出现了错误，那么返回NULL。

在Linux系统中，dirent结构体定义如下：

       struct dirent { 
             ino_t          d_ino;       /* inode number */ 
             off_t          d_off;       /* offset to the next dirent */ 
             unsigned short d_reclen;    /* length of this record */ 
             unsigned char  d_type;      /* type of file */ 
             char           d_name[256]; /* filename */ 
         };

readdir函数返回的值会被后续调用的（针对同一目录流的）readdir函数返回值所覆盖。

RETURN VALUE

readdir函数，成功时返回一个指向dirent结构体的指针；失败时或读到end-of-file时，返回NULL，并且设置相应的错误代码errno。

三、closedir - close a directory
SYNOPSIS 
#include <sys/types.h>

#include <dirent.h>

int closedir(DIR *dir);

DESCRIPTION

closedir函数关闭与指针dir相联系的目录流。关闭后，目录流描述符dir不再可用。

RETURN VALUE

closedir函数，成功时返回0；失败是返回-1，并设置相应的错误代码errno。

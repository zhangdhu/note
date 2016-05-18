io.md
Java的I/O功能通过java.io包下的类和接口来支持,在java.io包下主要包括输入/输出两种IO流,每种输入/输出流又可分为字节流和字符流两大类.字节流支持以字节(8位)为单位的IO操作,
而字符流则以字符(16位-Java中)为单位进行IO操作.

除此之外,Java的IO流还使用装饰者模式,将IO流分成底层节点流和上层处理流,节点流直接和底层的物理存储节点关联,虽然不同的物理节点获取的节点流可能存在差异,但程序可以把不同的物理节点包装成统一的处理流,从而允许程序使用统一的IO代码来操作不同的物理节点.




Java I/O
分享到： 15
原文出处： 翡青
Java的I/O功能通过java.io包下的类和接口来支持,在java.io包下主要包括输入/输出两种IO流,每种输入/输出流又可分为字节流和字符流两大类.字节流支持以字节(8位)为单位的IO操作,而字符流则以字符(16位-Java中)为单位进行IO操作.

除此之外,Java的IO流还使用装饰者模式,将IO流分成底层节点流和上层处理流,节点流直接和底层的物理存储节点关联,虽然不同的物理节点获取的节点流可能存在差异,但程序可以把不同的物理节点包装成统一的处理流,从而允许程序使用统一的IO代码来操作不同的物理节点.

File

Java使用java.io.File来提供对底层文件的抽象, File能够新建/删除/重命名文件和目录,但不能访问文件内容本身(需要使用IO流).

File类提供了很多实用的方法,我们可以将其分为以下几类:

文件名相关方法
getAbsoluteFile() getAbsolutePath() getName() getParent() getParentFile() getPath() renameTo(File dest)
文件状态相关方法
exists() canExecute() canRead() canWrite() isFile() isDirectory() isAbsolute()(UNIX/Linux中是否以/开头) isHidden() lastModified()length()
文件操作
createNewFile() createTempFile(String prefix, String suffix) delete() deleteOnExit() setExecutable(boolean executable) setReadOnly()
目录操作
如: mkdir() mkdirs() list() list(FilenameFilter filter) listFiles() listFiles(FileFilter filter) listRoots()
这儿只是大致介绍File类提供的功能,细节请参考


InputStream / Reader

InputStream与Reader是所有输入流的抽象基类, 虽然本身不能创建实例来执行输入, 但作为所有输入流的模板, 他们的方法是所有输入流都通用的.
InputStream包含如下三个方法:

int read()
int read(byte[] b)
int read(byte[] b, int off, int len)
Reader包含如下三个方法:

int read()
int read(char[] cbuf)
int read(char[] cbuf, int off, int len)
对比InputStream和Reader所提供的方法, 这两个类的功能基本相同, 只是一个提供了字节byte读, 一个提供了字符char读.
除此之外, InputStream和Reader还支持几个方法来移动记录指针以实现跳读, 重复读等操作.



Java I/O
分享到： 15
原文出处： 翡青
Java的I/O功能通过java.io包下的类和接口来支持,在java.io包下主要包括输入/输出两种IO流,每种输入/输出流又可分为字节流和字符流两大类.字节流支持以字节(8位)为单位的IO操作,而字符流则以字符(16位-Java中)为单位进行IO操作.

除此之外,Java的IO流还使用装饰者模式,将IO流分成底层节点流和上层处理流,节点流直接和底层的物理存储节点关联,虽然不同的物理节点获取的节点流可能存在差异,但程序可以把不同的物理节点包装成统一的处理流,从而允许程序使用统一的IO代码来操作不同的物理节点.

File

Java使用java.io.File来提供对底层文件的抽象, File能够新建/删除/重命名文件和目录,但不能访问文件内容本身(需要使用IO流).

File类提供了很多实用的方法,我们可以将其分为以下几类:

文件名相关方法
getAbsoluteFile() getAbsolutePath() getName() getParent() getParentFile() getPath() renameTo(File dest)
文件状态相关方法
exists() canExecute() canRead() canWrite() isFile() isDirectory() isAbsolute()(UNIX/Linux中是否以/开头) isHidden() lastModified()length()
文件操作
createNewFile() createTempFile(String prefix, String suffix) delete() deleteOnExit() setExecutable(boolean executable) setReadOnly()
目录操作
如: mkdir() mkdirs() list() list(FilenameFilter filter) listFiles() listFiles(FileFilter filter) listRoots()
这儿只是大致介绍File类提供的功能,细节请参考JDK文档.
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
/**
 
 * 模拟tree命令
 
 *
 
 * @author jifang
 
 * @since 16/1/6下午5:20.
 
 */
 
public class Tree {
 
    public static void main(String[] args) {
 
        // 打印当前目录
 
        if (args == null || args.length == 0) {
 
            displayFiles(new File("."), 0);
 
        } else {
 
            displayFiles(new File(args[0]), 0);
 
        }
 
    }
 
    private static void displayFiles(File directory, int depth) {
 
        File[] files = directory.listFiles();
 
        if (files != null) {
 
            for (File file : files) {
 
                for (int i = 0; i < depth - 1; ++i) {
 
                    System.out.print("|   ");
 
                }
 
                if (depth != 0) {
 
                    System.out.print("|-- ");
 
                }
 
                System.out.println(file.getName());
 
                if (file.isDirectory()) {
 
                    displayFiles(file, depth + 1);
 
                }
 
            }
 
        }
 
    }
 
}
I/O流体系



InputStream / Reader

InputStream与Reader是所有输入流的抽象基类, 虽然本身不能创建实例来执行输入, 但作为所有输入流的模板, 他们的方法是所有输入流都通用的.
InputStream包含如下三个方法:

int read()
int read(byte[] b)
int read(byte[] b, int off, int len)
Reader包含如下三个方法:

int read()
int read(char[] cbuf)
int read(char[] cbuf, int off, int len)
对比InputStream和Reader所提供的方法, 这两个类的功能基本相同, 只是一个提供了字节byte读, 一个提供了字符char读.
除此之外, InputStream和Reader还支持几个方法来移动记录指针以实现跳读, 重复读等操作.

方法

释义

void mark(int readlimit)

Marks the current position in this input stream.

boolean markSupported()

Tests if this input stream supports the mark and reset methods.

void reset()

Repositions this stream to the position at the time the mark method was last called on this input stream.

long skip(long n)

Skips over and discards n bytes of data from this input stream.

OutputStream / Writer

两个流都提供了如下三个方法:

void write(byte[]/char[] b)
void write(byte[]/char[] b, int off, int len)
void write(int b)
因为字符流直接以字符作为操作单位, 所以Writer可以用字符串来代替字符数组(以String对象作为参数). Writer还包含如下方法:

void write(String str)
void write(String str, int off, int len)
Writer append(char c)
Writer append(CharSequence csq)
Writer append(CharSequence csq, int start, int end)


    package com.zhangdh.mvc.io;

import java.io.*;

/**
 * Created by guqianqian on 16/5/17.
 */
public class Copy {
    public static final int BUFFER_LENGTH = 1024;

    public static void main(String[] args){
        String[] aa = {"/Users/guqianqian/tmp/Cleanup.java", "/Users/guqianqian/tmp/Cleanup2.java"};
        str(aa);
    }

    public static void str(String[] args) {

        if (args == null || args.length != 2) {

            throw new RuntimeException("Use like: copy <src-file> <dest-file>");

        }

        Reader reader = null;
        Writer writer = null;
        try {
            reader = new FileReader(args[0]);
            writer = new FileWriter(args[1]);

            char[] buffer = new char[BUFFER_LENGTH];
            int count;
            while ((count =reader.read(buffer))!= -1){
                writer.write(buffer, 0, count);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                reader.close();
                writer.close();
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }
    }


小结:

使用Java IO流执行完IO后,不能忘记关闭流,关闭流才可以保证物理资源会被回收(关闭输出流还可以保证将缓冲区中的数据flush到物理节点中,因为在执行close()方法之前,会自动执行输出流的flush()方法).
Java 1.7改写了所有的IO资源类,他们都实现了AutoCloseable接口,因此都可通过自动关闭的try语句来自动关闭这些流.
通常来说,字节流的功能比字符流的功能强大,因为计算机里所有的数据都是二进制的,因此字节流可以处理所有所有的二进制文件.
如果使用字节流来处理文本文件,则需要将这些字节转换成字符,增加了编程的复杂度.所以有一个规则:如果进行IO是文本内容,则应该考虑使用字符流;如果进行IO的是二进制内容, 则应该考虑使用字节流.

节点流/处理流

节点流的的构造参数是物理IO节点,而处理流的构造参数是已经存在的流.

处理流与节点流相比可以隐藏底层节点流的差异,对外提供更加统一的IO方法,让开发人员只需关心高级流的操作(使用更加简单, 执行效率更高).
使用处理流的思路:使用处理流来包装节点流,程序通过处理流执行IO,让节点流与底层IO设备/文件交互.
在使用处理流包装了节点流之后, 关闭输入/输出流资源时, 只要关闭最上层的处理流即可.关闭最上层的处理流时, 系统会自动关闭该处理流包装的节点流.
































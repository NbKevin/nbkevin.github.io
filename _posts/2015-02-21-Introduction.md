---
layout: post
title: Nb Helper
---

####Nb Helper is a set of python tools which simplifies several daily tasks and improve work efficiency.
####It includes following parts:
- NbException: set of customised exceptions.
- NbTool: set of tools.
- NbCrypt: simplified interface for several encryption algorithm
- NbDecorator: decorators for unsafe, unrecommended and obsolete methods
- NbConfig: configuration file for NbDecorator
- NbFile: simple interface for file operations
- NbMath: wrapper for several math calculations
- NbStructure: usual data structures such as stack and queue
- NbSupport: supportive module

##Examples
#### Math: factorial, primes and etc.
```python
>>> from NbHelper.NbMath import NbMath
>>> NbMath.factorial(4)
24
>>> NbMath.count_primes_under(100)
25
```
#### Crypt: random key, md5, sha256, crc32
```python
>>> from NbHelper.NbCrypt import NbCrypt
>>> NbCrypt.get_random_key()
'u1r6o7rk2wgmfjfodmcvick2dwhw8tij'
>>> NbCrypt.get_md5('XDXD')
'348c3a77b7f65daedef265d6fceffc62'
```
#### File: md5, split, restore & zip
```python
>>> from NbHelper.NbFile import NbFile
>>> instance = NbFile('NbSupport.py')
>>> instance.md5
'd82fb07b179a287139dd09cc409b70ce'
>>> instance.split_to(3)
>>> NbFile.restore('NbSupport.py1')
>>> instance.zip_into('NbSupport.gzip')
>>> instance.dispose()
```
#### Structure: stack and queue
```python
>>> from NbTool import NbStructure
>>> example = NbStructure.NbStack(3)
>>> example.push(10)
>>> example.push(20)
>>> example.push(NbStack)
>>> example.is_full()
<class 'NbHelper.NbStructure.NbStack'>
>>> example.pop()
True
>>> for i in example:
        print(i)
20
10
>>> example.is_empty()
True
```
##Documentation
###NbFile
####constructor `(path, read_immediately=False)`
`__init__` method is called when constructing a new instance of NbFile. It accepts two argument. The first is the path to the file and the second one decides whether to read this file immediately or not. For resource and efficiency reason, it is recommended to leave this argument to False. Another suggestion is to always use the absolute path of file in case that relative reference varies from platform to platform.
####name, size
`name` field stores the name of the instance file, including its extension name. `size` gives out its size in byte.
####path, absolute_path, parent_dir
`path` gives the path used to initialize the instance, whether relative or absolute. To get the absolute path of the instance file, use `absolute_path` and `parent_dir` gives the parent directory of it.
####last_access_time, last_modification_time, creation_time
These three attributes gives information as their name tells in the format of UNIX time stamp.
####file, read, file_content
`file` field refers to a general `IO Wrapper` instance in which the instance file is the target. To access the text content of a file, use `file_content`. However you must call `read` method first before using this field because the open and read operation is asynchronised. As a consequence, you must release this file either implicitly or explicitly or it would remain locked until python process terminates and no other process would be able to access this file. The `__del__` magic method ensures that file handles would be automatically released during recycling. Still, it is strong recommended to release it manually by calling `dispose` method.
####binary, read_binary, binary_content
Access to binary content of instance file is provided with a similar interface. A proper disposal is also required after calling `read_binary` method.
####md5, crc32, sha1, sha224, sha256, sha384, sha512
These are shortcuts to get the hash value of the instance file. For efficiency reason, they are implemented as property getter so that the value would only be calculated when being called.
These properties rely on `NbCrypt` module.
####copy `(source_file, target_file)`, copy_to `(target_path)`
Copy a file to a target path. Arguments can either be a path of file or a NbFile instance. Automatically release file handles.
#####move `(source_file, target_file)`, move_to `(target_path)`
#####delete `(file)`, delete_self  `()`
#####rename `(original_file, new_name)`, rename_to `(new_name)`
####copy_directory `(source_directory, target_directory)`
Copy a directory to a new place. Recursion is used in its implementation. Therefore it may crash or exceeds the maximum recursion depth of python, which varies from computer to computer but usually comes near 1000.
####split_to `(number_of_pieces)`
Split a large file to comparatively small pieces. Can be useful when transferring data through Internet.
####restore `(first_file)`
Restore a complete file from separate pieces. Notice that since `split_to` method does not involve any kind of compression and thus has no verification record. Lost of any piece could lead to the complete damage of the original file.
####zip `(original_file, zipped_file)`, zip_into `(zipped_file)`
Compress a file using `gzip` module. No fancy feature is available at this time :)
####equal `(file, another_file)`, equal_to `(another_file)`
Tell if a file is equal to another file. It uses md5 to compare file by default which, of course, could be changes into other algorithm since you have the source code. Also you can use `instance_a == instance_b` with the implementation of `__eq__` method.
####dispose `()`, dispose_all `()`
Close all opened handles of the instance and clear itself from the reference set. `dispose_all` method would close all handles created by NbFile in current namespace (if it is called this name).
####iterator
NbFile implements the `__iter__` and `__next__` method which makes its instance iterable. By default, this iterator iters  text content line by line. To iter binary content, use `binary_iter` method.
```python
>>> sample = NbFile(‘Sample.txt’)
>>> for text in sample:
            print(text)
Love me little, love me long
Love that lasteth till ’tis old
Fadeth not in haste
```#Nb Helper
####Nb Helper is a set of python tools which simplifies several daily tasks and improve work efficiency.
####It includes following parts:
- NbException: set of customised exceptions.
- NbTool: set of tools.
- NbCrypt: simplified interface for several encryption algorithm
- NbDecorator: decorators for unsafe, unrecommended and obsolete methods
- NbConfig: configuration file for NbDecorator
- NbFile: simple interface for file operations
- NbMath: wrapper for several math calculations
- NbStructure: usual data structures such as stack and queue
- NbSupport: supportive module

##Examples
#### Math: factorial, primes and etc.
```python
>>> from NbHelper.NbMath import NbMath
>>> NbMath.factorial(4)
24
>>> NbMath.count_primes_under(100)
25
```
#### Crypt: random key, md5, sha256, crc32
```python
>>> from NbHelper.NbCrypt import NbCrypt
>>> NbCrypt.get_random_key()
'u1r6o7rk2wgmfjfodmcvick2dwhw8tij'
>>> NbCrypt.get_md5('XDXD')
'348c3a77b7f65daedef265d6fceffc62'
```
#### File: md5, split, restore & zip
```python
>>> from NbHelper.NbFile import NbFile
>>> instance = NbFile('NbSupport.py')
>>> instance.md5
'd82fb07b179a287139dd09cc409b70ce'
>>> instance.split_to(3)
>>> NbFile.restore('NbSupport.py1')
>>> instance.zip_into('NbSupport.gzip')
>>> instance.dispose()
```
#### Structure: stack and queue
```python
>>> from NbTool import NbStructure
>>> example = NbStructure.NbStack(3)
>>> example.push(10)
>>> example.push(20)
>>> example.push(NbStack)
>>> example.is_full()
<class 'NbHelper.NbStructure.NbStack'>
>>> example.pop()
True
>>> for i in example:
        print(i)
20
10
>>> example.is_empty()
True
```
##Documentation
###NbFile
####constructor `(path, read_immediately=False)`
`__init__` method is called when constructing a new instance of NbFile. It accepts two argument. The first is the path to the file and the second one decides whether to read this file immediately or not. For resource and efficiency reason, it is recommended to leave this argument to False. Another suggestion is to always use the absolute path of file in case that relative reference varies from platform to platform.
####name, size
`name` field stores the name of the instance file, including its extension name. `size` gives out its size in byte.
####path, absolute_path, parent_dir
`path` gives the path used to initialize the instance, whether relative or absolute. To get the absolute path of the instance file, use `absolute_path` and `parent_dir` gives the parent directory of it.
####last_access_time, last_modification_time, creation_time
These three attributes gives information as their name tells in the format of UNIX time stamp.
####file, read, file_content
`file` field refers to a general `IO Wrapper` instance in which the instance file is the target. To access the text content of a file, use `file_content`. However you must call `read` method first before using this field because the open and read operation is asynchronised. As a consequence, you must release this file either implicitly or explicitly or it would remain locked until python process terminates and no other process would be able to access this file. The `__del__` magic method ensures that file handles would be automatically released during recycling. Still, it is strong recommended to release it manually by calling `dispose` method.
####binary, read_binary, binary_content
Access to binary content of instance file is provided with a similar interface. A proper disposal is also required after calling `read_binary` method.
####md5, crc32, sha1, sha224, sha256, sha384, sha512
These are shortcuts to get the hash value of the instance file. For efficiency reason, they are implemented as property getter so that the value would only be calculated when being called.
These properties rely on `NbCrypt` module.
####copy `(source_file, target_file)`, copy_to `(target_path)`
Copy a file to a target path. Arguments can either be a path of file or a NbFile instance. Automatically release file handles.
#####move `(source_file, target_file)`, move_to `(target_path)`
#####delete `(file)`, delete_self  `()`
#####rename `(original_file, new_name)`, rename_to `(new_name)`
####copy_directory `(source_directory, target_directory)`
Copy a directory to a new place. Recursion is used in its implementation. Therefore it may crash or exceeds the maximum recursion depth of python, which varies from computer to computer but usually comes near 1000.
####split_to `(number_of_pieces)`
Split a large file to comparatively small pieces. Can be useful when transferring data through Internet.
####restore `(first_file)`
Restore a complete file from separate pieces. Notice that since `split_to` method does not involve any kind of compression and thus has no verification record. Lost of any piece could lead to the complete damage of the original file.
####zip `(original_file, zipped_file)`, zip_into `(zipped_file)`
Compress a file using `gzip` module. No fancy feature is available at this time :)
####equal `(file, another_file)`, equal_to `(another_file)`
Tell if a file is equal to another file. It uses md5 to compare file by default which, of course, could be changes into other algorithm since you have the source code. Also you can use `instance_a == instance_b` with the implementation of `__eq__` method.
####dispose `()`, dispose_all `()`
Close all opened handles of the instance and clear itself from the reference set. `dispose_all` method would close all handles created by NbFile in current namespace (if it is called this name).
####iterator
NbFile implements the `__iter__` and `__next__` method which makes its instance iterable. By default, this iterator iters  text content line by line. To iter binary content, use `binary_iter` method.
{% highlight python %}
>>> sample = NbFile(‘Sample.txt’)
>>> for text in sample:
            print(text)
Love me little, love me long
Love that lasteth till ’tis old
Fadeth not in haste
{% endhighlight %}

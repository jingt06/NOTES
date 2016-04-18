1 . What is the definition of a **file** given in the notes? What is the definition of a **file system**

- **file**: persistent, named objects
- **file systerm**: a collection of files which sharea common name space

2 . Describe **operations** described in class that an application can perform on a file

- open: returns a file identifier
- close
- read: read copies data from a file into a virtual address space
- write: copies data from a virtual adddress into a file
- seek: enables non-sequential reading.writing
- get/set: file meta-data

3 . **File position** may be implicit, Why is this, and because of this how is **non-sequential I/O** performed?

- File position will update current file postion after a read/write, this make sequential file I/O easy for an applications to request. 
- For a non-sequential(random) file I/O, use:
   - a **seek** operation(lseek) to adjust file position before reading or writing
   - a positioned read or write operation. eg. pread, pwrite

4 . What happens when you seek past the end of file?

- fails

5 . What is the difference of **hard link** and a **soft link**

- **hard link**: is an association between a name and an i-number.
- **soft link** (synbolic links): is an associate between a name and a pathname.

6 . What limitations of hard links do soft links not have?

- hard link enforce **referential integrity** while softlink not.
- hard link cannot cross file system boundaries, while softlink do not have this limitation
- hard link cannot link to a directory

7 . What problems can occur with the use of soft links?

8 . Why can't hard links cross file system boundaries?

- Because hard links are associated with a i-number. i-number are unique in different file system. Second, it is different to enforce referential intergrity with multiple file systems.

9 . If we wish to operate with multiple file systems, what are the two most common options in organizing the system

- DOS/Windows: use two-part file names: file system name, pathname within, file systems
- Unix: create single hierarchical namespace that combines the namespaces of two file system (mount)

10 . What kind of meta-data is contained in a Unix i-node?

- file type, file permissions, file length, number of file blocks, time of last file access, time of last i-node update, last file update, number of hard links to this file, direct dta blcok pointers, single/double/triple indirect data block pointers.

11 . What are advantages of using single/double/triple blocks instead of just direct blocks?

- increase max file size.

12 . What are advantages to leave large gaps between sections of used space on disk?

- file size may increase in the future.

13 . How are directories implemented

- Implemented as a special type of file, contains directory entries, each consist a file name and a corresponding i-number

14 . Describe how to implement hard links and soft links.

- soft links can be implemented as a special type of file, create a new softlink file, add a new entry in directory, store the pathname string as contests of the new file
- hard links are simply directory entries, find out the internal file identifier of the origin file, create a new entry in the directory and the new file identifier is the  is the i-number of previous file.

15 . What does the open() system call have to differently wehn handling a symlink file?

- read context and open the pathname in the content.

16 . What are two ways for a file system to handle/clean up after a failure?

- **special-purpose consistency checkers**: run after a crash, before normal operations resume, find and attempt to repair inconsistent file system data strucutres
- **journaling**: record file system meta-data changes in a journal, so that sequences of changes can be written to disk in a single operations, after chanages ahve been journaled, update the disk data structures, after a failure, redo journaled updates in case they were not done before the failure
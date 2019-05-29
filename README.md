# Checksums & GnuPG Signing

A checksum is a small-sized datum derived from a block of digital data for the purpose of detecting errors which may have been introduced during its transmission or storage. It is usually applied to an installation file after it is received from the download server. By themselves, checksums are often used to verify data integrity but are not relied upon to verify data authenticity.

###### File formats
A checksum file is a small file that contains the checksums of other files.
There are a few known checksum file formats
Several utilities, such as md5deep, can use such checksum files to automatically verify an entire directory of files in one operation.
The particular hash algorithm used is often indicated by the file extension of the checksum file.

1. ".sha1" file extension indicates a checksum file containing 160-bit SHA-1 hashes in sha1sum format.
2. ".md5" file extension, or a file named "MD5SUMS", indicates a checksum file containing 128-bit MD5 hashes in md5sum format.
3. ".sfv" file extension indicates a checksum file containing 32-bit CRC32 checksums in simple file verification format.
4. "crc.list" file indicates a checksum file containing 32-bit CRC checksums in brik format.
5. ".gpg" GNU Privacy Guard (GnuPG or GPG) is an encryption tool and digital signatures is a replacement for the PGP (Pretty Good Privacy) but with the main difference being free software licensed under the GPL. GPG uses the IETF standard called OpenPGP.

# Linux - Ubuntu 18.04

Generate algorythm for Linux
```sh
- echo www.google.com |md5sum

- echo www.google.com |shasum
```
Verify file integrity
```sh
md5sum filename.zip

sha1sum filename.zip
```

Return something like the following bond
```
MD5 ba6aafee992a08a8504102864fa36934c  filename.zip
SHA1 7771ddaffb7bc23c7cb94c7bbfdb92b94c60e820   filename.zip
```

# Microsoft

Alternative is surfing for explorer and generate archive or carpet algorythm

## Microsoft (R) File Checksum Integrity Verifier
___________________________________________________________________________________________________

###### 1. What is File Checksum Integrity Verifier (FCIV)?
2. Features
3. Syntax
4. Database storage format
5. Verification
###### 6. History

## Download Microsoft Command Line
[Download](https://www.microsoft.com/en-us/download/details.aspx?id=11533)

###### 1.What is fciv?
---------------
Fciv is a command line utility that computes and verifies hashes of files.

It computes a MD5 or SHA1 cryptographic hash of the content of the file.
If the file is modified, the hash is different.

With fciv, you can compute hashes of all your sensitive files.
When you suspect that your system has been compromised, you can run a verification to determine which files have been modified.
You can also schedule verifications regularily.

###### 2.Features:
-----------
- Hash algorithm: MD5 , SHA1 or both ( default MD5).
- Display to screen or store hash and filename in a xml file.
- Can recursively browse a directory ( ex fciv.exe c:\ -r ).
- Exception list to specify files or directories that should not be computed.
- Database listing.
- hashes and signature verifications.
- store filename with or without full path.

###### 3.Syntax:
---------
Usage:  fciv.exe [Commands] <Options>

Commands: ( Default -add )

        -add    <file | dir> : Compute hash and send to output (default screen).

                dir options:
                -r       : recursive.
                -type    : ex: -type *.exe.
                -exc file: list of directories that should not be computed.
                -wp      : Without full path name. ( Default store full path)
                -bp      : base path. The base path is removed from the path name of each entry

        -list            : List entries in the database.

        -v               : Verify hashes.
                         : Option: -bp basepath.

        -? -h -help      : Extended Help.

Options:
        -md5 | -sha1 | -both    : Specify hashtype, default md5.
        -xml db                 : Specify database format and name.

To display the MD5 hash of a file, type fciv.exe filename

Compute hashes:
        fciv.exe c:\mydir\myfile.dll
        fciv.exe c:\ -r -exc exceptions.txt -sha1 -xml dbsha.xml
        fciv.exe c:\mydir -type *.exe
        fciv.exe c:\mydir -wp -both -xml db.xml

List hashes stored in database:
        fciv.exe -list -sha1 -xml db.xml

Verifications:
        fciv.exe -v -sha1 -xml db.xml
        fciv.exe -v -bp c:\mydir -sha1 -xml db.xml
        
###### 4.Database storage format:
--------------------------
xml file.

The hash is stored in base 64.
<?xml version="1.0" encoding="utf-8"?>
<FCIV>
	<FILE_ENTRY>
		<name> </name>
		<MD5> </MD5>
		<SHA1> </SHA1>
	</FILE_ENTRY>
</FCIV>	

###### 5.Verification:
---------------
You can build a hash database of your sensitive files and verify them regularily or when you suspect that your system
has been compromised.

It checks each entry stored in the db and verify that the checksum was not modified.

###### 6.History:
-----------
- Fciv 1.2 : Added event log.
- Fciv 1.21: Fixed bad keyset error on some computers.
- Fciv 1.22: Added -type option. Support up to 10 masks. *.exe *.dll ...
- Fciv 2.0:  xml as unique storage. Added -both option.
- Fciv 2.01: Exit with error code to allow detections of problem in a script.
- Fciv 2.02: Improved perfs. When both alg are specified, it's now done in one pass.
- Fciv 2.03: Added -wp and -bp options. Fciv now stores full path or relatives paths.
- Fciv 2.04: Removed several options to simplify it.
- Fciv 2.05: Added success message if the verification did not detect any errors.

_________________________________________________________________________________________________________________________________

# Generate GPG File
Generate a GPG key pair. Since there are multiple versions of GPG, you many need to consult the relevant man page to find the appropriate key generation command. Your GPG key must use RSA with a key size of 4096 bits.

###### Create GPG Keys

```sh
gpg --full-generate-key
```
1. Select what kind of key you want. We recommend RSA and RSA (default) [1].
1. Enter the desired key size. We recommend the maximum key size of 4096.
2. Enter the length of time the key should be valid. Press Enter to specify the default selection, indicating that the key doesn't expire [0].
3. Verify that your selections are correct [y/N].
4. Enter your user ID information.
a) Real Name:
b) E-mail:
c) Comment:
d) Confirmm the information write is correct.
e) Enter password:


Use the
```sh
gpg --list-secret-keys --keyid-format
```
LONG command to list GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.

From the list of GPG keys, copy the GPG key ID you'd like to use. In this example, the GPG key ID is 3AA5C34371567BD2:
```sh
gpg --list-secret-keys --keyid-format LONG
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot 
ssb   4096R/42B317FD4BA89E7A 2016-03-10
Paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is 3AA5C34371567BD2:
```
and

```sh
gpg --armor --export 3AA5C34371567BD2
# Prints the GPG key ID, in ASCII armor format
```
Copy your GPG key, beginning with -----BEGIN PGP PUBLIC KEY BLOCK----- and ending with -----END PGP PUBLIC KEY BLOCK-----.

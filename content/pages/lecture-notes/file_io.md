---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: File I/O
uid: 2ce7068a-3337-c8e9-62a1-5faf2e352343
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Introduction](#Intro)
2.  [Text Input](#Input)
3.  [Text Output](#Output)
4.  [Binary Input and Output](#Binary)

{{< anchor "Intro" >}}{{< /anchor >}}1\. Introduction
-----------------------------------------------------

Java® uses a stream-based approach to input and output. A stream in this context is a flow of data, which could either be read in from a data source (e.g. file, keyboard or socket) or written to a data sink (e.g file, screen, or socket). Java® currently supports two types of streams:

*   8-bit streams. These are intended for binary data i.e. data that will be manipulated at the byte level. The abstract base classes for 8-bit streams are InputStream and OutputStream.
*   16-bit streams. These are intended for character data. 16-bits streams are required becuase Java®'s internal representation for characters is the 16-bit Unicode format rather than the 8-bit ASCII format. The abstract base classes for 16-bit streams are Reader and Writer.

It is possible to create a 16-bit Reader from an 8-bit InputStream using the InputStreamReader class e.g.

_Reader r = new InputStreamReader(System.in);      // System.in is an example of an InputStream_.

Likewise, it is possible to create a 16-bit Writer from an 8-bit OutputStream using the OutputStreamWriter class e.g.

_Writer w = new OutputStreamWriter(System.out);     // System.out is an example of an OutputStream_.

{{< anchor "Input" >}}{{< /anchor >}}2\. Text Input
---------------------------------------------------

The _FileReader_ class is used to read characters from a file. This class can only read one 16-bit Unicode character at a time (characters that are stored in 8-bit ASCII will be automatically promoted to Unicode.) In order to read a full line of text at once, we must layer a _BufferedReader_ on top of the _FileReader_. Next, the individual words in the line of text can be extracted using a _StringTokenizer_. If the text contains numbers, we must also perform _String_ to _Number_ conversion operations, like _Integer.parseInt()_ and _Double.parseDouble()_.

_import java.io.\*;_  
_import java.util.\*;_

 _public class Main {_  
 _public static void main(String\[\] args) {_  
 _try {_  
 _readText(args\[0\]);_  
 _}_  
 _catch (IOException e) {_  
 _e.printStackTrace();_  
 _}_  
 _}_

 _// This function will read data from an ASCII text file._  
 _public static void readText(String fileName) throws IOException {_  
 _// First create a FileReader.  A Reader is a 16-bit input stream,_  
 _// which is intended for all forms of character (text) input._  
 _Reader reader = new FileReader(fileName);_

 _// Now create a BufferedReader from the Reader.  This allows us to_  
 _// read in an entire line at a time._  
 _BufferedReader bufferedReader = new BufferedReader(reader);_  
 _String nextLine;_

 _while ((nextLine = bufferedReader.readLine()) != null) {_  
 _// Next, we create a StringTokenizer from the line we have just_  
 _// read in.  This permits the extraction of nonspace characters._  
 _StringTokenizer tokenizer = new StringTokenizer(nextLine);_

 _// We can now extract various data types as follows._  
 _String companyName = tokenizer.nextToken();_  
 _int numberShares = Integer.parseInt(tokenizer.nextToken());_  
 _double sharePrice = Double.parseDouble(tokenizer.nextToken());_

 _// Print the data out on the screen._  
 _System.out.print(companyName + " has " + numberShares);_  
 _System.out.println(" million shares valued at $" + sharePrice);_

 _// Close the file._  
 _bufferedReader.close();_  
 _}_  
 _}_  
_}_

This program can be easily converted to read in data from the keyboard. Simply replace

 _Reader reader = new FileReader(fileName);_

with

    _Reader = new InputStreamReader(System.in);_

{{< anchor "Output" >}}{{< /anchor >}}3\. Text Output
-----------------------------------------------------

The _FileWriter_ class is used to write text to a file. This class is only capable of writing out individual characters and strings. We can layer a _PrintWriter_ on top of the _FileWriter_, so that we can write out numbers as well.

_import java.io.\*;_  
_import java.util.\*;_  
_import java.text.\*;_

 _public class Main {_  
 _public static void main(String\[\] args) {_  
 _try {_  
 _writeText(args\[0\]);_  
 _}_  
 _catch (IOException e) {_  
 _e.printStackTrace();_  
 _}_  
 _}_

 _// This function will write data to an ASCII text file._  
 _public static void writeText(String fileName) throws IOException {_  
 _// First create a FileWriter.  A Writer is a 16-bit output stream,_  
 _// which is intended for all forms of character (text) output._  
 _Writer writer = new FileWriter(fileName);_

 _// Next create a PrintWriter from the Writer.  This allows us to_  
 _// print out other data types besides characters and Strings._  
 _PrintWriter printWriter = new PrintWriter(writer);_

 _// Now print out various data types._  
 _boolean b = true;_  
 _int i = 20;_  
 _double d = 1.124;_  
 _String str = "This is some text.";_

 _printWriter.print(b);_  
 _printWriter.print(i);_  
 _printWriter.print(d);_  
 _printWriter.println("\\n" + str);_

 _// This is an example of formatted output.  In the format string,_  
 _// 0 and # represent digits.  # means that the digit should not_  
 _// be displayed if it is 0._  
 _DecimalFormat df = new DecimalFormat("#.000");_  
 _printWriter.println(df.format(200.0));  // 200.000_  
 _printWriter.println(df.format(0.123));  // .123_

 _// This will flush the PrintWriter's internal buffer, causing the_  
 _// data to be actually written to file._  
 _printWriter.flush();_

 _// Finally, close the file._  
 _printWriter.close();_  
 _}_  
_}_

{{< anchor "Binary" >}}{{< /anchor >}}4\. Binary Input and Output
-----------------------------------------------------------------

Binary input and output is done using the 8-bit streams. To read binary data from a file, we create a _FileInputStream_ and then layer a _DataInputStream_ on top of it. To write binary data to a file, we create a _FileOutputStream_ and then layer a _DataOutputStream_ on top of it. The following example illustrates this.

_import java.io.\*;_

 _public class Main {_  
 _public static void main(String\[\] args) {_  
 _try {_  
 _writeBinary(args\[0\]);_  
 _readBinary(args\[0\]);_  
 _}_  
 _catch (IOException e) {_  
 _e.printStackTrace();_  
 _}_  
 _}_

 _// This function will write binary data to a file._  
 _public static void writeBinary(String fileName) throws IOException {_  
 _// First create a FileOutputStream._  
 _OutputStream outputStream = new FileOutputStream(fileName);_

 _// Now layer a DataOutputStream on top of it._  
 _DataOutputStream dataOutputStream = new DataOutputStream(outputStream);_

 _// Now write out some data in binary format.  Strings are written out_  
 _// in UTF format, which is a bridge between ASCII and Unicode._  
 _int i = 5;_  
 _double d = 1.124;_  
 _char c = 'z';_  
 _String str = "Some text";_

 _dataOutputStream.writeInt(i);           // Increases file size by 4 bytes._  
 _dataOutputStream.writeDouble(d);   // Increases file size by 8 bytes._  
 _dataOutputStream.writeChar(c);      // Increases file size by 2 bytes._  
 _dataOutputStream.writeUTF(str);     // Increases file size by 2+9 bytes._

 _// Close the file._  
 _dataOutputStream.close();_  
 _}_

 _// This function will read binary data from a file._  
 _public static void readBinary(String fileName) throws IOException {_  
 _// First create a FileInputStream._  
 _InputStream inputStream = new FileInputStream(fileName);_

 _// Now layer a DataInputStream on top of it._  
 _DataInputStream dataInputStream = new DataInputStream(inputStream);_

 _// Now read in data from the binary file._  
 _int i;_  
 _double d;_  
 _char c;_  
 _String str;_

 _i = dataInputStream.readInt();_  
 _d = dataInputStream.readDouble();_  
 _c = dataInputStream.readChar();_  
 _str = dataInputStream.readUTF();_

 _System.out.print("integer " + i + " double " + d);_  
 _System.out.println(" char " + c + " String " + str);_

 _// Close the file._  
 _dataInputStream.close();_  
 _}_  
_}_
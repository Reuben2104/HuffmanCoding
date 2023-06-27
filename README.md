# HuffmanCoding

**Overview:**
Compression is just about everywhere, it is the process of representing data with fewer bits. Imagine that you run out of storage space in your computer and you can’t get a new one. You could delete some photos but you don’t want to. Instead you could free up some space by compressing each photo, reducing the file size. There are many ways to compress data, the algorithm used depends on the type of data you need to compress.
In this assignment you will implement a form of data compression. That is, given some data, we want to express the same information using less space. For this project, we will specifically focus on compressing text files, so we must first understand how computers represent text internally.
Recall that computers store data as a sequence of bytes. A byte consists of eight bits, and it represents a value between 0 and 255 inclusive. To represent English text, we need a way of assigning each English letter, punctuation symbol, special character, etc. to a sequence of eight bits (a value from 0 to 255). This mapping is provided by the ASCII encoding, which is shown in the table below. Notice that ASCII only uses 128 out of the 256 possible values that a byte can store.

**Methods that need to be implemented**

**makeSortedList**

Implement this method to read the file referenced by filename character by character, and store a sorted ArrayList of CharFreq objects, sorted by frequency, in sortedCharFreqList. Characters that do not appear in the input file will not appear in your ArrayList.
Notice that your provided code begins by setting the file with StdIn. You can now use methods like StdIn.hasNextChar() and StdIn.readChar() which will operate on the file as if it was standard input. 
Also notice that there are only 128 ASCII values. This means that you can keep track of the number of occurrences of each character in an array of size 128. You can use a char as an array index, and it will automatically convert to the corresponding ASCII int value. You can convert an ASCII int value “num” back into its corresponding char with (char) num.
The Huffman Coding algorithm does not work when there is only 1 distinct character. For this specific case, you must add a different character with probOcc 0 to your ArrayList, so you can build a valid tree and encode properly later. For this assignment, simply add the character with ASCII value one more than the distinct character. If you are already at ASCII value 127, wrap around to ASCII 0. DO NOT add more than one of these, and also DO NOT add any characters with frequency 0 in any normal input case. 
Because the CharFreq object has been implemented to compare based on probOcc primarily, you can simply use Collections.sort(list) before returning your final ArrayList. You do not need to implement your own sorting method.

**makeTree**
Implement this method to use sortedCharFreqList and store the root of a valid Huffman Coding tree in huffmanRoot.
You will be using the TreeNode class to represent one node of your Huffman Coding tree. It contains a CharFreq object as its data, and references to the left and right.
You will be using the provided Queue class to code the Huffman Coding process. You must use the Huffman Coding algorithm outlined above. 
TreeNodes which do not have any children represent encodings for characters. These nodes of your Huffman Coding tree must contain both a “character” and a “probOcc” in their CharFreq object. 
TreeNodes which have at least one child do not represent encodings for characters. These nodes of your Huffman Coding tree must contain a null “character”, and their “probOcc” must be the sum of their children. The root TreeNode will have a “probOcc” of 1.0.

**makeEncodings**
Implement this method to use huffmanRoot and store a String array of size 128 containing a String of 1’s and 0’s for every character in encodings. Characters not present in the Huffman Coding tree will have their spots in the array left null.
Remember that going to the left child of your Huffman Coding tree represents adding a ‘0’ to your encoding for a character, and going to the right child represents adding a ‘1’. The encoding for a character is simply given by the path to get to that node from the root.
Remember that only TreeNodes with no children contain a character, and only the paths to these TreeNodes will receive an encoding. 
You can convert a Character object to its int ASCII code by casting it with (int).
Below is an example of running the driver to help test this method.

**encode**
Implement this method to use encodings, an input file containing some text we want to encode, and an output file we want to encode into. It will write the compressed encoding of the input file into the output file.
Notice that your provided code begins by setting the file with StdIn. You can now use methods like StdIn.hasNextChar() and StdIn.readChar() which will operate on the file as if it was standard input.
You are to create a String of ones and zeros which represents your encoding of the input text file using your encodings array. The last line of this method must use the writeBitString method to write this String to the file in bits. DO NOT try to write to the file manually.
If the file was successfully compressed, your output file will have a significantly smaller file size than the original text file. Feel free to open your file explorer and check!

**decode**
Implement this method to take in your encoded file and use huffmanRoot, and print out the decoding. If done correctly, the decoding will be the same as the contents of the text file used for encoding.
Notice that your provided code begins by setting the output file with StdOut. You can now use methods like StdOut.println() and StdOut.print() which will operate on the decodings file as if it was standard output.
You must start your method using the provided readBitString method in order to get the string of ones and zeros from the encoded file. DO NOT try to read the encoded file manually.
You must then use your tree and the procedure outlined above to decode the bit string into characters, according to the tree’s encoding scheme. 


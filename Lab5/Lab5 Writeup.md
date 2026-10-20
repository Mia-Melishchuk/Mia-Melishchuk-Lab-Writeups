# Lab 5 Writeup
## Code
```
package cs1501_lzw_lab;

public class LZW {
    private static final int R = 256; // number of input chars
    private static int L = 512; // number of codewords = 2^W
    private static int maxW = 16; // codeword width
    private static int W = 9;

    public static void compress() {
        L = 512;
        W = 9;

        String input = BinaryStdIn.readString();
        TST<Integer> st = new TST<Integer>();
        for (int i = 0; i < R; i++)
            st.put("" + (char) i, i);
        int code = R + 1; // R is codeword for EOF

        while (input.length() > 0) {
            String s = st.longestPrefixOf(input); // Find max prefix match s.
            BinaryStdOut.write(st.get(s), W); // Print s's encoding.
            int t = s.length();

            // my stuff
            if (t < input.length() && code < L) // Add s to symbol table.
                st.put(input.substring(0, t + 1), code++);
            else if (t < input.length() && code >= L && W < maxW) {
                W++; // increase the width of codewords
                L *= 2; // increase the number of codewords
                st.put(input.substring(0, t + 1), code++);
            }


            input = input.substring(t); // Scan past s in input.
        }
        BinaryStdOut.write(R, W);
        BinaryStdOut.close();
    }

    public static void expand() {
        L = 512;
        W = 9;

        String[] st = new String[65536]; // now has enough space for everything
        int i; // next available codeword value

        // initialize symbol table with all 1-character strings
        for (i = 0; i < R; i++)
            st[i] = "" + (char) i;
        st[i++] = ""; // (unused) lookahead for EOF

        int codeword = BinaryStdIn.readInt(W);
        if (codeword == R)
            return; // expanded message is empty string
        String val = st[codeword];

        while (true) {
            BinaryStdOut.write(val);

            // my stuff
            if (i + 1 > L && W < 16) {
                L *= 2;
                W++;
            }

            codeword = BinaryStdIn.readInt(W);
            if (codeword == R)
                break;
            String s = st[codeword];
            if (i == codeword)
                s = val + val.charAt(0); // special case hack
            if (i < L)
                st[i++] = val + s.charAt(0);
            val = s;
        }
        BinaryStdOut.close();
    }
}
```
## Description
The goal of this problem was to take the prewritten LZW compression algorithm and configure it to use variable-length encoding, allowing it to start compression with smaller codewords and make them longer as the file got longer and the codebook filled up.
The way to do this was by checking if the number of codewords we already have is greater than the maximum possible with the current bit length (for example, if we have more than 2^9 codewords when the bit length is only 9).
Once the number of codewords reaches that threshold, I increase the bit length of each new code word by 1, and naturally double the number of possible codewords that can be stored in the symbol table.
This works well in both methods, allowing longer and longer files to be compressed more efficiently by increasing the bit lengths as needed.

## Time and Space Complexity
The compress method has O(n^2) runtime because the substring method copies all of the remaining input, which is about n operations per loop.
The expand method has O(n) runtime because each loop does work for every character in the string that gets read in at the top of the loop, so each character is processed about once.

For space, the compress is O(n) for the input size plus the tree, which has a constant space independent of n.
The expand method is also O(n) because I created an array with 65,536 references and the number of strings it stores should add up to about n characters.

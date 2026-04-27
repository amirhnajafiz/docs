# Sed

To replace all occurrences of a string within a file in Linux, the sed (stream editor) command is commonly used.

To replace all occurrences of "old-string" with "new-string" in a file named yourfile.txt, use the following command:

```bash
sed -i 's/old-string/new-string/g' yourfile.txt
```

Explanation:

- sed: The command for the stream editor.
- -i: This option specifies that the changes should be made "in place," meaning the original file will be modified directly. Without this, sed would print the modified content to standard output.
- 's/old-string/new-string/g': This is the substitution command.
- s: Indicates the substitute command.
- /old-string/: The regular expression representing the string to be found.
- /new-string/: The string that will replace the found string.
- /g: The "global" flag, which ensures that all occurrences of "old-string" on each line are replaced, not just the first one.
- yourfile.txt: The name of the file you want to modify.

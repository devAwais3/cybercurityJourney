# Bandit Level 7 → Level 8
*Maintained by Muhammad Awais*

## 1. Overview

This level introduces text searching in Linux using the `grep` command. The objective is to find a specific word inside a file containing a large amount of text and retrieve the password associated with it.

- **Platform:** OverTheWire Bandit
- **Level:** 7 → 8
- **Difficulty:** Beginner
- **Operating System:** Kali GNU/Linux 2026.3 (VM)
- **Connection:** SSH (Port 2220)

## 2. Goal

The password for the next level is stored in the file `data.txt`, next to the word `millionth`.

The task is to search the file and identify the line containing the specified word.

## 3. Approach

1. Connected to the Bandit server as `bandit7` using SSH.
2. Used `ls` to check the available files in the home directory.
3. Used `cat` to inspect the contents of `data.txt`.
4. Used `grep` to search for the word `millionth`.
5. Retrieved the password from the matching line.

## 4. Commands Used

**List files in the current directory:**

```bash
ls
```

**Find line numbers of a large file before displaying it:**

```bash
wc -l data.txt
```

**Search for the word millionth:**

```bash
cat data.txt | grep -i "millionth"
```

Connect to the next level:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

## 5. Explanation

### Understanding the grep Command

`grep` is a Linux command-line utility used to search for specific words, patterns, or text inside files.

General syntax:

```bash
grep [options] "pattern" filename
```

In this level, the command used was:

```bash
cat data.txt | grep -i "millionth"
```

Breaking it down:

- `cat data.txt`: Displays the contents of the file.
- `|`: The pipe operator sends the output of the first command as input to the next command.
- `grep`: Searches the received text for a matching pattern.
- `-i`: Makes the search case-insensitive, so it matches `millionth`, `Millionth`, or `MILLIONTH`.
- `"millionth"`: The word being searched for.

**Important Concept:**

The pipe operator (`|`) allows multiple Linux commands to work together. Instead of displaying all the file contents, we can pass the output of `cat` directly to `grep` and display only matching lines.

### A Simpler Alternative

Since `grep` can read files directly, the same search can be performed without using `cat` or the pipe operator:

```bash
grep -i "millionth" data.txt
```

This is shorter and more efficient for searching inside a file.

## 6. Result

Successfully used `grep` to search for the word `millionth` inside `data.txt`.

The matching line displayed the password required to access Bandit Level 8.

![Bandit Level 7 to 8](assets/Screenshot-1.png)

## 7. Key Takeaway

- Learned how to search for specific text using `grep`.
- Understood case-insensitive searching with the `-i` option.
- Practised combining commands using the pipe (`|`) operator.
- Learned that `grep` can read directly from a file without requiring `cat`.
- Understood how to extract relevant information from a file containing many lines.

## Helpful Resources

- [OverTheWire – Bandit Level 8](https://overthewire.org/wargames/bandit/bandit8.html)
- [grep Manual](https://manpages.ubuntu.com/manpages/noble/man1/grep.1.html)
- [Bash Pipelines](https://www.gnu.org/software/bash/manual/html_node/Pipelines.html)
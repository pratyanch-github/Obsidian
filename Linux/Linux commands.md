# **Linux Terminal Basics: Input/Output Redirection Cheat Sheet**  

## **1. Basic Redirection**
### **Output to File (Overwrite)**
```bash
command > file.txt        # Overwrites file.txt with command's output
```
**Example:**  
```bash
ls > files_list.txt       # Saves directory listing to files_list.txt
```

### **Output to File (Append)**
```bash
command >> file.txt       # Adds output to the end of file.txt
```
**Example:**  
```bash
date >> log.txt           # Appends current date to log.txt
```

### **Input from File**
```bash
command < file.txt        # Uses file.txt as input instead of keyboard
```
**Example:**  
```bash
wc -w < document.txt      # Counts words in document.txt
```

---

## **2. Combining Commands**
### **Pipe (`|`) - Send Output to Another Command**
```bash
command1 | command2       # command1's output → command2's input
```
**Example:**  
```bash
ls | grep ".txt"          # Lists only .txt files
```

### **Chaining Commands**
```bash
cmd1 ; cmd2               # Runs cmd1, then cmd2 (always runs both)
cmd1 && cmd2              # Runs cmd2 only if cmd1 succeeds
cmd1 || cmd2              # Runs cmd2 only if cmd1 fails
```
**Examples:**  
```bash
mkdir folder && cd folder # Creates folder and enters it only if successful
cat file.txt || echo "File not found!"  # Shows error if file.txt doesn't exist
```

---

## **3. Advanced Redirection**
### **Redirect Errors (`2>`)**
```bash
command 2> error.log      # Saves errors to error.log
```
**Example:**  
```bash
ls /wrongpath 2> errors.txt  # Logs "No such file" errors
```

### **Redirect Both Output & Errors (`&>`)**
```bash
command &> all_output.log # Saves both output and errors
```
**Example:**  
```bash
python script.py &> log.txt  # Logs everything
```

---

## **4. Here Documents (`<<EOF`) for Multi-Line Input**
```bash
cat <<EOF >> file.txt  
Line 1  
Line 2  
EOF                     # Appends multiple lines to file.txt
```
**Example:**  
```bash
cat <<CONFIG >> settings.conf  
username=admin  
password=1234  
CONFIG
```

---

## **5. Common Mistakes Fixed**
❌ **Wrong:** `cat < echo "text" >> file.txt`  
✅ **Correct:** `echo "text" >> file.txt`  

❌ **Wrong:** `cat < file1 file2 > output.txt`  
✅ **Correct:** `cat file1 file2 > output.txt`  

---

## **Summary Table**
| **Syntax** | **Effect**                 | **Example**                    |     |              |
| ---------- | -------------------------- | ------------------------------ | --- | ------------ |
| `>`        | Overwrite file with output | `ls > files.txt`               |     |              |
| `>>`       | Append to file             | `date >> log.txt`              |     |              |
| `<`        | Read input from file       | `sort < data.txt`              |     |              |
| `2>`       | Redirect errors            | `cmd 2> errors.log`            |     |              |
| `&>`       | Redirect output + errors   | `cmd &> all.log`               |     |              |
| `          | `                          | Pipe output to another command | `ls | grep ".txt"` |
| `<<EOF`    | Insert multi-line input    | `cat <<EOF > note.txt`         |     |              |

---

### **Final Tips**
✔ Use `man command` (e.g., `man cat`) for help  
✔ Test redirections with harmless commands (`ls`, `echo`) first  
✔ Avoid `>` on important files (it overwrites!)  

Now you can chain commands like a pro! 🚀 Practice these, and you'll master the terminal.

### Key Property of `cat`:
- It takes input from either:
  - Files you specify as arguments (`cat file.txt`)
  - Standard input (if no files given)
- It outputs to standard output (your terminal by default)

Here's a detailed **File & Text Operations** command reference table with common variants:

---

### **File Operations Master Table**

| **Command** | **Syntax**                     | **Effect**                                      | **Common Options**              | **Example**                                  |
|-------------|--------------------------------|------------------------------------------------|---------------------------------|---------------------------------------------|
| **cp**      | `cp [OPTIONS] SOURCE DEST`     | Copy files/directories                         | `-r` (recursive), `-i` (prompt), `-v` (verbose) | `cp -rv dir1/ dir2/` (copy dir recursively) |
|             | `cp file1 file2`               | Copy file1 to file2                            |                                 | `cp notes.txt backup.txt`                  |
|             | `cp *.txt /backup`             | Copy all .txt files to /backup                 |                                 | `cp -i *.log ~/logs/` (prompt before overwrite) |
| **mv**      | `mv [OPTIONS] SOURCE DEST`     | Move/rename files                              | `-n` (no overwrite), `-v` (verbose) | `mv -v old.txt new.txt` (rename with feedback) |
|             | `mv dir1/ dir2/`               | Move directory (if dir2 exists)                |                                 | `mv /tmp/*.png ~/Pictures/`               |
| **rm**      | `rm [OPTIONS] FILE`            | Delete files                                   | `-r` (recursive), `-f` (force)  | `rm -rf old_dir/` (force-delete directory) |
|             | `rm -- -weirdfile`             | Delete files with '-' prefix                   | `--` (end options)              | `rm -- -myfile.txt`                       |
| **chmod**   | `chmod [OPTIONS] MODE FILE`    | Change file permissions                        | `-R` (recursive)                | `chmod 755 script.sh` (rwx for owner, rx others) |
|             | `chmod u+x file`               | Add execute permission for owner               | `u=user, g=group, o=others`     | `chmod g-w shared_file.txt` (remove group write) |

---

### **Text Operations Master Table**

| **Command** | **Syntax**                     | **Effect**                                      | **Common Options**              | **Example**                                  |
|-------------|--------------------------------|------------------------------------------------|---------------------------------|---------------------------------------------|
| **cat**     | `cat [OPTIONS] FILE`           | Display file contents                          | `-n` (number lines), `-b` (number non-blanks) | `cat -n notes.txt`                         |
|             | `cat file1 file2 > combined`   | Concatenate files                              |                                 | `cat *.log > all_logs.txt`                 |
| **grep**    | `grep [OPTIONS] PATTERN FILE`  | Search text patterns                           | `-i` (ignore case), `-r` (recursive), `-v` (invert match) | `grep -ri "error" /var/log/` |
|             | `grep -E "pattern1\|pattern2"` | Extended regex (OR condition)                  | `-E` (extended regex)           | `grep -E "404\|500" access.log`            |
| **sed**     | `sed 's/old/new/' FILE`        | Stream editor (find/replace)                   | `-i` (in-place edit)            | `sed -i 's/foo/bar/g' file.txt`            |
|             | `sed '/pattern/d' FILE`        | Delete lines matching pattern                  |                                 | `sed '/^#/d' config.cfg` (remove comments) |
| **awk**     | `awk '/pattern/ {action}' FILE` | Pattern scanning and processing               | `-F` (set field separator)      | `awk -F: '{print $1}' /etc/passwd`        |
|             | `awk '{print NF}' FILE`        | Print number of fields per line                |                                 | `awk '{sum+=$3} END{print sum}' data.csv`  |
| **head**    | `head [OPTIONS] FILE`          | Show first lines of file                       | `-n NUM` (number of lines)      | `head -n 5 large_file.log`                |
| **tail**    | `tail [OPTIONS] FILE`          | Show last lines of file                        | `-f` (follow changes)           | `tail -f /var/log/syslog` (live monitoring) |
| **sort**    | `sort [OPTIONS] FILE`          | Sort lines                                     | `-r` (reverse), `-u` (unique)   | `sort -nr data.txt` (numeric reverse)      |
| **uniq**    | `uniq [OPTIONS] FILE`          | Filter adjacent duplicates                     | `-c` (count occurrences)        | `sort file.txt \| uniq -c`                |

---

### **Key Variations & Pro Tips**
1. **Safety First**:
   - Always use `-i` with `rm`/`cp`/`mv` for prompts:  
     ```bash
     alias cp='cp -i'   # Add to ~/.bashrc to make permanent
     ```
   - Use `--preserve=all` with `cp` to keep metadata

2. **Text Processing Combos**:
   ```bash
   # Count unique IPs in a log:
   grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' access.log | sort | uniq -c | sort -nr
   ```

3. **Permission Shortcuts**:
   ```bash
   chmod +x script.sh    # Quick executable permission
   chmod a-w file.txt    # Remove write for ALL (user+group+others)
   ```

4. **Undo Protection**:
   ```bash
   # Make backup before mass edits:
   sed -i.bak 's/old/new/g' file.txt  # Creates file.txt.bak
   ```

--- 

Would you like me to add any specific advanced use cases?
# Reverse

## Nanocombattant

### Difficile

```py
import subprocess

def execute_program(i, j):
    global found, max_count, best_char_candidate
    # Replace 'your_program' with the actual command to execute your program
    process = subprocess.Popen(['strace', './nanocombattant'], stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)

    # Send input to the program
    user_input = found + "a"*(19-len(found))
    string_list = list(user_input)
    string_list[i] = chr(j)
    user_input = "".join(string_list)
    
    out, err = process.communicate(user_input)

    count = err.count("PTRACE_SETREGS")
    
    char = ""
    if count > max_count:
        #print("({}: char, count): ({}; {})".format(i, chr(j), count))
        best_char_candidate = chr(j)
        max_count = count

    # Close the process
    process.terminate()
    
    return char

if __name__ == "__main__":
    found = ""
    for i in range(19):
        max_count = 0
        best_char_candidate = ""
        for j in range(32, 127):
            execute_program(i, j)
        found += best_char_candidate
    print("flag: ", found)
```

**404CTF{fi3r_n4n0comb4ttant}**

# Reverse

## Nanocombattant

### Difficile

1. L'input doit faire 19 caractères
2. Le père copie du code dans les variables "buffer1" et "buffer2"
3. Il spawn 2 processus fils et se met en attente du 1er
4. Le 1er processus fait appel à PTRACE_TRACEME et exécute le code de "buffer1" avec l'input en argument
5. Le 2e processus fait appel à PTRACE_TRACEME et exécute le code de "buffer2" (sans paramètre ? à vérifier)
6. Quand le code de "buffer1" déclenche un SIGTRAP le père reprend la main
7. Le père fait les choses suivantes:
	- Il se met en attente du 2e fils
	- Quand le code de "buffer2" déclenche un SIGTRAP le père reprend la main
	- Il récupère les registres du 2e fils, les modifie et lui rend le contrôle
	- Il rend le contrôle au 1er fils, incrémente "cpt" et se met en attente du 1er
	- Quand le code de "buffer1" déclenche un SIGTRAP le père reprend la main
	- Il récupère les registres du 1er fils, les modifie et lui rend le contrôle
	- Si "cpt" est égal à 19 (si tous les caractères de l'input ont été vérifiés correctement) => c'est gagné

<p align="center">
	<img src="https://github.com/SamNzo/CTFs/blob/main/404CTF/reverse/img/nanocombattants_father_child1.drawio.png?raw=true">
</p>
Registres correspondants aux variables de father_child1

<p align="center">
	<img src="https://github.com/SamNzo/CTFs/blob/main/404CTF/reverse/img/nanocombattants_father_child2.drawio.png?raw=true">
</p>
Registres correspondants aux variables de father_child2

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

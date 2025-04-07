# FCSC 2025
## Pré-chall

Dans le code source de la page principale du site (https://fcsc.fr) on trouve ce joli dessin.
```
    /--------------------------\      
   |       Hello Friend,        |
   |   Welcome to FCSC 2025 \o/ |
   |   Let's start the prechall |
   |         at /teasing        |
    \--------------------------/      
            \                      
             \                      
              \_ .~q`,
                 {__,  \
                     \' \
                      \  \
                       \  \
                        \  `._            __.__
                         \    ~-._  _.==~~     ~~--.._
                          \        '                  ~-.
                           \      _-   -_                `.
                            \    /       }        .-    .  \
                             `. |      /  }      (       ;  \
                               `|     /  /       (       :   '\
                                \    |  /        |      /       \    =
                                 |     /`-.______.\     |^-.      \
                                 |   |/           (     |   `.      \_
                                 |   ||            ~\   \      '._    `-.._____..----.._=__
                                 |   |/             _\   \      =~-.__________.-~~~~~~~~~'''
                               .o'___/            .o______}  
```

A l'adresse indiquée https://fcsc.fr/teasing on a 3 épreuves à réussir pour avoir le flag avec cette commande:
```
echo -n "FCSC{flag1/3}" "FCSC{flag2/3}" "FCSC{flag3/3}" | sha256sum | sed 's/ .*$/}/; s/^/FCSC{/'
```

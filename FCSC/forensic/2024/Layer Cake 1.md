# Layer Cake 1/3
## Forensic
### Intro

voir https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/docker-forensics

```shell
┌──(kali㉿kali)-[~]
└─$ sudo docker history --no-trunc anssi/fcsc2024-forensics-layer-cake-1
IMAGE                                                                     CREATED        CREATED BY                                                                                          SIZE      COMMENT
sha256:0faa62781dd1db0ebb6cd83836bb4ba24f8b58b0cd761ac0cbae426bccc7666f   2 months ago   CMD ["/bin/sh"]                                                                                     0B        buildkit.dockerfile.v0
<missing>                                                                 2 months ago   USER guest                                                                                          0B        buildkit.dockerfile.v0
<missing>                                                                 2 months ago   ARG FIRST_FLAG=FCSC{a1240d90ebeed7c6c422969ee529cc3e1046a3cf337efe51432e49b1a27c6ad2}               0B        buildkit.dockerfile.v0
<missing>                                                                 2 months ago   /bin/sh -c #(nop)  CMD ["/bin/sh"]                                                                  0B        
<missing>                                                                 2 months ago   /bin/sh -c #(nop) ADD file:37a76ec18f9887751cd8473744917d08b7431fc4085097bb6a09d81b41775473 in /    7.38MB 
```

**FCSC{a1240d90ebeed7c6c422969ee529cc3e1046a3cf337efe51432e49b1a27c6ad2}**

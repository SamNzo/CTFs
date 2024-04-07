# Layer Cake 2/3
## Forensic
### Intro

```shell
┌──(kali㉿kali)-[~/Documents/forensic]
└─$ sudo docker history --no-trunc anssi/fcsc2024-forensics-layer-cake-2                                              
IMAGE                                                                     CREATED        CREATED BY                                                                                          SIZE      COMMENT
sha256:03014d9fc4801b1810b112fd53e05e35ea127e55c82d1304b5622cfe257c0ad8   13 days ago    CMD ["/bin/sh"]                                                                                     0B        buildkit.dockerfile.v0
<missing>                                                                 13 days ago    USER guest                                                                                          0B        buildkit.dockerfile.v0
<missing>                                                                 13 days ago    RUN /bin/sh -c rm /tmp/secret # buildkit                                                            0B        buildkit.dockerfile.v0
<missing>                                                                 13 days ago    COPY secret /tmp # buildkit                                                                         71B       buildkit.dockerfile.v0
<missing>                                                                 2 months ago   /bin/sh -c #(nop)  CMD ["/bin/sh"]                                                                  0B        
<missing>                                                                 2 months ago   /bin/sh -c #(nop) ADD file:37a76ec18f9887751cd8473744917d08b7431fc4085097bb6a09d81b41775473 in /    7.38MB
```
on voit le fichier /tmp/secret etre supprimé

avec dive aussi on peut voir le fichier mais pas contenu

```shell
┌──(kali㉿kali)-[~/Documents/forensic]
└─$ sudo docker inspect anssi/fcsc2024-forensics-layer-cake-2                                             
[
    {
        "Id": "sha256:03014d9fc4801b1810b112fd53e05e35ea127e55c82d1304b5622cfe257c0ad8",
        "RepoTags": [
            "anssi/fcsc2024-forensics-layer-cake-2:latest"
        ],
        "RepoDigests": [
            "anssi/fcsc2024-forensics-layer-cake-2@sha256:86a863f674adbbae9168d1a5d233478cd9747a587a322b8950fcb39f3992be7a"
        ],
        "Parent": "",
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2024-03-25T10:05:42.229491951+01:00",
        "Container": "",
        "ContainerConfig": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": null,
            "Cmd": null,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "DockerVersion": "",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "guest",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh"
            ],
            "ArgsEscaped": true,
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "com.docker.compose.project": "fcsc2024-forensics-layer-cake",
                "com.docker.compose.service": "layer2",
                "com.docker.compose.version": "2.23.1"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 7377145,
        "VirtualSize": 7377145,
        "GraphDriver": {
            "Data": {   TODO: REGARDER ICI
                "LowerDir": "/var/lib/docker/overlay2/6521d7550c525fa1797010eb2fc5bb88a16020027ed1a602ce2f051f7955eb30/diff:/var/lib/docker/overlay2/0e588bc9a7b6e79f9c7969477a44dafdff87bca001ec6dee20aca96e8f5ed31a/diff",
                "MergedDir": "/var/lib/docker/overlay2/2b5d8dd722733333e8c7d0ab7cf6535670e570e6d8a188338dacefd154253c4d/merged",
                "UpperDir": "/var/lib/docker/overlay2/2b5d8dd722733333e8c7d0ab7cf6535670e570e6d8a188338dacefd154253c4d/diff",
                "WorkDir": "/var/lib/docker/overlay2/2b5d8dd722733333e8c7d0ab7cf6535670e570e6d8a188338dacefd154253c4d/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:d4fc045c9e3a848011de66f34b81f052d4f2c15a17bb196d637e526349601820",
                "sha256:eebed19322aaa0082058596cc4cff6c33253f1ce4327e9ae4399edb2f657242e",
                "sha256:fe62c480fd0c4bba858571806e7474fa5aa061ce78292de1988db0cd54d494b6"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]

┌──(kali㉿kali)-[~/Documents/forensic]
└─$ sudo cat /var/lib/docker/overlay2/6521d7550c525fa1797010eb2fc5bb88a16020027ed1a602ce2f051f7955eb30/diff/tmp/secret
FCSC{b38095916b2b578109cbf35b8be713b04a64b2b2df6d7325934be63b7566be3b}
```

**FCSC{b38095916b2b578109cbf35b8be713b04a64b2b2df6d7325934be63b7566be3b}**

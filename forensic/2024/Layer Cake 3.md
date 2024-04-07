# Layer Cake 3
## Forensic
### Intro

```shell
┌──(kali㉿kali)-[~]
└─$ sudo docker inspect anssi/fcsc2024-forensics-layer-cake-3
[
    {
        "Id": "sha256:269cd0c184df7781e86c030d8270e686b3f07ef203f56f209370ac0ad674ef35",
        "RepoTags": [
            "anssi/fcsc2024-forensics-layer-cake-3:latest"
        ],
        "RepoDigests": [
            "anssi/fcsc2024-forensics-layer-cake-3@sha256:f11c3351c870c7839ce1a266c71307ae11de11b9261137e89b32fca07ba457e4"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "1970-01-01T00:00:01Z",
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
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [],
            "Cmd": [  TODO: interessant
                "/nix/store/m8ww0n3iqndg8zaiwbsnij6rvmpmjbry-hello/bin/hello"
            ],
            "Image": "",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 34210387,
        "VirtualSize": 34210387,
        "GraphDriver": {
            "Data": {
                "MergedDir": "/var/lib/docker/overlay2/a73c1912c181cf8583b2b00506e721e7bb9db93f8461bcae8bcfc808687b92cf/merged",
                "UpperDir": "/var/lib/docker/overlay2/a73c1912c181cf8583b2b00506e721e7bb9db93f8461bcae8bcfc808687b92cf/diff",
                "WorkDir": "/var/lib/docker/overlay2/a73c1912c181cf8583b2b00506e721e7bb9db93f8461bcae8bcfc808687b92cf/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:8ea6eb4812d48d7aee7de57a65ba99e4d3c3958fee6eb973419cf7aace4c7fec"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```

```shell
┌──(kali㉿kali)-[~]
└─$ sudo cat /var/lib/docker/overlay2/a73c1912c181cf8583b2b00506e721e7bb9db93f8461bcae8bcfc808687b92cf/diff/nix/store/m8ww0n3iqndg8zaiwbsnij6rvmpmjbry-hello/bin/hello 
#!/nix/store/5lr5n3qa4day8l1ivbwlcby2nknczqkq-bash-5.2p26/bin/bash
exec /nix/store/rnxji3jf6fb0nx2v0svdqpj9ml53gyqh-hello-2.12.1/bin/hello -g "FCSC{c12d9a48f1635354fe9c32b216f144ac66f7b8466a5ac82a35aa385964ccbb61}" -t
```

**FCSC{c12d9a48f1635354fe9c32b216f144ac66f7b8466a5ac82a35aa385964ccbb61}**

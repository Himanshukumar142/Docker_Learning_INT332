# Docker_Learning_INT332

Microsoft Windows [Version 10.0.26200.8037]
(c) Microsoft Corporation. All rights reserved.

C:\Users\hroya>docker volume create mydata
mydata

C:\Users\hroya>docker volume ls
DRIVER    VOLUME NAME
local     91b411169a9cec9c622127de5be707d95d95ae2b663e1ccada8c6d4fd091cf41
local     5768f1ea9dd1371a9587185f011f48687b142415c7cb2792d806d39dc941852b
local     7806f26177b580e89597d4aeead40d5669cbdfc2a70c7e26f7f1c4134dcdfd7d
local     a4f84bd2f3fdc7854cc969189408112164a60c442c09da8eb9d10f8c1c048466
local     mydata

C:\Users\hroya>docker volume inspect mydata
[
    {
        "CreatedAt": "2026-04-01T06:58:01Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mydata/_data",
        "Name": "mydata",
        "Options": null,
        "Scope": "local"
    }
]

C:\Users\hroya>docker run -dit -v mydata:/app/data --name container1
docker: 'docker run' requires at least 1 argument

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

See 'docker run --help' for more information

C:\Users\hroya>docker run -dit -v mydata:/app --name container1
docker: 'docker run' requires at least 1 argument

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

See 'docker run --help' for more information

C:\Users\hroya>docker run -dit -v mydata:/app --name container1 ubuntu
fb9788ff2fcc85b299cc091719869a37fbcbd6c2619bebe2b0a18de89780c4fc

C:\Users\hroya>docker exec -it container1 bash
root@fb9788ff2fcc:/# echo "hello Docker volume" > /app/file.txt
root@fb9788ff2fcc:/# cat /app/file.txt
hello Docker volume
root@fb9788ff2fcc:/# exit
exit

C:\Users\hroya>docker rm -f container1
container1

C:\Users\hroya>docker run -it -v mydata:/app ubuntu bash
root@bef80e0f0886:/# cat /app/file.txt
hello Docker volume
root@bef80e0f0886:/# exit
exit

C:\Users\hroya>docker volume rm mydata
Error response from daemon: remove mydata: volume is in use - [bef80e0f0886feb6a56feb0651bb2c09cd19597b6aef9ab157c4965218275a6b]

C:\Users\hroya>docker volume prune
WARNING! This will remove anonymous local volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
Total reclaimed space: 0B

C:\Users\hroya>docker volume ls
DRIVER    VOLUME NAME
local     91b411169a9cec9c622127de5be707d95d95ae2b663e1ccada8c6d4fd091cf41
local     5768f1ea9dd1371a9587185f011f48687b142415c7cb2792d806d39dc941852b
local     7806f26177b580e89597d4aeead40d5669cbdfc2a70c7e26f7f1c4134dcdfd7d
local     a4f84bd2f3fdc7854cc969189408112164a60c442c09da8eb9d10f8c1c048466
local     mydata

C:\Users\hroya>docker volume rm mydata
Error response from daemon: remove mydata: volume is in use - [bef80e0f0886feb6a56feb0651bb2c09cd19597b6aef9ab157c4965218275a6b]

C:\Users\hroya>docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

C:\Users\hroya>docker rm bef80e0f0886feb6a56feb
bef80e0f0886feb6a56feb

C:\Users\hroya>docker volume rm mydata
mydata

C:\Users\hroya>docker volume ls
DRIVER    VOLUME NAME
local     91b411169a9cec9c622127de5be707d95d95ae2b663e1ccada8c6d4fd091cf41
local     5768f1ea9dd1371a9587185f011f48687b142415c7cb2792d806d39dc941852b
local     7806f26177b580e89597d4aeead40d5669cbdfc2a70c7e26f7f1c4134dcdfd7d
local     a4f84bd2f3fdc7854cc969189408112164a60c442c09da8eb9d10f8c1c048466

C:\Users\hroya>

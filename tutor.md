d build -t node .
d ps -a | awk '{print $1}' | xargs sudo docker.io rm

d run -i --name=n1 -t node
d inspect n1
ssh root@10.0.0.13
eval `ssh-agent`
ssh-add id_rsa

# ping all hosts
ansible all -m ping

# ping specific group
ansible all -m ping

ansible all -a "ls -lah" -f 1

# run custom command on app group 3 in parallel
ansible all -a "ls -lah" -f 3


# shell commands using module shell

ansible raleigh -m shell -a 'echo $TERM'

# copy files on all app nodes
ansible app -m copy -a "src=tmp dest=/tmp/files"
ansible app -a "ls /tmp/files"


ansible all -m file -a "dest=/srv/foo/a.txt mode=600"
ansible all -m file -a "dest=/srv/foo/b.txt mode=600owner=mdehaan group=mdehaan"
ansible all -m file -a "dest=/path/to/c mode=755 owner=mdehaan group=mdehaan state=directory"
ansible all -m file -a "dest=/path/to/c state=absent"


ansible app -m apt -a "name=curl state=present"
ansible app -m apt -a "name=nginx state=present"
ansible app -m service -a 'name=nginx status=started'
ansible app -m shell -a 'curl localhost'

### Testing role 'jpnewman.elk-filebeat' template

~~~
mkdir tmp

ansible-playbook ./test_template.yml -i "127.0.0.1," -c local -vvv
~~~

#### With test data

~~~
ansible-playbook ./test_template.yml -i "127.0.0.1," -c local --extra-vars "varfile=./defaults/main_proxy.yml" -vvv
~~~

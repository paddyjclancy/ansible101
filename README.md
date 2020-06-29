# Setting up Ansible

1) Vagrant init
2) Vagrant file:

```
Vagrant.config ("2") do |config|
	
  app.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
  end
```

3) touch playbook.yml

```
---

- host: [APP]
  remote_user: [SUDO]
  become: true
  task:
  - name: ensure nginx is at the latest version
    apt:
      name: nginx
      state: latest
  - name: start nginx
    service: 
      name: nginx
      state: started
    become: yes
  - name: copy in app folder
    copy:
      src: ./app/
      dest: /home/ubuntu/app-from-playbook/
```

4) vagrant up
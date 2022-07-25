# Laboratório kubernetes com Vagrant + ansible

Uma base inicial para rodar um pequeno cluster baseado em maquinas virtuais usando ***Vagrant***.

Também é usado ```ansible``` para o gerenciamento de configuração de todo nosso lab.

## Dependências
- Vagrant
- ansible

## Vagrant

O HashiCorp Vagrant é usado para criar e manter ambientes de desenvolvimento virtuais, para isso pode ser utilizado:
- VirtualBox
- KVM
- Hyper-V
- Docker containers
- VMware
- AWS

Com ele será mas rápido subir VMs e manter uma gerência de configuração das virtualizações para aumentar a produtividade do desenvolvimento.

Uma coisa legal de se usar vagrant é poder manter nossos Labs usando ***infraestructure as code***

## Como usar?

### Passo 1
Para criar as maquinas use: ***vagrant up***
Se tudo correr bem, um diretorio .vagrant será criado, navege nele até o diretorio ```.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory```
### Passo 2 
Copie este arquivo ***vagrant_ansible_inventory*** renomeando o arquivo para ***inventory***.

> cp .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory inventory

### Passo 3
Verifique o conteudo do arquivo ***inventory***. Nele está os IPs das máquinas que foram provisionadas pelo vagrant. Agora copie e guarde o valor do endereço IP da maquina ***masternode1***, vamos precisar deste endereço.

### Passo 4
Abra o arquivo da playbook ***kubernetes.yaml*** e também ***roles/kubernetes/defaults/main.yml*** procure a variável ***kubernetes_master*** e cole o valor do IP copiado no passo anterior em ambos os arquivos e salve.

```
    kubernetes_master: 192.168.121.107
```

### Passo 5
Para provisionar o nosso ***cluster kubernetes*** vamos usar a playbook ***kubernetes.yaml***.  Esta playbook ira rodar algumas roles, que estão no diretrório ```roles/```, vejamos:

> tree roles -L 2
```
roles
├── common
│   ├── defaults
│   ├── files
│   ├── tasks
│   └── templates
└── kubernetes
    ├── defaults
    ├── files
    └── tasks
```

### Passo 6

Execute a playbook. 

> ansible-playbook -u vagrant -i inventory kubernetes.yaml
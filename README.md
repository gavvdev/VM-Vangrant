# VM Vagrant - Apache2

Projeto de configuração de uma máquina virtual com Vagrant, provisionada automaticamente para instalar e executar o servidor Apache2.

## O que foi feito

- Criação de um `Vagrantfile` versionado no repositório
- Definição da máquina virtual: `ubuntu/jammy64`
- Definição da porta: redirecionamento da porta 80 (guest) para a porta 8080 (host)
- Provisionamento automático via shell script, instalando e iniciando o Apache2
- Teste de acesso ao servidor pelo navegador na porta definida

## Como rodar

Pré-requisitos: [Vagrant](https://www.vagrantup.com/) e [VirtualBox](https://www.virtualbox.org/) instalados.

```bash
git clone https://github.com/gavvdev/VM-Vangrant.git
cd VM-Vangrant
vagrant up
```

Aguarde o provisionamento terminar. O Apache2 será instalado e iniciado automaticamente dentro da VM.

## Acessando o servidor

Após o `vagrant up` finalizar, acesse no navegador:
http://localhost:8080


Deve aparecer a página padrão do Apache2 ("Apache2 Ubuntu Default Page").

## Outros comandos úteis

```bash
vagrant ssh              # acessa a VM
vagrant status            # verifica se a VM está rodando
vagrant reload             # reinicia a VM e reaplica o Vagrantfile
vagrant halt               # desliga a VM
vagrant destroy             # remove a VM
```

## Vagrantfile

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
    systemctl start apache2
    systemctl enable apache2
  SHELL
end
```

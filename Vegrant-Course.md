### Curso de Vagrant

1. **Introdução ao Vagrant**
2. **Instalação e Configuração**
3. **Criando e Gerenciando Máquinas Virtuais**
4. **Provisionamento com Vagrant**
5. **Sincronização de Diretórios**
6. **Redes e Configurações**
7. **Projeto Final: Site Simples com Apache**

---

### 1. Introdução ao Vagrant

#### Arquivo: `README.md`

```markdown
# Curso de Vagrant

## Seção 1: Introdução ao Vagrant

### O que é Vagrant?

Vagrant é uma ferramenta para construir e gerenciar ambientes de desenvolvimento virtualizados. Ele fornece uma maneira fácil de configurar, compartilhar e provisionar ambientes de desenvolvimento, permitindo que desenvolvedores trabalhem em um ambiente consistente.

### Vantagens de Usar Vagrant

- Consistência nos ambientes de desenvolvimento.
- Facilidade de compartilhamento de ambientes.
- Automação da configuração e provisionamento.
- Suporte a vários provedores de virtualização (VirtualBox, VMware, AWS, etc.).

### Casos de Uso

- Desenvolvimento de software.
- Testes e integração contínua.
- Simulação de ambientes de produção.
```

---

### 2. Instalação e Configuração

#### Arquivo: `README.md`

````markdown
# Seção 2: Instalação e Configuração

### Instalando o Vagrant

1. Baixe e instale o Vagrant a partir do site oficial: [Download Vagrant](https://www.vagrantup.com/downloads).
2. Baixe e instale o VirtualBox: [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads).

### Configuração Inicial

1. Verifique se o Vagrant está instalado corretamente:
   ```bash
   vagrant --version
   ```
````

2. Verifique se o VirtualBox está instalado corretamente:

   ```bash
   VBoxManage --version
   ```

3. Crie um diretório para o projeto:

   ```bash
   mkdir curso-vagrant
   cd curso-vagrant
   ```

4. Inicialize um novo projeto Vagrant:
   ```bash
   vagrant init
   ```

````

---

### 3. Criando e Gerenciando Máquinas Virtuais

#### Arquivo: `README.md`

```markdown
# Seção 3: Criando e Gerenciando Máquinas Virtuais

### Criando uma Máquina Virtual
1. Edite o arquivo `Vagrantfile` gerado na configuração inicial:
   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/bionic64"
   end
````

2. Inicie a máquina virtual:

   ```bash
   vagrant up
   ```

3. Acesse a máquina virtual via SSH:
   ```bash
   vagrant ssh
   ```

### Comandos Básicos do Vagrant

- `vagrant up`: Inicia e provisiona a máquina virtual.
- `vagrant ssh`: Acessa a máquina virtual via SSH.
- `vagrant halt`: Desliga a máquina virtual.
- `vagrant destroy`: Destroi a máquina virtual.

````

---

### 4. Provisionamento com Vagrant

#### Arquivo: `README.md`

```markdown
# Seção 4: Provisionamento com Vagrant

### O que é Provisionamento?
Provisionamento é o processo de configurar automaticamente a máquina virtual após sua criação. Vagrant suporta vários métodos de provisionamento, incluindo Shell, Ansible, Chef e Puppet.

### Provisionamento com Shell Script
1. Crie um arquivo de script chamado `setup.sh`:
   ```bash
   #!/bin/bash
   sudo apt-get update
   sudo apt-get install -y apache2
````

2. Edite o `Vagrantfile` para usar o script de provisionamento:

   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/bionic64"
     config.vm.provision "shell", path: "setup.sh"
   end
   ```

3. Provisione a máquina virtual:
   ```bash
   vagrant up --provision
   ```

````

---

### 5. Sincronização de Diretórios

#### Arquivo: `README.md`

```markdown
# Seção 5: Sincronização de Diretórios

### Sincronização de Diretórios
Vagrant permite sincronizar diretórios entre o host e a máquina virtual. Isso facilita o desenvolvimento, pois alterações feitas no host são refletidas na máquina virtual.

### Configurando Sincronização
1. Edite o `Vagrantfile` para adicionar sincronização de diretórios:
   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/bionic64"
     config.vm.synced_folder "./data", "/var/www/html"
   end
````

2. Crie o diretório `data` no host:

   ```bash
   mkdir data
   ```

3. Coloque um arquivo `index.html` no diretório `data`:

   ```html
   <!DOCTYPE html>
   <html>
     <head>
       <title>Site Simples</title>
     </head>
     <body>
       <h1>Olá, Mundo!</h1>
     </body>
   </html>
   ```

4. Reinicie a máquina virtual para aplicar as mudanças:
   ```bash
   vagrant reload
   ```

````

---

### 6. Redes e Configurações

#### Arquivo: `README.md`

```markdown
# Seção 6: Redes e Configurações

### Configurando Redes
Vagrant permite configurar redes para a máquina virtual, como redes privadas e públicas.

### Configurando uma Rede Privada
1. Edite o `Vagrantfile` para adicionar uma rede privada:
   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/bionic64"
     config.vm.network "private_network", ip: "192.168.33.10"
   end
````

2. Reinicie a máquina virtual para aplicar as mudanças:

   ```bash
   vagrant reload
   ```

3. Acesse o site através do IP configurado:
   - Abra um navegador e vá para `http://192.168.33.10`

````

---

### 7. Projeto Final: Site Simples com Apache

#### Arquivo: `README.md`

```markdown
# Seção 7: Projeto Final: Site Simples com Apache

### Objetivo
Configurar um site simples que será servido pelo Apache de forma automatizada.

### Passo a Passo
1. Crie o arquivo `Vagrantfile`:
   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/bionic64"
     config.vm.network "private_network", ip: "192.168.33.10"
     config.vm.synced_folder "./data", "/var/www/html"
     config.vm.provision "shell", path: "setup.sh"
   end
````

2. Crie o script de provisionamento `setup.sh`:

   ```bash
   #!/bin/bash
   sudo apt-get update
   sudo apt-get install -y apache2
   ```

3. Crie o diretório `data` e adicione o arquivo `index.html`:

   ```html
   <!DOCTYPE html>
   <html>
     <head>
       <title>Site Simples</title>
     </head>
     <body>
       <h1>Olá, Mundo!</h1>
     </body>
   </html>
   ```

4. Inicie e provisione a máquina virtual:

   ```bash
   vagrant up
   ```

5. Acesse o site através do IP configurado:
   - Abra um navegador e vá para `http://192.168.33.10`

### Estrutura do Projeto

```
curso-vagrant/
│
├── data/
│   └── index.html
│
├── setup.sh
│
└── Vagrantfile
```

````

---

### Subindo o Projeto no GitHub

1. Crie um repositório no GitHub.
2. Clone o repositório no seu computador.
3. Adicione os arquivos do curso ao repositório.
4. Faça commit e push das mudanças.

#### Comandos Git

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/curso-vagrant.git
cd curso-vagrant

# Adicione os arquivos do curso
git add .

# Faça commit das mudanças
git commit -m "Adiciona curso completo de Vagrant"

# Envie as mudanças para o GitHub
git push origin master
````

---

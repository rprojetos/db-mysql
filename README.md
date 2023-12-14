# db-mysql

Linux - Ubuntu

## 1.Desinstalar MySQL Server no Ubuntu

### 1-1. Parar o MySQL Server

Verifique o status do mysql:

```
sudo systemctl status mysql
```

Se estiver operando [Status: "Server is operational"] , pare-o:

```
sudo systemctl stop mysql
```

Verifique o status novamente, e ele deverá estar parado. [Status: "Server shutdown complete"]

```
sudo systemctl status mysql
```



### 1-2. Desinstalar o MySQL Server

Para desinstalar os pacotes MySql, use o comando a seguir:

```
sudo apt purge mysql-server*
```

ou 

pode ser usado este comando abaixo para garantir que qualquer tipo de MySQL instalado em seu sistema seja desinstalado.

```
sudo apt purge mysql-server mysql-client mysql-common mysql-server-core-* mysql-client-core-*
```


### 1-3.Desinstalar banco de dados MySQL e arquivos de log

Execute as instruções abaixo para ver se há arquivo nos diretórios listados nos comandos:

```
ls /etc/mysql

sudo ls /var/lib/mysql
```

Execute o comando a seguir para excluir esses arquivos de configuração, chaves de segurança e arquivos de banco de dados.

```
sudo rm -r /etc/mysql /var/lib/mysql
```

### 1-4.Desinstalar dependências

Ao ser instalado o MySQL Sever, o gerenciador de pacotes também instala várias dependências adicionais necessárias para executar o servidor. Porém, como excluímos o pacote principal, MySQL Server, essas dependências não são mais necessárias e devem ser desinstaladas. Essas dependências são conhecidas como "Pacotes Órfãos", pois seu pacote pai foi excluído e esses pacotes não são mais úteis. 

Execute o seguinte comando apt abaixo, para remover essas dependências.

```
sudo apt autoremove
```

O servidor MySQL foi completamente desinstalado do seu sistema operacional Ubuntu.


## 2.Instalar MySQL Server no Ubuntu

### 2-1. Instalando o MySQL Server

Atualize o índice do pacote em seu servidor, caso não tenha feito isso recentemente:

```
sudo apt update
```

Instale o pacote MySQL Server

```
sudo apt install mysql-server
```

Certifique-se de que o servidor esteja em execução usando o comando systemctl start:

```
sudo systemctl start mysql.service
```

```
sudo systemctl status mysql
```

### 2-1. Configurando o MySQL Server

Abra o prompt do MySql:

```
sudo mysql
```

Execute o comando **ALTER USER** para alterar o método de autenticação do usuário root para um que use uma senha:

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

Após alteração feche o prompt MySql:

```
exit
```

Rode o script de segurança com sudo:

```
sudo mysql_secure_installation
```

Iniciará alguns questionários, da CLI do MySql:

```
Securing the MySQL server deployment.

Enter password for user root: "Digite a senha definida no 2º comando do item 2.1"
```

O VALIDATE PASSWORD COMPONENT será utilizado para melhorar a segurança com senhas:

```
VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: y  <----------escolhemos aqui "y"
```

No próximo questionário escolhemos o nível de segurança e podemos alterar a senha root do MySql:

```
LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 0
Using existing password for root.

Estimated strength of the password: 50 
Change the password for root ? ((Press y|Y for Yes, any other key for No) : y <--- alterar senha root

New password: 

Re-enter new password: 

```

Agora podemos escolher continuar com a nova senha root fornecida:

```
Estimated strength of the password: 50 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
```

Para as próximas questões podemos responder "y" e `<ENTER>`


Para autenticar como usuário root no MySql, use o comando abaixo:

```
sudo mysql -u root -p
```


## Referências:

ref.: [How to properly uninstall MySQL Server in Ubuntu](https://www.fosslinux.com/96135/how-to-properly-uninstall-mysql-server-in-ubuntu.htm)

ref.: [How To Install MySQL on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04)

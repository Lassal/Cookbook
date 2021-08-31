# Ferramentas de conexão segura

O acesso a plataformas remotas Unix deve ser feita usando ferramentas [OpenSSH](https://www.openssh.com/manual.html)

Em linhas gerais com OpenSSH conseguimos criar chaves privadas para comunicação com servidores remotos, manter configurações (e chaves) distintas por configuração.
A suite conta com ferramentas para logon remoto (ssh), FTP (sftp) e copia remota (scp).

[Veja detalhes aqui](https://www.hostinger.com/tutorials/ssh-tutorial-how-does-ssh-work)


## Setup

O processo de configuração funciona com estas etapas

   1. Gerar (ou reutilizar) ssh key pair
   2. Adicionar chaves ao agente SSH
   3. Salvar configurações no arquivo `~/.ssh/config`

```bash
  #1. Gerar (ou reutilizar) ssh key pair
    # example ED25519
     ssh-keygen -t ed25519 -C "<comment>"
    # example 2048-bit RSA
     ssh-keygen -t rsa -b 2048 -C "<comment>"


  #2. Adicionar chaves ao agente S
     eval $(ssh-agent -s)
     ssh-add <directory to private SSH key>

```

*IMPORTANTE:* é necessário configurar onde pegar a chave correta para fazer a autenticação e o hostname caso contrário a autenticação não funciona

```
  #3.  Salvar configurações no arquivo `~/.ssh/config`

    # GitLab.com
    Host gitlab.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/gitlab_com_rsa

    # Private GitLab instance
    Host gitlab.company.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/example_com_rsa
```

NOTAS:

  - Usar uma passfrase especifica adiciona um nível a mais de segurança a estas chaves que ficam disponíveis na máquina.
  - O nível de segurança das chaves locais pode ser ampliado seguindo este [POST aqui](https://martin.kleppmann.com/2013/05/24/improving-security-of-ssh-private-keys.html) , fala como subir nível de criptografia.


##  ssh : Conexão para terminal remoto

```bash
ssh <usuario@servidor configurado no config>
```

Para acessar qualquer site precisamos ou ter adicionado diretório ou chave privada usando `ssh-add <diretório ou caminho chave privada>` ou adicionar a entrada no arquivo `~/.ssh/config` 

Caso a chave para o hostname não esteja configurada é provável que o erro abaixo apareça:

> ssh: Could not resolve hostname spodcmgt0015: Temporary failure in name resolution

## Cópia de arquivos: scp & sftp

Temos duas opções de cópia de arquivos seguro de forma remota

  - scp : OpenSSH secure file copy
  - sftp : OpenSSH secure file transfer

A forma recomendada é utilizar sftp conforme a documentação do [OpenSSH](https://man.openbsd.org/scp.1#s)

Uma vez feito o mesmo setup do ssh, conseguimos fazer chamadas no mesmo formato que o ssh

```bash

sftp usuario@servidor_configurado

```

A partir dai podemos usar os comandos FTP conforme este [documentação](https://man.openbsd.org/sftp.1#INTERACTIVE_COMMANDS)

Segue os principais
```
ls -la
cd
ln -s # cria link simbolico
pwd   # informa diretório local


# Local
lcd        # troca diretorio local
lmkdir     # cria diretório local
lls        # lista arquivos no diretório local
lpwd       # informa o diretório local atual
```

 
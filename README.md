# PROJECT.LINUX.00
#!/bin/bash

echo "Configurando ambiente..."

# Criar diretórios
mkdir -p /publico /adm /ven /sec

echo "Preparando grupos..."

# Criar grupos de usuários
groupadd GRP_ADM
groupadd GRP_VEN
groupadd GRP_SEC

echo "Adicionando usuários..."

# Função para criar usuário em grupo
create_user() {
    username=$1
    groupname=$2
    password=$3
    useradd $username -m -s /bin/bash -p $(openssl passwd -crypt $password) -G $groupname
}

# Criar usuários em grupos
create_user_and_group() {
    create_user $1 $2 $3
}

create_user_and_group carlos GRP_ADM Senha123
create_user_and_group maria GRP_ADM Senha123
create_user_and_group joao GRP_ADM Senha123

create_user_and_group debora GRP_VEN Senha123
create_user_and_group sebastiana GRP_VEN Senha123
create_user_and_group roberto GRP_VEN Senha123

create_user_and_group josefina GRP_SEC Senha123
create_user_and_group amanda GRP_SEC Senha123
create_user_and_group rogerio GRP_SEC Senha123

echo "Definindo permissões..."

# Definir proprietários e permissões
chown root:GRP_ADM /adm
chown root:GRP_VEN /ven
chown root:GRP_SEC /sec

chmod 770 /adm /ven /sec
chmod 777 /publico

echo "Configuração concluída!"

Automação de infraestrutura de usuários e...

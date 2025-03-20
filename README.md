# AWS Infra — Atividade Prática

## ✅ Descrição  
Este repositório documenta a atividade prática de criação de infraestrutura na AWS, composta por:  
- Configuração de Security Groups (para EC2 e RDS);  
- Criação de uma instância EC2 (Amazon Linux);  
- Configuração de um banco de dados RDS (PostgreSQL);  
- Instalação do Git e Docker na EC2;  
- Clonagem do repositório e ajuste do `compose.rds.yml`;  
- Configuração do arquivo `.env` com o endpoint do RDS;  
- Inicialização do PostgreSQL via Docker.  

---

## ✅ Etapas Realizadas  

### 1. Security Groups criados  

#### a) EC2 Security Group:  
- Porta **22 (SSH)** liberada apenas para meu IP pessoal;  
- Porta **80 (HTTP)** liberada para qualquer IP (0.0.0.0/0).  

#### b) RDS Security Group:  
- Porta **5432 (PostgreSQL)** liberada apenas para o Security Group da EC2.

---

### 2. Instância EC2 criada  
- AMI: **Amazon Linux 2**  
- Tipo: **t2.small** (A micro faltou ram)
- Associada ao Security Group EC2 criado;
- Par de chaves utilizado para acesso SSH;  
- Após o acesso via SSH, foi realizada a instalação dos pacotes necessários, git, docker e docker-compose:  
```bash
sudo yum update -y
sudo yum install -y git docker
sudo usermod -a -G docker $USER
sudo service docker start
sudo systemctl enable docker

sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```  

---

### 3. Configuração do ambiente na EC2  
- Clonagem do repositório:  
```bash
git clone https://github.com/caiogazen/pru-next
cd pru-next
```  
- Criação e configuração do arquivo `.env` com o endpoint do RDS:  
```env
POSTGRES_HOST=<endpoint-do-rds>
POSTGRES_USER=postress
POSTGRES_PASSWORD=****
POSTGRES_DB=pru_db
.....
```  
- Alteração do `compose.rds.yml` para utilizar variáveis de ambiente do `.env`.  

---

### 4. Banco de Dados RDS (PostgreSQL) criado  
- Engine: PostgreSQL  
- Nome do banco inicial: `pru_db`  
- Usuário master: `postgres`  
- Senha: ******
- Security Group: RDS Security Group (criado anteriormente)
- Endpoint anotado para utilização no `.env`  
---

### 5. Inicialização do ambiente com Docker  
- Com o `.env` configurado, a aplicação e o PostgreSQL foram inicializados usando o comando:  
```bash
sudo docker-compose -f compose.rds.yml up -d
```  
- Foi validada a conexão correta com o banco RDS.  
---

## ✅ Evidências (prints)  

### Security Groups  
![EC2 Security Group](caminho/para/print-ec2-sg.png)  
![RDS Security Group](caminho/para/print-rds-sg.png)  

### Instância EC2  
![Instância EC2](caminho/para/print-ec2.png)  

### Banco RDS  
![RDS](caminho/para/print-rds.png)  

---

## ✅ Demonstração em vídeo  
O vídeo gravado mostra:  
- Acesso SSH à EC2;  
- Clonagem do repositório;  
- Configuração do `.env`;  
- Alteração do compose.rds.yml;  
- Inicialização do ambiente Docker;  
- Conexão bem-sucedida ao banco RDS.  

O vídeo foi enviado via Google Classroom.  

---

## ✅ Estrutura do repositório  
```
aws-infra-atividade/
│
├── prints/
│   ├── print-ec2-sg.png
│   ├── print-rds-sg.png
│   ├── print-ec2.png
│   └── print-rds.png
├── compose.rds.yml
├── .env (não versionado)
├── README.md
└── (opcional) user-data.sh
```  

---

## ✅ Conclusão  
A atividade foi concluída com sucesso:  
- Infraestrutura na AWS criada e funcionando;  
- Instância EC2 conectada ao banco RDS via Docker;  
- Configuração documentada e validada.  

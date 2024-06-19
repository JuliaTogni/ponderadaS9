---
sidebar_position: 1
---

# Tutorial: Como Construir uma Instância AWS com Terraform

## Introdução

Este tutorial irá guiá-lo através do processo de criação de uma instância EC2 na AWS usando o Terraform. Vamos configurar o ambiente, inicializar o Terraform, aplicar a configuração e verificar a instância criada na AWS.

## Pré-requisitos

- Inicializar o AWS Academy
- Terraform instalado

## Primeira parte: Configurar o Ambiente

Crie um diretório de trabalho para o seu projeto Terraform e navegue até ele:

```sh
mkdir terraform-aws-setup
cd terraform-aws-setup
```

## Segunda parte: Instalando o Terraform CLI

#### Passo 1:  
Abra o PowerShell como Administrador. Utilize o shortcut ``` Windows + R ``` que abrirá a janela 'Executar'. Digite 'powershell' e clique ``` Ctrl + Shift + Enter ```, isso irá abrir uma aba PowerShell com direitos de Administrador.

#### Passo 2 :  
Baixe o Terraform executando o comando:
```sh 
Invoke-WebRequest -Uri https://releases.hashicorp.com/terraform/1.0.11/terraform_1.0.11_windows_amd64.zip -OutFile terraform.zip
```

Extraia o arquivo ZIP:
```sh
Expand-Archive -Path terraform.zip -DestinationPath C:\terraform
```

Adicione o Terraform ao PATH do sistema:
```sh
[System.Environment]::SetEnvironmentVariable('PATH', $env:PATH + ';C:\terraform', [System.EnvironmentVariableTarget]::Machine)
```

Verifique a instalação executando:
```sh
terraform -v
```

## Terceira parte: Instalando o AWS CLI
#### Passo 1 : 
<li>Abra novamente o PowerShell como Administrador.</li>

Baixe o instalador do AWS CLI executando:
```sh
Invoke-WebRequest -Uri https://awscli.amazonaws.com/AWSCLIV2.msi -OutFile AWSCLIV2.msi
```

Instale o AWS CLI executando:
```sh
Start-Process msiexec.exe -Wait -ArgumentList '/I AWSCLIV2.msi /quiet'
```

Verifique a instalação executando:
```sh
aws --version
```

## Quarta parte: Configurando as Credenciais da AWS

Configure suas credenciais da AWS executando o comando:
```sh
aws configure
```

Forneça suas credenciais de acesso, elas estão no tópico ``` AWS Details ``` no AWS Academy:
```sh 
AWS_ACCESS_KEY_ID="TEMPORARY_ACCESS_KEY_ID"
AWS_SECRET_ACCESS_KEY="TEMPORARY_SECRET_ACCESS_KEY"
AWS_SESSION_TOKEN="TEMPORARY_SESSION_TOKEN"
AWS_DEFAULT_REGION="us-east-1"
```

## Quinta parte: Criando uma Instância EC2 com Terraform

#### Passo 1:
Crie um arquivo de configuração Terraform chamado ```main.tf``` com o seguinte conteúdo:
```sh
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c02fb55956c7d316"  # Amazon Linux 2 AMI (HVM), SSD Volume Type
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformExample"
  }
}
```

#### Passo 2:
Abra o PowerShell no diretório onde está o arquivo ```main.tf``` e execute:
```sh
terraform -init
```

#### Passo 3: 
Para visualizar a infraestrutura criada execute o comando: 
```sh
terraform plan
```

#### Passo 4: 
Para criar a instância do EC2, execute o comando: 
```sh
terraform apply
```
E digite ```yes``` quando solicitado, para confirmar a aplicação das configurações. 

### Limpando a infraestrutura
Caso queira limpar a infraestrutura construída, execute o comando: 
```sh
terraform destroy
```
E digite ```yes``` quando solicitado, para confirmar a destruição da infraestrutura. 

#### Execute esse comando apenas só se tiver certeza que deseja deletar a instância criada.
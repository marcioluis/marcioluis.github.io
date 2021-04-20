---
title: "Instalar WSL 2 no Windows com Ubuntu e Docker"
categories:
  - posts
tags:
  - wsl2
  - windows
  - ubuntu
---

Esse post tem como objetivo construir um passo-a-passo para a instalação e ativação do WSL2 no Windows. 
Também servirá como base para a instalação do Docker e futuros desenvolvimentos.

# Windows com WSL2

Utilizar o Windows como plataforma de desenvolvimento funciona muito bem, agora com a adição do WSL versão 2  ficou ainda melhor e mais produtivo, pois adiciona novas ferramentas e possibilidades de virtualização dos ambientes de desenvolvimento, evitando que uma configuração de ambiente possa danificar outra já existente.

## Modo manual

Inicie um novo terminal como administrador:

* botão direito em Iniciar >> Windows PowerShell (admin)

outro modo de iniciar pode ser:

* dentro do PowerShell execute: `Start-Process powershell -Verb runAs`

### Habilitando WSL

No terminal execute o seguinte comando para habilitar o _WSL_

`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

### Atualizando para WSL2

Verifique a versão do Windows executando o seguinte comando no terminal: `winver`

Existem alguns pré-requisitos para usar a versão wsl2 que são os seguintes:

* Possuir o Windows 10 **Versão 1903** ou superior, com a **Build 18362** ou superior

Pode atualizar o Windows usando o assistente em:
<https://www.microsoft.com/software-download/windows10>

### Habilitando a Virtualização

Um passo muito importante é habilitar a virtualização do hardware em seu computador para consumo pelo WSL e Docker.
Isso é necessário pois, de agora em diante, tudo que essas aplicações irão consumir será virtual, memória, cpu, disco, etc.

Execute o seguinte comando no terminal:

`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

Reinicie seu computador e durante o processo de _boot_ entre nas configurações de BIOS do seu computador.
Como chegar lá depende de cada fabricante, alguns precisa apertar a tecla _DEL_ outros _F11_, _ESC_, _F4_, varia muito o importante é verificar se a função de virtualização está ativada.

Realize os seguintes passos:

* Nas configurações de BIOS, encontre as configurações relacionadas a CPU. Podem estar sob os menus Processador, Chipset ou Northbridge.
* Habilite a virtualização; essa opção pode ser chamada de VT-x, AMD-V, SVM, ou Vanderpool. Habilite Intel VT-d ou AMD IOMMU se possível.
* **Salve tudo e reinicie**

### Atualizar o Kernel do Linux

Execute e instale o seguinte pacote:

[WSL2 Linux kernel update](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

### Finalizando

* Configure WSL2 como a versão padrão

`wsl --set-default-version 2`

* Instale pela Store a versão do Linux da sua escolha, eu instalei e recomendo o Ubuntu 20

[Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)

A instalação deve demorar um pouco e após deve criar um usuário e senha para essa instalação.
Esse usuário e senha não tem relação com o Windows então não precisam ser iguais.

Após a instalação e criação do usuário, acesse a distribuição pelo menu iniciar e pesquisando por _Ubuntu_, deve aparecer o nome da distribuição instalada _Ubuntu 20.04 LTS_.

Execute o seguinte comando para atualizar a distribuição:

`sudo apt update && sudo apt upgrade`

C:\Users\<<nome do meu usuario>>
criar o arquivo .wslconfig

adicionar o seguinte conteúdo:

[wsl2]
memory=3.5GB # Limits VM memory in WSL 2
processors=2 # Makes the WSL 2 VM use two virtual processors

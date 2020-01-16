---
layout: post
title: Guia de customizações SDK Senior X
subtitle: Guia de customizações SDK Senior X
---

# Guia de customizações utilizando o SDK de desevolvimento do Senior X Platform <!-- omit in toc -->

O SDK da Plataforma Senior X, é um Kit de desenvolvimento que fornece um ambiente de customização de regras de
negócios da Plataforma através da interceptação de primitivas (Endpoints) , possibilitando a implementações de regras
de negócios customizadas.

O SDK utiliza como base a criação de funções Lambdas no provedor de Cloud AWS e edição do código fonte através
da IDE Cloud9.(https://aws.amazon.com/pt/cloud9/)

A linguagem adotada como padrão de desenvolvimento utilizando o SDK é Javascript, rodando na plataforma Nodejs.

## Conceitos

Abaixo estão alguns conceitos importantes para a compreensão do funcionamento do SDK e das customizações na Plataforma Senior X. 
 
- `AWS lambda:` O AWS Lambda permite que você execute códigos sem provisionar ou gerenciar servidores. Ou seja, seu código é implantado em um formato de função que é executada através de gatilho de outros serviços da própria AWS. Isso garante que o desenvolvedor foca apenas na regra de negócio do software, sem se preocupar com a infraestrutura de servidores. 
 
- `Cloud9:` É um ambiente de desenvolvimento integrador totalmente na nuvem, com suporte a várias plataformas e linguagens de programação. Esse é o editor padrão para o desenvolvimento de funções lambda na AWS. 
 
- `NodeJs:` É um interpretador de Javascript que roda do server-side (servidor). 

## Vantagens

- Possibilita o desenvolvimento de customizações sem a necessidade de instalações locais. 

- As customizações são feitas em uma linguagem de marcado altamente poderosa e com uma grande comunidade global. 

- Criação de customizações “Endpoints” de forma rápida. 

- Cliente gerencia o acesso de quem pode editar suas customizações. 

- Possibilidade de utilizar bibliotecas de terceiros para ganhar produtividade no desenvolvimento

## Utilização

- Possuir um tenant para acesso a plataforma Senior X, com um usuário com permissões de Administrador. 
  
- Validar se o tenant do cliente está devidamente configurado para realizar o envio de e-mails: 
   Através do menu: Tecnologia / Configuração / Por Tenant / Aba Sistema: Validar se as configurações de envio de email estão preenchidas: 

![Configuração de envio de e-mail](/_posts/.docs/images/emailconfig.png "Configuração de envio de e-mail")

Obs.: Certificar-se que as configurações estão corretas é primordial para seguir com os exemplos desse documento. 
 
Através do menu: Tecnologia / Configurações / Validação de envio de E-mail: Realizar um teste de envio para um determinado e-mail e verificar se o mesmo é recebido: 

![Validação de envio de e-mail](/_posts/.docs/images/validacaoemail.png "Validação de envio de e-mail")

Caso o e-mail for executado com sucesso e recebido pelo destinatário, as configurações estão corretas. 

## Configurando o ambiente de customização 

Para configurar um ambiente de customização, será necessário navegar até a tela de gerenciamento de acesso, que fica em Tecnologia>Customizações>Configurar Ambiente>Gerenciar Acesso: 

![Configuração do ambiente](/_posts/.docs/images/amb1.png "Configuração do ambiente")

Nesta tela você pode visualizar o status de configuração do ambiente e informar chaves do provedor cloud. (Atualmente apenas a AWS é suportada). 

**Configurando chaves de acesso** 

Para que seja possível configurar o ambiente é necessário garantir que as chaves de acesso ao provedor cloud já estejam devidamente configuradas, por padrão o serviço utiliza as chaves já informadas nas configurações globais, no entanto, existe a possibilidade de sobrescrever as chaves de acesso de duas maneiras diferentes: 

**Através do gerenciamento de acesso** 

Basta clicar no botão Informar chaves de acesso, e será exibido o formulário contendo o identificador da conta e a região já preenchidos.

![Configuração do ambiente](/img/hello_world.jpeg "Configuração do ambiente")


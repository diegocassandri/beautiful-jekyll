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

![Configuração de envio de e-mail](/img/emailconfig.png "Configuração de envio de e-mail")

Obs.: Certificar-se que as configurações estão corretas é primordial para seguir com os exemplos desse documento. 
 
Através do menu: Tecnologia / Configurações / Validação de envio de E-mail: Realizar um teste de envio para um determinado e-mail e verificar se o mesmo é recebido: 

![Validação de envio de e-mail](/img/validacaoemail.png "Validação de envio de e-mail")

Caso o e-mail for executado com sucesso e recebido pelo destinatário, as configurações estão corretas. 

## Configurando o ambiente de customização 

Para configurar um ambiente de customização, será necessário navegar até a tela de gerenciamento de acesso, que fica em Tecnologia>Customizações>Configurar Ambiente>Gerenciar Acesso: 

![Configuração do ambiente](/img/amb1.png "Configuração do ambiente")

Nesta tela você pode visualizar o status de configuração do ambiente e informar chaves do provedor cloud. (Atualmente apenas a AWS é suportada). 

**Configurando chaves de acesso** 

Para que seja possível configurar o ambiente é necessário garantir que as chaves de acesso ao provedor cloud já estejam devidamente configuradas, por padrão o serviço utiliza as chaves já informadas nas configurações globais, no entanto, existe a possibilidade de sobrescrever as chaves de acesso de duas maneiras diferentes: 

**Através do gerenciamento de acesso** 

Basta clicar no botão Informar chaves de acesso, e será exibido o formulário contendo o identificador da conta e a região já preenchidos.

![Configuração do ambiente](/img/amb2.png "Configuração do ambiente")

Após preencher as informações basta clicar em salvar e aguardar a notificação de sucesso. 

**Através das Configurações do tenant** 

Navegar para Tecnologia>Configuração>Por tenant, e procurar os campos destinados as chaves de configuração do provedor cloud: 

![Configuração do ambiente](/img/amb3.png "Configuração do ambiente")

Após preencher as informações basta clicar em salvar e aguardar a notificação de sucesso. 
 
Obs.: As informações de chave de acesso nos ambientes de Produção e Homologx da Plataforma já estão configuradas por padrão em uma conta da Senior destinada a customizações de clientes. As chaves só devem ser alteradas caso o cliente possua uma conta AWS própria e gostaria de utilizá-la. Entretanto é necessário ficar ciente de possíveis cobranças na utilização de uma conta própria. Nesse caso é necessário validar a política de cobranças da AWS. 
 

**Configurando o ambiente**

Com as chaves de acesso devidamente configuradas clicar no botão “Criar Ambiente”. 
 
O processo iniciará e é possível acompanhar as etapas da criação utilizando o botão “Atualizar Status”. Esse procedimento pode demorar alguns minutos. 
 
Em caso de falha em alguma das etapas, o botão tentar novamente será habilitado bastando clicar no mesmo para que o serviço tente configurar o ambiente novamente. 
 
Uma vez que o processo foi finalizado com sucesso a tela ficará da seguinte forma: 

![Configuração do ambiente](/img/amb4.png "Configuração do ambiente")

Note que o botão abrir ambiente foi habilitado. 
 
Nesse momento um e-mail com as credenciais de acesso ao ambiente do Cloud9 foi enviado para o e-mail do usuário da plataforma que realizou a criação do ambiente.  
 
Obs.: Esses dados devem ser guardados, pois são os dados do Administrador do ambiente de customização do Tenant. 
 
Clicar no botão “Abrir Ambiente” e na tela que se abrirá informar os dados de acesso recebidos: 

![Configuração do ambiente](/img/aws.png "Configuração do ambiente")

Se o ambiente foi criado com as chaves do provedor Cloud padrão da Senior a Conta a ser preenchida é “seniorxcustom”, caso for uma conta privada do cliente, deve-se verificar essa informação. 
 
O Nome de usuário e senha, devem ser os recebidos por e-mail. Note que no primeiro acesso a senha precisa ser redefinida. 
 
Ao clicar em fazer login, você será redirecionado para a página inicial do Cloud9. 

![Cloud9](/img/cloud9.png "Cloud9")

Com isso o ambiente de customização está devidamente configurado. 

## Permissões de Acesso ao ambiente

 Após a criação do ambiente, apenas o usuário que realizou a criação do mesmo possui o acesso. Essas credenciais recebidas **Não** devem ser compartilhadas com terceiros, consultores e usuários internos.  Para conceder o acesso a outros desenvolvedores existem as seguintes opções: 

 `Consultores:` Estes são mantidos pela Senior e disponibilizados para todos os tenants.

 Para convidar um consultor Basta navegar até o menu Customização > Configurar Ambiente > Convidar consultores em seguida será exibida a listagem de consultores que já foram convidados para o tenant em questão e para convidar um novo consultor basta clicar em Adicionar. 

- Selecione o usuário da plataforma que será associado ao consultor que será convidado, permitindo que o mesmo tenha acesso ao tenant do cliente. 
- Selecione o consultor e clique em salvar. 

![Cadastro consultor](/img/consultores.png "Cadastro consultor")

Por padrão os consultores são convidados sem acesso ao ambiente por tanto estarão com o status desativado, e por tanto ainda não poderá acessar o ambiente do tenant, para ativa-lo basta clicar no toggle contido na coluna de status. 

- Após habilitado o consultor estará apito a realizar customizações nas primitivas da plataforma. 

`Desenvolvedores:` Estes são criados pelo tenant e existem apenas no tenant que os criou, para que sejam criados será necessário ter acesso ao recurso de cadastro de desenvolvedores. 
 
Para cadastrar um desenvolvedor basta navegar para o menu Customização > Configurar Ambiente > Desenvolvedores em seguida você será direcionado para a listagem de desenvolvedores já cadastrados, para adicionar um novo desenvolvedor basta clicar na opção Adicionar, em seguida você será direcionado para o formulário de cadastro, basta selecionar o usuário do tenant e automaticamente as informações necessárias para a criação da conta de acesso a AWS serão preenchidas e enviadas para o email. 

![Cadastro desenvolvedor](/img/desenvolvedores.png "Cadastro desenvolvedor")

Por padrão os desenvolvedores são criados sem acesso ao ambiente por tanto estarão com o status desativado, e não poderá acessar o ambiente do tenant, para ativa-lo basta clicar no toggle contido na coluna de status.

Tento em mente a forma de acesso ao ambiente de customização já é possível realizar as customizações.

## Criando uma nova customização 

Para exemplificar a criação de uma customização, vamos descrever um cenário que não depende de nenhum produto específico, utilizando apenas uma primitiva do core da plataforma responsável pela criação de novos usuários, visto que as primitivas dos produtos ex: HCM, ERP, ERPX, dependem que os mesmos estejam implantados no tenant do cliente. 

###  Cenário   

Considerando um cenário hipotético, um determinado cliente deseja que o campo “Descrição” da tela de criação de usuário seja obrigatório.   Por padrão, esse campo na tela não é obrigatório, e não é possível via configuração definir essa obrigatoriedade. A alternativa para esse caso seria interceptar a primitiva de criação de usuários e criar uma customização que valide se essa propriedade foi preenchida, caso não estiver devolver uma mensagem informando a obrigatoriedade e bloquear a operação.

Tela de cadastro de novo Usuário, menu: Tecnologia / Administração / Gestão de Usuários, botão “Adicionar”.

![Novo usuário](/img/adduser.png "Novo usuário")

## Identificando a primitiva 

Após possuirmos a definição do problema a ser resolvido, o próximo passo é encontrar qual a primitiva que deve ser customizada.   

Existem várias formas para obter essa informação. O mais comum é consultar a documentação das API’s através do Portal Senior DEV: (https://dev.senior.com.br/
apis/) 

Porém também é possível encontrar a primitiva através do “developer tools” do navegador, bastante realizar a operação na tela, nesse caso o cadastro de um novo usuário e através da aba “network”.      

Após criar um novo usuário podemos ver que a primitiva chamada é a: **/platform/user/actions/createUser**

![Configuração do ambiente](/img/primitiva.png "Configuração do ambiente")


Todas as chamadas da plataforma possuem o mesmo padrão no caso do recurso **/platform/user/actions/createUser**,  os valores correspondem as seguintes informações: 
 
**Domínio:** Platform 
**Serviço:** User 
**Primitiva:** CreateUser

Agora que sabemos qual o endpoint e primitiva que a tela executa ao se cadastrar um novo usuário, já podemos criar a customização. 

## Criando a customização 

Para criar a customização acesso o seguinte menu: Tecnologia / Customização / Regras / Nova customização   Através da busca digitar o nome da primitiva no caso “CreateUser”.      

Localizar no resultado a primitiva de acordo com Domínio/Serviço/Primitiva a ser customizada através do botão “Selecionar”. 

![Cadastro extensão](/img/extensao.png "Cadastro extensão")

Na próxima tela devemos selecionar algumas opções: 

![Cadastro extensão](/img/funcionalidade.png "Cadastro extensão")
---
layout: post
title: Desenvolvendo uma API Rest com Deno
subtitle: Desenvolvendo uma API Rest com Deno
bigimg:
    - "/img/Deno.jpeg" : ""
---

# Desenvolvendo uma API Rest com Deno

![Deno](/img/Deno.jpeg)

Recentemente o Deno na sua versão 1.0 Beta foi lançado. Mas de fato o que seria o Deno? Ele vai substituir o Node? O que esperar para o futuro?

Vamos entender nesse artigo qual é o objetivo base do Deno e quais são os problemas que o mesmo se propõe a resolver.

Após isso vamos desenvolver junto uma simples API Rest utilizando o Deno.

Assim você entenderá quais são os objetivos do Deno e se deve utiliza-lo em seus projetos no futuro.

## O que é o Deno?

Deno é um Runtime Javascript como o NodeJs e foi criado em conjunto com um dos mesmos criadores do NodeJs **Ryan Daahl**.  O Deno vem então para resolver alguns problemas que o Node possui na visão do próprio Ryan.

O Slogan do Deno é " A secure runtime for javaScript and TypeScript". Dai nós já podemos tirar algumas conclusões de qual é o principal propósito do Deno. Que de fato é ser um ambiente de execução javaScript e TapeScript seguro por padrão.

Essa questão da segurança vem principalmente pela linguagem que o Deno foi construído que é o Rust. Uma linguagem de programação com com mesmo propósito, construir aplicações seguras por padrão.

## Principais recursos do Deno

- O Deno suporta TypeScript sem a necessidade de transpilação manual. Ou Seja o Deno faz isso de forma automática para gente.
- Sem node_modules. O Deno não usa o NPM para a instalação de pacotes. Ao invés disso ele importa as bibliotecas de servidores externos diretamente de sua URL. EX:  import {server} from '[https://deno.land/std@0.50.5/http/server.ts](https://deno.land/std@0.50.5/http/server.ts)'
- Já possui nativamente os recursos mais recentes do ECMAScript. Algo que no Node existe um tempo maior para liberação desses recursos.
- É essencialmente um loop for que permite percorrer um array infinito, você pode dizer um array infinito de dados e eventos recebidos.

![API%20REST%20com%20Deno%204d3e5bdb1b304b71af7c1a4a2c590116/1_jQQC7ySp-thNY3cHrSRgYQ.png](/img/1_jQQC7ySp-thNY3cHrSRgYQ.png)

- Para maiores informações a respeito do Deno e seus recursos vale dar uma olhadinha no BLOG do projeto.

> [https://deno.land/v1](https://deno.land/v1)

### O Deno vai substituir o Node?

Tenha em mente que o NodeJs é largamente utilizado por grandes empresas atualmente. Muitos projetos e bibliotecas são desenvolvidos no contexto do NodeJS, uma serie de frameworks Frontend inclusive utilizam do Node em tempo de desenvolvimento. Dessa forma não podemos considerar que o Node é apenas um Runtime JavaScript, hoje ele é muito mais que isso.

O Deno surge como uma alternativa ao node, porém ainda muito imaturo, com alguns bugs. Ainda não sabemos o que o time de desenvolvimento do Deno vai tomar de decisões para o futuro.

Atualmente o Deno ainda não possui suporte para Pacotes Node e nem sabemos ainda se isso vai ser possível.

Sendo assim o Deno é uma tecnologia muito recente para dizermos com certeza como o mesmo vai evoluir e como o mercado vai reagir.

Porém vale sempre acompanhar a evolução da tecnologia e sinceramente um Runtime TypeScript nativo é algo que definitivamente deve ser olhado com carinho.

## Construindo nossa primeira API com DENO

Agora que entendemos um pouco do Deno chegou a hora de colocarmos a mão na massa para construir nossa primeira API Rest.

### Nossos objetivos

- Instalação do Deno
- Criar uma API para manutenção de produtos
- Prover rotar de GET,POST,PUT e DELETE
- Salvar criar/atualizar produtos em um arquivo JSON local

### Instalação

Vou mostrar aqui duas formas de instalação Mac/Linux e Windows. Porém no link a seguir você pode consultor a instalação para outros sistemas operacionais. 

> [https://deno.land/#installation](https://deno.land/#installation)

Shell (Mac, Linux):

```bash
curl -fsSL https://deno.land/x/install/install.sh | sh
```

PowerShell (Windows):

```powershell
iwr https://deno.land/x/install/install.ps1 -useb | iex
```

Para verificar se o Deno foi instalado bem como sua versão utilizar o comando *deno --version*

```powershell
deno --version
deno 1.0.0
v8 8.4.300
typescript 3.9.2
```

### Executando uma aplicação Deno

Executando o comando deno run [https://deno.land/std/examples/welcome.ts](https://deno.land/std/examples/welcome.ts). o mesmo será baixado e compilado. Esse exemplo te ajudará a tentar o ambiente do Deno em sua máquina.

```powershell
deno run https://deno.land/std/examples/welcome.ts
Download https://deno.land/std/examples/welcome.ts
Warning Implicitly using master branch https://deno.land/std/examples/welcome.ts
Compile https://deno.land/std/examples/welcome.ts
Welcome to Deno 🦕
```

Se você executar o comando novamente vai perceber que o código não será baixado novamente, o Deno vai usar o código já baixado da sua área de cache.

### Lista de parâmetros de permissão

Como o Deno é seguro por padrão as aplicações criadas não possuir qualquer permissão de acesso a recursos. Para isso é preciso dizer explicitamente o que a aplicação tem permissão no momento da execução da mesma. Isso é feito através da passagem de parâmetros para a aplicação:

- **`— allow-env:`** Allow environment access. (Acesso ao ambiente)
- **`— allow-hrtime:`** Allow high-resolution time measurement.
- **`— allow-net:`** Allow network access. (Acesso a recrusos de rede)
- **`— allow-plugin:`** Allow loading plugins.
- **`— allow-read:`** Allow file system read access. (Acesso de leitura ao sistema de arquivos)
- **`— allow-run:`** Allow running subprocesses.
- **`— allow-write:`** Allow file system write access. (Acesso de escrita ao sistema de arquivos)
- **`— allow-all:`:** Give all access. (Permitir Tudo)

### Iniciando

Nós vamos desenvolver uma simples API Rest usando TypeScript e o framework oak para trabalhar com requisições http. A API vai fornecer rotas par a operações de CRUD de produtos. Para testar os endpoints vamos utilizar o Postman.

Se você está usando o Visual Studio Code é recomendado que use o Plugin para trabalhar com o Deno. Caso contrário terá erros de importação das dependências. Deno Plugin [deno](https://marketplace.visualstudio.com/items?itemName=justjavac.vscode-deno).

> Passo 1 : Estrutura do Projeto

![API%20REST%20com%20Deno%204d3e5bdb1b304b71af7c1a4a2c590116/Untitled.png](/img/Untitled.png)

- **Controllers:** Tem a lógica da aplicação e trabalha com as requisições recebidas.
- **Routes.ts:** contém as rotas da aplicação.
- **Server.ts:** codigo para rodar o servidor.
- **Types.ts:** contém nossa definição de modelos.

> Passo 2: A escolha de um framework Web

Como no Node nós temo o Express no Deno nós temos o Oak que foi lançado em sua primeira versão juntamente com o Deno.

> Passo 3: Subindo um servidor Local.

crie o arquivo `server.ts` e importe:  

```tsx
import { Application } from 'https://deno.land/x/oak/mod.ts'
const port = 8000

console.log(`Server running on port ${port}`)
```

> Passo 4: Criando as rotas

Agora vamos cruar o arquivo `routes.ts`e importar: 

```tsx
import { Router } from 'https://deno.land/x/oak/mod.ts'
import { getProducts, getProduct, addProduct, updateProduct, deleteProduct } from './controllers/products.ts'

const router = new Router()

router.get('/api/v1/products', getProducts)
    .get('/api/v1/products/:id', getProduct)
    .post('/api/v1/products', addProduct)
    .put('/api/v1/products/:id', updateProduct)
    .delete('/api/v1/products/:id', deleteProduct)

export default router
```

Não se confundir com os métodos das rotas. Nós vamos cria-los a seguir no nosso controller.

Agora, voltando no nosso arquivo `server.ts`, importe nossoa rquivo de rotas, e crie uma isntancia da aplicação que vai ouvir na porta definida. A vesão final do `server.ts` ficará assim:

```tsx
import { Application } from 'https://deno.land/x/oak/mod.ts'
import router from './routes.ts'
const port = 8000

const app = new Application()

app.use(router.routes())
app.use(router.allowedMethods())

console.log(`Server running on port ${port}`)

await app.listen({ port })
```

> Passo 5: Criando nosso model

`types.ts` será uma interface que representa nossa entidade produto.

```tsx
export interface Product {
    id: string;
    name: string;
    description: string;
    price: number;
}
```

> Passo 6: Criando nosso Controller

Vamos criar um array de produtos inicial para começar.

```tsx
import { v4 } from 'https://deno.land/std/uuid/mod.ts'
import { Product } from '../types.ts'

let products: Product[] = [
    {
      id: "1",
      name: "Product One",
      description: "This is product one",
      price: 99.99,
    },
    {
      id: "2",
      name: "Product Two",
      description: "This is product two",
      price: 150.99,
    },
    {
      id: "3",
      name: "Product Three",
      description: "This is product three",
      price: 199.99,
    },
  ];
```

Agora vamos criar diferentes métodos no nosso controller `products.ts` e testar no Postman.

**getProducts:** Vai retornar todos os produtos da lista. Fazendo uma requisição GET  para `/api/v1/producs`

```tsx
const getProducts = ({ response }: { response: any }) => {
    response.body = {
        success: true,
        data: products
    }
}
```

> Testando no Postman

![GETPRODUCTS](/img/APIDENO/GET.png)

**getProduct:** Vai retornar um único produto pelo seu Id e um erro se o produto não for encontrado. Fazendo uma requisição GET para `/api/v1/products/:id`

```tsx
const getProduct = ({ params, response }: { params: { id: string }, response: any }) => {
    const product: Product | undefined = products.find(p => p.id === params.id)

    if (product) {
        response.status = 200
        response.body = {
            success: true,
            data: product
        }
    } else {
        response.status = 404
        response.body = {
            success: false,
            msg: 'No product found'
        }
    }
}
```

> Testando no Postman

![GETONEPRODUCT](/img/APIDENO/GETONE.png)

Produto não encontrado

![GETNOTPRODUCT](/img/APIDENO/GETNOT.png)

Error: Produto não encontrado

**addProduct:** Vai adicionar um novo produto na lista. Fazendo uma requisição POST para `/api/v1/products.`

```tsx
const addProduct = async ({ request, response }: { request: any, response: any }) => {    
    const body = await request.body()

    if (!request.hasBody) {
        response.status = 400
        response.body = {
            success: false,
            msg: 'No data'
        }
    } else {
        const product: Product = body.value
        product.id = v4.generate()
        products.push(product)
        response.status = 201
        response.body = {
            success: true,
            data: product
        }
    }
}
```

> Testando no Postman

![POST](/img/APIDENO/POST.png)

![POSTRESPONSE](/img/APIDENO/POSTRESPONSE.png)

**updateProduct:** Vai atualizar um produto. Fazendo uma requisição PUT para`/api/v1/products/:id.`

```tsx
const updateProduct = async({ params, request, response }: { params: { id: string }, request: any, response: any }) => {
    const product: Product | undefined = products.find(p => p.id === params.id)

    if (product) {
        const body = await request.body()

        const updateData: { name?: string; description?: string; price?: number } = body.value

        products = products.map(p => p.id === params.id ? { ...p, ...updateData } : p)

        response.status = 200
        response.body = {
            success: true,
            data: products
        }
    } else {
        response.status = 404
        response.body = {
            success: false,
            msg: 'No product found'
        }
    }
}
```

> Testando no Postman


![PUT](/img/APIDENO/PUT.png)

Dados para atualizar o nome do Produto

![PUTRESPONSE](/img/APIDENO/PUTRESPONSE.png)

Nome do produto Id: 2 atualizado.

**deleteProduct:** Vai deletar um produto da lista. Fazendo uma requisição DELETE para `/api/v1/product/:id`

```tsx
const deleteProduct = ({ params, response }: { params: { id: string }, response: any }) => {
    products = products.filter(p => p.id !== params.id)
    response.body = { 
        success: true,
        msg: 'Product removed'
    }
}
```

> Testando no Postman

![DELETE](/img/APIDENO/DELETE.png)

Após criado nosso métodos, nós precisamos importa-lós no nosso arquivo de rotas. Exportando os mesmos do nosso arquivo `product.ts`

```tsx
export { getProducts, getProduct, addProduct, updateProduct, deleteProduct }

```

## Conclusão

Chegamos ao final do nosso guia, passamos pela introdução do Deno, instalação e desenvolvemos uma API simples usando o Deno. Caso queria saber mais recomendo dar uma olhada na documentação oficial  [documentação](https://deno.land/manual).  Deno possui uma lisa incrível de bibliotecas padrões [Standard Library](https://deno.land/std) e [Third-Party Modules.](https://deno.land/x)

O código completo do guia pode ser encontrado no meu GitHub:  

[diegocassandri/deno-api-example](https://github.com/diegocassandri/deno-api-example)

Esse artigo foi baseado em dois artigos que cito referências abaixo:

[Let's meet Deno the Dinosaur 🦕](https://medium.com/@pushkar.thakur28/lets-meet-dino-the-dinosaur-2b406ad0db1c)

[Pushkar Thakur - Medium](https://medium.com/@pushkar.thakur28)
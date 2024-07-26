# **2. Real World Vue.JS3 (API de Composição)**

## **Este repositório possui um curso sobre a construção de uma _app_ Vue.JS 3**

Neste curso, criaremos um aplicativo de nível de produção usando Vue.JS versão 3. Começaremos criando o projeto usando o comando ``create-vue``. Em seguida, aprenderemos sobre componentes ``.vue`` e como eles podem ser usados para criar um aplicativo de página única (**Single Page Application**). Depois abordaremos os fundamentos do "**Vue Router**" para que possamos navegar entre as diferentes visualizações de nosso aplicativo e até mesmo buscar dados externos reais usando chamadas de API com o "**Axios**". Terminaremos aprendendo sobre o processo de construção e como implantar nosso aplicativo em produção.

## **IDE recomendado**

Vai-se utilizar o VSCode. Caso você ainda não o tenha [baixe-o](https://code.visualstudio.com/download), e depois instale-o.

Instale, também uma extensão do VSCode chamada [es6-string.html](https://marketplace.visualstudio.com/items?itemName=Tobermory.es6-string-html)


## **Tutorial 7. Fazendo o _deploy_ com o Render**

Agora nosso aplicativo de exemplo tem todos os recursos necessários. Vários conceitos foram vistos ao longo do caminho e exploramos as práticas fundamentais de desenvolvimento de aplicativos Vue. Agora estamos prontos para levar nosso projeto para a próxima etapa de qualquer aplicativo do mundo real, que é fazer a implantação dele (i.e. _fazendo o deploy_). Neste tutorial, entenderemos o que acontece no processo de construção e como implantar sem problemas nosso aplicativo com uma plataforma conveniente chamada [**Render**](https://render.com/). Ver figura abaixo.

![build_deploy_with_render](img_readme/build_deploy_with_render.png)



### **Passo 1. O que acontece quando criamos nosso _app_?**

Antes de fazermos o _deploy_ do nosso aplicativo Vue, ele deve primeiro ser _construído_. Se esse conceito é novo para você, estou me referindo ao processo de compilar todo o nosso código em um estado pronto para ser lançado na Internet para uso das pessoas.

Lembra-se no início do curso, quando aprendemos como o arquivo "**index.html**" é a “*página única*” (i.e. _single page_) do nosso SPA? Vimos como nosso aplicativo está sendo carregado no elemento ``<div>`` com o ``id`` de "**app**" neste arquivo:

```html
<div id="app"></div>
```

É aqui que os arquivos construídos, implantados e concluídos terminarão quando construirmos nosso aplicativo. Podemos obter uma melhor compreensão de como isso se parece executando o processo de construção.

Para a produção dentro do arquivo "**main.js**" faremos a criação e a "montagem" do nosso _app_. Veja a figura abaixo.

![create_mount_app](img_readme/create_mount_app.png)

Todo o processo pode ser visualizado na figura abaixo.

![vue_whole_process](img_readme/vue_whole_process.png)



___

Surgue a pergunta: o que acontece quando construímos (_build_) nosso _app_?

Se dermos uma olhada no arquivo "**package.json**" do nosso projeto, veremos esses scripts Vue CLI disponíveis para nós. (ver código abaixo).

```javascript
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview --port 4173",
  "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs --fix --ignore-path .gitignore"
},
```

Já estamos familiarizados com a execução do comando ``dev`` para ativar nosso projeto em um host local. Nós o usamos ao longo dos tutoriais enquanto desenvolvemos o código do aplicativo. Já que estamos prontos para levar nosso projeto para o mundo real, podemos passar a usar o comando ``build``, que obviamente transforma nosso projeto em um produto utilizável que pode ser implantado. Vamos ver o que acontece quando digitamos o comando ``npm run build`` em nosso terminal (estando na pasta raiz do projeto).

#### Terminal
```
$ npm run build

vite v3.1.3 building for production...
✓ 79 modules transformed.
dist/index.html                  0.42 KiB
dist/assets/index.0707a6d6.css   0.60 KiB / gzip: 0.38 KiB
dist/assets/index.a62f66a8.js    104.29 KiB / gzip: 40.77 KiB
```

> Como podemos ver, nosso aplicativo foi compilado com sucesso e enviado para um novo diretório chamado ``dist``. Esse diretório contém o código pronto para produção que implantaremos.

![dist_folder](img_readme/dist_folder.jpg)

Dando uma olhada dentro deste novo diretório ``dist``, veremos uma pasta chamada ``assets`` que contém nosso código CSS e JS integrado. Esta pasta ``dist`` também contém um arquivo "**index.html**". O seu conteúdo conterá, entre outras coisas o trecho de código abaixo.

```javascript
<head>
  ...
  <script type="module" crossorigin src="/assets/index.a62f66a8.js"></script>
  <link rel="stylesheet" href="/assets/index.0707a6d6.css">
</head>
```

> Quando olhamos dentro desse arquivo, vemos que nossos arquivos construídos foram injetados automaticamente.

Agora que entendemos como é esse processo de construção (i.e. _building_), como realmente implementamos esse código na produção? É o que veremos no próximo passo.


### **Passo 2. Uma dor de cabeça de alto risco**

Ao falar sobre _deployment_, na verdade, estamos falando de um processo bastante complexo e cheio de nuances.

Para fazer isso direito, você precisa:

1. Encontre um serviço de hospedagem na web responsável por servir seu aplicativo

2. Conecte o seu site a um domínio personalizado

3. Obtenha certificados ``SSL - https`` para garantir que você tenha um domínio seguro

4. Crie o site localmente e faça o _upload_ desses arquivos para o servidor

5. Certifique-se de que tudo está sendo servido corretamente

Depois que seu aplicativo é implantado, há preocupações adicionais em mantê-lo e continuar a implantar versões novas e aprimoradas dele de maneira estável e garantir que você possa reverter para versões anteriores em caso de emergência. Isso tudo pode ser doloroso. Se você não está confiante sobre o que está fazendo, é um risco muito alto assumir tudo isso sozinho.

Felizmente, existem plataformas que fazem muito do trabalho pesado de implantação (e reimplantação) para nós. O que nos leva à uma solução sobre a qual aprenderemos neste tutorial: o [**Render**](https://render.com/).

![render_home_page](img_readme/render_home_page.png)

Render fornece _deploys_ instantâneos para seus aplicativos. Basta conectá-lo ao repositório do seu projeto e ele cria e implanta automaticamente seu aplicativo em um site ao vivo que os usuários podem ver e interagir. Ele também pode executar atualizações automáticas para você, para que, sempre que ao enviar algo para seu repositório, o ``Render`` reconstrói e implanta automaticamente seu site sem nenhum trabalho adicional de sua parte.

![how_render_works](img_readme/how_render_works.png)

Para começar a usá-lo para implantar nosso aplicativo Vue, basta criar uma conta gratuita. Clique no botão ``Sign in`` no canto superior à direita. Você será direcionado para a página abaixo.

![render_sign_in_page](img_readme/render_sign_in_page.png)

Caso seja a primeira vez que você acessa o site, clique no botão ``SIGN UP`` quase no rodapé da página. A página será esta.

![render_sign_up_page](img_readme/render_sign_up_page.png)

Após criar a sua conta, você receberá um link de verificação por e-mail, no qual clicará para entrar em sua nova conta. Ao entrar, você verá que há vários serviços disponíveis no Render. Vamos começar clicando no botão azul ``New +``, que revela um menu suspenso com algumas opções. Ver figura abaixo.

![new_button_with_options](img_readme/new_button_with_options.jpg)

Como você pode ver, podemos implantar um site estático servido em um CDN global com a capacidade de adicionar um domínio personalizado, além de SSL pronto para uso. Se você não estiver familiarizado, o **SSL (Secure Sockets Layer)** é um protocolo para navegadores e servidores da Web que permite a autenticação, criptografia e descriptografia de dados enviados pela Internet. Em outras palavras: é uma medida de segurança integrada que vem de graça com o Render.

Selecionaremos esta opção ``Static Site`` para implantar nosso aplicativo Vue com Render, que nos solicitará a seleção de um repositório para o site que desejamos implantar. Como ainda não conectamos nenhum repositório à nossa conta do Render, clicaremos no link “**Github**” para fazer isso. Se você ainda não estiver conectado ao Github, faça login para instalar o Render em sua conta do Github e selecione o repositório que deseja conectar.

> **IMPORTANTE**: Para seguir essas etapas, você precisará dar um _fork_ no repositório do curso Vue Mastery para sua conta pessoal do Github. Dessa forma, você poderá conectar o repositório nesta etapa. Veja figura abaixo.

![install_render](img_readme/install_render.jpg)

Ao clicar em instalar (``install``), você será redirecionado de volta ao Render, onde deverá ver o repositório recém-conectado aparecendo. Veja figura abaixo.

![install_repo_showing_up](img_readme/install_repo_showing_up.jpg)

Agora estamos prontos para selecionar esse repositório e implantá-lo como um site estático, que é um processo muito simples. Como a página diz de forma inteligente: “Você parece estar usando Vue.js, então preenchemos automaticamente alguns campos de acordo.”

Daremos um nome ao nosso site. Vamos chamá-lo de "**Real World Vue 3**".

Quanto à ramificação (_Branch_), é aqui que você normalmente selecionaria ``Master`` (que é a seleção padrão), pois a maioria dos aplicativos implanta a ramificação mestre de seu repo. No entanto, em nosso caso, como venho construindo o aplicativo de forma incremental com cada nova lição terminando com sua própria ramificação final, selecionaremos ``t6-end``, pois isso inclui o código final de todo o nosso aplicativo de exemplo.

Podemos deixar o comando ``Build`` preenchido automaticamente inalterado, bem como o nome do diretório para publicar: ``dist`` (parece familiar?).

Também existem opções avançadas (i.e. ``Advanced``) adicionais, incluindo a capacidade de adicionar variáveis de ambiente (``Add Environment Variables`` e/ou um arquivo secreto (``Secret File``), mas vamos ignorá-las por enquanto.

Quero chamar sua atenção para o campo ``Auto Deploy``, que é definido como “**Yes**” por padrão. Isso significa que nosso aplicativo será reimplantado automaticamente sempre que uma alteração for enviada para essa ramificação, o que é um recurso incrível. Se quiséssemos lidar com isso manualmente, alternaríamos isso para "**No**" e, em vez disso, poderíamos acionar uma implantação manual com o botão de mesmo nome. Veja figura abaixo.

![manual_deploy](img_readme/manual_deploy.jpg)

Agora estamos prontos para clicar no botão ``Create Static Site`` e assistir o **Render** transformar nosso site para que fique ao vivo.


### **Passo 3. Ajustando o ``History Mode``**

Agora podemos clicar no link que o Render criou para nosso site, que no nosso caso é ``https://real-world-vue-3.onrender.com``, para visualizar nosso aplicativo ao vivo!

À medida que clicamos, parece que está funcionando. Mas observe o que acontece quando abrimos uma nova aba e tentamos ir para uma página específica, como: ```https://real-world-vue-3.onrender.com/event/123```.

![render_page_not_found](img_readme/render_page_not_found.jpg)

Oh não… estamos recebendo uma mensagem “**Not Found**” e há esse erro **404** no console. Por que isso está acontecendo?

No Tutorial 04 (**Vue Router Essentials**), vimos que nosso roteador está usando o modo de histórico (i.e. [**history mode**](https://router.vuejs.org/guide/essentials/history-mode.html)). Bem, isso agora se tornou muito relevante. Veja o conteúdo do arquivo "**src/router/index.js**".

```javascript
const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})
```

No modo de histórico, nosso aplicativo aproveita a API ``history.pushState`` do browser para alterar o URL sem recarregar a página. Veja a figura abaixo.

![understanding_history_mode](img_readme/understanding_history_mode.jpg)

O problema que estamos enfrentando atualmente é o fato de que nosso aplicativo é um aplicativo de página única (**SPA**), o que significa que tudo precisa ser servido a partir de "**index.html**". Embora nosso servidor de desenvolvimento tenha sido configurado para funcionar dessa maneira para nós, precisamos configurar as regras do Render para que ele sempre forneça "**index.html**", não importando em qual URL naveguemos.

Podemos fazer isso de maneira muito simples na guia Redirecionar/Reescrever (``Redirect/Rewrite``) do painel do nosso site estático:

![static_site_dashboard](img_readme/static_site_dashboard.jpg)

Adicionaremos um _catchall_  de ``/*`` e diremos a ele para sempre _Rewrite_ para ``/index.html`` Agora, não importa qual URL solicitamos, ele será servido a partir de "**index.html**". Problema resolvido.

A propósito… Se você está se perguntando por que tudo parecia funcionar bem inicialmente, antes de colar aquele URL em uma nova guia e tudo quebrar, é porque quando visitamos nosso novo site pela primeira vez, visitamos a rota raiz (``'/'`` ) que serviu inerentemente "**index.html**", e o modo de histórico assumiu a partir daí.

Com esse _catchall_ implementado, agora resolvemos nosso problema e implantamos nosso site com sucesso. Antes de terminarmos, vamos percorrer o Render um pouco mais para entender o que mais é possível.


### **Passo 4. Fazendo um Tour com o Render**

#### Guia (Tab) ``Events``

Já vimos a guia ``Redirects/Rewrites``, mas existem outras guias aqui que são igualmente úteis, como ``Events``, que mostra um histórico de implantações que foram feitas. É aqui que podemos executar uma reversão para uma compilação anterior, se necessário. Ver figura abaixo.

![render_events_tab](img_readme/render_events_tab.jpg)

#### Guia (Tab) ``Pull Requests``

Vamos explorar agora a guia ``Pull Request`` (**PR**). Nela, você pode habilitar os _pull requests_ e o Render criará automaticamente uma nova instância do seu site sempre que uma _pull request_ for criada em sua ramificação implantada (i.e. _deployed branch_). Com seu próprio URL, ele pode ser usado para revisar o código antes da fusão e será excluído automaticamente quando o **PR** for fechado. Isso facilita os testes e a colaboração.

Falando em colaboração, você também pode criar e trabalhar em equipes no Render, o qual um titular de conta individual pode criar a partir do menu suspenso conforme figura abaixo.

![render_team_collaboration](img_readme/render_team_collaboration.jpg)


#### Render efetua a escalabilidade com você

À medida que seu aplicativo escala, talvez com um back-end mais robusto ou alguma renderização do lado do servidor, você também pode escalar seus serviços do **Render** — horizontalmente (adicionar mais instâncias de um serviço) ou verticalmente (adicionar mais CPU e RAM a uma instância) — com recursos incluindo:

* Serviços web
* Bancos de Dados PostgreSQL gerenciados
* Tarefas cronológicas
* serviços privados
* Trabalhadores em segundo plano

E você pode escolher entre vários ambientes:

* Docker
* Node
* Ruby
* Go
* Elixir
* Python
* Rust


> Se você ficar travado ao usar o **Render**, eles também têm um [**fórum comunitário**](https://community.render.com/) que pode ajudá-lo a resolver o problema.


### **Passo 5. Fazendo o Fechamento**

Agora que terminamos de codificar nosso aplicativo e o implantamos, para onde vamos a partir daqui? Há muito mais recursos a serem adicionados e conceitos a serem conhecidos e, no próximo tutorial, veremos as diferentes maneiras de levar esse aplicativo para o próximo nível.

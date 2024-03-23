# Projeto ADS 5A Software Product
Código Fonte APP => https://github.com/lvteixeira/sp-blog-app

Código Fonte API => https://github.com/lvteixeira/sp-blog-api

# Blog Application
Projeto de prototipagem escrito para o desafio técnico de desenvolvimento de software da Tokio Marine. Consiste em aplicação web que possibilite o usuário agendar uma transação bancária vide regra de negócio.

# Decisões Arquiteturais
O planejamento do projeto teve foco na entrega dos requisitos funcionais explicitados no requisito visando entregar um protótipo de qualidade, com eficiência e no menor tempo possível.

Em um projeto de maior dimensão e.g: "O servidor recebe milhões de requisições de agendamento simultâneas e depende do processamento de informações por diferentes microsserviços para fazer uma transferência ou pagamento", certamente seria plausível implementar uma arquitetura de microsserviços com solução de mensageria. Para atender aos requisitos, uma arquitetura em três camadas com um banco de dados em memória, uma API REST e outro servidor responsável pela apresentação dos dados e interação com o usuário foi suficiente.

A api é orientada à serviços, no padrão MVCS, arquitetura REST recebendo e respondendo requisições HTTP no formato JSON. A arquitetura orientada à serviços provê melhor _readability_ e separação de responsabilidades (SRP), fazendo com que a regra de negócio seja aplicada de forma mais organizada, coesa e possa ser granularizada com maior facilidade de acordo com necessidades futuras, o que facilita alteração, manutenção, integração e portabilidade e escalabilidade.

O código da API utiliza o padrão de injeção de dependência, o que permite que uma classe obtenha suas dependências a partir de outra, tornando o código mais limpo e desacoplado, além de reutilizável e melhor testável. Uma classe de serviço pode injetar uma classe de repositório para acessar dados do banco de dados, um controlador pode injetar uma classe de serviço para processar solicitações HTTP, uma classe de configuração pode injetar uma classe de bean para configurar a aplicação.

Trafegar DTOs e não Entitys! O que trafega na camada de aplicação não é a serialização de um objeto Data Entity mas sim de um objeto de transferência de dados, provendo separação e melhor implementação do que diz respeito a modelagem de dados/regra de negócio e o que é devolvido ao cliente.

Por sua vez, o front end é um SPA responsável por prover a interface de usuário. As páginas HTML são renderizadas e dinamizadas de acordo com as ações do usuário utilizando React e Javascript. Para estilos, foi utilizado Prime React e Prime Flex CSS.

A componentizaçao das telas ajuda a desenhar o fluxo de funcionamento do app e facilita a implementação de novas funcionalidades pois ajuda na separação das responsabilidades, além de deixar o código mais organizado e facilitar ainda a configuração de estilos. O Prime Flex CSS fica responsável por aplicar estilos pré definidos direto no `className` do elemento otimizando a escrita de CSS e o Prime React é responsável pelo design dos componentes.

## Tech Stack

**Frontend:** Next.js(React), Prime React, Prime Flex CSS;

**Backend:** SpringBoot, Banco de Dados (h2);

A api foi escrita em Java, utilizando o framework Spring Boot persistindo dados em banco h2. Para a interface de usuário considerei a utilização do Next.js para facilitar a manipulação de eventos de ciclo de vida dos componentes, o que ajudou a acelerar a entrega do protótipo, além de ser um framework de alta performance (seu compilador é escrito em Rust) e de fácil integração com diversos recursos.

https://nextjs.org/docs/architecture/nextjs-compiler

https://swc.rs

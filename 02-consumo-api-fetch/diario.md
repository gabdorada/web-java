## Consumo de APIs com Fetch 🐱

### Visão Geral do Projeto
Neste projeto, desenvolvi uma aplicação web interativa que exibe curiosidades (fatos) sobre gatos acompanhadas de fotos fofas a cada clique de botão. 

Para proporcionar uma boa experiência de usuário totalmente em português, integrei **três APIs REST diferentes** atuando de forma assíncrona.

---

### APIs Utilizadas

1. **[Cat Facts API](https://catfact.ninja/fact)**
   * **Finalidade:** Fornecer fatos e curiosidades aleatórias sobre gatos (retorna em inglês).
   * **Formato de Resposta:** JSON com a propriedade `fact`.

2. **[MyMemory Translation API](https://mymemory.translated.net/)**
   * **Finalidade:** Traduzir em tempo real o fato obtido em inglês para o português do Brasil (`en|pt-BR`).
   * **Uso:** Encadeada logo após o retorno do texto da *Cat Facts API* usando `encodeURIComponent()`.

3. **[The Cat API](https://api.thecatapi.com/v1/images/search)**
   * **Finalidade:** Buscar imagens aleatórias de gatos em alta qualidade.
   * **Formato de Resposta:** Array de objetos JSON contendo a propriedade `url` da imagem.

---

## O que Aprendi e Principais Conceitos

### 1. Encadeamento de Requisições Asfíncronas (`fetch` + `.then()`)
* Aprendi como pegar o resultado de uma API (texto em inglês) e repassá-lo como entrada para outra API (tradutor) antes de renderizar a informação na tela.

### 2. Requisições Simultâneas
* O fato (texto) e a foto (imagem) são buscados em fluxos paralelos, permitindo que os dados sejam carregados simultaneamente ao clicar no botão.

### 3. Tratamento e Limpeza de Dados (Sanitização)
* **O desafio:** A API de tradução ocasionalmente retornava caracteres com barras de escape ou aspas formatadas incorretamente (ex: `\"alto\"`).
* **A solução:** Implementei uma rotina de tratamento de strings utilizando `.replaceAll()` para sanitizar o texto antes de exibi-lo no `<textarea>`:

  ```javascript
  let textoLimpo = textoTraduzido
      .replaceAll('\\"', '"')
      .replaceAll('\\', '');
    ```

---

## Demonstração do Funcionamento

Veja abaixo a aplicação realizando as chamadas das APIs e renderizando os dados na tela em tempo real:

<img src="./demonstracao.gif" alt="Demonstração do App" width="100%">

---
## Nota sobre o uso de IA e Aprendizado

Sendo bem transparente: para a construção deste projeto, utilizei a inteligência artificial como uma ferramenta de **mentoria e suporte técnico**. 

Em vez de apenas gerar código pronto, o foco foi usá-la para:
* Guiar o raciocínio na estruturação e encadeamento dos `fetch` assíncronos.
* Entender e debugar erros comuns (como erros de sintaxe, escopo de variáveis e respostas da API).
* Aprender a tratar e sanitizar retornos de texto incomuns (`.replaceAll()`).

A cada erro e ajuste, busquei compreender **o porquê** da solução aplicada, garantindo que o aprendizado do fluxo do consumo de APIs com JavaScript estivesse consolidado.

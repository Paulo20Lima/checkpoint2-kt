# 📲 Aplicativo Android - Cotação do Bitcoin em Tempo Real

👨‍🎓 **Aluno:** Paulo Henrique da Silva Lima  
🏫 **Turma:** 3SIR - FIAP

Este é um projeto Android desenvolvido em Kotlin que consome uma API pública do **Mercado Bitcoin** para mostrar a cotação atual do Bitcoin. O usuário pode atualizar o valor em tempo real clicando no botão **"Atualizar"**.

---

## 📸 Imagens  
![img2 (2)](https://github.com/user-attachments/assets/97561634-5af1-47f1-a388-15bb0a4f1b15)


*Capturas de tela realizada diretamente do meu celular durante os testes do aplicativo.*

---

## 🔧 Tecnologias e ferramentas utilizadas  

- **Kotlin** – Linguagem principal do app  
- **Android Studio** – Ambiente de desenvolvimento  
- **Retrofit** – Cliente HTTP utilizado para chamadas REST  
- **Gson Converter** – Conversor de JSON para objetos Kotlin  
- **Coroutines** – Utilizadas para chamadas assíncronas sem travar a interface  
- **Material Design** – Estilização da interface com Toolbar e componentes visuais  
- **API pública do Mercado Bitcoin** – Fonte dos dados de cotação  

---

## 📁 Estrutura e explicação dos arquivos Kotlin

### 1. `MainActivity.kt`  
Arquivo principal da aplicação, responsável por exibir os dados na interface e realizar a chamada à API.

**Responsabilidades:**  
- Configura a `Toolbar` com título e cores personalizadas  
- Detecta o clique no botão “Atualizar” e executa a função `makeRestCall()`  
- Realiza a requisição REST de forma assíncrona com Coroutines  
- Exibe o valor atual do Bitcoin e a data/hora da última atualização  

**Explicação das principais funções:**  
- `onCreate()` → Define o layout e configura o botão e a toolbar  
- `configureToolbar()` → Personaliza a barra superior com título e cor  
- `makeRestCall()` 
  - Cria uma Coroutine na thread principal  
  - Chama a API via Retrofit  
  - Trata o resultado e formata os dados com `NumberFormat` e `SimpleDateFormat`  
  - Mostra um `Toast` em caso de falha

### 🔍 Detalhe importante

O valor `last` representa o **último preço negociado do Bitcoin** e é obtido diretamente do objeto `Ticker`, que está dentro do `TickerResponse`, retornado pela API.

Este valor é acessado no código por meio da seguinte linha:

* val lastValue = tickerResponse?.ticker?.last?.toDoubleOrNull()

### 🧠 Como funciona?
**tickerResponse** é o corpo da resposta da API (TickerResponse).

* .ticker acessa o objeto Ticker dentro da resposta.

* .last pega o valor do último preço negociado do Bitcoin.

* .toDoubleOrNull() converte o valor para Double de forma segura, caso ele venha como String.

---

### 2. `MercadoBitcoinService.kt`  
Interface de comunicação com a API do Mercado Bitcoin (localizada no package `service`).

**Responsabilidades:**  
- Define o endpoint `GET api/BTC/ticker/` usando a anotação `@GET`  
- Retorna um objeto `TickerResponse` com os dados da API  

**Resumo:**  
- Interface com método `getTicker()`  
- Simplifica chamadas HTTP usando Retrofit  

---

### 3. `MercadoBitcoinServiceFactory.kt`  
Classe responsável por configurar o Retrofit para chamadas HTTP (também no package `service`).

**Responsabilidades:**  
- Define a URL base da API: `https://www.mercadobitcoin.net/`  
- Adiciona o conversor `GsonConverterFactory`  
- Retorna uma instância pronta da interface `MercadoBitcoinService`  

**Resumo:**  
- Usa `Retrofit.Builder()` com URL e conversor JSON  
- Cria o serviço com `.create(MercadoBitcoinService::class.java)`

---

### 4. `TickerResponse.kt`  
Modelos de dados utilizados para mapear a resposta JSON da API (localizado no package `model`).

**Estrutura dos dados:**  
A classe `TickerResponse` contém um único atributo `ticker`, do tipo `Ticker`, que representa os dados da cotação.

high: valor mais alto  
low: valor mais baixo  
vol: volume negociado  
last: último preço  
buy: preço de compra  
sell: preço de venda  
date: timestamp da cotação  

## 📲 Como usar  

- Baixe o projeto ou clone e abra no Android Studio  
- Execute em um dispositivo Android ou emulador  
- Clique em **Atualizar** para ver o valor atual do Bitcoin  
- Os dados serão exibidos com o preço em real e a data da última atualização
  
⚠ **É necessário ter conexão com internet**

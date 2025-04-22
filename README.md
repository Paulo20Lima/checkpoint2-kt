# 📲 Aplicativo Android - Cotação do Bitcoin em Tempo Real  

Este é um projeto Android desenvolvido em Kotlin que consome uma API pública do **Mercado Bitcoin** para mostrar a cotação atual do Bitcoin. O usuário pode atualizar o valor em tempo real clicando no botão **"Atualizar"**.

---

## 📸 Imagens  
![img](https://github.com/user-attachments/assets/1c160725-4fca-49f7-bd85-4732f2cc5729)

*Captura de tela realizada diretamente do meu celular durante os testes do aplicativo.*

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
- `makeRestCall()` →  
  - Cria uma Coroutine na thread principal  
  - Chama a API via Retrofit  
  - Trata o resultado e formata os dados com `NumberFormat` e `SimpleDateFormat`  
  - Mostra um `Toast` em caso de falha

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

```kotlin
high: valor mais alto  
low: valor mais baixo  
vol: volume negociado  
last: último preço  
buy: preço de compra  
sell: preço de venda  
date: timestamp da cotação  

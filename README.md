# 💵 Alerta de Cotação do Dólar com n8n

Automação desenvolvida em **n8n** para consultar automaticamente a cotação atual do dólar em relação ao real, analisar o valor e executar diferentes ações de acordo com a cotação encontrada.

O projeto utiliza uma API pública de câmbio, Google Sheets e Gmail.

---

## 🚀 O que essa automação faz?

O fluxo funciona da seguinte maneira:

1. Recebe uma requisição através de um Webhook.
2. Consulta a cotação atual do dólar.
3. Converte o valor retornado pela API.
4. Analisa a cotação utilizando um Switch.
5. Dependendo do valor:
   - registra a cotação em uma planilha;
   - ou envia um alerta por e-mail.

Fluxo resumido:

Webhook  
↓  
HTTP Request  
↓  
Cotação USD/BRL  
↓  
Conversão do valor  
↓  
Switch  
├── Cotação alta → Google Sheets  
└── Cotação baixa → Gmail  

---

## 🛠 Tecnologias utilizadas

- n8n
- REST API
- HTTP Request
- Webhook
- Google Sheets
- Gmail
- JSON
- AwesomeAPI
- Git
- GitHub

---

## 📊 API utilizada

A automação utiliza a **AwesomeAPI** para consultar a cotação USD/BRL.

Endpoint:

https://economia.awesomeapi.com.br/json/last/USD-BRL

A API retorna os dados atuais da cotação do dólar.

O workflow utiliza o campo `bid` retornado pela API e transforma o valor em um número que pode ser analisado pelo n8n.

---

## 🧠 Regras da automação

Depois de consultar a API, o workflow cria o campo:

`valor_convertido`

Esse valor é enviado para um node **Switch**.

Atualmente foram configuradas duas regras.

### 🔴 Cotação acima de R$ 5,30

Condição:

`valor_convertido > 5.30`

A cotação é direcionada para o fluxo identificado como:

`nao comprar`

Nesse caminho, o valor é registrado no Google Sheets.

### 🟢 Cotação menor ou igual a R$ 5,22

Condição:

`valor_convertido <= 5.22`

A cotação é direcionada para:

`comprar muito`

Nesse caso, o usuário recebe um alerta por e-mail informando que o dólar está em baixa.

---

## 📁 Estrutura do projeto

n8n-alerta-dolar/  
├── alerta-dolar.json  
└── README.md  

O arquivo principal do projeto é:

`alerta-dolar.json`

Ele contém toda a estrutura do workflow do n8n.

---

## 📥 Como instalar

### 1. Baixe o projeto

Você pode baixar pelo GitHub utilizando:

`Code → Download ZIP`

Ou pelo Git:

`git clone https://github.com/emanuelvitorfn7-gif/n8n-alerta-dolar.git`

Depois entre na pasta:

`cd n8n-alerta-dolar`

---

## 2. Abra o n8n

Você precisa ter uma instalação do n8n.

Em uma instalação local, normalmente o n8n pode ser acessado através de:

`http://localhost:5678`

Também é possível utilizar o n8n Cloud.

---

## 3. Importe o workflow

Dentro do n8n:

1. Abra a área de workflows.
2. Clique no menu do workflow.
3. Escolha a opção de importar arquivo.
4. Selecione:

`alerta-dolar.json`

O workflow será carregado no seu n8n.

---

## 🔑 Configure suas credenciais

As credenciais pessoais não devem ser compartilhadas pelo GitHub.

Por isso, quem importar o projeto deverá configurar suas próprias contas.

---

## 📈 Google Sheets

Abra o node:

`salva a cotaçao na planilha`

Conecte sua conta Google e escolha sua própria planilha.

A planilha pode possuir duas colunas:

| data | cotaçao |
|------|---------|
| 2026/10/04 18:30 | 5.21 |

Depois selecione a planilha e a aba desejada dentro do node do Google Sheets.

---

## 📧 Gmail

Abra o node:

`Send an Email`

Conecte sua própria conta Gmail.

Depois configure o endereço que receberá os alertas.

Você também pode personalizar:

- destinatário;
- assunto;
- conteúdo;
- mensagem do alerta.

Exemplo de mensagem:

**Assunto:** Cotação do dólar

**Mensagem:**

O dólar está em baixa.

Cotação atual: R$ 5.21

---

## 🌐 Webhook

O workflow começa através de um Webhook.

Método:

`POST`

Caminho configurado:

`nova_transaçao`

Depois de ativar o workflow, o n8n disponibilizará uma URL de produção.

Em uma instalação local, ela pode ser semelhante a:

`http://localhost:5678/webhook/nova_transaçao`

Você pode enviar uma requisição POST para iniciar o fluxo.

Exemplo no PowerShell:

`Invoke-WebRequest -Method POST -Uri "http://localhost:5678/webhook/nova_transaçao"`

Também é possível utilizar:

- Postman
- Insomnia
- curl
- outro sistema
- outra automação

---

## ▶️ Como executar

Depois de configurar Gmail e Google Sheets:

1. Importe o workflow.
2. Configure suas credenciais.
3. Escolha sua própria planilha.
4. Configure o e-mail de destino.
5. Ative o workflow.
6. Copie a URL de produção do Webhook.
7. Envie uma requisição POST.
8. O n8n consultará a cotação atual.
9. O valor será analisado.
10. O fluxo executará a ação correspondente.

Fluxo esperado:

Webhook  
↓  
HTTP Request  
↓  
Conversão Dolar X Real  
↓  
Switch  
↓  
Decisão  
├── Google Sheets  
└── Gmail  

---

## 🔧 Personalizando os valores

Você pode alterar os valores usados para decidir quando uma ação será executada.

Abra o node:

`cotaçao do dolar`

Depois altere as condições.

Por exemplo:

Comprar:

`<= 5.00`

Não comprar:

`> 5.50`

Assim, cada pessoa pode adaptar a automação conforme o objetivo do projeto.

---

## 🔄 Outras moedas

O projeto também pode ser adaptado para consultar outros pares de moedas.

Exemplos:

- EUR-BRL
- BTC-BRL
- USD-BRL

Para isso, é necessário alterar o endpoint da API e ajustar os campos utilizados no workflow.

---

## ⚠️ Aviso

Este projeto possui finalidade:

- educacional;
- demonstrativa;
- estudo de automação;
- integração de APIs;
- aprendizado de n8n.

As mensagens como `comprar` ou `não comprar` fazem parte da lógica demonstrativa da automação e não representam recomendação financeira.

---

## 🔐 Segurança

Nunca publique no GitHub:

- senhas;
- tokens;
- API Keys;
- credenciais OAuth;
- arquivos `.env`;
- credenciais pessoais.

Cada pessoa que baixar este projeto deve configurar suas próprias credenciais diretamente no n8n.

---

## 💡 Melhorias futuras

Algumas melhorias que podem ser adicionadas:

- Schedule Trigger para execução automática;
- alertas pelo Telegram;
- alertas pelo WhatsApp;
- histórico completo da cotação;
- banco de dados;
- dashboard;
- gráficos de variação;
- múltiplos níveis de alerta;
- suporte a diferentes moedas;
- tratamento de erros;
- logs de execução.

---

## 👨‍💻 Autor

**Emanuel Vítor Fernandes Nascimento**

Desenvolvimento Back-end e Automação

GitHub:

https://github.com/emanuelvitorfn7-gif

---

## ⭐ Sobre o projeto

Este projeto foi desenvolvido para praticar conceitos importantes de automação e desenvolvimento, incluindo:

- consumo de APIs REST;
- requisições HTTP;
- manipulação de JSON;
- lógica condicional;
- integração entre serviços;
- Webhooks;
- automação de e-mails;
- Google Sheets;
- Git;
- GitHub;
- n8n.

Se este projeto foi útil para seus estudos, considere deixar uma ⭐ no repositório.

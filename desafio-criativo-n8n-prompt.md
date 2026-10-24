[prompt_de_automa_o_n8n.md](https://github.com/user-attachments/files/33915844/prompt_de_automa_o_n8n.md)
# 🎯 Desafio Criativo: Planejando Automações com n8n

Este repositório contém a resolução do **Desafio Criativo** proposto na plataforma da DIO, focando no planejamento de automações no n8n a partir da criação de um prompt estruturado.

## 📝 1. Construção da Ideia (Passo a Passo)

Para chegar ao prompt ideal, o desafio foi dividido na definição clara das regras de negócio, ferramentas e atores envolvidos:

* **Objetivo da Automação:** Registrar automaticamente novos pedidos recebidos por um formulário de encomendas, salvando os dados e notificando a gestão.
* **Público/Responsável:** Eu mesma (otimizando a rotina do meu negócio artesanal).
* **Ferramentas Envolvidas:** Google Forms, Google Sheets e Gmail.
* **Regras Importantes:** Ignorar registros sem e-mail válido.

## 🚀 2. O Prompt Final e a Estrutura do Workflow

Com base nas definições acima, estruturamos o cenário e a lógica da nossa automação:

```text
Atue como um especialista em N8N.

Crie uma automação para registrar automaticamente novos pedidos recebidos por um formulário de encomendas, salvando os dados e notificando a gestão.

Público:
Eu mesma (otimizando a rotina do meu negócio artesanal).

Ferramentas envolvidas:
Google Forms, Google Sheets e Gmail.

Fluxo:
1. Receber uma nova resposta do formulário.
2. Registrar os dados na planilha.
3. Enviar um e-mail de confirmação.

Regras:
Ignorar registros sem e-mail válido.

### 🧩 Nós Utilizados (Nodes)

1. **Google Forms Trigger** (Gatilho)
2. **If** ou **Filter** (Validador de Regra)
3. **Google Sheets** (Armazenamento)
4. **Gmail** (Notificação)

### ⚙️ Lógica de Funcionamento Passo a Passo

**1. Nó de Entrada (Google Forms Trigger)**
* O que faz: Este nó fica "escutando" o seu formulário. Assim que um cliente preenche e clica em enviar, o n8n captura os dados em tempo real.
* Configuração: Autenticação da conta Google e seleção do formulário de encomendas específico.

**2. Nó de Validação (If Node / Filter)**
* O que faz: Aplica a regra de negócio solicitada ("Ignorar registros sem e-mail válido").
* Configuração: Condição apontando para o campo de e-mail capturado no passo 1. A regra verificará se o campo *não está vazio* e se *contém o caractere `@`*.
* Fluxo:
  * Caminho True (Verdadeiro): O e-mail é válido. O fluxo continua para o próximo nó.
  * Caminho False (Falso): O e-mail é inválido. A execução termina aqui silenciosamente.

**3. Nó de Armazenamento (Google Sheets)**
* O que faz: Conectado à saída "True" do nó anterior, pega os dados do pedido e insere em uma planilha de controle.
* Configuração: Operação definida como `Append Row` (Adicionar Linha). Mapeamento dos campos do formulário (Nome do Cliente, Produto, Quantidade, etc.) para as respectivas colunas da planilha.

**4. Nó de Notificação (Gmail)**
* O que faz: Envia o e-mail de confirmação automático, finalizando o processo.
* Configuração: Operação `Send Email`. No campo "To" (Para), utiliza-se o e-mail validado do cliente ou o da gestão. O corpo do e-mail utiliza variáveis para personalização (ex: "Olá {{Nome}}, recebemos sua encomenda!").

### 🔄 Resumo do Fluxo Visual

[Google Forms Trigger] ---> [IF Node] --- (True) ---> [Google Sheets] ---> [Gmail]
```

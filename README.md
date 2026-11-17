# Projeto Prático de QA: Validação de Fluxo de Login e API
Este repositório documenta meus estudos práticos em **Garantia de Qualidade de Software ( QA )*,aplicando análise de requisitos, leitura de fluxogramas, escrita de cenários de testes e validação básica de APIs.


## 1. Análise de Requisitos ( Regras de Negócios )
Sistema analisado: Tela de Autenticação de Usuário (Baseado no ambiente de testes SauceDemo).

*REQ-01:* O usuário deve informar um nome de usuário e senha válidos para acessar o sistema.
*REQ-02:* O sistema deve bloquear o acesso e exibir uma mensagem de erro caso a senha esteja incorreta.
*REQ-03:* O sistema não deve permitir o envio do formulário com campos obrigatórios vazios.


##2. Fluxograma Lógico de Validação Representação do fluxo de decisão durante a tentativa de login:

text
[Início]
    |
    V
(Usuário preenche Login e Senha)
    |
    V
<Campos estão preenchidos ?>--- Não ---> [Exibe erro: "Campo obrigatório"] ---> [Fim]
    |
    V
    Sim
    |
    v
    <Usuário e Senha Válidos?>---Não---> [Exibe erro:"Dados inválidos"] ---> [Fim]
    |
    V
    Sim
    |
    V
    [Redireciona para a tela inicial]
    |
    V
    [Fim]



##3. Cenário de Testes (Formato BDD)

### Cenário 01: Login com sucesso
°*Dados* que o usuário está na página de login
°*Quando* preenche o usuário válido "standard_user" e a senha "secret_sauce"
°*E* clica no botão "Login"
°*Então* o sistema deve redirecionar para a vitrine de produtos.

### Cenário 02: Login com senha inválida
° *Dado* que o usuário está na página de login
° *Quando* preenche um usuário válido e uma senha incorreta
° *E* clica no botão "Login"
° *Então* o sistema deve manter o usuário na tela e exibir mensagem de credenciais inválidas.

### Cenário 03: Tentativa de login com  campos em branco
° *Dados* que o usuário está na página de login
° *Quando* clica no botão "Login" sem preencher os campos
° *Então* o sistema deve exibir alerta indicando que o nome de usuário é obrigatório.

### Cenário 04: Reporte de Bug (Exemplo Documentado)
° *Título:* Botão de login permite múltiplos cliques seguidos durante lentidão de rede.
° *Severidade:* Baixa | *Prioridade:* Média
° *Passo a passo:* 1. Acessar tela de login; 2. Inserir dados válidos; 3. Clicar rapidamente 3 vezes no botão "Login".
° *Resultado Esperado:* O botão deve ficar desabilitado após o primeiro clique.
° *Resultado Atual:* O sistema envia múltipla requisições simultâneas.

### Cenário 05: Validação Básica de API (Consultoria CEP)
Teste de requisição HTTP GET realizado na API pública ViaCEP:
° *Endpoint:* https://viacep.com.br
° *Método:* GET
° *Status Code Esperando:* 200 ok
° Validação:* Retorno em formato JSON contendo os campos cep , logradouro e uf preenchidos corretamente.

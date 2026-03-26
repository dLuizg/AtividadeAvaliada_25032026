# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Luiz Gustavo Paliares Diniz  
RA: 25001239
Data: 25/03/2026  

---

# 1. Definição do MVP
Descreva aqui **qual parte do sistema** foi incluída no seu MVP.  
Explique claramente:

- O que está **dentro** do MVP  
- O que está **fora** do MVP  
- Por que você fez essas escolhas  

Exemplo de início:  
> “Meu MVP cobre o processo de venda desde a identificação/cadastro do cliente até a emissão do comprovante, incluindo tratamento de estoque insuficiente.”

---

# 2. Regras de Negócio (mínimo: 5)
Liste e descreva **cada RN** de forma clara.

**RN01 — Vendas a prazo devem gerar automaticamente um lançamento em contas a receber com data de vencimento e status "Aberta"**
Toda venda realizada na modalidade a prazo deve, no momento da confirmação, criar automaticamente um registro no módulo de contas a receber, contendo o valor total, a data de vencimento conforme o prazo acordado e o status inicial "Aberta". O registro só deve ser encerrado após a confirmação do pagamento pelo operador ou pelo sistema.

**RN02 — Solicitar abastecimento do estoque quando estiver baixo**
O sistema deve monitorar continuamente o nível de estoque de cada produto e, ao atingir ou ultrapassar o ponto de reposição definido no cadastro do produto, gerar automaticamente uma solicitação de compra ou um alerta para o responsável pelo abastecimento. Cada produto pode ter seu próprio ponto de reposição configurável.

**RN03 — Bloquear venda de produtos sem estoque**
O sistema não deve permitir a finalização de uma venda que contenha produtos com quantidade zero ou insuficiente no estoque da unidade. A tentativa deve ser bloqueada com uma mensagem clara ao operador, indicando o produto e a quantidade disponível, impedindo assim vendas de itens inexistentes fisicamente.

**RN04 — Ao final de cada dia o sistema deve enviar o relatório para o gerente**
Diariamente, em horário configurável pelo administrador, o sistema deve compilar e enviar automaticamente um relatório de fechamento ao gerente da unidade, contendo informações como total de vendas, receitas, movimentações de estoque e ocorrências relevantes do dia. O envio deve ocorrer mesmo que não haja movimentações, registrando o dia como sem atividade.

**RN05 — Compras de fornecedores devem gerar automaticamente um lançamento em contas a pagar e atualizar o estoque da unidade recebedora.**
Ao registrar a entrada de uma compra de fornecedor, o sistema deve realizar duas ações automáticas e simultâneas: criar um lançamento no módulo de contas a pagar com o valor, a data de vencimento e o fornecedor vinculados; e atualizar o saldo de estoque da unidade recebedora com os itens e quantidades constantes na nota de entrada.

**RN06 — Produtos controlados só podem ser vendidos mediante validação de receita por um farmacêutico.**
Medicamentos classificados como controlados não podem ser vendidos sem que um farmacêutico responsável valide a receita médica apresentada pelo cliente. O sistema deve identificar automaticamente esses produtos pelo cadastro, solicitar o registro da receita e exigir a confirmação do farmacêutico antes de prosseguir com a venda, bloqueando qualquer tentativa de finalização sem essa etapa.

---

# 3. Requisitos Funcionais (mínimo: 8)
Liste os requisitos funcionais do seu MVP.

**RF01 —  Permitir login de usuários**
O sistema deve disponibilizar uma tela de autenticação onde cada usuário acessa com credenciais próprias (usuário e senha). O acesso às funcionalidades deve ser liberado conforme o perfil atribuído ao usuário, como atendente, farmacêutico, gerente ou administrador.

**RF02 —  Permitir cadastro de unidades**
O sistema deve permitir o cadastro e a gestão de múltiplas unidades da farmácia, contendo dados como nome, endereço, CNPJ e farmacêutico responsável. Cada unidade deve operar com estoque próprio e dados isolados, mas visíveis para a gestão central.

**RF03 —  Processar vendas**
O sistema deve permitir ao atendente registrar vendas, adicionando produtos por código de barras ou busca, selecionando a forma de pagamento (dinheiro, cartão, PIX ou a prazo) e emitindo o comprovante ao final. Vendas com produtos controlados devem seguir o fluxo de validação de receita.

**RF04 —  Cadastrar produtos**
O sistema deve permitir o cadastro completo de produtos, incluindo nome, código de barras, categoria, fornecedor, preço de custo e venda, unidade de medida, ponto de reposição e classificação (produto comum ou controlado). O cadastro deve ser acessível apenas por perfis autorizados.

**RF05 —  Calcular estoque**
O sistema deve manter o controle de estoque em tempo real por unidade, atualizando automaticamente as quantidades a cada venda, entrada de compra, devolução, perda ou transferência registrada. Deve exibir o saldo atual e alertar quando o estoque atingir o ponto de reposição.

**RF06 —  Gerar relatórios**
O sistema deve permitir a geração de relatórios gerenciais, incluindo:

vendas por período
produtos mais vendidos
posição de estoque
contas a receber e a pagar
movimentações por unidade

**RF07 —  Registrar devoluções, perdas e transferências de estoque.**
O sistema deve permitir o registro de devoluções de clientes, perdas (vencimento, avaria) e transferências entre unidades, com justificativa obrigatória em cada caso. Todas as movimentações devem impactar automaticamente o saldo de estoque e gerar histórico rastreável.

**RF08 —  Cadastrar e consultar clientes, vinculando compras ao histórico.**
O sistema deve permitir o cadastro de clientes com dados pessoais e de contato, possibilitando vincular cada venda ao cadastro do cliente. O histórico de compras deve ser consultável por atendentes e gerentes, facilitando o atendimento e o rastreamento de receitas de produtos controlados.

---

# 4. Requisitos Não Funcionais (mínimo: 4)
Liste os RNFs do sistema conforme seu MVP.

**RNF01 — O sistema deve responder em até 2 segundos**
Todas as operações principais, como registrar uma venda, consultar estoque ou autenticar um usuário, devem ser concluídas e retornar resposta ao operador em no máximo 2 segundos, garantindo agilidade no atendimento ao cliente na frente de caixa.

**RNF02 — Sistema deve estar disponível 99,9% do tempo**
O sistema deve operar com disponibilidade mínima de 99,9%, o que equivale a menos de 9 horas de indisponibilidade por ano. Manutenções programadas devem ser comunicadas com antecedência e realizadas em períodos de baixo movimento, como madrugada.

**RNF03 — O sistema deve autenticar usuários e restringir acesso conforme perfil**
O sistema deve implementar controle de acesso baseado em perfis, garantindo que cada usuário visualize e opere apenas as funcionalidades pertinentes ao seu cargo. Atendentes não devem acessar relatórios financeiros, assim como apenas farmacêuticos devem validar receitas de produtos controlados.

**RNF04 — A interface deve ser simples o suficiente para uso por atendentes sem treinamento técnico avançado.**
A interface do sistema deve ser intuitiva e objetiva, com fluxos de venda e consulta de estoque acessíveis sem necessidade de treinamento técnico aprofundado. Elementos visuais claros, mensagens de erro compreensíveis e poucos cliques para as operações do dia a dia são requisitos de usabilidade esperados.

---

# 5. Casos de Uso (mínimo: 10)
### Inserir **diagrama de casos de uso geral**, demonstrando claramente:
- os 10 casos
- relação entre eles e atores
- pelo menos 3 includes
- pelo menos 3 extends

---

# 6. Documentação dos Casos de Uso
Para **cada caso de uso**, utilize o template abaixo:
---

## **UC01 — Cadastrar funcionáiro**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC02 — Cadastrar unidade**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC03 — Cadastrar produtos**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC04 — Cadastrar cliente**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC05 —  Validar receita**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC06 — Processar vendas**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC07 — Nome do Caso de Uso**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC08 — Registrar compra**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC09 — Calcular estoque**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC10 — Gerar relatórios**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC11 — Registrar Baixa em Conta a PagarFinanceiro**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## **UC12 — Solicitar transferencia entre unidades**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---
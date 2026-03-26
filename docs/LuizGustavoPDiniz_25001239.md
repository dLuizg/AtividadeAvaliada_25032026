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

## **UC01 — Cadastrar funcionário**
**Ator(es):** Administrador ou Gerente.
**Descrição:** Permite a inclusão de novos colaboradores no sistema, definindo suas credenciais de acesso e perfil (Atendente, Farmacêutico, etc.).
**Pré-condições:** Usuário autenticado com perfil de gestor; Unidade de trabalho já cadastrada.
**Pós-condições:** Funcionário habilitado para operar o sistema conforme seu perfil.

### Fluxo Principal
1. O gestor acessa o menu "Configurações" e seleciona "Cadastrar Funcionário".
2. O sistema exibe o formulário de cadastro (Nome, CPF, Cargo, Unidade, Login e Senha).
3. O gestor preenche os dados e confirma.
4. O sistema valida os dados e salva o registro.

### Fluxos Alternativos / Exceções
- **FA01 — CPF já cadastrado:** O sistema impede o registro e sugere a edição do perfil existente.
- **FA02 — Dados incompletos:** O sistema destaca os campos obrigatórios vazios.

### Relacionamentos
- **Include:** N/A

---

## **UC02 — Cadastrar unidade**
**Ator(es):** Administrador.
**Descrição:** Registro de uma nova filial ou matriz da rede no sistema.
**Pré-condições:** Usuário autenticado como Administrador.
**Pós-condições:** Nova unidade disponível para alocação de estoque e funcionários.

### Fluxo Principal
1. O administrador seleciona "Gestão de Unidades" e "Nova Unidade".
2. Insere CNPJ, Razão Social, Endereço e Farmacêutico Responsável.
3. O sistema valida o CNPJ via integração ou máscara de dados.
4. O administrador confirma a gravação.

### Fluxos Alternativos / Exceções
- **FA01 — CNPJ Inválido:** O sistema emite alerta e impede o salvamento.

### Relacionamentos
- **Include:** N/A

---

## **UC03 — Cadastrar produtos**
**Ator(es):** Gerente ou Administrador.
**Descrição:** Inclusão de novos medicamentos ou itens de conveniência no catálogo global.
**Pré-condições:** Usuário autenticado; Categoria do produto existente.
**Pós-condições:** Produto disponível para entrada de estoque e venda.

### Fluxo Principal
1. O ator acessa "Cadastro de Produtos".
2. Preenche Nome, Código de Barras, Tipo (Controlado ou Comum) e Preço.
3. Define o ponto de reposição (estoque mínimo).
4. O sistema salva os dados e gera o ID único.

### Fluxos Alternativos / Exceções
- **FA01 — Código de barras duplicado:** O sistema informa que o produto já existe.

### Relacionamentos
- **Include:** N/A

---

## **UC04 — Cadastrar cliente**
**Ator(es):** Atendente ou Gerente.
**Descrição:** Registro de dados pessoais de clientes para histórico de compras e vendas a prazo.
**Pré-condições:** Usuário autenticado.
**Pós-condições:** Cliente apto a realizar compras vinculadas ao CPF.

### Fluxo Principal
1. O atendente acessa o módulo "Clientes".
2. Insere Nome, CPF, Telefone e Endereço.
3. O sistema valida o CPF.
4. O atendente confirma o cadastro.

### Fluxos Alternativos / Exceções
- **FA01 — Cliente já cadastrado:** O sistema abre a tela de edição/consulta.

### Relacionamentos
- **Extend:** Este caso de uso estende o **UC06 (Processar Vendas)** quando o cliente não é encontrado.

---

## **UC05 — Validar receita**
**Ator(es):** Farmacêutico.
**Descrição:** Conferência e registro de receita médica para liberação de medicamentos controlados.
**Pré-condições:** Venda de produto controlado iniciada.
**Pós-condições:** Item liberado para finalização da venda.

### Fluxo Principal
1. O farmacêutico recebe a solicitação de validação no sistema.
2. Insere os dados da receita (Médico, CRM, Data).
3. Anexa ou confirma a retenção da receita.
4. O sistema marca o item como "Validado".

### Fluxos Alternativos / Exceções
- **FA01 — Receita Vencida:** O farmacêutico nega a validação e o sistema bloqueia o item na venda.

### Relacionamentos
- **Extend:** Estende o **UC06 (Processar Vendas)** em caso de produtos restritos.

---

## **UC06 — Processar vendas**
**Ator(es):** Atendente.
**Descrição:** Registro de itens, escolha de pagamento e finalização da transação comercial.
**Pré-condições:** Usuário autenticado; Estoque disponível.
**Pós-condições:** Venda concluída, estoque baixado e comprovante emitido.

### Fluxo Principal
1. O atendente lê os códigos de barras dos produtos.
2. O sistema identifica os itens e soma os valores.
3. O atendente seleciona a forma de pagamento.
4. O sistema finaliza a venda e emite o cupom.

### Fluxos Alternativos / Exceções
- **FA01 — Pagamento a Prazo:** O sistema gera registro em Contas a Receber (RN01).
- **FA02 — Estoque insuficiente:** O sistema bloqueia a venda (RN03).

### Relacionamentos
- **Include:** **UC09 (Calcular estoque)** — obrigatório para atualizar o saldo.
- **Extend:** **UC05 (Validar receita)** e **UC04 (Cadastrar cliente)**.



---

## **UC07 — Gerar Alerta de Estoque Baixo**
**Ator(es):** Sistema (Automático).
**Descrição:** Notifica o gerente quando um item atinge o ponto de reposição.
**Pré-condições:** Alteração no saldo de estoque (venda ou perda).
**Pós-condições:** Alerta visível no painel do gerente.

### Fluxo Principal
1. O sistema verifica o saldo após cada movimentação.
2. Compara o saldo atual com o ponto de reposição definido no **UC03**.
3. Se Saldo $\le$ Ponto de Reposição, o sistema gera uma notificação de alerta.

### Relacionamentos
- **Extend:** Estende o **UC09 (Calcular estoque)**.

---

## **UC08 — Registrar compra**
**Ator(es):** Gerente ou Setor Financeiro.
**Descrição:** Entrada de mercadorias enviadas por fornecedores.
**Pré-condições:** Fornecedor cadastrado.
**Pós-condições:** Estoque atualizado e lançamento em Contas a Pagar.

### Fluxo Principal
1. O ator seleciona "Entrada de Nota Fiscal/Compra".
2. Insere os produtos e quantidades recebidas.
3. O sistema atualiza o custo médio e o saldo.
4. O sistema gera a duplicata no financeiro (RN05).

### Relacionamentos
- **Include:** **UC09 (Calcular estoque)**.

---

## **UC09 — Calcular estoque**
**Ator(es):** Sistema.
**Descrição:** Motor lógico que soma ou subtrai itens do inventário em tempo real.
**Pré-condições:** Movimentação de estoque iniciada (venda, compra, devolução).
**Pós-condições:** Saldo de estoque atualizado.

### Fluxo Principal
1. Recebe a quantidade e o tipo de operação (+ ou -).
2. Localiza o registro do produto na unidade específica.
3. Aplica a operação aritmética no banco de dados.
4. Registra o log da movimentação.

### Relacionamentos
- **Include:** Acionado por **UC06**, **UC08** e **UC12**.
- **Extend:** **UC07 (Gerar Alerta de Estoque Baixo)**.

---

## **UC10 — Gerar relatórios**
**Ator(es):** Gerente ou Financeiro.
**Descrição:** Compilação de dados sobre vendas, financeiro e estoque para análise.
**Pré-condições:** Existência de dados no período selecionado.
**Pós-condições:** Relatório exibido em tela ou exportado.

### Fluxo Principal
1. O ator escolhe o tipo de relatório (ex: Vendas por período).
2. Define os filtros (data, unidade).
3. O sistema processa os dados e gera o visual.

### Relacionamentos
- **Include:** **Autenticação de Usuário** (Para garantir permissão de acesso).

---

## **UC11 — Registrar Baixa em Conta a Pagar**
**Ator(es):** Financeiro.
**Descrição:** Baixa manual de boletos de fornecedores ou despesas fixas.
**Pré-condições:** Conta lançada no sistema com status "Aberta".
**Pós-condições:** Status alterado para "Paga" e registro de data de pagamento.

### Fluxo Principal
1. O financeiro pesquisa a conta por vencimento ou fornecedor.
2. Seleciona a conta e informa a data/forma de pagamento.
3. O sistema confirma a liquidação do título.

---

## **UC12 — Solicitar transferência entre unidades**
**Ator(es):** Gerente.
**Descrição:** Movimentação de itens de uma filial para outra para suprir demandas urgentes.
**Pré-condições:** Estoque disponível na unidade de origem.
**Pós-condições:** Saldo debitado na origem e creditado no destino.

### Fluxo Principal
1. O gerente da unidade A solicita itens da unidade B.
2. O sistema verifica a disponibilidade na unidade B.
3. Ao confirmar a saída, o sistema abate o estoque de B e adiciona em A.

### Relacionamentos
- **Include:** **UC09 (Calcular estoque)**.


### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---
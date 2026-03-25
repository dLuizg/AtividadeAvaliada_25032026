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
**RN02 — Solicitar abastecimento do estoque quando estiver baixo**
**RN03 — Bloquear venda de produtos sem estoque**
**RN04 — Ao final de cada dia o sistema deve enviar o relatório para o gerente**
**RN05 — Compras de fornecedores devem gerar automaticamente um lançamento em contas a pagar e atualizar o estoque da unidade recebedora.**
**RN06 — Produtos controlados só podem ser vendidos mediante validação de receita por um farmacêutico.**

(Adicione mais se quiser.)

---

# 3. Requisitos Funcionais (mínimo: 8)
Liste os requisitos funcionais do seu MVP.

**RF01 —  Permitir login de usuários**
**RF02 —  Permitir cadastro de unidades**
**RF03 —  Processar vendas**
**RF04 —  Cadastrar produtos**
**RF05 —  Calcular estoque**
**RF06 —  Gerar relatórios**
**RF07 —  Registrar devoluções, perdas e transferências de estoque.**
**RF08 —  Cadastrar e consultar clientes, vinculando compras ao histórico.**

(Adicione mais se quiser.)

---

# 4. Requisitos Não Funcionais (mínimo: 4)
Liste os RNFs do sistema conforme seu MVP.

**RNF01 — O sistema deve responder em até 2 segundos**
**RNF02 — Sistema deve estar disponível 99,9% do tempo**
**RNF03 — O sistema deve autenticar usuários e restringir acesso conforme perfil**
**RNF04 — A interface deve ser simples o suficiente para uso por atendentes sem treinamento técnico avançado.**

(Adicione mais se quiser.)

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

## **UCXX — Nome do Caso de Uso**
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

> Repita essa estrutura para **todos os seus casos de uso** (mínimo 10).


Casos de uso:
- Cadastrar unidade
- Cadastrar usuários
- Cadastrar produtos
- Cadastrar cliente
- Validar receita
- Processar vendas
- Registrar compra
- Calcular estoque
- Gerar relatórios
- Registrar Baixa em Conta a PagarFinanceiro
- Registrar Baixa em Conta a ReceberFinanceiro
- Solicitar transferencia entre unidades


# 🦁 Lion App - Simulador de Imposto de Renda em Excel

> Um simulador prático e intuitivo em Excel para desmistificar a declaração de Imposto de Renda (IRPF) e apoiar quem não tem o hábito de declarar por conta própria.

---

## 🎯 Sobre o Projeto

Fazer a declaração do Imposto de Renda pela primeira vez ou sem auxílio profissional costuma ser um desafio: termos técnicos difíceis, diversos informes bancários dispersos e a complexidade do programa oficial da Receita Federal.

O **Lion App** foi desenvolvido para funcionar como um **guia preparatório e simulador prévio**. Com ele, o contribuinte reúne, organiza e valida suas informações fiscais em etapas simples antes de fazer o envio definitivo à Receita Federal.

---

## ✨ Recursos da Aplicação

O arquivo [`Lion_app.xlsx`](./Lion_app.xlsx) é dividido em seções planejadas de forma sequencial:

### 1. 👤 Dados do Titular (`TITULAR`)
- Coleta de dados cadastrais essenciais (Nome, CPF, Data de Nascimento, Cônjuge, Endereço e Contatos).
- Controle de **dependentes**.
- Registro de situação cadastral (ex: residente no exterior, alterações em relação ao ano anterior).

### 2. 🏦 Informes de Rendimentos Bancários (`INFORMES`)
- Lista integrada com mais de 50 instituições bancárias e fintechs (Banco do Brasil, Caixa, Itaú, Bradesco, Santander, Nubank, Inter, XP Investimentos, PicPay, PagBank, C6 Bank, entre outros).
- Registro detalhado dos valores em conta, aplicações e investimentos informados pelas instituições.
- Mapeamento e controle de anexos comprobatórios (PDFs dos informes bancários).

### 3. 📑 Entradas, Holerites e Notas Fiscais (`NOTAS`)
- Controle cronológico mês a mês das receitas recebidas (salários, prestação de serviços, pró-labore).
- Categorização clara dos lançamentos para apuração correta dos rendimentos tributáveis.
- Totalizadores automáticos para comparação com a base de cálculo.

---

## 📂 Estrutura das Planilhas

```text
Lion_app.xlsx
 │
 ├── 📋 TITULAR    -> Cadastro pessoal, dependentes e status declaratório
 ├── 🏦 INFORMES   -> Saldos bancários, lista de bancos e links para comprovantes
 └── 📄 NOTAS      -> Lançamento mensal de entradas (salários, holerites e notas)
```

---

## 🚀 Como Utilizar

1. **Baixar o arquivo**: Faça o download do [`Lion_app.xlsx`](./Lion_app.xlsx).
2. **Abrir no Excel**: Compatível com Microsoft Excel (Desktop ou Web).
3. **Preencher na ordem recomendada**:
   1. Comece pela aba **TITULAR** com seus dados pessoais e de dependentes.
   2. Em seguida, na aba **INFORMES**, selecione seus bancos e insira os saldos informados no documento anual fornecido por cada instituição.
   3. Na aba **NOTAS**, lance os seus rendimentos de cada mês (holerites, notas fiscais, rendas extras).
4. **Conferência**: Use o resumo final para facilitar o preenchimento do programa da Receita Federal ou para conferência contábil.

---

## 🛠️ Tecnologias e Ferramentas

- **Microsoft Excel**: Listas suspensas de validação de dados, fórmulas de consolidação e organização modular.
- **Git & GitHub**: Versionamento de código e compartilhamento open-source.

---

## ⚠️ Aviso Legal

> Este projeto é uma ferramenta de apoio educacional e simulador de organização pessoal, não substituindo o **Programa Gerador de Declaração (PGD)** ou o portal oficial **e-CAC da Receita Federal do Brasil**.

---

## 👨‍💻 Autor

Desenvolvido por **Edson** no âmbito de estudos e projetos práticos com Excel e Inteligência Artificial.

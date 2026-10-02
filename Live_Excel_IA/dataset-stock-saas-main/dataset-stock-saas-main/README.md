<div align="center">

<h1>🧪 SaaS Data Lab</h1>

<p>Doze exportações mensais de um SaaS de assinaturas, propositalmente "sujas", para um laboratório de tratamento de dados com IA.</p>

<p></p>

<a href="#-introdução">Introdução</a>
<span>&nbsp;&nbsp;❖&nbsp;&nbsp;</span>
<a href="#-começando">Começando</a>
<span>&nbsp;&nbsp;❖&nbsp;&nbsp;</span>
<a href="#-formato-dos-arquivos">Formato</a>
<span>&nbsp;&nbsp;❖&nbsp;&nbsp;</span>
<a href="#-problemas-propositais">Problemas</a>
<span>&nbsp;&nbsp;❖&nbsp;&nbsp;</span>
<a href="#-exercícios">Exercícios</a>
<span>&nbsp;&nbsp;❖&nbsp;&nbsp;</span>
<a href="#-contribuir">Contribuir</a>

![Lab Badge](https://img.shields.io/badge/Lab-Tratamento_de_dados_com_IA-8957E5?style=flat)
![CSV Badge](https://img.shields.io/badge/Formato-CSV_bruto-1F6FEB?style=flat)
![Linhas Badge](https://img.shields.io/badge/Linhas-~40.6k-217346?style=flat)
![Competência Badge](https://img.shields.io/badge/Compet%C3%AAncia-2025-D29922?style=flat)
![Python Badge](https://img.shields.io/badge/Script-Python_3-3776AB?logo=python&logoColor=fff&style=flat)
![GitHub repo size](https://img.shields.io/github/repo-size/digitalinnovationone/dataset-stock-saas)
![GitHub last commit](https://img.shields.io/github/last-commit/digitalinnovationone/dataset-stock-saas)

</div>

## 🧪 Introdução

[**SaaS Data Lab**](https://github.com/digitalinnovationone/dataset-stock-saas) é um dataset para **laboratório de tratamento de dados com IA**, construído sobre exportações brutas de um sistema fictício de assinaturas SaaS. Os arquivos reproduzem o que sai de um "Salvar como CSV" real: bloco de metadados no topo, rodapé misturado aos dados, colunas que mudam de nome no meio do ano e valores fora do padrão.

- 📦 **12 arquivos CSV mensais** (`saas_assinaturas_2025_MM_mes.csv`), de janeiro a dezembro de 2025.
- 📊 Aproximadamente **40.627 linhas brutas** no conjunto completo.
- 📘 Uma planilha `.xlsx` de **dimensões de referência** com os planos e status oficiais.
- 🧨 **Problemas de qualidade propositais**: nulos, duplicidades, datas mistas, moeda como texto, schema drift.
- 🎯 Foco em **limpeza, padronização, tipagem, deduplicação e métricas de SaaS** (MRR, churn, inadimplência) com apoio de IA.

## 🚀 Começando

> Use a ferramenta de IA e o ambiente de dados de sua preferência. O laboratório não depende de nenhuma ferramenta específica.

### - Baixar

```bash
# com git:
git clone https://github.com/digitalinnovationone/dataset-stock-saas.git

# ou pelo GitHub:
# Code → Download ZIP
```

### - Explorar

Antes de tratar, olhe as primeiras e as últimas linhas de um arquivo para entender a estrutura da exportação:

```bash
# bloco de metadados + cabeçalho:
head -n 10 01_bases_mensais/saas_assinaturas_2025_09_set.csv

# rodapé:
tail -n 4 01_bases_mensais/saas_assinaturas_2025_09_set.csv
```

### - Tratar

O tratamento precisa resolver, no mínimo, estes pontos em cada arquivo antes de consolidar os 12 meses em uma única tabela:

- **Localizar o cabeçalho dinamicamente**: é a linha cujo primeiro campo é `assinatura_id`. Tudo acima dela é metadado da exportação.
- **Descartar o rodapé**: as linhas `Total de registros;N` e `Fim da exportacao`, além das linhas em branco.
- **Unificar os nomes de coluna**: alguns meses renomeiam, removem ou adicionam colunas (veja [Mudanças de schema](#-mudanças-de-schema)).
- **Não assumir largura fixa**: os arquivos têm 41, 42 ou 43 colunas.

> ✍️ Prompt de partida para a IA, com os fatos que ela precisa saber sobre os arquivos:

```text
Tenho 12 exportações mensais em CSV (separador ";", UTF-8 com BOM, quebra de linha CRLF).
O cabeçalho não está na primeira linha: é a linha cujo primeiro campo é "assinatura_id",
e cai entre a linha 6 e a linha 9 dependendo do arquivo. Acima dele há um bloco de
metadados (Competencia, Sistema origem, Gerado em e, em alguns meses, Usuario, Filtro e
Fuso horario). No fim há uma linha em branco, "Total de registros;N" e "Fim da exportacao".
Os nomes de coluna mudam em alguns meses. Consolide tudo em uma tabela única e limpa.
```

> 💡 Bônus: extraia `Competencia` e `Sistema origem` do bloco de metadados e adicione-os como colunas na tabela consolidada.

## 📁 Formato dos arquivos

- Separador `;`, codificação **UTF-8 com BOM**, quebra de linha **CRLF**.
- Números tipados exportados com **vírgula decimal** (`49,9`); datas como `dd/mm/yyyy` e data-hora como `dd/mm/yyyy hh:mm:ss`. Valores que já eram texto mantêm a forma original (`R$ 299,90`, `129.90`, `27-01-25`, `2024-07-08`).
- **O cabeçalho não está na primeira linha.** Cada arquivo começa com um bloco de metadados da exportação (título, competência, sistema de origem, gerado em e, em alguns meses, usuário, filtro e fuso horário), seguido de uma linha em branco. Como o bloco varia de tamanho, o cabeçalho cai **entre a linha 6 e a linha 9**.
- **Rodapé** em todos os arquivos: linha em branco, `Total de registros;N` e `Fim da exportacao`.
- Linhas completamente vazias do sistema aparecem como uma sequência de `;`.

**Anatomia de um arquivo** (setembro, com duas linhas opcionais de metadados e a coluna extra `taxa_setup`):

```text
Relatorio de assinaturas - exportacao bruta
Competencia;2025-09
Sistema origem;crm_export
Gerado em;30/09/2025 23:50:00
Usuario;integracao.bi
Fuso horario;America/Sao_Paulo

assinatura_id;cliente_id;empresa;contato_principal;email;pais;uf;...;taxa_setup
SUB-002799;CLI-002206;Pulse Digital;Thiago Rodrigues;thiago_rodrigues163corp.io;Brasil;PR;...
SUB-002929;CLI-001476;Pulse Studio;Gustavo Nascimento;gustavo_nascimento359@gmail.com;Brasil;BA;...
...

Total de registros;4090
Fim da exportacao
```

## 🧨 Problemas propositais

- Valores nulos em campos críticos e não críticos.
- Duplicidades exatas e quase duplicidades.
- Datas em múltiplos formatos.
- Valores monetários como número e como texto (`R$`, vírgula decimal, espaços).
- Planos e status com caixa, espaços e aliases inconsistentes.
- IDs com espaços extras.
- E-mails inválidos e ausentes.
- Moeda escrita de formas diferentes (`BRL`, `Real`).
- Linhas completamente em branco dentro do dataset.
- Valores impossíveis ocasionais, como `seats_ativos > seats_contratados`, seats negativos e preço líquido negativo.
- Inconsistências de regra de negócio entre status e data de cancelamento.
- Pequeno percentual de registros omitidos em determinadas competências.
- **Schema drift** em alguns meses: colunas renomeadas, removidas ou adicionadas.
- **Cabeçalho fora da linha 1**, em posição diferente em cada arquivo, com bloco de metadados acima.
- **Rodapé** com total de registros e marcador de fim de exportação misturado aos dados.
- **Número de colunas diferente entre arquivos** (41, 42 e 43), o que quebra qualquer combinação que assuma largura fixa.

## 🧩 Mudanças de schema

| Mês      | Mudança                                                            |
| -------- | ------------------------------------------------------------------ |
| Março    | `plano` → `plano_nome`                                             |
| Maio     | coluna `cupom` **ausente** (41 colunas)                            |
| Julho    | `status_assinatura` → `subscription_status`, `mrr` → `receita_mrr` |
| Setembro | coluna **extra** `taxa_setup` (43 colunas)                         |
| Novembro | `cliente_id` → `customer_id`                                       |

## ✅ Exercícios

1. Carregar os 12 arquivos da pasta `01_bases_mensais` (separador `;`, codificação UTF-8 com BOM).
2. **Localizar dinamicamente a linha do cabeçalho** em cada arquivo (primeiro campo igual a `assinatura_id`), descartar as linhas acima e promover o cabeçalho.
3. Remover o rodapé (`Total de registros`, `Fim da exportacao`) e as linhas vazias.
4. Bônus: extrair `Competencia` e `Sistema origem` do bloco de metadados e adicioná-los como colunas.
5. Padronizar os nomes de colunas antes de consolidar os meses em uma única tabela.
6. Remover duplicidades.
7. Normalizar plano, status, moeda, UF e método de pagamento.
8. Converter datas tratando os múltiplos formatos e a localidade pt-BR.
9. Converter preços e MRR para número decimal (atenção à vírgula decimal e aos textos com `R$`).
10. Criar flags de qualidade para e-mail, seats e status/cancelamento.
11. Cruzar com `dimensoes_referencia_saas.xlsx` para validar planos e status.
12. Criar visão mensal com **Novos Clientes, Cancelamentos, Reativações, MRR, Churn e Inadimplência**.

## 📦 Estrutura do repositório

```text
.
├── 01_bases_mensais/
│   ├── saas_assinaturas_2025_01_jan.csv
│   ├── saas_assinaturas_2025_02_fev.csv
│   ├── ...
│   └── saas_assinaturas_2025_12_dez.csv
├── 02_referencias/
│   └── dimensoes_referencia_saas.xlsx
├── .scripts/
│   └── converter_xlsx_para_csv_bruto.py
├── manifesto_arquivos.csv
└── README.md
```

## 🧰 Arquivos de apoio (instrutor)

- `manifesto_arquivos.csv`: linhas aproximadas e número de colunas de cada arquivo (gabarito).
- `.scripts/converter_xlsx_para_csv_bruto.py`: gera e verifica os CSV brutos a partir das planilhas `.xlsx` originais (preâmbulo de metadados, rodapé, BOM, CRLF, vírgula decimal).
- `_backup_xlsx_originais/` (não versionada): cópias dos `.xlsx` originais, exigidas pelo script para a opção `--remover-xlsx`.

<details>
<summary><b>Gabarito: linha do cabeçalho e colunas por arquivo</b></summary>

<p></p>

| Arquivo                            | Cabeçalho na linha | Colunas | Linhas aprox. |
| ---------------------------------- | -----------------: | ------: | ------------: |
| `saas_assinaturas_2025_01_jan.csv` |                  6 |      42 |         1.906 |
| `saas_assinaturas_2025_02_fev.csv` |                  7 |      42 |         2.171 |
| `saas_assinaturas_2025_03_mar.csv` |                  6 |      42 |         2.419 |
| `saas_assinaturas_2025_04_abr.csv` |                  8 |      42 |         2.671 |
| `saas_assinaturas_2025_05_mai.csv` |                  7 |      41 |         2.954 |
| `saas_assinaturas_2025_06_jun.csv` |                  9 |      42 |         3.236 |
| `saas_assinaturas_2025_07_jul.csv` |                  6 |      42 |         3.512 |
| `saas_assinaturas_2025_08_ago.csv` |                  7 |      42 |         3.803 |
| `saas_assinaturas_2025_09_set.csv` |                  8 |      43 |         4.087 |
| `saas_assinaturas_2025_10_out.csv` |                  6 |      42 |         4.361 |
| `saas_assinaturas_2025_11_nov.csv` |                  9 |      42 |         4.675 |
| `saas_assinaturas_2025_12_dez.csv` |                  7 |      42 |         4.832 |

</details>

## 🙌 Contribuir

1. [Faça um fork do repositório](https://github.com/digitalinnovationone/dataset-stock-saas/fork) e clone:

```bash
git clone git@github.com:SEU_USUARIO/dataset-stock-saas.git
```

2. Para regenerar os CSV a partir das planilhas `.xlsx` (coloque-as em `01_bases_mensais`):

```bash
# dependência única:
pip install openpyxl

# gera e verifica os 12 CSV:
python .scripts/converter_xlsx_para_csv_bruto.py

# idem e, se tudo passar, remove os .xlsx (exige backup em _backup_xlsx_originais/):
python .scripts/converter_xlsx_para_csv_bruto.py --remover-xlsx
```

3. Abra um pull request descrevendo o problema de qualidade que você adicionou ou corrigiu 🚀

<a href="https://github.com/digitalinnovationone/dataset-stock-saas/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=digitalinnovationone/dataset-stock-saas" />
</a>

<p></p>

## 🏫 Créditos

Laboratório desenvolvido para as lives de **tratamento de dados com IA** da [Digital Innovation One](https://www.dio.me). Todos os dados são **fictícios**, gerados para fins didáticos.

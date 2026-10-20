# Porsche · Vendas Brasil

Painel analítico de vendas Porsche no Brasil: receita por linha, versão, estado, cidade, propulsão e forma de pagamento.

**Acesse o painel:** abra o `index.html` pelo GitHub Pages deste repositório.

> ⚠️ **Base simulada para demonstração.** Os números não representam vendas reais da Porsche Brasil.

---

## O que o painel mostra

| # | Visão | Pergunta que responde |
|---|---|---|
| — | Indicadores | Quanto foi vendido? Unidades, ticket médio, maior venda e variação contra o ano anterior. |
| — | Leituras automáticas | Três conclusões do recorte atual, recalculadas a cada filtro. |
| 01 | Receita por ano | Como a receita evoluiu? Toque em um ano para filtrar. |
| 02 | Receita por linha | Quais famílias (911, 718, Taycan, Panamera, Cayenne, Macan) mais faturam? |
| 03 | Mapa por estado | Onde estão as vendas? Toque em um estado para filtrar. |
| 04 | Composição | Mix por segmento, propulsão e região. |
| 05 | Faixa de preço | Como os preços se distribuem dentro de cada linha. |
| 06 | Versões | As oito versões que mais faturaram. |
| 07 | Cidades | Receita por praça com Porsche Center. |
| 08 | Pagamento | Pix, financiamento, leasing etc. |
| 09 | Registros | Tabela com busca, ordenação, total e exportação do recorte em CSV. |

Filtros disponíveis: linha, ano, estado, propulsão e forma de pagamento. Todos os filtros se combinam.

## Estrutura do repositório

```
index.html                      painel (HTML + CSS + JS, sem dependências)
assets/img/                     fotos das linhas 911, Taycan, Cayenne e Macan
data/Porsche-Vendas-Brasil.xlsx planilha-fonte (abas Leia-me, Resumo, Vendas, Premissas, Dicionário)
data/vendas-porsche-brasil.csv  mesma base em CSV (separador ;, UTF-8)
README.md                       este documento
```

## De onde vêm os dados

1. **Origem.** Uma tabela de demonstração com 100 vendas (versão, ano, cidade, pagamento e valor), que alimentava a primeira versão deste painel. Essa tabela trazia cidades dos EUA e valores em US$.
2. **Valores em R$.** Para cada venda, o valor é o **preço de entrada da linha no Brasil × fator de versão**, arredondado a R$ 1.000. O fator de versão é o preço da versão dividido pelo preço da versão mais barata da mesma linha na tabela original (1,00x = preço de entrada).
3. **Território.** As vendas foram distribuídas pelas 13 cidades com Porsche Center no Brasil (14 lojas; São Paulo tem duas), com peso maior para os mercados maiores.
4. **Campos derivados.**
   - **Segmento:** Esportivo (911, 718), Sedã / GT (Taycan, Panamera), SUV (Cayenne, Macan).
   - **Propulsão:** Elétrico (Taycan, Macan Electric), Híbrido (E-Hybrid), Combustão (demais).
   - **Região:** segundo o IBGE.
5. **Pagamento.** Formas adaptadas ao mercado brasileiro:

   | Original | No Brasil |
   |---|---|
   | Wire Transfer | Pix |
   | Bank Transfer | TED |
   | ACH | Boleto |
   | Cash | Dinheiro |
   | Financing | Financiamento |
   | Lease | Leasing |

### Preços de entrada usados (aba *Premissas*)

| Linha | Preço de entrada |
|---|---|
| Macan | R$ 580.000 |
| Cayenne | R$ 810.000 |
| 718 | R$ 820.000 |
| Taycan | R$ 850.000 |
| Panamera | R$ 960.000 |
| 911 | R$ 980.000 |

### Fontes

- Preços de entrada: [Vrum / Estado de Minas — "Porsche no Brasil: preços atualizados dos modelos", fev/2026](https://www.vrum.com.br/mercado/2026/02/7348831-porsche-no-brasil-precos-atualizados-dos-modelos-e-o-mais-desejado.html)
- Rede de concessionárias: [Porsche Brasil](https://www.porsche.com/brazil/pt/aboutporsche/porschebrasil)

## Dicionário de dados (`data/vendas-porsche-brasil.csv`)

| Coluna | Tipo | Descrição |
|---|---|---|
| `id` | texto | Identificador da venda (VND-001 a VND-100) |
| `versao` | texto | Versão vendida, ex.: 911 Carrera S |
| `linha` | texto | Família do modelo |
| `segmento` | texto | Esportivo, Sedã / GT ou SUV |
| `propulsao` | texto | Combustão, Híbrido ou Elétrico |
| `ano` | texto | Ano da venda (2020–2026) |
| `cidade` | texto | Cidade do Porsche Center |
| `uf` | texto | Sigla do estado |
| `regiao` | texto | Região do IBGE |
| `forma_pagamento` | texto | Pix, TED, Boleto, Dinheiro, Cartão, Financiamento, Leasing, Criptomoeda |
| `fator_versao` | número | Preço da versão ÷ preço de entrada da linha |
| `valor_brl` | inteiro | Valor da venda em reais |

## Como atualizar os dados

1. Edite a aba **Vendas** (ou os preços na aba **Premissas**) da planilha `data/Porsche-Vendas-Brasil.xlsx`.
2. Exporte a aba **Vendas** como CSV (separador `;`) e substitua `data/vendas-porsche-brasil.csv`.
3. No `index.html`, a constante `DADOS` guarda a mesma base em JSON. Substitua-a para refletir os novos números.

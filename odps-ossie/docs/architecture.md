# Arquitetura da POC — ODPS + Apache Ossie

**Projeto:** Estudos de Data Products e Interoperabilidade Semântica  
**Domínio:** Mercado de Trabalho  
**Data Product:** DP01 — Mercado de Trabalho (RAIS)  
**Versão:** 0.1

## 1. Objetivo

Esta POC tem como objetivo avaliar a aplicação de padrões abertos para especificação, documentação, governança e interoperabilidade semântica de Data Products, utilizando como arquitetura base a Data Platform e o AI Lakehouse.

Serão avaliados:

- Open Data Product Standard (ODPS): especificação dos Data Products.
- Open Data Contract Standard (ODCS): definição dos contratos de dados.
- Apache Ossie: representação e intercâmbio de modelos semânticos.

O cenário de negócio será baseado nos microdados públicos da RAIS 2024, com abrangência no estado da Paraíba.

## 2. Arquitetura de referência

A POC utilizará os componentes da Data Platform e do AI Lakehouse, sem introduzir uma infraestrutura independente.

### 2.1 Componentes

| Componente | Responsabilidade |
|---|---|
| OCI Object Storage | Armazenamento dos dados e arquivos do Lakehouse |
| OCI Data Flow | Execução dos processos Spark |
| Apache Iceberg | Formato de tabelas e gerenciamento de metadados |
| Oracle AI Data Catalog (OADC) | Iceberg REST Catalog |
| AIDP Master Catalog | Descoberta e governança dos ativos de dados |
| ODPS | Especificação dos Data Products |
| ODCS | Contratos de dados |
| Apache Ossie | Interoperabilidade dos modelos semânticos |

### 2.2 Separação de responsabilidades

A arquitetura preservará a separação entre os catálogos:

- O AIDP Master Catalog será utilizado para descoberta e governança corporativa dos ativos.
- O Oracle AI Data Catalog será utilizado como catálogo técnico Iceberg REST.
- Os descritores ODPS e os modelos Ossie serão artefatos versionados em Git.

A integração entre esses componentes será objeto de avaliação da POC.

## 3. Arquitetura de dados

O processamento seguirá a organização Medallion Architecture.

### 3.1 Bronze

Responsável pela preservação dos dados originais.

- Ingestão dos microdados públicos da RAIS 2024.
- Armazenamento dos arquivos originais no OCI Object Storage.
- Registro da origem e dos parâmetros de ingestão.
- Preservação dos dados recebidos.

### 3.2 Silver

Responsável pela preparação e padronização dos dados.

- Extração e leitura dos arquivos de origem.
- Padronização dos nomes e tipos de campos.
- Validação dos registros.
- Aplicação do filtro geográfico da Paraíba.
- Persistência dos dados tratados em tabelas Apache Iceberg.

### 3.3 Gold

Responsável pela disponibilização dos dados para consumo analítico.

Serão construídos conjuntos de dados para:

- Vínculos empregatícios por município.
- Distribuição do emprego por atividade econômica.
- Distribuição por ocupação.
- Indicadores de remuneração.
- Indicadores demográficos e educacionais, conforme disponibilidade dos dados.

## 4. Data Product

Será desenvolvido o seguinte produto:

**Identificador:** dp01-market-labor

**Nome:** Mercado de Trabalho

**Domínio:** Trabalho e Emprego

**Fonte:** RAIS 2024

**Abrangência:** Paraíba

**Granularidade principal:** Vínculo empregatício.

**Objetivo de negócio:** Disponibilizar informações estruturadas sobre o mercado formal de trabalho, permitindo análises de emprego, remuneração e distribuição territorial e setorial.

O produto será documentado utilizando ODPS.

## 5. Contratos de dados

Os contratos serão especificados utilizando ODCS.

Deverão contemplar:

- Identificação do conjunto de dados.
- Estrutura e tipos dos campos.
- Descrição dos atributos.
- Regras de qualidade.
- Restrições e condições de consumo.
- Responsabilidades e informações de evolução do contrato.

Os contratos deverão estar associados aos respectivos pontos de saída do Data Product.

## 6. Modelo semântico

O Apache Ossie será utilizado para representar as definições semânticas do Data Product.

O modelo inicial contemplará:

**Métricas:**
- Quantidade de vínculos empregatícios.
- Remuneração média.
- Remuneração mediana.

**Dimensões:**
- Município.
- Unidade da Federação.
- Atividade econômica (CNAE).
- Ocupação (CBO).
- Sexo.
- Faixa etária.
- Escolaridade.
- Ano-base.

As definições deverão refletir as características reais dos dados e as regras de negócio estabelecidas.

## 7. Fluxo de processamento

1. Obtenção dos microdados públicos da RAIS.
2. Armazenamento dos arquivos originais no Object Storage.
3. Processamento com OCI Data Flow.
4. Construção das tabelas Bronze, Silver e Gold.
5. Registro das tabelas no catálogo Iceberg.
6. Descoberta dos ativos pelo AIDP Master Catalog.
7. Publicação da especificação ODPS.
8. Publicação dos contratos ODCS.
9. Publicação do modelo semântico Ossie.
10. Validação dos mecanismos de consumo e interoperabilidade.

## 8. Consumo dos Data Products

O Data Product deverá permitir consumo por diferentes tipos de consumidores:

- Ferramentas de BI.
- Consultas SQL.
- Aplicações analíticas.
- Agentes de IA.

A POC avaliará especialmente a possibilidade de reutilização das definições semânticas por consumidores distintos, evitando a duplicação das regras de negócio.

## 9. Estrutura do projeto

O repositório `odps-ossie` manterá os artefatos da POC:

```text
odps-ossie/
├── data-products/
│   └── dp01-market-labor/
│       ├── product.yaml
│       ├── contracts/
│       └── semantic/
├── notebooks/
├── scripts/
│   ├── ingestion/
│   ├── validation/
│   └── deployment/
├── docs/
│   └── architecture.md
└── README.md
```

Os documentos de especificação e os códigos serão versionados em Git.

## 10. Critérios de sucesso

A POC será considerada bem-sucedida quando demonstrar:

1. Dados reais da RAIS processados e disponibilizados no AI Lakehouse.
2. Data Product descrito de acordo com ODPS.
3. Contrato de dados válido segundo ODCS.
4. Modelo semântico válido segundo Apache Ossie.
5. Associação entre o Data Product, os contratos e as tabelas físicas.
6. Descoberta do produto no catálogo corporativo.
7. Interoperabilidade semântica demonstrada por pelo menos dois consumidores ou formatos compatíveis.
8. Possibilidade de consumo das métricas e dimensões por uma aplicação analítica ou agente de IA.

## 11. Premissas e pontos de validação

- A infraestrutura será baseada nos serviços existentes da Data Platform e do AI Lakehouse.
- O processamento será realizado por OCI Data Flow.
- O armazenamento será realizado no OCI Object Storage.
- O Oracle AI Data Catalog será utilizado como Iceberg REST Catalog.
- O AIDP Master Catalog continuará responsável pela descoberta e governança corporativa.
- As versões das especificações ODPS, ODCS e Ossie serão fixadas e registradas no projeto.
- A compatibilidade entre as versões Spark, Iceberg e OADC será validada experimentalmente.
- A integração entre os padrões e os catálogos não será presumida: será demonstrada durante a POC.

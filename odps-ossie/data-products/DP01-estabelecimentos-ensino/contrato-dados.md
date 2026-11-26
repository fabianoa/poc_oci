# Contrato de Dados — DP01 Estabelecimentos de Ensino

## 1. Identificação

| Atributo | Definição |
|---|---|
| Produto de Dados | DP01 — Estabelecimentos de Ensino |
| Domínio | Educação |
| Fonte primária | Microdados do Censo Escolar 2024 — INEP |
| Camada de publicação | Prata |
| Tabela | `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO` |
| Formato | Apache Iceberg |
| Granularidade | Um registro por estabelecimento de ensino e ano do censo |
| Chave de negócio | `NU_ANO_CENSO` + `CO_ENTIDADE` |
| Situação | Versão inicial — Censo Escolar 2024 |

## 2. Descrição do produto

O DP01 disponibiliza dados cadastrais e características dos estabelecimentos de ensino, incluindo localização, dependência administrativa, situação de funcionamento, regulamentação, condições de saneamento, infraestrutura, acessibilidade, equipamentos e conectividade.

O produto não tem como objetivo publicar os detalhes de matrículas, turmas ou profissionais da educação, tratados nos demais produtos de dados do domínio.

## 3. Regras do contrato

1. Cada registro representa um estabelecimento de ensino em um ano de referência do Censo Escolar.
2. A combinação de `NU_ANO_CENSO` e `CO_ENTIDADE` identifica unicamente um registro.
3. Os campos de origem foram selecionados dos microdados do INEP e publicados na camada Prata.
4. Os campos categóricos e indicadores numéricos selecionados são publicados como `INT`.
5. Os demais campos são publicados como `STRING`.
6. Valores ausentes são preservados como `NULL`; não são convertidos automaticamente para zero ou texto vazio.
7. Códigos de domínio, inclusive valores como `9` observados em alguns indicadores, devem ser interpretados conforme o dicionário oficial do INEP. Até essa validação, os códigos são preservados sem atribuição de significado.
8. A tabela é armazenada em formato Iceberg e pode ser consultada por mecanismos compatíveis com o catálogo configurado.

## 4. Estrutura lógica

O contrato contém **85 atributos**, distribuídos em:

| Grupo | Quantidade | Tipo publicado |
|---|---:|---|
| Identificação, localização, gestão, funcionamento e saneamento | 45 | 24 `STRING` e 21 `INT` |
| Infraestrutura, acessibilidade, equipamentos e conectividade | 40 | 40 `INT` |
| **Total** | **85** | **64 `STRING` e 21 `INT`** |

> A classificação acima descreve a estrutura técnica publicada. A semântica detalhada de cada código deve ser consultada no dicionário oficial do INEP.

## 5. Atributos

### 5.1 Identificação, localização, gestão, funcionamento e saneamento

| Atributo | Tipo |
|---|---|
| `NU_ANO_CENSO` | `INT` |
| `CO_ENTIDADE` | `STRING` |
| `NO_ENTIDADE` | `STRING` |
| `NO_REGIAO` | `STRING` |
| `CO_REGIAO` | `STRING` |
| `NO_UF` | `STRING` |
| `SG_UF` | `STRING` |
| `CO_UF` | `STRING` |
| `NO_MUNICIPIO` | `STRING` |
| `CO_MUNICIPIO` | `STRING` |
| `NO_DISTRITO` | `STRING` |
| `CO_DISTRITO` | `STRING` |
| `DS_ENDERECO` | `STRING` |
| `NU_ENDERECO` | `STRING` |
| `DS_COMPLEMENTO` | `STRING` |
| `NO_BAIRRO` | `STRING` |
| `CO_CEP` | `STRING` |
| `TP_DEPENDENCIA` | `INT` |
| `TP_CATEGORIA_ESCOLA_PRIVADA` | `INT` |
| `TP_LOCALIZACAO` | `INT` |
| `TP_LOCALIZACAO_DIFERENCIADA` | `INT` |
| `TP_SITUACAO_FUNCIONAMENTO` | `INT` |
| `TP_REGULAMENTACAO` | `INT` |
| `TP_RESPONSAVEL_REGULAMENTACAO` | `INT` |
| `IN_AGUA_POTAVEL` | `INT` |
| `IN_AGUA_REDE_PUBLICA` | `INT` |
| `IN_AGUA_POCO_ARTESIANO` | `INT` |
| `IN_AGUA_CACIMBA` | `INT` |
| `IN_AGUA_FONTE_RIO` | `INT` |
| `IN_AGUA_INEXISTENTE` | `INT` |
| `IN_AGUA_CARRO_PIPA` | `INT` |
| `IN_ENERGIA_REDE_PUBLICA` | `INT` |
| `IN_ENERGIA_GERADOR_FOSSIL` | `INT` |
| `IN_ENERGIA_RENOVAVEL` | `INT` |
| `IN_ENERGIA_INEXISTENTE` | `INT` |
| `IN_ESGOTO_REDE_PUBLICA` | `INT` |
| `IN_ESGOTO_FOSSA_SEPTICA` | `INT` |
| `IN_ESGOTO_FOSSA_COMUM` | `INT` |
| `IN_ESGOTO_FOSSA` | `INT` |
| `IN_ESGOTO_INEXISTENTE` | `INT` |
| `IN_LIXO_SERVICO_COLETA` | `INT` |
| `IN_LIXO_QUEIMA` | `INT` |
| `IN_LIXO_ENTERRA` | `INT` |
| `IN_LIXO_DESTINO_FINAL_PUBLICO` | `INT` |
| `IN_LIXO_DESCARTA_OUTRA_AREA` | `INT` |

### 5.2 Infraestrutura, acessibilidade, equipamentos e conectividade

Todos os atributos deste grupo são publicados como `INT`.

- `IN_ALMOXARIFADO`
- `IN_AREA_VERDE`
- `IN_AUDITORIO`
- `IN_BANHEIRO`
- `IN_BANHEIRO_PNE`
- `IN_BIBLIOTECA`
- `IN_BIBLIOTECA_SALA_LEITURA`
- `IN_COZINHA`
- `IN_LABORATORIO_CIENCIAS`
- `IN_LABORATORIO_INFORMATICA`
- `IN_PATIO_COBERTO`
- `IN_PATIO_DESCOBERTO`
- `IN_PARQUE_INFANTIL`
- `IN_QUADRA_ESPORTES`
- `IN_QUADRA_ESPORTES_COBERTA`
- `IN_REFEITORIO`
- `IN_ACESSIBILIDADE_CORRIMAO`
- `IN_ACESSIBILIDADE_ELEVADOR`
- `IN_ACESSIBILIDADE_PISOS_TATEIS`
- `IN_ACESSIBILIDADE_RAMPAS`
- `IN_ACESSIBILIDADE_SINAL_SONORO`
- `IN_ACESSIBILIDADE_SINAL_TATIL`
- `IN_ACESSIBILIDADE_SINAL_VISUAL`
- `IN_ACESSIBILIDADE_INEXISTENTE`
- `IN_COMPUTADOR`
- `IN_EQUIP_IMPRESSORA`
- `IN_EQUIP_IMPRESSORA_MULT`
- `IN_EQUIP_SCANNER`
- `IN_EQUIP_TV`
- `IN_EQUIP_LOUSA_DIGITAL`
- `IN_DESKTOP_ALUNO`
- `IN_COMP_PORTATIL_ALUNO`
- `IN_TABLET_ALUNO`
- `IN_INTERNET`
- `IN_INTERNET_ALUNOS`
- `IN_INTERNET_ADMINISTRATIVO`
- `IN_INTERNET_APRENDIZAGEM`
- `IN_ACESSO_INTERNET_COMPUTADOR`
- `IN_ACES_INTERNET_DISP_PESSOAIS`
- `IN_BANDA_LARGA`

## 6. Chaves e unicidade

**Chave de negócio:** `NU_ANO_CENSO` + `CO_ENTIDADE`.

Validação realizada na carga inicial do Censo Escolar 2024:

- Registros publicados: 215.545
- Chaves distintas: 215.545
- Registros sem `CO_ENTIDADE`: 0

A unicidade foi confirmada para a versão inicial de 2024. Novas cargas ou anos de referência devem repetir essa validação.

## 7. Campos obrigatórios e nulabilidade

Na validação inicial, os seguintes atributos não apresentaram valores nulos ou vazios:

- `NU_ANO_CENSO`
- `CO_ENTIDADE`
- `NO_ENTIDADE`
- `CO_UF`
- `SG_UF`
- `CO_MUNICIPIO`
- `NO_MUNICIPIO`

Os demais atributos podem apresentar `NULL`, conforme a disponibilidade e as regras da fonte. Ausência de informação não deve ser interpretada automaticamente como inexistência da característica.

## 8. Compatibilidade e acesso

- Formato de tabela: Apache Iceberg.
- Catálogo: catálogo REST configurado no ambiente OCI.
- Identificador da tabela: `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO`.
- Tipos numéricos publicados: `INT`.
- Tipos textuais publicados: `STRING`.

O acesso efetivo depende das permissões concedidas no ambiente e da compatibilidade do mecanismo consumidor com o catálogo e a versão do Iceberg utilizada.

## 9. Evolução e versionamento

Esta versão representa a publicação inicial baseada nos microdados do Censo Escolar 2024.

Alterações futuras na seleção de atributos, tipos, regras de transformação, chave, granularidade ou significado dos dados devem ser registradas e avaliadas quanto ao impacto nos consumidores. Mudanças incompatíveis devem ser comunicadas antes da publicação.

## 10. Pendências para homologação do contrato

- Confirmar a descrição e os domínios de todos os atributos com o dicionário oficial do INEP.
- Documentar formalmente os códigos válidos dos campos `TP_*` e `IN_*`.
- Definir responsável de negócio e responsável técnico pelo produto.
- Definir política de atualização, periodicidade e SLA.
- Definir classificação da informação e regras de compartilhamento.
- Avaliar e documentar os indicadores de completude dos campos de endereço.
- Investigar a diferença de nulidade observada em `IN_BANDA_LARGA` em relação a outros indicadores.

## 11. Documentos relacionados

- [README — DP01 Estabelecimentos de Ensino](README.md)
- [Dicionário de Dados](dicionario-dados.md)
- [Regras de Qualidade](regras-qualidade.md)
- [Linhagem de Dados](linhagem.md)

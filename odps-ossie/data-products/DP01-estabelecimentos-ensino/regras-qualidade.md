# Regras de Qualidade — DP01 Estabelecimentos de Ensino

## 1. Objetivo

Este documento registra as verificações de qualidade aplicadas ao produto DP01 — Estabelecimentos de Ensino, publicado na camada Prata a partir dos microdados do Censo Escolar 2024 do INEP.

As regras e os resultados abaixo refletem as validações efetivamente executadas durante a POC. Observações ainda não homologadas são identificadas como pontos de acompanhamento, e não como falhas definitivas.

## 2. Identificação do conjunto avaliado

| Atributo | Valor |
|---|---|
| Produto | DP01 — Estabelecimentos de Ensino |
| Tabela | `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO` |
| Fonte | Microdados do Censo Escolar 2024 — INEP |
| Registros avaliados | 215.545 |
| Atributos avaliados | 85 |
| Chave de negócio | `NU_ANO_CENSO` + `CO_ENTIDADE` |
| Formato | Apache Iceberg |

## 3. Regras e resultados

### RQ01 — Integridade da chave de negócio

**Regra:** a combinação de `NU_ANO_CENSO` e `CO_ENTIDADE` deve identificar unicamente cada registro.

**Validação executada:** comparação entre a quantidade total de registros e a quantidade de combinações distintas da chave.

| Métrica | Resultado |
|---|---:|
| Total de registros | 215.545 |
| Chaves distintas | 215.545 |
| Registros sem `CO_ENTIDADE` | 0 |

**Resultado:** conforme na carga avaliada. Não foram observadas duplicidades da chave de negócio.

### RQ02 — Preenchimento dos campos essenciais

**Regra:** os atributos essenciais abaixo devem estar preenchidos na publicação:

- `NU_ANO_CENSO`
- `CO_ENTIDADE`
- `NO_ENTIDADE`
- `CO_UF`
- `SG_UF`
- `CO_MUNICIPIO`
- `NO_MUNICIPIO`

**Validação executada:** contagem de valores nulos ou vazios para cada atributo.

| Atributo | Valores nulos ou vazios |
|---|---:|
| `NU_ANO_CENSO` | 0 |
| `CO_ENTIDADE` | 0 |
| `NO_ENTIDADE` | 0 |
| `CO_UF` | 0 |
| `SG_UF` | 0 |
| `CO_MUNICIPIO` | 0 |
| `NO_MUNICIPIO` | 0 |

**Resultado:** conforme na carga avaliada.

### RQ03 — Completude dos atributos de endereço

**Regra:** monitorar a presença dos atributos de endereço. A ausência de complemento ou número não deve ser tratada automaticamente como erro, pois pode refletir a informação disponível na fonte.

**Resultados observados:**

| Atributo | Valores ausentes | Percentual |
|---|---:|---:|
| `DS_ENDERECO` | 1 | 0,00% |
| `NU_ENDERECO` | 41.917 | 19,45% |
| `DS_COMPLEMENTO` | 144.569 | 67,07% |
| `NO_BAIRRO` | 28.640 | 13,29% |
| `CO_CEP` | 0 | 0,00% |

**Tratamento:** preservar os valores ausentes como `NULL`. Acompanhar especialmente `NU_ENDERECO` e `NO_BAIRRO`; não preencher artificialmente sem regra de negócio aprovada.

### RQ04 — Preservação dos valores dos indicadores

**Regra:** os indicadores devem manter os valores recebidos da fonte após a conversão técnica para `INT`, sem converter automaticamente códigos especiais ou valores ausentes.

**Validações executadas:** inspeção da distribuição de valores em indicadores selecionados.

Exemplos observados:

| Atributo | `NULL` | 0 | 1 | 9 |
|---|---:|---:|---:|---:|
| `IN_ACESSO_INTERNET_COMPUTADOR` | 34.480 | 119.712 | 57.095 | 4.258 |
| `IN_ACES_INTERNET_DISP_PESSOAIS` | 34.480 | 141.453 | 35.354 | 4.258 |
| `IN_BANDA_LARGA` | 48.774 | 21.576 | 145.195 | — |

**Resultado:** os valores foram preservados na tabela. O significado do código `9` deve ser confirmado no dicionário oficial do INEP antes de qualquer interpretação ou transformação semântica.

**Atenção:** `NULL`, `0`, `1` e `9` devem permanecer distintos. Não assumir que `NULL` equivale a zero ou que `9` representa uma condição específica sem validação documental.

### RQ05 — Conversão e compatibilidade dos tipos

**Regra:** os campos selecionados para representação numérica devem ser publicados como `INT`, e os demais como `STRING`, conforme o contrato do produto.

**Resultado observado:**

| Tipo físico | Quantidade de atributos |
|---|---:|
| `STRING` | 64 |
| `INT` | 21 |
| **Total** | **85** |

A validação da carga não identificou perda de registros decorrente das conversões realizadas. A interpretação semântica dos códigos permanece sujeita ao dicionário oficial.

### RQ06 — Reconciliação da quantidade de registros

**Regra:** a quantidade de registros publicada na Prata deve corresponder à quantidade de estabelecimentos carregada da Bronze para o recorte avaliado.

| Métrica | Resultado |
|---|---:|
| Registros na Bronze | 215.545 |
| Registros na Prata | 215.545 |
| Diferença | 0 |

**Resultado:** conforme na carga avaliada.

### RQ07 — Integridade da publicação Iceberg

**Regra:** a tabela publicada deve estar acessível pelo catálogo e apresentar metadados de snapshot coerentes com a carga realizada.

**Evidências da publicação avaliada:**

| Métrica | Resultado |
|---|---|
| Tabela | `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO` |
| Operação do snapshot | `overwrite` |
| Registros no snapshot | 215.545 |
| Arquivos de dados | 2 |
| Arquivos de exclusão | 0 |
| Tamanho dos arquivos de dados | 9.228.860 bytes |
| Snapshot ID | `5786147089056358094` |

**Resultado:** publicação realizada e validada por consulta à tabela e aos metadados Iceberg.

## 4. Pontos de acompanhamento

Os itens abaixo não foram classificados como falhas confirmadas:

1. **Domínios dos indicadores:** confirmar no dicionário oficial do INEP o significado de todos os códigos dos campos `TP_*` e `IN_*`, especialmente o valor `9` observado em alguns indicadores.
2. **Completude de endereço:** acompanhar a ausência de `NU_ENDERECO` e `NO_BAIRRO` e avaliar se há necessidade de indicadores de qualidade específicos.
3. **`IN_BANDA_LARGA`:** investigar a quantidade de valores nulos (48.774), superior à observada em vários outros indicadores (34.480). Não preencher nem inferir valores sem conhecer a regra da fonte.
4. **Atualização de dados:** definir como as regras serão reaplicadas em novas edições do Censo Escolar.
5. **Limites de qualidade:** estabelecer metas ou limites de aceitação somente após validação com os responsáveis de negócio e entendimento das regras da fonte.

## 5. Recomendações para execução recorrente

Em cada nova carga ou atualização do DP01, recomenda-se executar e registrar:

- Contagem total de registros.
- Contagem de chaves distintas e registros sem chave.
- Verificação de nulos/vazios nos campos essenciais.
- Completude dos campos de endereço.
- Distribuição de valores dos indicadores e códigos não previstos no domínio homologado.
- Comparação da quantidade de registros entre origem e destino.
- Verificação do snapshot e dos arquivos Iceberg publicados.

Os resultados devem ser registrados por edição do Censo, data de processamento e versão do produto, permitindo comparação histórica.

## 6. Escopo e limitações

As evidências deste documento correspondem à carga do Censo Escolar 2024 realizada durante a POC. Elas não demonstram, por si só, a qualidade de edições futuras nem substituem a validação dos conceitos e domínios pelo INEP.

As verificações descritas são controles técnicos e de completude. Regras semânticas adicionais — por exemplo, combinações permitidas entre indicadores ou coerência entre categorias — devem ser definidas após a homologação do dicionário oficial e das regras de negócio.

## 7. Documentos relacionados

- [README — DP01 Estabelecimentos de Ensino](README.md)
- [Contrato de Dados](contrato-dados.md)
- [Dicionário de Dados](dicionario-dados.md)
- [Linhagem de Dados](linhagem.md)

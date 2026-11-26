# Dicionário de Dados — DP01 Estabelecimentos de Ensino

## 1. Objetivo e escopo

Este documento descreve os 85 atributos publicados pelo produto DP01 — Estabelecimentos de Ensino, derivado dos microdados do Censo Escolar 2024 do INEP.

A tabela publicada é `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO`. A granularidade é um registro por estabelecimento e ano do censo, com chave de negócio `NU_ANO_CENSO` + `CO_ENTIDADE`.

## 2. Convenções de leitura

- `CO_`: código identificador ou classificatório.
- `NO_`: nome ou descrição nominal.
- `DS_`: descrição textual.
- `NU_`: atributo numérico ou de referência numérica; no contrato publicado, o tipo físico pode ser `STRING` quando preservar zeros à esquerda ou formatação.
- `TP_`: variável de tipo/categoria, representada por código.
- `IN_`: variável indicadora.
- Tipos abaixo são os tipos físicos da tabela Prata, não necessariamente os tipos do arquivo CSV original.

**Atenção:** as descrições deste documento são descrições funcionais preliminares, elaboradas a partir dos identificadores dos campos e da organização do produto. Não substituem a descrição oficial do dicionário de dados do INEP. Os domínios/códigos válidos não foram reproduzidos sem conferência do arquivo oficial da edição 2024.

## 3. Dicionário de atributos

### 3.1. Identificação e referência

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `NU_ANO_CENSO` | `INT` | Ano de referência do Censo Escolar. |
| `CO_ENTIDADE` | `STRING` | Código identificador do estabelecimento de ensino. |
| `NO_ENTIDADE` | `STRING` | Nome do estabelecimento de ensino. |

### 3.2. Localização geográfica

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `NO_REGIAO` | `STRING` | Nome da região geográfica. |
| `CO_REGIAO` | `STRING` | Código da região geográfica. |
| `NO_UF` | `STRING` | Nome da unidade da Federação. |
| `SG_UF` | `STRING` | Sigla da unidade da Federação. |
| `CO_UF` | `STRING` | Código da unidade da Federação. |
| `NO_MUNICIPIO` | `STRING` | Nome do município. |
| `CO_MUNICIPIO` | `STRING` | Código do município. |
| `NO_DISTRITO` | `STRING` | Nome do distrito. |
| `CO_DISTRITO` | `STRING` | Código do distrito. |

### 3.3. Endereço

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `DS_ENDERECO` | `STRING` | Descrição/logradouro do endereço do estabelecimento. |
| `NU_ENDERECO` | `STRING` | Número do endereço do estabelecimento. |
| `DS_COMPLEMENTO` | `STRING` | Complemento do endereço. |
| `NO_BAIRRO` | `STRING` | Nome do bairro. |
| `CO_CEP` | `STRING` | Código de Endereçamento Postal. |

### 3.4. Gestão, categoria e funcionamento

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `TP_DEPENDENCIA` | `INT` | Código do tipo de dependência administrativa do estabelecimento. |
| `TP_CATEGORIA_ESCOLA_PRIVADA` | `INT` | Código da categoria da escola privada; aplicável conforme a condição do estabelecimento. |
| `TP_LOCALIZACAO` | `INT` | Código do tipo de localização do estabelecimento. |
| `TP_LOCALIZACAO_DIFERENCIADA` | `INT` | Código da localização diferenciada do estabelecimento. |
| `TP_SITUACAO_FUNCIONAMENTO` | `INT` | Código da situação de funcionamento do estabelecimento. |
| `TP_REGULAMENTACAO` | `INT` | Código relativo à regulamentação/autorização de funcionamento. |
| `TP_RESPONSAVEL_REGULAMENTACAO` | `INT` | Código do responsável pela regulamentação do estabelecimento. |

### 3.5. Saneamento e serviços básicos

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `IN_AGUA_POTAVEL` | `INT` | Indicador de existência de água potável. |
| `IN_AGUA_REDE_PUBLICA` | `INT` | Indicador de abastecimento de água por rede pública. |
| `IN_AGUA_POCO_ARTESIANO` | `INT` | Indicador de abastecimento de água por poço artesiano. |
| `IN_AGUA_CACIMBA` | `INT` | Indicador de abastecimento de água por cacimba. |
| `IN_AGUA_FONTE_RIO` | `INT` | Indicador de abastecimento de água por fonte ou rio. |
| `IN_AGUA_INEXISTENTE` | `INT` | Indicador de inexistência de abastecimento de água. |
| `IN_AGUA_CARRO_PIPA` | `INT` | Indicador de abastecimento de água por carro-pipa. |
| `IN_ENERGIA_REDE_PUBLICA` | `INT` | Indicador de fornecimento de energia por rede pública. |
| `IN_ENERGIA_GERADOR_FOSSIL` | `INT` | Indicador de fornecimento de energia por gerador de fonte fóssil. |
| `IN_ENERGIA_RENOVAVEL` | `INT` | Indicador de fornecimento de energia renovável. |
| `IN_ENERGIA_INEXISTENTE` | `INT` | Indicador de inexistência de fornecimento de energia. |
| `IN_ESGOTO_REDE_PUBLICA` | `INT` | Indicador de esgotamento sanitário por rede pública. |
| `IN_ESGOTO_FOSSA_SEPTICA` | `INT` | Indicador de utilização de fossa séptica. |
| `IN_ESGOTO_FOSSA_COMUM` | `INT` | Indicador de utilização de fossa comum. |
| `IN_ESGOTO_FOSSA` | `INT` | Indicador relacionado à utilização de fossa; definição específica deve ser conferida no dicionário do INEP. |
| `IN_ESGOTO_INEXISTENTE` | `INT` | Indicador de inexistência de sistema de esgotamento sanitário. |
| `IN_LIXO_SERVICO_COLETA` | `INT` | Indicador de coleta de resíduos por serviço de coleta. |
| `IN_LIXO_QUEIMA` | `INT` | Indicador de destinação de resíduos por queima. |
| `IN_LIXO_ENTERRA` | `INT` | Indicador de destinação de resíduos por enterramento. |
| `IN_LIXO_DESTINO_FINAL_PUBLICO` | `INT` | Indicador de destinação dos resíduos em área/serviço público de destino final. |
| `IN_LIXO_DESCARTA_OUTRA_AREA` | `INT` | Indicador de descarte de resíduos em outra área. |

### 3.6. Ambientes e instalações

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `IN_ALMOXARIFADO` | `INT` | Indicador de existência de almoxarifado. |
| `IN_AREA_VERDE` | `INT` | Indicador de existência de área verde. |
| `IN_AUDITORIO` | `INT` | Indicador de existência de auditório. |
| `IN_BANHEIRO` | `INT` | Indicador de existência de banheiro. |
| `IN_BANHEIRO_PNE` | `INT` | Indicador de existência de banheiro acessível a pessoas com deficiência ou mobilidade reduzida. |
| `IN_BIBLIOTECA` | `INT` | Indicador de existência de biblioteca. |
| `IN_BIBLIOTECA_SALA_LEITURA` | `INT` | Indicador de existência de biblioteca ou sala de leitura, conforme definição do instrumento de coleta. |
| `IN_COZINHA` | `INT` | Indicador de existência de cozinha. |
| `IN_LABORATORIO_CIENCIAS` | `INT` | Indicador de existência de laboratório de ciências. |
| `IN_LABORATORIO_INFORMATICA` | `INT` | Indicador de existência de laboratório de informática. |
| `IN_PATIO_COBERTO` | `INT` | Indicador de existência de pátio coberto. |
| `IN_PATIO_DESCOBERTO` | `INT` | Indicador de existência de pátio descoberto. |
| `IN_PARQUE_INFANTIL` | `INT` | Indicador de existência de parque infantil. |
| `IN_QUADRA_ESPORTES` | `INT` | Indicador de existência de quadra de esportes. |
| `IN_QUADRA_ESPORTES_COBERTA` | `INT` | Indicador de existência de quadra de esportes coberta. |
| `IN_REFEITORIO` | `INT` | Indicador de existência de refeitório. |

### 3.7. Acessibilidade

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `IN_ACESSIBILIDADE_CORRIMAO` | `INT` | Indicador de existência de corrimão como recurso de acessibilidade. |
| `IN_ACESSIBILIDADE_ELEVADOR` | `INT` | Indicador de existência de elevador como recurso de acessibilidade. |
| `IN_ACESSIBILIDADE_PISOS_TATEIS` | `INT` | Indicador de existência de pisos táteis. |
| `IN_ACESSIBILIDADE_RAMPAS` | `INT` | Indicador de existência de rampas. |
| `IN_ACESSIBILIDADE_SINAL_SONORO` | `INT` | Indicador de existência de sinalização sonora. |
| `IN_ACESSIBILIDADE_SINAL_TATIL` | `INT` | Indicador de existência de sinalização tátil. |
| `IN_ACESSIBILIDADE_SINAL_VISUAL` | `INT` | Indicador de existência de sinalização visual. |
| `IN_ACESSIBILIDADE_INEXISTENTE` | `INT` | Indicador de inexistência dos recursos de acessibilidade considerados no levantamento. |

### 3.8. Equipamentos e tecnologia

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `IN_COMPUTADOR` | `INT` | Indicador de existência de computador no estabelecimento. |
| `IN_EQUIP_IMPRESSORA` | `INT` | Indicador de existência de impressora. |
| `IN_EQUIP_IMPRESSORA_MULT` | `INT` | Indicador de existência de impressora multifuncional. |
| `IN_EQUIP_SCANNER` | `INT` | Indicador de existência de scanner. |
| `IN_EQUIP_TV` | `INT` | Indicador de existência de televisão. |
| `IN_EQUIP_LOUSA_DIGITAL` | `INT` | Indicador de existência de lousa digital. |
| `IN_DESKTOP_ALUNO` | `INT` | Indicador de existência/disponibilidade de computadores desktop para uso dos alunos. |
| `IN_COMP_PORTATIL_ALUNO` | `INT` | Indicador de existência/disponibilidade de computadores portáteis para uso dos alunos. |
| `IN_TABLET_ALUNO` | `INT` | Indicador de existência/disponibilidade de tablets para uso dos alunos. |

### 3.9. Conectividade

| Atributo | Tipo Prata | Descrição funcional preliminar |
|---|---|---|
| `IN_INTERNET` | `INT` | Indicador de acesso à internet no estabelecimento. |
| `IN_INTERNET_ALUNOS` | `INT` | Indicador de acesso à internet para uso dos alunos. |
| `IN_INTERNET_ADMINISTRATIVO` | `INT` | Indicador de acesso à internet para uso administrativo. |
| `IN_INTERNET_APRENDIZAGEM` | `INT` | Indicador de acesso à internet para atividades de ensino e aprendizagem. |
| `IN_ACESSO_INTERNET_COMPUTADOR` | `INT` | Indicador de acesso à internet por meio de computador. |
| `IN_ACES_INTERNET_DISP_PESSOAIS` | `INT` | Indicador de acesso à internet por dispositivos pessoais. |
| `IN_BANDA_LARGA` | `INT` | Indicador de disponibilidade de conexão de banda larga. |

## 4. Domínios de valores e interpretação

Os campos `TP_*` e `IN_*` são publicados como inteiros. Entretanto, o tipo `INT` não define, por si só, o significado de cada código.

- Para campos `TP_*`, consultar as categorias e respectivas descrições no dicionário oficial do Censo Escolar 2024.
- Para campos `IN_*`, não assumir automaticamente que todos os valores se limitam a `0` e `1`.
- Na carga analisada foram observados valores `9` em alguns indicadores. O significado desse código deve ser confirmado no dicionário oficial antes de qualquer regra de conversão, agregação ou classificação.
- `NULL` representa ausência de valor na tabela e deve permanecer distinto de `0` e de qualquer código informado pela fonte.
- Não somar ou agregar indicadores sem confirmar previamente o domínio e a regra de interpretação aplicável.

## 5. Observações sobre tipos físicos

| Tipo | Quantidade | Observação |
|---|---:|---|
| `STRING` | 64 | Mantém códigos e atributos textuais sem conversão numérica indevida. |
| `INT` | 21 | Aplicado aos campos numéricos selecionados na preparação da camada Prata. |
| **Total** | **85** | |

## 6. Fonte de referência e validação pendente

Fonte dos dados: INEP — Microdados do Censo Escolar da Educação Básica 2024.

- Página oficial: https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/censo-escolar
- Arquivo de microdados da edição 2024: https://download.inep.gov.br/dados_abertos/microdados_censo_escolar_2024.zip

O pacote oficial da edição deve ser consultado para completar e homologar: descrição oficial de cada variável, categorias de `TP_*`, valores válidos de `IN_*`, códigos especiais, regras de aplicabilidade e eventuais observações do instrumento de coleta.

**Status:** estrutura e tipos físicos conferidos com a tabela Prata; descrições funcionais preliminares; domínios oficiais pendentes de homologação.

## 7. Documentos relacionados

- [README — DP01 Estabelecimentos de Ensino](README.md)
- [Contrato de Dados](contrato-dados.md)
- [Regras de Qualidade](regras-qualidade.md)
- [Linhagem de Dados](linhagem.md)

# DP01 -- Estabelecimentos de Ensino

## Identificação

  Propriedade            Valor
  ---------------------- --------------------------------
  Identificador          DP01
  Nome                   Estabelecimentos de Ensino
  Domínio de dados       Educação
  Fonte                  INEP -- Censo Escolar 2024
  Ano de referência      2024
  Camada                 Prata
  Catálogo / namespace   `aicat.PRATA`
  Tabela                 `DP01_ESTABELECIMENTOS_ENSINO`
  Formato                Apache Iceberg
  Status técnico         Implementado e validado

## Objetivo

Disponibilizar uma visão estruturada dos estabelecimentos de ensino
brasileiros, reunindo informações de identificação, localização,
características administrativas, situação de funcionamento,
infraestrutura, acessibilidade e recursos tecnológicos.

O produto pode apoiar análises sobre a distribuição territorial dos
estabelecimentos de ensino e as condições de infraestrutura da rede
educacional.

## Escopo funcional

O DP01 contempla os seguintes grupos de informações:

-   **Identificação:** ano do censo, código e nome do estabelecimento.
-   **Localização:** região, unidade federativa, município, distrito e
    endereço.
-   **Gestão:** dependência administrativa e categoria da escola
    privada.
-   **Funcionamento e regulamentação:** situação de funcionamento e
    informações de regulamentação.
-   **Infraestrutura básica:** abastecimento de água, energia,
    esgotamento sanitário e destinação de resíduos.
-   **Instalações:** biblioteca, cozinha, banheiros, laboratórios,
    quadras, auditórios e outras instalações.
-   **Acessibilidade:** corrimãos, elevadores, pisos táteis, rampas e
    sinalizações.
-   **Tecnologia e conectividade:** computadores, equipamentos,
    dispositivos dos alunos e acesso à internet.

Informações detalhadas sobre matrículas, turmas e profissionais da
educação não fazem parte do escopo deste produto. Esses assuntos poderão
ser tratados em Data Products específicos.

## Granularidade e chave de negócio

A granularidade do produto é **um registro por estabelecimento de ensino
e ano de referência**.

**Chave de negócio:** `NU_ANO_CENSO + CO_ENTIDADE`.

Na carga validada do Censo Escolar 2024, foram encontrados:

-   215.545 registros;
-   215.545 combinações distintas da chave;
-   nenhuma duplicidade identificada para a chave de negócio.

## Estrutura disponibilizada

A tabela contém 85 atributos:

  ------------------------------------------------------------------------
  Tipo de dado                            Quantidade Uso
  --------------------- ---------------------------- ---------------------
  `STRING`                                        64 Identificação,
                                                     localização, endereço
                                                     e códigos geográficos

  `INT`                                           21 Ano, códigos
                                                     categóricos e
                                                     indicadores

  **Total**                                   **85** 
  ------------------------------------------------------------------------

Os códigos geográficos foram mantidos como texto para preservar sua
representação. Os campos categóricos e indicadores numéricos foram
armazenados como `INT`, tipo compatível com a tabela Iceberg.

A relação completa de atributos e suas descrições está no [dicionário de
dados](dicionario-dados.md).

## Origem e processamento

**Fonte:** microdados do Censo Escolar 2024, disponibilizados pelo INEP.

**Arquivo de origem:** `microdados_ed_basica_2024.csv`.

Fluxo implementado:

1.  **Landing:** armazenamento do arquivo original.
2.  **Bronze:** ingestão dos dados brutos na tabela
    `aicat.BRONZE.CENSO_ESCOLAR_2024`, com 426 colunas.
3.  **Prata:** seleção de 85 atributos, conversão de tipos e gravação do
    DP01 na tabela `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO`.

A linhagem e as etapas de transformação estão descritas em
[linhagem](linhagem.md).

## Qualidade dos dados

A carga foi validada com os seguintes resultados:

  Verificação                                                   Resultado
  ----------------------------------------------------------- -----------
  Total de registros                                              215.545
  Total de atributos                                                   85
  Chaves distintas                                                215.545
  Valores nulos ou vazios nos campos obrigatórios definidos             0
  Duplicidades da chave de negócio                                      0

Os campos obrigatórios verificados foram `NU_ANO_CENSO`, `CO_ENTIDADE`,
`NO_ENTIDADE`, `CO_UF`, `SG_UF`, `CO_MUNICIPIO` e `NO_MUNICIPIO`.

Foram identificadas ausências em alguns atributos opcionais de endereço.
Os valores nulos foram preservados, sem preenchimento artificial. Também
foram preservados códigos especiais encontrados nos indicadores,
pendentes de confirmação semântica no dicionário oficial do INEP.

Os resultados detalhados, incluindo completude e distribuição dos
indicadores, estão em [regras de qualidade](regras-qualidade.md).

## Armazenamento e tecnologia

  Propriedade               Valor
  ------------------------- --------------------------------------------
  Plataforma                OCI AI Data Platform
  Engine de processamento   Apache Spark 3.5.0
  Formato de tabela         Apache Iceberg
  Catálogo                  Iceberg REST Catalog
  Namespace                 `PRATA`
  Tabela                    `aicat.PRATA.DP01_ESTABELECIMENTOS_ENSINO`

Snapshot da carga validada:

-   **Data/hora do commit:** 2026-11-26 13:15:53
-   **Snapshot ID:** `5786147089056358094`
-   **Operação:** `overwrite`
-   **Registros adicionados:** 215.545
-   **Arquivos de dados:** 2
-   **Tamanho total dos arquivos:** 9.228.860 bytes
-   **Arquivos de exclusão:** 0

## Documentação do produto

  -----------------------------------------------------------------------
  Documento                           Finalidade
  ----------------------------------- -----------------------------------
  [Contrato de                        Define o que o produto entrega e as
  dados](contrato-dados.md)           condições de consumo

  [Dicionário de                      Lista os atributos, tipos e
  dados](dicionario-dados.md)         descrições

  [Regras de                          Registra critérios, validações e
  qualidade](regras-qualidade.md)     resultados

  [Linhagem](linhagem.md)             Descreve origem, processamento e
                                      destino dos dados
  -----------------------------------------------------------------------

## Responsabilidades e pendências

O produto está implementado e validado tecnicamente para a referência
2024. Para completar sua governança, ainda precisam ser definidos ou
concluídos:

-   responsável pelo produto (*Data Product Owner*);
-   responsável técnico formal;
-   periodicidade de atualização;
-   SLA de disponibilidade e atualização;
-   política de versionamento e comunicação de mudanças;
-   classificação dos dados conforme a política corporativa;
-   confirmação das descrições e domínios dos códigos com o dicionário
    oficial do INEP;
-   investigação da quantidade diferenciada de valores nulos em
    `IN_BANDA_LARGA`.

## Relação com os demais Data Products

O DP01 integra a iniciativa de produtos de dados educacionais, que
prevê:

-   **DP01 -- Estabelecimentos de Ensino**
-   **DP02 -- Matrículas e Turmas**
-   **DP03 -- Profissionais da Educação**
-   **DP04 -- Indicadores Educacionais**

Esses produtos poderão ser integrados posteriormente em um produto da
camada Ouro denominado **Perfil da Educação Pública Municipal**.

------------------------------------------------------------------------

**Status:** implementado e validado tecnicamente. A complementação do
dicionário semântico e a definição das responsabilidades e níveis de
serviço permanecem como atividades de governança.

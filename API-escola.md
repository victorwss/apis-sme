# API de escolas

## Estruturas

### Endereço

| Campo                                        | Tipo                                                         |
|----------------------------------------------|--------------------------------------------------------------|
| `logradouro`                                 | String                                                       |
| <a name="endereco-tipo">`tipo`</a>           | String                                                       |
| <a name="endereco-numero">`numero`</a>       | String                                                       |
| `complemento`                                | String                                                       |
| `cep`                                        | String no formato da expressão regular `[0-9]{5}\-[0-9\]{3}` |
| `bairro`                                     | String                                                       |
| `distrito`                                   | String                                                       |
| `latitude`                                   | Ponto flutuante entre -90.0 e +90.0                          |
| `longitude`                                  | Ponto flutuante entre -180.0 e +180.0                        |
| <a name="endereco-municipio">`municipio`</a> | String                                                       |
| <a name="endereco-estado">`estado`</a>       | String                                                       |
| <a name="endereco-pais">`pais`</a>           | String                                                       |

Observações:

* O [campo `eol`](#endereco-tipo) pode especificar rua, avenida, praça, estrada, alameda, quadra, rodovia, travessa, etc.
* O [campo `numero`](#endereco-numero), apesar do nome, nem sempre é numérico. Por exemplo: "Baker Street, 221B".
* No caso do município de São Paulo, o [campo `distito`](#endereco-distrito) corresponde a subprefeitura.
* O [campo `municipio`](#endereco-municipio) na maioria das vezes conterá o valor "São Paulo". Mas no caso do endereço de alunos ou professores, pode ser um outro município.
* O [campo `estado`](#endereco-estado) na maioria das vezes conterá o valor "São Paulo". Mas no caso do endereço de alunos ou professores, pode ser um outro estado.
* O [campo `pais`](#endereco-pais) na maioria das vezes conterá o valor "Brasil". Mas no caso do endereço de alunos ou professores, pode ser um outro país.

### Telefone

| Campo                                          | Tipo                                  |
|------------------------------------------------|---------------------------------------|
| <a name="telefone-ddi">`ddi`</a>               | String numérica                       |
| <a name="telefone-codigoArea">`codigoArea`</a> | String numérica                       |
| `numero`                                       | String numérica                       |
| `ramal`                                        | String numérica                       |
| `tipo`                                         | [Tipo de telefone](#tipo-de-telefone) |
| `operadora`                                    | String                                |

Observações:

* O [campo `ddi`](#telefone-ddi) na maioria das vezes será fixado como "55". Mas no caso de telefones fora do Brasil, pode vir com algum outro valor.
* O [campo `codigoArea`](#telefone-codigoArea) para telefones no Brasil corresponde ao DDD de 2 dígitos. No entanto, para telefones em outros países, pode ter uma quantidade de dígitos diferentes ou estar em branco.

### Faixa etária

| Campo    | Tipo    |
|----------|---------|
| `inicio` | Inteiro |
| `fim`    | Inteiro |

### Link

| Campo                            | Tipo   |
|----------------------------------|--------|
| <a name="link-tipo">`tipo`</a>   | String |
| <a name="link-valor">`valor`</a> | String |

* O [campo `tipo`](#link-tipo) pode ser "Twitter", "Instagram", "Facebook", "Youtube", "Blog", "Website", etc.
* O [campo `valor`](#link-valor) pode ser uma URL, nome de domínio, nome de usuário ou algo equivalente que sirva para identificar unicamente a entidade na respectiva rede.

### DRE

| Campo                       | Tipo                                                       |
|-----------------------------|------------------------------------------------------------|
| <a name="dre-eol">`eol`</a> | String numérica                                            |
| `endereco`                  | [Endereço](#endereço)                                      |
| `nome`                      | String                                                     |
| `telefones`                 | Lista de [telefones](#telefone)                            |
| `emails`                    | Lista de strings                                           |
| `status`                    | String representando a [situação da DRE](#situação-da-dre) |
| `dataAtualizacao`           | String com data no formato "DD/MM/AAAA".                   |

Observações:

* O [campo `eol`](#dre-eol) é o código da DRE de acordo com o sistema EOL.

### Escola

| Campo                                           | Tipo                                                                                       |
|-------------------------------------------------|--------------------------------------------------------------------------------------------|
| <a name="escola-eol">`eol`</a>                  | String numérica                                                                            |
| <a name="escola-inep">`inep`</a>                | String numérica                                                                            |
| <a name="escola-papa">`papa`</a>                | String numérica                                                                            |
| <a name="escola-cie">`cie`</a>                  | String numérica?                                                                           |
| `nome`                                          | String                                                                                     |
| `nomesAnteriores`                               | Lista de strings                                                                           |
| `endereco`                                      | [Endereço](#endereço)                                                                      |
| <a name="escola-tipo">`tipo`</a>                | String representando o [tipo da escola](#tipo-de-escola)                                   |
| `telefones`                                     | Lista de [telefones](#telefone)                                                            |
| `emails`                                        | Lista de strings                                                                           |
| `status`                                        | String representando a [situação da escola](#situação-da-escola)                           |
| <a name="escola-dre">`dre`</a>                  | [DRE](#dre)                                                                                |
| `redesSociais`                                  | Lista de [links](#link)                                                                    |
| `dataCriacao`                                   | String com data no formato "DD/MM/AAAA".                                                   |
| `dataCriacaoDOM`                                | String com data no formato "DD/MM/AAAA".                                                   |
| `dataInicioFuncionamento`                       | String com data no formato "DD/MM/AAAA".                                                   |
| `dataInicioConvenio`                            | String com data no formato "DD/MM/AAAA".                                                   |
| `dataAutorizacao`                               | String com data no formato "DD/MM/AAAA".                                                   |
| `dataExtincao`                                  | String com data no formato "DD/MM/AAAA".                                                   |
| <a name="escola-faixa-etaria">`faixaEtaria`</a> | [Faixa etária](#faixa-etária)                                                              |
| <a name="escola-capacidade>`capacidade`</a>     | Inteiro maior ou igual a zero                                                              |
| `turnos`                                        | Objeto onde chaves são anos e valores são listas de strings representando [turnos](#turno) |
| `rede`                                          | String representando uma [Rede escolar](#rede escolar)                                     |
| `dataAtualizacao`                               | String com data no formato "DD/MM/AAAA".                                                   |

Observações:

* O [campo `eol`](#escola-eol) é o código da escola de acordo com o sistema EOL.
* O [campo `inep`](#escola-inep) é o código da escola de acordo com o INEP.
* O [campo `papa`](#escola-papa) é o código da escola de acordo com o sistema PAPA.
* O [campo `cie`](#escola-cie) é o código CIE da escola de acordo com a Secretaria Estadual de Educação de São Paulo (SEE-SP).
* O [campo `dre`](#escola-dre) não é uma string e nem o código da DRE. Contém o objeto correspondente a DRE completo a ser aninhado dentro da estrutura da escola.
* O [campo `faixaEtaria`](#escola-faixa-etaria) é um objeto que representa a faixa etária em anos de atendimento da escola.
* O [campo `capacidade`](#escola-capacidade) representa a capacidade em número de matrículas da escola.

## Enums

### Tipo de escola

| Nome             | Descrição                                                             |
|------------------|-----------------------------------------------------------------------|
| `CCA`            | Centro para Crianças e Adolescentes                                   |
| `CCI/CIPS`       | Centro de Convivência Infantil / Centro Integrado de Proteção e Saúde |
| `CECI`           | Centro de Educação e Cultura Indígena                                 |
| `CEI DIRET`      | Centro de Educação Infantil Direto                                    |
| `CEI INDIR`      | Centro de Educação Infantil Indireto Conveniado                       |
| `CEMEI`          | Centro Municipal de Educação Infantil                                 |
| `CEU`            | Centro Educacional Unificado                                          |
| `CEU AT COM`     | Unidade CEU para atendimento exclusivo de Atividades Complementares   |
| `CEU CEI`        | Centro de Educação Infantil integrante de CEU                         |
| `CEU EMEF`       | Escola Municipal de Ensino Fundamental integrante de CEU              |
| `CEU EMEI`       | Escola Municipal de Educação Infantil integrante de CEU               |
| `CIEJA`          | Centro Integrado de Educação de Jovens e Adultos                      |
| `CMCT`           | Centro Municipal de Capacitação e Treinamento                         |
| `CR.P.CONV`      | Creche Privada Conveniada                                             |
| `DIR EDUC`       | Diretoria Regional de Educação                                        |
| `E TECNICA`      | Escola Técnica                                                        |
| `EMEBS`          | Escola Municipal de Educação Bilíngue para Surdos                     |
| `EMEF`           | Escola Municipal de Ensino Fundamental                                |
| `EMEFM`          | Escola Municipal de Ensino Fundamental e Médio                        |
| `EMEI`           | Escola Municipal de Educação Infantil                                 |
| `ESC.PART.`      | Escola Particular                                                     |
| `ESP CONV`       | Especial Conveniada                                                   |
| `MOVA`           | Movimento de Alfabetização de Jovens e Adultos                        |
| `OUT-PMSP`       | Outras - Prefeitura Municipal de São Paulo                            |

### Situação da escola

| Nome       | Observações                      |
|------------|----------------------------------|
| `Criada`   | Ainda não está em funcionamento. |
| `Ativa`    |                                  |
| `Extinta`  |                                  |

### Situação da DRE

| Nome      |
|-----------|
| `Ativa`   |
| `Extinta` |

### Turno

| Nome  | Significado   | Descrição                         |
|-------|---------------|-----------------------------------|
| `M`   | Manhã         | Aula regular no período da manhã. |
| `I`   | Intermediário | Aula das 11:00 às 15:00.          |
| `T`   | Tarde         | Aula regular no período da tarde. |
| `V`   | Vespertino    | Aula das 15:00 às 19:00.          |
| `G`   | Integral      | Aula de manhã e pela tarde.       |
| `N`   | Noite         | Aula regular no período da noite. |

Observações:

* A maioria das escolas mantém apenas os turnos regulares `M` (manhã), `T` (tarde) e `N` (noite).
* Há algumas escolas que oferecem o turno `G` (integral) nos períodos da manhã e da tarde, principalmente no caso de creches.
* Escolas que tenham os turnos `M` (manhã), `I` (intermediário) e `V` (vespertino) são casos raros e excepcionais. Correspondem a três turnos diurnos distintos de aulas em um mesmo dia.

### Rede escolar

| Nome         |
|--------------|
| `Direta`     |
| `Conveniada` |

### Tipo de telefone

| Nome      |
|-----------|
| `Fixo`    |
| `Celular` |
| `Fax`     |

## Operações

### Pesquisar escolas por código EOL

* *Método HTTP*: **GET**
* *URL*:  `/escolas/eol/{código}`
* Resultado esperado: [Escola](#escola)

#### Parâmetros

| Nome     | Local | Significado                              |
|----------|-------|------------------------------------------|
| `codigo` | URL   | [Código EOL](#escola-eol) de uma escola. |

#### Erros:

* 404 - Se o `código` não corresponder a uma string numérica ou não corresponder ao código EOL de nenhuma escola.

### Pesquisar escolas por código INEP

* *Método HTTP*: **GET**
* *URL*:  `/escolas/inep/{código}`
* Resultado esperado: [Escola](#escola)

#### Parâmetros

| Nome     | Local | Significado                                |
|----------|-------|--------------------------------------------|
| `codigo` | URL   | [Código INEP](#escola-inep) de uma escola. |

#### Erros:

* 404 - Se o `código` não corresponder a uma string numérica ou não corresponder ao código INEP de nenhuma escola.

### Pesquisar escolas por código PAPA

* *Método HTTP*: **GET**
* *URL*:  `/escolas/papa/{código}`
* Resultado esperado: [Escola](#escola)

#### Parâmetros

| Nome     | Local | Significado                                |
|----------|-------|--------------------------------------------|
| `codigo` | URL   | [Código PAPA](#escola-papa) de uma escola. |

#### Erros:

* 404 - Se o `código` não corresponder a uma string numérica ou não corresponder ao código PAPA de nenhuma escola.

### Pesquisar escolas por código CIE

* Método HTTP: **GET**
* URL:  `/escolas/cie/{código}`
* Resultado esperado: [Escola](#escola)

#### Parâmetros

| Nome     | Local | Significado                              |
|----------|-------|------------------------------------------|
| `codigo` | URL   | [Código CIE](#escola-cie) de uma escola. |

#### Erros:

* 404 - Se o `código` não corresponder a uma string numérica ou não corresponder ao código CIE de nenhuma escola.

### Pesquisar escolas por DRE

* *Método HTTP*: **GET**
* *URL*:  `/dres/{código}/escolas`
* Resultado esperado: Lista de [escolas](#escola).

#### Parâmetros

| Nome     | Local | Significado                     |
|----------|-------|---------------------------------|
| `codigo` | URL   | [Código EOL da DREs](#dre-eol). |

#### Erros:

* 404 - Se o `código` não corresponder a uma string numérica ou não corresponder ao código EOL de nenhuma DRE.

### Pesquisar DRE por código

* Método HTTP: **GET**
* URL:  `/dres/{código}`
* Resultado esperado: [DRE](#dre)

#### Parâmetros

| Nome     | Local | Significado                     |
|----------|-------|---------------------------------|
| `codigo` | URL   | [Código EOL da DREs](#dre-eol). |

#### Erros:

* 404 - Se o `código` não corresponder a uma string numérica ou não corresponder ao código EOL de nenhuma DRE.

### Listar DREs

* *Método HTTP*: **GET**
* *URL*:  `/dres`
* Resultado esperado: Lista de [DREs](#dre).

#### Parâmetros

Não há.

#### Erros:

* **404**: Se o `código` não corresponder a uma string numérica ou não corresponder ao código EOL de nenhuma DRE.

### Listar escolas

* Método HTTP: **GET**
* URL: `/escolas?{parâmetros}`
* Resultado esperado: Lista de [escolas](#escola).

#### Parâmetros

| Nome                                                | Local        | Significado                                                               |
|-----------------------------------------------------|--------------|---------------------------------------------------------------------------|
| <a name="lista-escolas-tipo">`tipo`</a>             | Query string | Tipos de escolas a serem pesquisados.                                     |
| <a name="lista-escolas-nome">`nome`</a>             | Query string | Nomes das escolas a serem pesquisados.                                    |
| <a name="lista-escolas-divisao">`divisao`</a>       | Query string | Bairros, distritos e subprefeituras a serem pesquisados.                  |
| <a name="lista-escolas-logradouro">`logradouro`</a> | Query string | Ruas a serem pesquisadas.                                                 |
| <a name="lista-escolas-latitude">`latitude`</a>     | Query string | Área circular onde as escolas serão procuradas.                           |
| <a name="lista-escolas-longitude">`longitude`</a>   | Query string | Área circular onde as escolas serão procuradas.                           |
| <a name="lista-escolas-raio">`raio`</a>             | Query string | Área circular onde as escolas serão procuradas.                           |
| <a name="lista-escolas-status">`status`</a>         | Query string | [Situações das escolas](#situação-da-escola) a serem pesquisadas.         |
| <a name="lista-escolas-dre">`dre`</a>               | Query string | [Códigos EOL de DREs](#dre-eol) das DREs das escolas a serem pesquisadas. |

Observações:

* O [campo `tipo`](#lista-escolas-tipo) corresponde aos [tipos de escolas](#escola-tipo) a serem pesquisados. Se for omitido, todos os tipos de escolas são consideradas. Múltiplos tipos de escolas podem ser pesquisados ao separá-los com `|`. Por exemplo, `?tipo=EMEF|EMEI` é utilizado para pesquisar por todas as escolas do tipo EMEF ou EMEI.
* O [campo `nome`](#lista-escolas-tipo) corresponde aos nomes de escolas a serem pesquisados. Se for omitido, todas as escolas são consideradas. Múltiplos nomes de escolas podem ser pesquisados ao separá-los com `|`. Expressões separadas por ponto-e-vírgula podem aparecer em qualquer parte e em qualquer ordem no nome. O `|` tem precedência sobre o `;`. Por exemplo, `?nome=João Pedro;Silva|Azevedo` pode encontrar escolas chamadas de "João Pedro Lima da Silva", "Carlos Silva de João Pedro" e "Ramos de Azevedo", mas não vai encontrar "João Silva Pedro".
* O [campo `divisao`](#lista-escolas-divisao) corresponde aos bairros, distritos, subdistritos ou subprefeituras onde a escola deve ser procurado. É aplicado com a mesma regra de busca dada pelo campo `nome`. Por exemplo, uma busca em `?divisao=Ipiranga|Sacomã|Cursino&nome=João` irá retornar todas as escolas que estejam no distrito, subprefeitura ou bairro do Ipiranga, Sacomã ou Cursino.
* O [campo `logradouro`](#lista-escolas-logradouro) corresponde ao nome da rua, avenida, praça, etc. onde a escola deve ser procurado. É aplicado com a mesma regra de busca dada pelo campo `nome`.
* Os campos [`latitude`](#lista-escolas-latitude), [`longitude`](#lista-escolas-longitude) e [`raio`](#lista-escolas-raio), se estiverem presentes, devem ser informados juntos. Não é permitido que um deles seja informado e os outros dois não ou que dois deles sejam informados e o terceiro não. Corresponde a busca por escolas que estejam dentro de um círculo centrado na latitude e longitude informados. Se omitidos, todas as escolas são consideradas.
* O [campo `latitude`](#lista-escolas-latitude) é dado em graus e está entre -90 e +90.
* O [campo `longitude`](#lista-escolas-longitude) é dado em graus e está entre -180 e +180.
* O [campo `raio`](#lista-escolas-raio) é dado em metros e deve ser um número maior ou igual a zero.
* O [campo `status`](#lista-escolas-status) corresponde às [situações da escola](#situação-da-escola) a serem pesquisados. Se for omitido, escolas em todas as situações são consideradas. Múltiplas situações de escolas podem ser pesquisados ao separá-los com `|`. Por exemplo, `?status=Criada|Ativa` é utilizado para pesquisar por todas as escolas do tipo Criada ou Ativa.
* O [campo `dre`](#lista-escolas-dre) corresponde aos [códigos EOL de DREs](#dre-eol) das DREs das escolas a serem pesquisadas. Se for omitido, escolas de todas as DREs são consideradas. Múltiplas DREs podem ser pesquisadas ao separá-los com `|`. Por exemplo, `?dres=1|2` é utilizado para pesquisar por todas as escolas nas DREs cujo números EOL sejam 1 ou 2.
* Todos os parâmetros textuais são *case insensitive*.

#### Erros:

* **422**: Se qualquer um dos parâmetros for apresentado mais do que uma vez na URL.
* **422**: Se apenas um ou apenas dois dos parâmetros `latitude`, `longitude` e `raio` forem especificados.
* **422**: Se a latitude for menor que -90.0, maior que +90.0 ou que não puder ser interpretada como um número.
* **422**: Se a longitude for menor que -180.0, maior que +180.0 ou que não puder ser interpretada como um número.
* **422**: Se o raio for menor que 0 ou que não puder ser interpretado como um número.
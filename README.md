# CNPJ Alfanumerico

Este projeto oferece exemplos de cálculo de DV e métodos de validação de CNPJ alfanuméricos em diferentes linguagens de programação.

[serpro.gov.br](serpro.gov.br)

## Cálculo dos dígitos verificadores de CNPJ alfanumérico

- [Python](src/python/README.md)
- [Javascript](src/javascript/README.md)
- [Typescript](src/typescript/README.md)
- [Java](src/java/README.md)

### 1. Cálculo dos dígitos verificadores

O CNPJ alfanumérico é composto por doze caracteres alfanuméricos e dois dígitos verificadores numéricos.

Os dígitos verificadores (DV) são calculados a parƟr dos doze primeiros caracteres em duas etapas, utilizando o módulo de divisão 11 e pesos distribuídos de 2 a 9.

#### 1.1. Cálculo do primeiro dígito verificador
Para cada um dos caracteres do CNPJ, atribuir o valor da coluna “Valor para cálculo do DV”, conforme a tabela abaixo (ou subtrair 48 do “Valor ASCII”):

Exemplo:

| CNPJ  | 1 | 2 | A  | B  | C  | 3 | 4 | 5 | 0 | 1 | D  | E  |
|-------|---|---|----|----|----|---|---|---|---|---|----|----|
| Valor | 1 | 2 | 17 | 18 | 19 | 3 | 4 | 5 | 0 | 1 | 20 | 21 |

Distribuir os pesos de 2 a 9 da direita para a esquerda (recomeçando depois do oitavo caracter), conforme o exemplo:

| CNPJ          | 1 | 2 | A  | B  | C   | 3  | 4  | 5  | 0 | 1 | D  | E  |
|---------------|---|---|----|----|-----|----|----|----|---|---|----|----|
| Valor         | 1 | 2 | 17 | 18 | 19  | 3  | 4  | 5  | 0 | 1 | 20 | 21 |
| Peso          | 5 | 4 | 3  | 2  | 9   | 8  | 7  | 6  | 5 | 4 | 3  | 2  |
| Multiplicação | 5 | 8 | 51 | 36 | 171 | 24 | 28 | 30 | 0 | 4 | 60 | 42 |

__Somatório (5+8+...+42) = 459__

Obter o resto da divisão do somatório por 11.
Se o resto da divisão for igual a 1 ou 0, o primeiro dígito será igual a 0 (zero).
Senão, o primeiro dígito será igual ao resultado de 11 – resto.

No exemplo:
__Resto da divisão 459/11 = 8.__
__=> 1º DV = 3__ (resultado de 11-8)

#### 1.2. Cálculo do segundo dígito verificador

Para o cálculo do segundo dígito é necessário acrescentar o primeiro DV ao final do CNPJ, formando assim treze caracteres, e repeƟr os passos realizados para o primeiro dígito.

Assim, no exemplo, temos:

| CNPJ                | 1 | 2  | A  | B  | C   | 3  | 4  | 5  | 0 | 1 | D  | E  | 3  |
|---------------------|---|----|----|----|-----|----|----|----|---|---|----|----|----|
| Atribuição de Valor | 1 | 2  | 17 | 18 | 19  | 3  | 4  | 5  | 0 | 1 | 20 | 21 | 3  |
| Atribuição de Peso  | 6 | 5  | 4  | 3  | 2   | 9  | 8  | 7  | 6 | 5 | 4  | 3  | 2  |
| Multiplicação       | 6 | 10 | 68 | 54 | 38  | 27 | 32 | 35 | 0 | 5 | 80 | 63 | 6  |

__Somatório (6+10+...+6) = 424__

__Resto da divisão 424/11 = 6__

__=> 2º DV = 5__ (resultado de 11-6)

__=> Resultado final: 12.ABC.345/01DE-35__


[serpro.gov.br](serpro.gov.br)
[Tutorial](https://tecnoblog.net/noticias/cnpj-vai-mudar-em-2026-e-serpro-libera-codigos-para-ajudar-na-transicao)
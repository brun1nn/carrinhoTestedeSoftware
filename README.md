# Carrinho de Compras

Uma implementacao simples de um carrinho de compras em JavaScript, criada para praticar **regras de negocio**, **testes automatizados** e **validacao de cenarios de borda**.

O projeto calcula o total de uma compra considerando subtotal dos itens, cupom de desconto e frete. A suite de testes documenta o comportamento esperado da aplicacao.

## Visao geral

```text
itens do carrinho
       |
       v
   subtotal -----> cupom PROMO10 -----> frete -----> total arredondado
```

## Regras de negocio

| Regra | Comportamento |
| --- | --- |
| Carrinho vazio | Lanca `Carrinho invalido` |
| Quantidade zero ou negativa | Lanca `Carrinho invalido` |
| Preco negativo | Lanca `Carrinho invalido` |
| Cupom `PROMO10` | Aplica 10% de desconto sobre o subtotal |
| Subtotal a partir de R$ 100 | Frete gratis |
| Subtotal abaixo de R$ 100 | Frete fixo de R$ 15 |
| Valor final | Arredondado para duas casas decimais |

## Tecnologias

- **Node.js**
- **JavaScript (CommonJS)**
- **Jest 30**
- **npm**

## Estrutura do repositorio

```text
.
├── carrinho.js       # Regra principal para calcular o total
├── carrinho.test.js  # Testes automatizados com Jest
├── index.js          # Execucao manual dos cenarios em caixa-preta
├── package.json      # Scripts e dependencias do projeto
├── package-lock.json # Versoes exatas das dependencias
└── .gitignore        # Arquivos ignorados pelo Git
```

## Como executar

### 1. Clone o repositorio

```bash
git clone URL_DO_SEU_REPOSITORIO
cd carrinho_testes
```

### 2. Instale as dependencias

```bash
npm install
```

### 3. Execute os testes automatizados

```bash
npm test
```

O Jest executa os seis casos da suite e informa se todas as regras foram atendidas.

### 4. Execute os testes manuais

```bash
node index.js
```

Essa execucao apresenta no terminal o resultado esperado, o valor obtido e o status de cada caso de teste.

## Cenarios testados

- **CT-01:** frete gratis para subtotal exatamente igual a R$ 100.
- **CT-02:** desconto de 10% com o cupom `PROMO10`.
- **CT-03:** erro para quantidade negativa ou igual a zero.
- **CT-04:** arredondamento do total para duas casas decimais.
- **CT-05:** erro para carrinho vazio.
- **CT-06:** cobranca de frete para subtotal abaixo de R$ 100.

## Exemplo de uso

```js
const { calcularTotal } = require('./carrinho');

const itens = [
  { preco: 50, quantidade: 1 },
  { preco: 25, quantidade: 2 }
];

const total = calcularTotal(itens, 'PROMO10');
console.log(total); // 90
```

Nesse exemplo, o subtotal e R$ 100. O cupom aplica 10% de desconto e o frete e gratis, resultando em R$ 90.

## Objetivo academico

Este repositorio foi desenvolvido como exercicio pratico para demonstrar como transformar requisitos de um carrinho de compras em uma funcao testavel. A proposta tambem reforca a importancia de testar valores-limite, entradas invalidas e regras de desconto e frete.

## Licenca

Projeto distribuido sob a licenca ISC, conforme definido no `package.json`.

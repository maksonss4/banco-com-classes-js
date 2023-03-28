#  Banco com classes

Classe `Cliente`

A classe `Cliente` deve possui os seguintes parâmetros em seu constructor:

- **idCliente:** string
- **tipoCliente:** string
- **dataCriacao:** string
- **codBanco:** number
- **agencia:** number
- **conta:** number
- **saldo:** number
- E terá o **historico** que será um parâmetro definido no constructor inicando como uma array vazia

Classe `Pessoa`, está classe é uma extensão da classe `Cliente` heardando todos os seus atributos e recebendo mais alguns que são:

- **nome:** string
- **cpf:** string
- **email:** string
- **telefone:** number
- **dataDeNascimento:** string

Classe `Empresa` que também é um extensão da classe `Cliente` herdando todos os seus atributos e recebendo alguns novos:

- **nomeFantasia:** string
- **cnpj:** string
- **email:** string
- **telefone:** number
- **dataDaFundacao:** string

Classe `Transacao` que é uma **classe estática** ou seja não recebe **nenhum parâmetro pelo constructor** e tem **todos seus métodos como estático**. Está classe é responsável por realizar todas as operações de pagamentos, depósitos, transferências e registro do histórico essas operações acontecendo por meio dos métodos abaixo:

Método estático `transferencia`:

Este método recebe por parâmetro:

- **contaOrigem:** Class (Podendo ser uma classe Empresa ou Pessoa)
- **contaDestino:** Class (Podendo ser uma classe Empresa ou Pessoa)
- **idTransacao**: number
- **dataDeTransacao**: string
- **valorDaTransferencia**: number

- Em sequência valida se a **contaOrigem** possui um **saldo** maior ou igual ao de **valorDaTransferencia**.
- Caso o **saldo** sejá maior adiciona no **histórico** da **contaOrigem** o objeto:

```javascript
{
  idTransacao: idTransacao,
  dataDeTransacao: dataDeTransacao,
  valorDaTransferencia: valorDaTransferencia,
  tipo: "pagamento",
}
```

- E ao **histórico** da **contaDestino** o seguinte objeto:

```javascript
{
  idTransacao: idTransacao,
  dataDeTransacao: dataDeTransacao,
  valorDaTransferencia: valorDaTransferencia,
  tipo: "recebimento",
}
```

- Ao final do sucesso deve retornar a seguinte mensagem:

```javascript
{
  mensagem: "Transferência realizada com sucesso!";
}
```

- Caso o **saldo** seja menor que o **valorDaTransferencia** retorna a mensagem:

```javascript
{
  mensagem: "Saldo insuficiente para transferência!";
}
```

Método estático `deposito`:

O método deposito recebe por parâmetro:

- **contaDestino:** Class (Podendo ser uma classe Empresa ou Pessoa)
- **idDeposito**: number
- **dataDoDeposito**: string
- **valorDoDeposito**: number

- Adiciona ao **saldo** da **contaDestino** o **valorDoDeposito**
- E Adiciona ao **historico** da **contaDestino** o objeto:

```javascript
{
  idDeposito: idDeposito,
  dataDoDeposito: dataDoDeposito,
  valorDoDeposito: valorDoDeposito,
  tipo: "recebimento",
}
```

- Retorna a mensagem:

```javascript
{
  mensagem: "Depósito realizado com sucesso!";
}
```

Método estático `pagamentoSalario`:

O método pagamentoSalario recebe por parâmetro:

- **contaOrigem:** Class (Podendo ser uma classe Empresa ou Pessoa)
- **contaDestino:** Class (Podendo ser uma classe Empresa ou Pessoa)
- **idPagamento**: number
- **dataDoPagamento**: string
- **valorDoSalario**: number

- Verifica se a **contaOrigem** é uma instância da classe **Pessoa** caso seja o **valorDoSalario** não pode ser maior 1000. Caso não passe nesta validação retorna a mensagem:

```javascript
{
  mensagem: "Seu limite máximo para este tipo de operação é de 1000, entre em contato com o banco!";
}
```

- Verifica se a **contaOrigem** tem o **valor** maior ou igual ao **valorDoSalario**.
- Caso a validação seja verdeira adiciona ao **saldo** da **contaDestino** o **valorDoSalario** e remove do **saldo** da **contaOrigem**
- Caso a validação seja verdadeira adiciona ao **historico** da **contaDestino** o objeto:

```javascript
{
    idPagamento: idPagamento,
    dataDoPagamento: dataDoPagamento,
    valorDoSalario: valorDoSalario,
    tipo: "recebimento",
}
        
```

- E ao **historico** da **contaOrigem** o objeto:

```javascript
{
  idPagamento: idPagamento,
  dataDoPagamento: dataDoPagamento,
  valorDoSalario: valorDoSalario,
  tipo: "pagamento",
}
```

- E retorna a mensagem:

```javascript
{
  mensagem: "Pagamento realizado com sucesso!";
}
```

- Caso o não passe na validação retorna a mensagem:

```javascript
{
  mensagem: "Saldo insuficiente para realizar o pagamento!";
}
```

## Teste

Insira o seguinte código no final do programa para verificar se ele está funcionando apropriadamente. **Atenção** (Não modifique este código!

```javascript
const ChurrosVictor = new Empresa(
  "01",
  "Vip",
  "16/05/2022",
  156,
  2798,
  987654321,
  1000,
  "Churros do Victor",
  "1011121314",
  "churrosVictor@email.com.br",
  1234567890,
  "16/05/2022"
);

const Joao = new Pessoa(
  "02",
  "Comum",
  "16/03/2022",
  156,
  2798,
  91919292,
  100,
  "João",
  "2345678901",
  "joao@kenzie.com.br",
  "90919293",
  "01/01/2019"
);

const Maria = new Pessoa(
  "03",
  "Vip",
  "16/03/2022",
  156,
  2798,
  10121416,
  5000,
  "Maria",
  "3456789012",
  "maria@kenzie.com.br",
  "90919293",
  "01/01/2019"
);

console.log(ChurrosVictor.saldo); // Deve retornar 1000
console.log(ChurrosVictor.nomeFantasia); // Deve retornar ChurrosVictor
console.log(ChurrosVictor.historico); // Deve retornar []
console.log(Joao.nome); // Deve retornar João
console.log(Joao.saldo); // Deve retornar 100
console.log(Maria.idCliente); // Deve retornar "03"
console.log(Maria.tipoCliente); // Deve retornar "Vip"

console.log(Transacao.transferencia(Joao, Maria, 1, "25/07/2022", 200)); // Deve retornar {mensagem: "Saldo insuficiente para transferência!"}

console.log(
  Transacao.transferencia(ChurrosVictor, Joao, 2, "20/07/2022", 500)
); // Deve retornar {mensagem: "Transferência realizada com sucesso!"}

console.log(ChurrosVictor.historico); // Deve retornar [{idTransacao: 2, dataDeTransacao: "20/07/2022", valorDaTransferencia: 500, tipo: "pagamento"}]
console.log(Joao.historico); // Deve retornar [{idTransacao: 2, dataDeTransacao: "20/07/2022", valorDaTransferencia: 500, tipo: "recebimento"}]

console.log(ChurrosVictor.saldo); // Deve retornar 500
console.log(Joao.saldo); // Deve retornar 600

console.log(Transacao.deposito(ChurrosVictor, 3, "02/07/2022", 650)); // Deve retornar {mensagem: "Depósito realizado com sucesso!"}

console.log(ChurrosVictor.historico[1]); // Deve retornar [{idDeposito: 3, dataDoDeposito: "02/07/2022", valorDoDeposito: 650, tipo: "recebimento"}]
console.log(ChurrosVictor.saldo); // Deve retornar 1150

console.log(Transacao.pagamentoSalario(Maria, Joao, 4, "22/07/2022", 1100)); // Deve retornar {mensagem: "Seu limite máximo para este tipo de operação é de 1000, entre em contato com o banco!"}
console.log(Transacao.pagamentoSalario(Joao, Maria, 5, "23/07/2022", 700)); // Deve retornar {mensagem: "Saldo insuficiente para realizar o pagamento!"}

console.log(Transacao.pagamentoSalario(Maria, Joao, 6, "22/12/2022", 900)); // Deve retornar {mensagem: "Pagamento realizado com sucesso!"}
console.log(Maria.saldo); // Deve retornar 4100
console.log(Maria.historico); // Deve retornar [{idPagamento: 6, dataDoPagamento: "22/12/2022", valorDaSalario: 900, tipo: "pagamento"}]
console.log(Joao.historico[1]); // Deve retornar [{idPagamento: 6, dataDoPagamento: "22/12/2022", valorDaSalario: 900, tipo: "recebimento"}]
```

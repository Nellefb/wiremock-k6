# 🚀 WireMock + K6

Projeto para simulação de uma API REST utilizando **WireMock** e execução de **testes de performance com K6**.

## Tecnologias

* WireMock 3.13.2
* K6
* Java
* JSON

## Estrutura do Projeto

```text
WIREMOCK-K6/
├── _files/
│   └── cars.json
├── mappings/
│   ├── api-cars.json
│   ├── post-cars.json
│   └── post-cars-500.json
├── tests/
│   ├── consulta.js
│   ├── test-sucesso.js
│   └── test-500.js
├── report/
│   └── test-500.html
└── wiremock-standalone-3.13.2.jar
```

## Executando o WireMock

```bash
java -jar wiremock-standalone-3.13.2.jar
```

A API ficará disponível em:

```text
http://localhost:8080
```

## Endpoints

### GET /api/cars

Retorna a lista de veículos cadastrados.

### POST /api/cars

Recebe os seguintes campos:

```json
{
  "brand": "Volkswagen",
  "model": "fusca",
  "year": 1978
}
```

#### Sucesso (201)

O cadastro é realizado apenas quando o campo `model` possui o valor:

```json
{
  "model": "fusca"
}
```

Resposta:

```json
{
  "message": "Car successfully registered!",
  "carId": 6
}
```

#### Erro (500)

A API retorna erro interno quando o campo `model` possui o valor:

```json
{
  "model": "up tsi"
}
```

Resposta:

```json
{
  "message": "Internal server error: model 'up tsi' is not allowed."
}
```

> Os valores `fusca` e `up tsi` devem ser enviados exatamente como configurados (minúsculos).

## Testes K6

Os scripts disponíveis são:

| Script          | Descrição                         |
| --------------- | --------------------------------- |
| consulta.js     | Teste do endpoint GET `/api/cars` |
| test-sucesso.js | Teste do cenário de sucesso (201) |
| test-500.js     | Teste do cenário de erro (500)    |

### Executar um teste

```bash
k6 run tests/consulta.js
```

ou

```bash
k6 run tests/test-sucesso.js
```

ou

```bash
k6 run tests/test-500.js
```

## Relatórios

Os relatórios gerados pelos testes ficam na pasta:

```text
report/
```

Exemplo:

```text
report/test-500.html
```

## Objetivo

Demonstrar a utilização do WireMock para mock de APIs REST e do K6 para execução de testes de carga e performance em cenários de sucesso e falha.

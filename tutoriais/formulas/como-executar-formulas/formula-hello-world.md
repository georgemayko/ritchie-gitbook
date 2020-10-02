---
description: >-
  Nesta seção, você encontrará o passo a passo para executar nosso "Hello
  World".
---

# Fórmula "Hello World"

## Hello World

Depois de finalizar os passos anteriores -  [**instalação**](../../../getting-started/installation/) e [**inicialização**](../../../getting-started/initialization.md) -,  para acessar a [**fórmula hello world**](https://github.com/ZupIT/ritchie-formulas/tree/master/demo/hello-world) para testar o Ritchie, será necessário adicionar o repositório [**ritchie-formulas-demo**](https://github.com/ZupIT/ritchie-formulas-demo) localmente.

Para fazer isso, você pode usar o comando **`rit add repo`**, ou executar a linha de comando abaixo:

```text
echo '{"provider":"Github", "name":"demo", "version":"2.0.0", "url":"https://github.com/ZupIT/ritchie-formulas-demo", "token": null, "priority":1}' | rit add repo --stdin
```

{% hint style="info" %}
É possível verificar os repositórios estão sendo usados executando o comando **`rit list repo`**.
{% endhint %}

**Agora que você adicionou o repositório de demo, você pode executar os comandos desse tutorial.**

No Ritchie, é possível, você tem 4 possibilidades de rodar uma fórmula: 

1. Via Prompt 
2. Via Prompt e Docker 
3. Via Stdin
4. Via Stdin e Docker 

Para isso, escreva um dos comandos abaixo:

### Caso 1: Usando Prompt

{% hint style="warning" %}
Como **essa fórmula  foi desenvolvida usando Golang**, é preciso ter **Golang** instalado para conseguir  executá-la **localmente**.
{% endhint %}

```text
rit demo hello-world
```

Selecione uma opção para cada parâmetro de entrada e veja a mágica acontecer:

![rit demo hello-world](../../../.gitbook/assets/large-gif-1054x366-%20%281%29.gif)

Essa é a execução padrão de linhas de comando no Ritchie, executando fórmulas localmente através de **prompt** \(interagindo com o CLI no terminal\) para informar os parâmetros de entrada.

### Caso 2: Usando Prompt & Docker

Você pode rodar o mesmo comando usando a flag **--docker** para executar a fórmula remotamente \(em um container\), mas ainda informando os parâmetros de entrada via **prompt**:

```text
rit demo hello-world --docker
```

{% hint style="warning" %}
O **Docker** precisa estar instalado e iniciado para conseguir executar comandos usando essa flag.  
Nesse caso, não é necessário ter **Golang** instalado.
{% endhint %}

### Caso 3: Usando Stdin

É também possível executar comando usando a flag **--stdin** \(Standard Input\). Dessa maneira, os parâmetros de entrada podem ser informados diretamente na linha de comando inicial:

```
echo '{"input_text":"Dennis", "input_bool":"false", "input_list":"everything", "input_password":"Ritchie"}' | rit demo hello-world --stdin
```

{% hint style="warning" %}
Ritchie usa o formato **JSON** para executar comandos STDIN.
{% endhint %}

{% page-ref page="../../como-usar-a-flag-stdin/" %}

### Caso 4: Usando Stdin & Docker

Quando são usadas as 2 flags **--stdin** e **--docker**, é possível executar o comando remotamente informando os parâmetros de entrada na linha de comando inicial, sem necessidade de ação humana:

```text
echo '{"input_text":"Dennis", "input_bool":"false", "input_list":"everything", "input_password":"Ritchie"}' | rit demo hello-world --stdin --docker
```

{% hint style="info" %}
Dê uma olhada nas fórmulas da comunidade \(ex: [**ritchie-formulas**](https://github.com/ZupIT/ritchie-formulas)\). 

A maioria das fórmulas tem um arquivo [**README**](https://github.com/ZupIT/ritchie-formulas/tree/master/demo/hello-world) explicando como executar a fórmula e para que ela serve.
{% endhint %}

## Próximos passos

Nessa seção, você viu como executar uma fórmula no Ritchie. Para continuar aprendendo:

👉Confira agora as fórmulas que você tem acesso usando o comando:

```text
rit --help
```

👉Veja como [**criar suas fórmulas**](../como-criar-formulas.md)**.**

# Level 3: API

## Objective

Create a formula on Ritchie that will **return the address datas from a ZipCode.**

{% hint style="info" %}
Command suggestion: **`rit brazil get address`**
{% endhint %}

## Inputs

This formula needs to contain \(at least\) this input parameter:

1. [ ] zipcode \(`ZIPCODE`\).

{% hint style="warning" %}
In Brazil we use a **CEP** as a **ZipCode**.   
  
Here is a suggestion of an API that return the address datas from a CEP to carry out the formula implementation: [**http://viacep.com.br/**](http://viacep.com.br/)\*\*\*\*
{% endhint %}

## Step by step

The formula needs to follow the next steps:

1. Validate the ZipCode input format. 
2. Call a service to get the address datas from the ZipCode. 
3. Convert address datas to JSON format. 
4. Return the result on the terminal.

## Improvement suggestions

 If you want to play a little more, here are some suggestions:

* [ ] Code a formula which will allow the user to get the ZipCode by entering address datas.

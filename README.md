## **Código Python: Histórico de Transações**

```python
import json
import os
from datetime import datetime

ARQUIVO = "transacoes.json"

# Carregar transações do arquivo
def carregar_transacoes():
    if not os.path.exists(ARQUIVO):
        return []
    with open(ARQUIVO, "r", encoding="utf-8") as file:
        return json.load(file)

# Salvar transações no arquivo
def salvar_transacoes(transacoes):
    with open(ARQUIVO, "w", encoding="utf-8") as file:
        json.dump(transacoes, file, indent=4, ensure_ascii=False)

# Adicionar nova transação
def adicionar_transacao(transacoes):
    tipo = input("Tipo (Entrada/Saída): ").strip().capitalize()
    if tipo not in ["Entrada", "Saída"]:
        print("Tipo inválido!")
        return
    descricao = input("Descrição: ")
    valor = float(input("Valor: R$ "))
    data = datetime.now().strftime("%d/%m/%Y %H:%M:%S")

    transacao = {
        "tipo": tipo,
        "descricao": descricao,
        "valor": valor,
        "data": data
    }

    transacoes.append(transacao)
    salvar_transacoes(transacoes)
    print("✅ Transação adicionada com sucesso!")

# Listar transações
def listar_transacoes(transacoes):
    if not transacoes:
        print("Nenhuma transação registrada.")
        return
    print("\n=== Histórico de Transações ===")
    for i, t in enumerate(transacoes):
        print(f"{i+1}. [{t['data']}] {t['tipo']} - {t['descricao']} : R$ {t['valor']:.2f}")
    print("===============================\n")

# Mostrar saldo atual
def saldo_atual(transacoes):
    saldo = 0
    for t in transacoes:
        if t["tipo"] == "Entrada":
            saldo += t["valor"]
        else:
            saldo -= t["valor"]
    print(f"💰 Saldo Atual: R$ {saldo:.2f}\n")

# Função principal
def main():
    transacoes = carregar_transacoes()

    while True:
        print("=== Sistema de Histórico de Transações ===")
        print("1 - Adicionar transação")
        print("2 - Listar transações")
        print("3 - Mostrar saldo atual")
        print("4 - Sair")
        escolha = input("Escolha uma opção: ")

        if escolha == "1":
            adicionar_transacao(transacoes)
        elif escolha == "2":
            listar_transacoes(transacoes)
        elif escolha == "3":
            saldo_atual(transacoes)
        elif escolha == "4":
            print("Saindo do sistema...")
            break
        else:
            print("Opção inválida, tente novamente!")

if __name__ == "__main__":
    main()
```

---

## **Funcionalidades**

* Registrar transações do tipo **Entrada** ou **Saída**
* Armazenar **descrição, valor e data/hora** da transação
* Listar todas as transações registradas
* Mostrar saldo atual calculado automaticamente
* Persistência de dados em **arquivo JSON**

---

## **Como Executar**

1. Salve o arquivo como `historico_transacoes.py`
2. Execute no terminal:

```bash
python historico_transacoes.py
```

3. Utilize o menu para adicionar e consultar transações.

---

## **Exemplo de Uso**

```text
=== Sistema de Histórico de Transações ===
1 - Adicionar transação
2 - Listar transações
3 - Mostrar saldo atual
4 - Sair
Escolha uma opção: 1

Tipo (Entrada/Saída): Entrada
Descrição: Venda de produto
Valor: 150
✅ Transação adicionada com sucesso!

=== Sistema de Histórico de Transações ===
Escolha uma opção: 2

=== Histórico de Transações ===
1. [22/09/2025 21:30:12] Entrada - Venda de produto : R$ 150.00
===============================

=== Sistema de Histórico de Transações ===
Escolha uma opção: 3
💰 Saldo Atual: R$ 150.00
```

---

## **README.md para GitHub**

````markdown
# 💳 Sistema de Histórico de Transações

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)

## Descrição
Este projeto implementa um **sistema simples de histórico de transações** utilizando Python.  
Permite registrar entradas e saídas financeiras, calcular saldo atual e manter persistência em arquivo JSON.

---

## Funcionalidades
- Adicionar transações do tipo Entrada ou Saída  
- Registrar descrição, valor e data/hora  
- Listar todas as transações  
- Mostrar saldo atual calculado automaticamente  
- Persistência de dados em arquivo JSON  

---

## Requisitos
- Python 3.x  

---

## Como Executar
1. Salve o arquivo `historico_transacoes.py`  
2. Execute no terminal:

```bash
python historico_transacoes.py
````

3. Use o menu para gerenciar suas transações.

---

## Melhorias Futuras

* Filtrar transações por data
* Relatórios mensais de receitas e despesas
* Interface gráfica (Tkinter ou PyQt)
* Versão web com Flask ou Django

---

## Licença

Uso pessoal.

# Seleção ótima de ondas em uma sessão de surfe

Projeto prático da disciplina **Otimização (COS360)**, Escola Politécnica da UFRJ.

**Autor:** Luiz Felipe Píccoli Cavalini

## Problema

Em uma sessão de surfe, só cerca de 8% do tempo é passado em pé na onda. O trabalho responde à
pergunta: **em quais ondas o surfista deve remar para passar o máximo de tempo em pé?**

As ondas chegam em séries, cada onda ocupa o surfista por um tempo (surfar, remar de volta ao pico e
tomar as ondas que chegam no caminho) e consome fôlego, que só se recupera durante a espera no pico.

## Modelo

- **Grafo:** cada onda é um nó; há um arco de $i$ para $j$ se, depois de surfar $i$ e voltar ao
  pico, ainda dá tempo de pegar $j$. Cada caminho do nó inicial ao final é uma sessão possível.
- **Variáveis:** $y_{ij} \in \{0,1\}$ (arco usado) e $f_{ij} \ge 0$ (energia ao chegar à onda $j$
  vindo de $i$).
- **Objetivo:** maximizar a soma dos segundos em pé das ondas escolhidas.
- **Restrições:** caminho único (conservação de fluxo), energia só em arcos usados, fôlego
  suficiente para cada onda e balanço de energia com recuperação durante a espera.
- **Classificação:** programa linear inteiro misto (MILP), NP-difícil, resolvido pelo Gurobi com
  *branch and bound*.

## Arquivo

| Arquivo | Conteúdo |
|---|---|
| `surf_projeto.ipynb` | Relatório e código: modelo, implementação, exemplo de 6 ondas, sessões sintéticas de 40 ondas, comparação com regras simples e análise de sensibilidade. O notebook já está executado, com todas as saídas. |

## Como executar

Requisitos: Python 3.10 ou superior e uma licença do Gurobi (a licença acadêmica é gratuita).

```bash
python -m venv .venv
source .venv/bin/activate
pip install gurobipy matplotlib jupyter
jupyter notebook surf_projeto.ipynb
```

Os dados das sessões são sintéticos, gerados com semente fixa, então os resultados são
reproduzíveis.

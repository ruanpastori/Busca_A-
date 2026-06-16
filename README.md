# 🚀 Busca A* (A-Star) no Mapa da Romênia

## 📖 Sobre o Projeto

Este projeto foi desenvolvido como atividade prática da disciplina de **Inteligência Artificial e Engenharia de Software** do curso de **Big Data**.

O objetivo é implementar o algoritmo de busca heurística **A*** (A-Star), um dos algoritmos mais utilizados em Inteligência Artificial para encontrar o caminho de menor custo entre dois pontos em um grafo.

O problema utilizado é o clássico **Mapa da Romênia**, apresentado por Russell e Norvig no livro *Artificial Intelligence: A Modern Approach*.

---

## 🎯 Objetivos

* Compreender o funcionamento da Busca A*.
* Aplicar conceitos de grafos.
* Utilizar heurísticas para otimização de buscas.
* Encontrar o menor caminho entre duas cidades.
* Demonstrar conceitos de Engenharia de Software através da documentação UML.

---

# 🧠 O que é o Algoritmo A*?

O algoritmo A* combina:

* Busca de Custo Uniforme (g(n))
* Busca Gulosa (h(n))

Utilizando a função:

```text
f(n) = g(n) + h(n)
```

Onde:

| Função | Descrição                                   |
| ------ | ------------------------------------------- |
| g(n)   | Custo real percorrido até o nó atual        |
| h(n)   | Estimativa do custo restante até o objetivo |
| f(n)   | Custo total estimado                        |

O algoritmo sempre expande o nó com menor valor de f(n).

---

# 🗺️ Problema Proposto

Encontrar o melhor caminho entre:

```text
Cidade Inicial: Arad
Cidade Objetivo: Bucharest
```

Utilizando:

* Distâncias reais entre cidades.
* Distância em linha reta até Bucharest como heurística.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/f9dd683c-d2b6-4215-9b7c-e4f4afd7d2a4" />

---

# ⚙️ Estrutura do Código

## 1. Importação da Biblioteca

```python
import heapq
```

### Explicação

A biblioteca `heapq` implementa uma fila de prioridades.

Ela permite que o algoritmo sempre selecione automaticamente o nó com menor valor de:

```text
f(n)
```

---

## 2. Definição do Grafo

```python
mapa_romenia = {
 ...
}
```

### Explicação

O grafo representa as cidades e suas conexões.

Exemplo:

```python
'Arad': [('Zerind', 75), ('Sibiu', 140)]
```

Significa:

* Arad → Zerind = 75 km
* Arad → Sibiu = 140 km

---

## 3. Definição da Heurística

```python
heuristica_bucareste = {
 ...
}
```

### Explicação

A heurística representa a distância em linha reta de cada cidade até Bucharest.

Exemplo:

```python
'Arad': 366
```

Indica que Arad está aproximadamente 366 km de Bucharest em linha reta.

---

## 4. Função Busca A*

```python
def busca_a_estrela(inicio, objetivo, grafo, heuristica):
```

### Explicação

Esta função implementa todo o algoritmo A*.

Recebe:

* Cidade inicial
* Cidade destino
* Grafo
* Heurística

Retorna:

* Caminho encontrado
* Custo total

---

## 5. Inicialização da Fronteira

```python
f_inicial = heuristica[inicio]
fronteira = [(f_inicial, 0, inicio, [inicio])]
```

### Explicação

A fronteira armazena os nós que ainda serão explorados.

Cada item possui:

```text
(f(n), g(n), cidade, caminho)
```

---

## 6. Controle de Custos

```python
custos_g = {inicio: 0}
```

### Explicação

Armazena o menor custo conhecido para cada cidade.

Evita expandir caminhos mais caros.

---

## 7. Expansão dos Nós

```python
f_atual, g_atual, cidade_atual, caminho = heapq.heappop(fronteira)
```

### Explicação

Seleciona automaticamente o nó com menor valor de:

```text
f(n)
```

---

## 8. Teste de Objetivo

```python
if cidade_atual == objetivo:
```

### Explicação

Verifica se o destino foi alcançado.

Se verdadeiro:

* Retorna o caminho.
* Retorna o custo total.

---

## 9. Exploração dos Vizinhos

```python
for vizinho, custo_estrada in grafo.get(cidade_atual, []):
```

### Explicação

Percorre todas as cidades conectadas ao nó atual.

---

## 10. Atualização dos Custos

```python
novo_g = g_atual + custo_estrada
```

### Explicação

Calcula o custo real acumulado até o vizinho.

---

## 11. Cálculo da Função A*

```python
f_vizinho = novo_g + heuristica[vizinho]
```

### Explicação

Aplica a fórmula:

```text
f(n) = g(n) + h(n)
```

---

## 12. Inserção na Fila de Prioridade

```python
heapq.heappush(...)
```

### Explicação

Insere o novo nó mantendo a fila ordenada automaticamente.

---

# 📊 Resultado Obtido

```text
Arad
 ↓
Sibiu
 ↓
Rimnicu Vilcea
 ↓
Pitesti
 ↓
Bucharest
```

Custo total:

```text
418 km
```
# 💻 Código Fonte Completo

```python
import heapq

# Grafo do mapa da Romênia (Russell & Norvig)
mapa_romenia = {
    'Arad': [('Zerind', 75), ('Sibiu', 140), ('Timisoara', 118)],
    'Zerind': [('Arad', 75), ('Oradea', 71)],
    'Oradea': [('Zerind', 71), ('Sibiu', 151)],
    'Sibiu': [('Arad', 140), ('Oradea', 151), ('Fagaras', 99), ('Rimnicu Vilcea', 80)],
    'Timisoara': [('Arad', 118), ('Lugoj', 111)],
    'Lugoj': [('Timisoara', 111), ('Mehadia', 70)],
    'Mehadia': [('Lugoj', 70), ('Drobeta', 75)],
    'Drobeta': [('Mehadia', 75), ('Craiova', 120)],
    'Craiova': [('Drobeta', 120), ('Rimnicu Vilcea', 146), ('Pitesti', 138)],
    'Rimnicu Vilcea': [('Sibiu', 80), ('Craiova', 146), ('Pitesti', 97)],
    'Fagaras': [('Sibiu', 99), ('Bucharest', 211)],
    'Pitesti': [('Rimnicu Vilcea', 97), ('Craiova', 138), ('Bucharest', 101)],
    'Bucharest': [('Fagaras', 211), ('Pitesti', 101), ('Giurgiu', 90), ('Urziceni', 85)],
    'Giurgiu': [('Bucharest', 90)],
    'Urziceni': [('Bucharest', 85), ('Vaslui', 142), ('Hirsova', 98)],
    'Hirsova': [('Urziceni', 98), ('Eforie', 86)],
    'Eforie': [('Hirsova', 86)],
    'Vaslui': [('Urziceni', 142), ('Iasi', 92)],
    'Iasi': [('Vaslui', 92), ('Neamt', 87)],
    'Neamt': [('Iasi', 87)]
}

# Heurística h(n): Distância em linha reta até Bucharest
heuristica_bucareste = {
    'Arad': 366, 'Bucharest': 0, 'Craiova': 160, 'Drobeta': 242,
    'Eforie': 161, 'Fagaras': 176, 'Giurgiu': 77, 'Hirsova': 151,
    'Iasi': 226, 'Lugoj': 244, 'Mehadia': 241, 'Neamt': 234,
    'Oradea': 380, 'Pitesti': 100, 'Rimnicu Vilcea': 193,
    'Sibiu': 253, 'Timisoara': 329, 'Urziceni': 80,
    'Vaslui': 199, 'Zerind': 374
}

def busca_a_estrela(inicio, objetivo, grafo, heuristica):

    f_inicial = heuristica[inicio]
    fronteira = [(f_inicial, 0, inicio, [inicio])]

    custos_g = {inicio: 0}

    print(f"--- Iniciando Busca A* de {inicio} para {objetivo} ---\n")

    while fronteira:

        f_atual, g_atual, cidade_atual, caminho = heapq.heappop(fronteira)

        print(
            f"Expandindo: {cidade_atual:15} | "
            f"g(n)={g_atual:<3} | "
            f"h(n)={heuristica[cidade_atual]:<3} | "
            f"f(n)={f_atual}"
        )

        if cidade_atual == objetivo:
            return caminho, g_atual

        for vizinho, custo_estrada in grafo.get(cidade_atual, []):

            novo_g = g_atual + custo_estrada

            if vizinho not in custos_g or novo_g < custos_g[vizinho]:

                custos_g[vizinho] = novo_g

                f_vizinho = novo_g + heuristica[vizinho]

                novo_caminho = caminho + [vizinho]

                heapq.heappush(
                    fronteira,
                    (f_vizinho, novo_g, vizinho, novo_caminho)
                )

    return None, float('inf')


# Execução do teste
caminho_final, custo_total = busca_a_estrela(
    'Arad',
    'Bucharest',
    mapa_romenia,
    heuristica_bucareste
)

print("\n--- Resultado do A* ---")

if caminho_final:
    print("Caminho ótimo encontrado:",
          " -> ".join(caminho_final))
    print(f"Custo real total da viagem: {custo_total}")
else:
    print("Não foi possível encontrar um caminho.")
```

---



# 📈 Complexidade

| Métrica | Complexidade |
| ------- | ------------ |
| Tempo   | O(b^d)       |
| Espaço  | O(b^d)       |

Onde:

* b = fator de ramificação
* d = profundidade da solução

---

# 🧩 Diagrama de Casos de Uso

```text
+----------------+
|    Usuário     |
+----------------+
         |
         |
         v
+-------------------------+
| Informar Cidade Inicial |
+-------------------------+
         |
         v
+-------------------------+
| Informar Cidade Final   |
+-------------------------+
         |
         v
+-------------------------+
| Executar Busca A*       |
+-------------------------+
         |
         v
+-------------------------+
| Exibir Melhor Caminho   |
+-------------------------+
```

---

# 🔄 Diagrama de Sequência

```text
Usuário
   |
   | Informa origem e destino
   v
Sistema
   |
   | Inicia Busca A*
   v
Busca A*
   |
   | Consulta Grafo
   v
Mapa da Romênia
   |
   | Retorna vizinhos
   v
Busca A*
   |
   | Calcula g(n), h(n) e f(n)
   |
   | Expande melhor nó
   |
   | Encontrou objetivo?
   |
   +---- Não ----+
   |             |
   +-------------+
   |
   Sim
   |
   v
Sistema
   |
   | Exibe caminho ótimo
   v
Usuário
```

---

# 🔁 Diagrama de Estados

```text
[Início]
    |
    v
[Aguardando Dados]
    |
    v
[Inicializar Busca]
    |
    v
[Expandir Nó]
    |
    v
[Calcular f(n)]
    |
    v
[Objetivo Encontrado?]
   / \
 Não  Sim
  |     |
  v     v
[Expandir Próximo Nó]
        |
        v
[Exibir Resultado]
        |
        v
      [Fim]
```

---

# 🏆 Conclusão

A implementação do algoritmo A* demonstrou a eficiência das buscas heurísticas na resolução de problemas de caminhos mínimos.

A utilização da heurística permitiu reduzir significativamente a quantidade de estados explorados quando comparado a algoritmos não informados, tornando a busca mais rápida e eficiente.

Além dos conceitos de Inteligência Artificial, o projeto aplicou práticas de Engenharia de Software através da documentação UML, contribuindo para uma melhor compreensão do sistema desenvolvido.

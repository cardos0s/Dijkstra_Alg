# **Dijkstra_Alg — Caminho mínimo lendo grafo de arquivo**

Implementação do algoritmo de **Dijkstra** (equivalente a UCS com pesos não-negativos) para encontrar o **melhor caminho** entre dois vértices,  
lendo o **grafo a partir de um arquivo** de texto. 

---

## **✅ Requisitos**
- .NET SDK **6.0+** (teste em .NET 9)  
- Qualquer SO (Windows/macOS/Linux)  

---

## **📂 Estrutura do projeto**

```
Dijkstra_Alg/
├─ Dijkstra_Alg.csproj
├─ Program.cs
├─ Graph.cs
├─ grafo.txt                 # exemplo básico (não-dirigido)
└─ graphs/
   ├─ grafo_multipath.txt    # exemplo com múltiplos caminhos
   └─ grafo_desconexo.txt    # exemplo sem caminho entre origem e destino
```

> O arquivo `grafo.txt` é copiado automaticamente para a pasta de saída no build (via `.csproj`).

---

## **📝 Formato do arquivo de grafo**

Cada linha representa uma aresta: `origem destino peso`  

- Separador: espaço(s) ou TAB  
- Comentários começam com `#`  
- Pesos **não-negativos** (pré-requisito do Dijkstra)  
- Por padrão, o grafo é **não-dirigido** (use `--directed` para torná-lo dirigido)  

**Exemplo (`grafo.txt`):**
```
# origem destino peso
A B 7
A C 8
B F 2
C F 6
C G 4
D F 8
E H 1
F D 8
F G 9
F H 3
H E 1
```

---

## **▶️ Como executar**

### **Opção A — do diretório raiz do repositório**
```bash
# macOS/Linux
dotnet run --project ./Dijkstra_Alg/Dijkstra_Alg.csproj ./Dijkstra_Alg/grafo.txt A H
```
```powershell
# Windows (PowerShell)
dotnet run --project .\Dijkstra_Alg\Dijkstra_Alg.csproj .\Dijkstra_Alg\grafo.txt A H
```

### **Opção B — de dentro da pasta do projeto**
```bash
cd Dijkstra_Alg
# graças à cópia automática do grafo para bin/, o relativo funciona
dotnet run grafo.txt A H
```

**Saída esperada (para o exemplo acima):**
```
Caminho ótimo: A -> B -> F -> H
Custo total: 12
```

### **Parâmetros**
```
Uso: dotnet run <arquivo_grafo> <origem> <destino> [--directed]
```
- `<arquivo_grafo>`: caminho do arquivo do grafo  
- `<origem>` / `<destino>`: rótulos dos vértices  
- `--directed`: interpreta as arestas como dirigidas  

---

## **🧪 Grafos de teste**

Crie a pasta `graphs/` e adicione os exemplos abaixo.

### **1) Múltiplos caminhos — `graphs/grafo_multipath.txt`**
```
# dois caminhos com custos diferentes entre A e H
A B 4
B H 10
A C 2
C D 2
D E 3
E H 4
```

**Exemplo:**
```bash
dotnet run --project ./Dijkstra_Alg/Dijkstra_Alg.csproj ./graphs/grafo_multipath.txt A H
# Caminho ótimo: A -> C -> D -> E -> H
# Custo total: 11
```

### **2) Grafo desconexo — `graphs/grafo_desconexo.txt`**
```
# dois componentes: {A,B} e {C,D}
A B 1
C D 1
```

**Exemplo:**
```bash
dotnet run --project ./Dijkstra_Alg/Dijkstra_Alg.csproj ./graphs/grafo_desconexo.txt A D
# Não existe caminho entre a origem e o destino.
```

---

## **🧩 Implementação (resumo)**
- Estrutura: `Graph.cs` (carrega arquivo e armazena adjacência), `Program.cs` (parse de argumentos e execução)  
- Dijkstra usando `PriorityQueue<TPriority,TElement>` (do .NET 6+)  
- Reconstrução de caminho via dicionário `prev`  
- Tratamento de erros: vértice inexistente, arquivo inválido, pesos negativos, grafo desconexo  

---

## **🐞 Solução de problemas**
- **“Arquivo não encontrado: grafo.txt”**  
  Use caminho absoluto ou a opção com `--project`, ou ajuste o **Working Directory** no Rider, ou use a estrutura acima (cópia para bin/).  

- **“Peso negativo”**  
  Dijkstra/UCS não suportam pesos negativos.  

- **Sem caminho**  
  A mensagem **“Não existe caminho…”** é esperada para componentes desconexos.  

---

✍️ **Qualquer dúvida técnica, consulte `Graph.cs` e `Program.cs`. O projeto está pronto para ser executado e testado com diferentes grafos.**


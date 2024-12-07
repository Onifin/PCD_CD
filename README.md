# README do Projeto

## Instruções de Uso

### Compilação do Código
1. Para compilar o pipeline sem suporte a OpenMP:
   ```bash
   g++ -pg -no-pie -fno-builtin -o pipe pipeline.cpp Compressor.cpp Descompressor.cpp
   ```

2. Para compilar com suporte a OpenMP:
   ```bash
   g++ -pg -no-pie -fno-builtin -fopenmp -o pipe pipeline.cpp Compressor.cpp Descompressor.cpp
   ```

### Execução
1. Execute o programa, especificando o arquivo a ser processado:
   ```bash
   ./pipe um_meio.mp4
   ```

2. Analise o desempenho usando o `gprof`:
   ```bash
   gprof ./pipe | less
   ```

3. Para gerar informações específicas de otimização do compilador, compile o arquivo `Descompressor.cpp` com as flags apropriadas:
   ```bash
   g++ -O3 -ftree-vectorize -fopt-info-vec-missed -c Descompressor.cpp -o Descompressor.o
   ```

4. Gere o gráfico de chamadas a partir do perfil coletado:
   ```bash
   gprof -b -q pipe gmon.out > call_graph.dot
   ```

### Notas
- O arquivo `call_graph.dot` pode ser visualizado usando ferramentas como o [Graphviz](https://graphviz.org/).
- Use a versão com OpenMP para explorar o paralelismo em sistemas com múltiplos núcleos.
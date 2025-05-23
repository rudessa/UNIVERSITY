# Описание алгоритма Дейкстры

Алгоритм Дейкстры позволяет находить кратчайший путь от одной вершины графа до другой. Этот алгоритм работает для взвешенных графов с положительными весами рёбер.

## Основные этапы работы алгоритма

1. **Инициализация**:
   - Устанавливается начальное расстояние до стартовой вершины равным 0, а до всех остальных вершин — бесконечностью.
   - Создаётся словарь `previous`, чтобы отслеживать предшественников каждой вершины в кратчайшем пути.
   - Все вершины считаются непосещёнными.

2. **Выбор текущей вершины**:
   - Выбирается вершина с наименьшим известным расстоянием из очереди с приоритетом.
   - Если такая вершина является конечной, то обработка завершается.

3. **Обновление соседей**:
   - Для каждого соседа текущей вершины пересчитывается расстояние через текущую вершину.
   - Если новое расстояние меньше ранее известного, оно обновляется.
   - Вершина добавляется в очередь с приоритетом с обновлённым расстоянием.

4. **Завершение работы**:
   - Алгоритм завершает работу, когда найдён кратчайший путь до конечной вершины или если очередь с приоритетом становится пустой.
   - Используя словарь `previous`, восстанавливается последовательность вершин, образующих кратчайший путь.

## Реализация

### Классы

- `Graph` — представляет граф в виде списка смежности. Вершины соединяются рёбрами с определёнными весами.
- `Vertex` — узел графа, содержащий уникальное значение (идентификатор).
- `Edge` — ребро графа, соединяющее вершины. Содержит вес и указатель на соседнюю вершину.
- `PriorityQueue` — очередь с приоритетом для выбора вершины с минимальным расстоянием. Реализована с использованием кучи (heap).

### Алгоритм (функция `dijkstra`)

```python

def dijkstra(graph, start, end):
    """
    Реализация алгоритма Дейкстры для нахождения кратчайшего пути в графе.

    Аргументы:
        graph (Graph): Граф, содержащий вершины и рёбра.
        start (Vertex): Стартовая вершина.
        end (Vertex): Конечная вершина.

    Возвращает:
        None. Выводит кратчайшее расстояние и путь до конечной вершины.
    """
```

1. Инициализируются:
   - `distances`: словарь с минимальными расстояниями до вершин.
   - `previous`: словарь для отслеживания предшественников.
   - `queue`: очередь с приоритетом.

2. Пока очередь не пуста:
   - Удаляется вершина с минимальным расстоянием.
   - Если вершина конечная, выводятся результаты (расстояние и путь).
   - Для каждого соседа пересчитывается расстояние, и если оно меньше текущего, обновляется информация.

3. Если очередь пуста и путь не найден, выводится, что путь недоступен.

## Пример работы

```python
vertices = [Vertex("A"), Vertex("B"), Vertex("C"), Vertex("D"), Vertex("E"), Vertex("F"), Vertex("G"), Vertex("H")]
A, B, C, D, E, F, G, H = vertices

adj_list = {
    A: [Edge(1.8, B), Edge(1.5, C), Edge(1.4, D)],
    B: [Edge(1.8, A), Edge(1.6, E)],
    C: [Edge(1.5, A), Edge(1.8, E), Edge(2.1, F)],
    D: [Edge(1.4, A), Edge(2.7, F), Edge(2.4, G)],
    E: [Edge(1.6, B), Edge(1.8, C), Edge(1.4, F), Edge(1.6, H)],
    F: [Edge(2.1, C), Edge(2.7, D), Edge(1.4, E), Edge(1.3, G), Edge(1.2, H)],
    G: [Edge(2.4, D), Edge(1.3, F), Edge(1.5, H)],
    H: [Edge(1.6, E), Edge(1.2, F), Edge(1.5, G)],
}

my_graph = Graph(adj_list)
dijkstra(my_graph, start=A, end=H)
```

## Используемые структуры данных

1. **Словари (`dict`)** — для хранения расстояний, предшественников и статуса посещённости вершин.
2. **Очередь с приоритетом** — для эффективного выбора вершины с минимальным расстоянием.
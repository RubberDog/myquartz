Einfache Sortieralgorithmen, Komplexität O(n²)
- Selection Sort
- Bubble Sort
- Insertion Sort

Effiziente Sortierverfahren, Komplexität O(n log n)
- Quick Sort
- Heap Sort
- Merge Sort

Suchalgorithmen mit je einem Satz

- Selection: Durchsucht die Menge nach dem kleinsten Element, packt den nach vorn
- Bubblesort: betrachtet zwei nebeneinanderliegende Elemente, tauscht wenn nötig
- Insertion: erstes Element gilt als "sortiert", weitere werden dann passend einsortiert

- Quicksort: Pivotelement auswählen, weitere werden links (kleiner) und rechts (größer) sortiert. Wichtig: NICHT verschoben, sondern werden nur vertauscht. Nutzt zwei "Pointer" dafür.
- Heapsort: baut nen sortierten Baum, dann wird das größte (root) Element entfernt. Baum korrigieren, wieder von vorn. ist der einzige dieser 5, der "von hinten" aus sortiert
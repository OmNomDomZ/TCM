# Что такое рациональная функция?
Рациональная функция — это функция, которая представляется в виде дроби, числитель и знаменатель которой являются многочленами.

# Что такое полином или многочлен?
Полином (или многочлен) — это математическое выражение, представляющее сумму одночленов.

# Что такое одночлен?
Одночлен — это произведение переменной в какой-то степени на коэффициент. 

# Как представлен полином в моей программе?
Используется структура дерево в дереве.
Полином представлен с использованием структуры PolySum, которая состоит из дерева.
1. Ключ дерева — это структура PolyMult.
2. Значение дерева — это коэффициент одночлена.

## Структура PolyMult
PolyMult представляет одночлен и также реализован как дерево, где:

1. Ключ — это переменная, связанная с одночленом.
2. Значение — это степень этой переменной.

# Что делает функция mergeTreeCustom?

mergeTreeCustom — это функция, которая объединяет два дерева, применяя к их значениям пользовательскую логику. Основная цель этой функции — пройтись по узлам двух деревьев и объединить их с использованием заданной функции, чтобы создать новое дерево с результатами объединения.

## На примере multPolySum:
### mergeTreeCustom в этой функции выполняет несколько задач:

1. Объединение степеней переменных: 
В mergeTreeCustom(k1.mult, k2.mult, \kk, vv1, vv2 -> {vv1 + vv2})  
одночлены из деревьев k1.mult и k2.mult объединяются по ключам переменных. Если переменная встречается в обоих одночленах, их степени складываются.
2. Суммирование коэффициентов: 
В mergeTreeCustom(acc2, makeTree1(multi, v1 * v2), \kk, vv1, vv2 -> {vv1 + vv2})  
дерево acc2 обновляется с добавлением нового одночлена (multi) с произведением коэффициентов. Если в acc2 уже есть одночлен с таким же ключом, их коэффициенты суммируются.


# Что делает функция foldTree?
foldTree — это обобщенная функция, используемая для обхода дерева и применения некоторой операции ко всем его узлам. Она работает по принципу свёртки.

foldTree обходит дерево рекурсивно и на каждом узле применяет переданную функцию, обновляя аккумулятор.

## На примере multPolySum:
1. Внутренний foldTree возвращает аккумулятор acc2, содержащий результат произведения одночленов текущего узла из p1.sum с каждым узлом из p2.sum.
2. mergeTreeCustom затем используется для объединения этих результатов с аккумулятором внешнего foldTree (acc1).
3. После завершения работы всех итераций дерево, содержащее результат умножения, фильтруется с помощью filterTree, чтобы удалить одночлены с нулевым коэффициентом.

 
# Как происходят вычисления?
Рекурсивно
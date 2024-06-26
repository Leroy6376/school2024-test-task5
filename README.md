# Тестовое задание для отбора на Летнюю ИТ-школу КРОК по разработке

## Условие задания

В теории управления проектами существует такое понятие как стейкхолдер или, иначе говоря, заинтересованная сторона (ЗС). Это лицо, которое может иметь влияние на ход проекта и с чьим мнением нужно считаться по совершенно разным причинам.

Тем не менее, очевидно, что каждый из стейкхолдеров по-своему важен для проекта, что является следствием разного уровня показателей интереса и влияния, потому реакция на обратную связь от каждого из стейкхолдеров определяется в соответствии с матрицей заинтересованных лиц, которая позволяет наглядно определить наиболее и наименее весомых из них.

Чаще всего такая матрица представляет собой график с осями X и Y, где по оси X располагается величина влияния, а по оси Y - величина интереса, и так как значения величин - сугубо неотрицательные числа, работа идет в правом верхнем квадранте. В свою очередь такой срез оси координат делится на 4 части в центрах осей.

Рассмотрим на примере. Допустим, у нас есть 5 ЗС. Первым делом построим ось координат XY и нанесем деления по обеим осям от 0 до 5. Далее поделим пополам каждую из осей (это будут точки (0; 2.5) и (2.5; 0)) и построим пунктирную линию для разделения матрицы на 4 квадранта. Таким образом, мы получим будущую матрицу стейкхолдеров, на которой сможем визуально расположить их по степени влияния и интереса.
![Матрица стейкхолдеров](https://github.com/croc-code/school2024-test-task5/blob/master/stakeholders_matrix.png)

Для того, чтобы определить положение стейкхолдера, используется метод попарного сравнения, схожий с рейтинговыми таблицами в спорте. Строятся матрицы (для интереса и влияния отдельно), в строках и столбцах которых располагаются стейкхолдеры в одинаковом порядке следования, а на пересечении строк и столбцов выставляются значения 0, 0.5 и 1 по следующим правилам:

- 1, если стейкхолдер в текущей строке имеет большее влияние/интерес, чем стейкхолдер в текущем столбце;
- 0.5, если стейкхолдеры в текущих строке и столбце имеют одинаковое влияние/интерес;
- 0, если стейкхолдер в текущей строке имеет меньшее влияние/интерес, чем стейкхолдер в текущем столбце.

По диагоналям значения не выставляются, так как сравнивать стейкхолдера с самим собой некорректно.

Далее полученные величины в строках складываются и получается итоговый ранг заинтересованной стороны. То же самое, но наглядно:
![alt text](https://github.com/croc-code/school2024-test-task5/blob/master/pair_compair.png)

Построив такие матрицы для интереса и влияния, мы получаем “координаты” каждого из стейкхолдеров в матрице и можем расположить в соответствующих квадратах.
Самыми важными для проекта ЗС будут те, что располагаются в правом верхнем квадранте, а те, чье мнение не обязательно учитывать здесь и сейчас, - в левом нижнем.

Вам необходимо реализовать программу, которая по полученным данным матриц влияния и интереса будет определять самых важных стейкхолдеров. В качестве входных данных используются два текстовых файла:

- interest.txt (матрица попарного сравнения стейкхолдеров по уровню интереса)
- influence.txt (матрица попарного сравнения стейкхолдеров по уровню влияния)

Каждый из файлов имеет следующий формат:

- в первой строке файла располагаются наименования заинтересованных сторон, разделенные символов “|”, соответствующие наименованию строк и столбцов матрицы в одинаковом порядке следования;
- последующие строки представляют собой матрицу попарного сравнения со значениями 0, 0.5, 1 в соответствии с правилами формирования;
- на главной диагонали (сравнение ЗС самой с собой) вместо значения идет символ “\_”.

Пример содержимого одного из входных файлов:

```
Stakeholder 1 | Stakeholder 2 | Stakeholder 3 | Stakeholder 4 | Stakeholder 5
_ 0 1 0 0
1 _ 0.5 1 1
0 0.5 _ 0 0.5
1 0 1 _ 1
1 0 0.5 0 _
```

В результате работы программа должна сформировать файл (result.txt), в котором будут располагаться самые важные стейкхолдеры (в произвольном порядке). Пример содержимого выходного файла:

```
Stakeholder 1
Stakeholder 3
```

## Автор решения

Вавилов Илья Максимович

## Описание реализации

Программа реализована на языке программирования Python и располагается в файле main.py. Программа по полученным данным матриц влияния и интереса определяет самых важных стейкхолдеров и записывает их имена в выходной файл. В качестве входных данных используются два текстовых файла: матрица попарного сравнения стейкхолдеров по уровню интереса и матрица попарного сравнения стейкхолдеров по уровню влияния. Программы действует по следующему алгоритму:

1. Определение входных файлов влияния и интереса, для этого в качестве аргументов командной строки при запуске программы можно указать название файла интереса, а затем файла влияния. Если названия файлов не будут указаны, будут использованы файлы по умолчанию.
2. Чтение входных файлов и выделение из них имен стейкхолдеров и матриц сравнения. Имена стейкхолдеров должны быть идентичны для обоих файлов, файлы существовать, а сами данные матриц должны соответствовать ранее указанному формату.
3. Счет итогового ранга для каждого стейкхолдера путем суммирования элементов строки для каждой матрицы, тем самым получаем координаты стейкхолдера на графике влияние/интерес.
4. Выбор всех стейкхолдеров, чьи координаты лежат в правом верхнем квадранте, то есть чьи координаты больше или равны половине всего количества стейкхолдеров.
5. Запись всех выбранных стейкхолдеров в выходной файл.

## Инструкция по сборке и запуску решения

Для запуска решения необходим установленный Python.

1. Клонировать репозиторий
2. Запустить main.py следующими командами:

```
python main.py interest_file.txt influence_file.txt
```

Где "interest_file.txt" и "influence_file.txt" - примеры входных файлов интереса и влияния

```
python main.py
```

В данном случае вместо входных файлов будут использоваться файлы по умолчанию: и 'interest.txt' и "influence.txt".

3. Результат работы программы будет в файле "result.txt"

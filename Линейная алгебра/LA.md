---
author:
- Александр Петров
date: 2023-01-04
title: Линейная алгебра
---

[]{#content label="content"}

## Введение

Данные конспекты были оцифрованы по нескольким причинам:

-   Во-первых, мне было интересно изучить глубже линейную алгебру, так
    как данный предмет является очень мощным инструментом, которым любой
    студент ФАЛТ МФТИ будет пользоваться практически во всех изучаемых
    науках.

-   Во-вторых, это была моя первая практика верстки текста в среде LaTeX

-   Ну и в третьих, я надеюсь что эти записи помогут кому нибудь еще при
    изучении линейной алгебры.

Так как лектор и семинарист у меня были разными людьми, я видел два
взгляда на линейную алгебру и попытался сформировать свой, который тут и
изложил.

***К сожалению, мне не удалось успеть закончить все темы (из-за нехватки
времени), поэтому я буду благодарен, если вы сообщите мне о пропуске той
или иной темы, а также о смысловых ошибках и опечатках.***

НАСТОЯТЕЛЬНО РЕКОМЕНДУЮ СВЕРЯТЬ ДАННЫЙ МАТЕРИАЛ С ОФИЦИАЛЬНЫМИ
ИСТОЧНИКАМИ: ЛЕКЦИЯМИ И КНИГАМИ.

Версии данных конспектов нумеруются как N.M, где N - количество
добавлений нового материала с сделанными правками, M - количество
сделанных правок без добавления нового материала.

## Обозначения

-   Def - определение

-   Th - теорема

-   Ex - пример

# Обратная матрица

Матрица $B$ называется обратной к матрице $A$, если выполняются
равенства: $$BA = AB = E, \qquad \text{ где } E \text{ - единичная}$$
Обозначается обратная матрица так: $B = A^{-1}$. В чем мотивация вводить
обратную матрицу? Можно привести два примера:

Во первых, если знать (уметь находить) обратную матрицу, то можно
мгновенно находить решения системы линейных уравнений с невырожденной
матрицей системы: $$Ax = b \Rightarrow x = A^{-1}b$$

Во-вторых, если $A$ - матрица преобразования координат, например,
поворота на угол $\varphi$ вокруг оси $Oz$, то можно, зная координаты
вектора $\boldsymbol{x}'$ в новой СК найти его координаты в старой СК:
$$\boldsymbol{x} = \begin{pmatrix}
x_1 \\
x_2 \\
x_3
\end{pmatrix} = \begin{pmatrix}
\text{cos } \varphi & \text{sin } \varphi & 0 \\
-\text{sin } \varphi & \text{cos } \varphi & 0 \\
0 & 0 & 1
\end{pmatrix}^{-1} \begin{pmatrix}
x_1' \\
x_2' \\
x_3'
\end{pmatrix} = A^{-1}\boldsymbol{x}'$$

::: problem
**Задача 1**. Чему равна $A^{-1}$ в примере с поворотом? (не пользуйтесь
методом Гаусса)
:::

## Свойства обратных матриц

### Существование и единственность {#существование-и-единственность .unnumbered}

Первое, что нужно определить: у всех ли матриц существуют обратные? И
бывает ли у одной матрицы несколько обратных к ней?

Из определения видно, что обратимыми матрицами могут быть только
квадратные (посмотрите что происходит, если предположить, что не
квадратная матрица имеет обратную).

::: problem
**Задача 2**. Попробуйте исследовать вопрос единственности
самостоятельно. Предположите что обратная матрица не единственна, и
найдите противоречие, или докажите, что обратных матриц действительно
бывает несколько.
:::

### Обратные матрицы к $AB$ и $A^T$ {#обратные-матрицы-к-ab-и-at .unnumbered}

Для удобной работы с обратными матрицами вам понадобится знать как в
общем случае найти обратную матрицу от произведения известных матриц $A$
и $B$, а также обратную матрицу от транспонированной (в жизни мне это ни
разу не пригодилось, но вдруг вам пригодится).

Что значит найти $(AB)^{-1}$? Это значит, что нужно выразить эту матрицу
через $A^{-1}$ и $B^{-1}$.

::: problem
**Задача 3**. Найдите $(AB)^{-1}$ и $(A^T)^{-1}$. Честное слово, это
делается в одну строчку. (при нахождении обратной к транспонированной
вспомните как транспонировать произведение)
:::

::: problem
**Задача 4** (**Критерий существования обратной матрицы**). Обратная
матрица - серьезная штука, и нельзя просто так взять и начать находить
обратную матрицу. Надо быть уверенным, что она вообще существует.
Оказывается, что для обратимости матрицы необходимо и достаточно, чтобы
она была невырожденной.

Докажите этот факт (используйте интернет и навык гугления).
:::

## Алгоритм нахождения $A^{-1}$ (Метод Гаусса)

Теперь перейдём к практике. Часто для нахождения обратной матрицы
используют метод Гаусса.

Суть его состоит в следующем: элементарными преобразованиями строк в
матрице $(A|E)$ мы сначала получаем из матрицы $A$ верхнетреугольную (с
ненулевыми элементами над главной диагональю) с единицами на главной
диагонали. Коротко это называется \"прямой ход метода Гаусса\". А затем
производим элементарные преобразования строк, чтобы получить единичную
матрицу на месте матрицы $A$ - \"обратный ход метода Гаусса\". При таких
манипуляциях со строками на месте исходной единичной матрицы появится
искомая $A^{-1}$.

Или короче:
$$\fbox{\textit{Общий вид: } $(A|E) \xrightarrow{\text{ЭП Строк}} (E|A^{-1})$}$$

Для наглядности приведу пример:

::: ex
**Ex 1**. $$\underbrace{\begin{pmatrix}
1 & 1 & 1 & 1 & 0 & 0 \\
1 & 2 & 2 & 0 & 1 & 0 \\
2 & 3 & 4 & 0 & 0 & 1 
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
1 & 1 & 1 & 1 & 0 & 0 \\
0 & 1 & 1 & -1 & 1 & 0 \\
0 & 1 & 2 & -2 & 0 & 1 
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
1 & 1 & 1 & 1 & 0 & 0 \\
0 & 1 & 1 & -1 & 1 & 0 \\
0 & 0 & 1 & -1 & -1 & 1 
\end{pmatrix}
\Rightarrow
}_{\text{прямой ход метода Гаусса}}$$ $$\underbrace{
\Rightarrow
\begin{pmatrix}
1 & 1 & 0 & 2 & 1 & -1 \\
0 & 1 & 0 & 0 & 2 & -1 \\
0 & 0 & 1 & -1 & -1 & 1 
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
1 & 0 & 0 & 2 & -1 & 0 \\
0 & 1 & 0 & 0 & 2 & -1 \\
0 & 0 & 1 & -1 & -1 & 1 
\end{pmatrix}
}_{\text{обратный ход метода Гаусса}}$$
:::

::: problem
**Задача 5** (**Обоснование метода Гаусса**). Вроде все очевидно, но
есть одно но: почему в правой части матрицы $(A|E)$ при применении
метода Гаусса появится именно обратная матрица? Подумайте об этом на
досуге.

*Подсказка:* для обоснования этого факта вам не помешает вспомнить о
том, что вообще такое элементарные преобразования столбцов и строк
матрицы (и чему они эквивалентны).
:::

Если вы обосновали метод Гаусса, то становится очевидным следующее:
$$\left(\frac{A}{B}\right)  \xrightarrow{\text{ЭП столбцов}} \left( \frac{E}{BA^{-1}}\right)$$
$$\left(A|B\right)  \xrightarrow{\text{ЭП строк}} \left(E|A^{-1}B\right)$$

На десерт в этой главе покажу вам красивую задачу, в которой фигурирует
так называемая нильпотентная матрица - матрица, для которой существует
целое число $m$, такое что $A^m = O$ - нулевая матрица.

::: problem
**Задача 6** (15.56). Итак, доказать, что для нильпотентной матрицы
выполняется равенство:
$$E + A  + A^{2} + \dots + A^{m-1} = (E - A)^{-1}$$ Сразу говорю: даже
не думайте о формуле Тейлора. Во-первых, это не правильно, а во-вторых,
тут тема \"обратные матрицы\" , вообще-то.
:::

Прежде чем смотреть доказательство

Доказательство:\
$$\begin{aligned}
+ 
\left\{
\begin{aligned}
(E - A)E &= E - A \\
(E - A)A &= A - A^{2} \\
(E - A)A^{2} &= A^{2} - A^{3} \\
\dots &\: \dots \\
(E - A)A^{m-1}&= A^{m-1} - A^{m} \\
\end{aligned} \;
\vline
\Rightarrow
\underbrace{(E - A)(E + A + A^{2} + \dots + A^{m-1}) = E - A^{m} = E}_{E + A + A ^{2} + \dots + A^{m-1} = (E - A)^{-1}}
\right. \\
\end{aligned}$$

::: flushright
[ч.т.д.]{.underline}
:::

# Ранг матрицы

Пусть $\mathscr{A}$ - набор столбцов высоты m (для строк аналогично)

::: defin
**Def 1** (**Столбцовый ранг**). Если в наборе $\mathscr {A}\ \exists$ r
ЛНЗ столбцов и $\forall$ набор из (r+1) столбца ЛЗ, то будем говорить,
что ранг $\mathscr {A}$ равен r
:::

::: oboz
*Обозначение 1*. $rg\ \mathscr {A} = r$
:::

**Свойства столбцового ранга:**

1.  $rg\ \mathscr {A} + rg\ \mathscr {B} \geqslant rg(\ \mathscr {A} \cup \mathscr {B})$
    (док-во тривиально - от противного)

2.  $\ \mathscr {A} \supset \ \mathscr {B} \Rightarrow rg\ \mathscr {A} \geqslant rg\ \mathscr {B}$

::: defin
**Def 2**. $\{A_{1}, \dots , A_{r}\} \subset  \mathscr {A}$ - **базисная
подсистема** $\mathscr {A}$, если:\
1) $\{A_{1}, \dots , A_{r}\}$ - ЛНЗ\
2) $\forall A \in \mathscr {A}$ линейно выражается через
$\{A_{1}, \dots , A_{r}\}$
:::

::: theorem
**Th 1**. *$$\begin{aligned}
\begin{aligned}
rg \ \mathscr {A} &= r  \\
\{A_{1}, \dots , A_{r}\} &\subset \mathscr {A} - ЛНЗ \\
\end{aligned} \;
\vline
\Rightarrow
\{A_{1}, \dots , A_{r}\} - \text{базисная подсистема для } \mathscr {A}
\end{aligned}$$*
:::

::: ev
*Доказательство 1*. $$\begin{aligned}
\bullet \quad &\{rg \ \mathscr {A} = r\} \Rightarrow \{\forall A \in \mathscr {A} \hookrightarrow \{A_{1}, \dots , A_{r}, A\} \subset \mathscr {A} - ЛЗ\}\Rightarrow \\ &\Rightarrow \left\{\exists \text{ нетривиальная ЛК } \lambda_{0}A + \sum_{k = 1}^{r}\lambda_{k}A_{k} = 0\right\}
\end{aligned}$$

$$\begin{aligned}
\bullet \quad &Если\ \lambda_{0} = 0,\text{ то получаем нетрив. ЛК } \{A_{1}, \dots , A_{r}\} \text{ равную 0 } \Rightarrow\ ?! \\
&Если\ \lambda_{0} \ne 0 \Rightarrow A = \sum_{k = 1}^{r}\left(- \frac{\lambda_{k}}{\lambda_{0}}\right) A_{k} \Rightarrow \text{ A линейно выражается через } \{A_{1}, \dots , A_{r}\}
\end{aligned}$$

$$\bullet \quad  Итог: 
\left\{
\begin{aligned}
\begin{aligned}
\{A_{1}, \dots , A_{r}\} \subset \mathscr {A} - ЛНЗ, \\
\forall A \in \mathscr {A} \text{ линейно выражается через } \{A_{1}, \dots , A_{r}\} 
\end{aligned} \
\vline
\Rightarrow
\{A_{1}, \dots , A_{r}\} - \text{б. п. для } \mathscr {A}
\end{aligned} 
\right.$$

::: flushright
[ч.т.д.]{.underline}
:::
:::

::: obs
*Замечание 1*. Рассмотрим $M_{m}$ - мн-во всех столбцов высоты m.\
Рассмотрим столбцы: $$\underbrace{e_{1} =
    \begin{pmatrix}
    1 \\
    0 \\
    \vdots \\
    0
    \end{pmatrix};\quad
    e_{2} =
    \begin{pmatrix}
    0 \\
    1 \\
    \vdots \\
    0
    \end{pmatrix}
    \quad \cdots \quad
    e_{m} =
    \begin{pmatrix}
    0 \\
    \vdots \\
    0 \\
    1
    \end{pmatrix}}_{\in M_{m}}$$

-   $\{e_{1}, \cdots, e_{m}\}$ - ЛНЗ

-   $\forall A \in M_{m} \text{ рассклад. по } \{e_{1}, \cdots, e_{m}\}$\
    $$A = 
    \begin{pmatrix}
    a_{1}\\
    \vdots \\
    a_{m}
    \end{pmatrix}
    = a_{1}e_{1} + \cdots + a_{m}e_{m}$$

Вывод: $\{e_{1}, \cdots, e_{m}\}$ - базисная подсистема в
$M_{m} \Rightarrow rg M_{m} = m$
:::

::: defin
**Def 3** (**ранг матрицы**). $$\underset{m \times n}{A} = 
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots &  & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
= 
\underbrace{\begin{pmatrix}
    a_{1\bullet} \\
    \vdots \\
    a_{m\bullet} 
    \end{pmatrix}}_{\text{строчная запись}}
=
\underbrace{\begin{pmatrix}
    a_{\bullet 1} & \cdots & a_{\bullet n} 
    \end{pmatrix}}_{\text{столбцовая запись}}$$

$\Rightarrow$\
*Иными словами, ранг матрицы - это **максимальное количество** ЛНЗ
столбцов или строк данной матрицы. Ранг матрицы равен ее строчному и
столбцовому рангам.*
:::

::: obs
*Замечание 2*. Равенство
$rg\ \{a_{\bullet 1}, \cdots, a_{\bullet n} \} = rg\ \{a_{1\bullet}, \cdots, a_{m\bullet} \}$
иногда называют **теоремой о рангах**
:::

::: obs
*Замечание 3*. Доказав равенство $rg\ A = rg\ A^{T}$, далее мы можем
говорить о том, что все свойства матриц связанные со столбцами так же
верны и для строк.
:::

::: theorem
**Th 2**. *Если к матрице приписать какой либо столбец (строку), то ранг
либо увеличится на 1, либо не изменится.*
:::

**Свойства ранга матрицы:**

1.  $rgA + rgB \geqslant rg(A + B)$

2.  min $\{rgA, rgB\} \geqslant rg(AB)$

    ::: ev
    *Доказательство 2*. Заметим, что столбцы $AB$ есть ЛК столбцов
    матрицы $A$. Но тогда $$rg\ AB \le rg\ (A|AB) = rg\ A$$ А на основе
    этого: $$rg\ (AB) = rg\ (AB)^T = rg\ B^T A^T \le rg\ B^T = rg\ B$$

    ::: flushright
    [ч.т.д.]{.underline}
    :::
    :::

3.  $rg(B) \geqslant rg(AB);\ \underbrace{(AB)_{i\bullet}}_{\text{i-ая строка АВ}} = \underbrace{\sum_{k=1}^{n}a_{ik}b_{k\bullet}}_{\text{ЛК строк В}}$

4.  $rg(AB) = rgB, \text{если А невырожденная }$ (аналогично при умн. на
    невыр. м-цу слева)\
    *Следовательно, при ЭП строк/столбцов ранг матрицы не изменяется
    (т.к. совокупность ЭП строк (столбцов) можно представить как
    умножение на невырожденную матрицу слева (справа))*

::: theorem
**Th 3** (**о базисном миноре**). *Квадратная подматрица на пересечении
r ЛНЗ столбцов и r ЛНЗ строк матрицы А - невырожденная. Где r - ранг А.*
:::

::: theorem
**Th 4** (**критерий невырожденности**).
*$A \in \underset{n\times n}{M}$ $$\begin{aligned}
\fbox{$rgA = n \Leftrightarrow |A| \ne 0 \Leftrightarrow \exists A^{-1}$}
\end{aligned}$$*
:::

::: ex
**Ex 2**. Док-ть:
$$\forall \{A, B\} \in \underset{n\times n}{M} \hookrightarrow rg
\begin{pmatrix}
A & E \\
BA & B 
\end{pmatrix} 
= n$$ Док-во: $$\begin{pmatrix}
A & E \\
BA & B 
\end{pmatrix}
= 
\underbrace{\begin{pmatrix}
E & O \\
B & O 
\end{pmatrix}}_{rg = n}
\underbrace{\begin{pmatrix}
A & E \\
A & E
\end{pmatrix}}_{rg = n}$$

::: flushright
ч.т.д.
:::
:::

## Как находить ранг матрицы?

Пытаемся собрать насильственными методами (элементарными
преобразованиями и вычеркиванием нулевых строк и столбцов)
единичную/невырожденную подматрицу в левом верхнем углу (а за счет того
что мы можем вычеркивать нулевые строки эта подматрица вообще может
располагаться в первых r столбцах). Её размер и будет рангом данной
матрицы.

::: ex
**Ex 3**. $rg\ A = ?$ $$A = 
\begin{pmatrix}
2 & 4 & 2 \\
-1 & -2 & -1 \\
1 & 5 & 3 \\
8 & 1 & -2 \\
2 & 7 & 4 
\end{pmatrix}
\rightarrow 
\begin{pmatrix}
2 & 4 & 2 \\
0 & 0 & 0 \\
1 & 5 & 3 \\
8 & 1 & -2 \\
2 & 7 & 4 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
2 & 4 & 2 \\
0 & 3 & 2 \\
0 & -15 & -10 \\
0 & 3 & 2 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
2 & 4 & 2 \\
0 & 3 & 2 
\end{pmatrix}$$ Ответ: $rg = 2$
:::

::: ex
**Ex 4** (16.19.4).
$rg\ A(\omega) =\ ?\ (\forall \omega \in \mathbb{R})$ $$A =
\begin{pmatrix}
1 & 1 & 1 \\
1 & \omega & \omega^{2} \\
1 & \omega^{2} & \omega 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
1 & 1 & 1 \\
0 & \omega - 1 & \omega^{2} - 1 \\
0 & \omega^{2} - 1 & \omega - 1
\end{pmatrix}
\rightarrow
\begin{pmatrix}
1 & 0 & 0 \\
0 & \omega - 1 & \omega^{2} - 1 \\
0 & \omega^{2} - 1 & \omega - 1
\end{pmatrix}$$ Рассмотрим\
$$\tilde{A} = 
\begin{pmatrix}
 \omega - 1 & \omega^{2} - 1 \\
 \omega^{2} - 1 & \omega - 1
\end{pmatrix}$$

-   Если $\omega = 1 \Rightarrow rg\ A = 1 + 0 = 1$

-   Если $\omega = 0, -2 \Rightarrow rg\ A = 1 + 1 = 2:$
    $$|\tilde{A}| = (\omega - 1)^{2}
    \begin{vmatrix}
    1 & \omega + 1 \\
    \omega + 1 & 1
    \end{vmatrix}
    = (\omega - 1)^{2}(1 - (\omega + 1)^{2}) = \underbrace{- \omega(\omega + 2)(\omega - 1)^{2} = 0}_{при \ \omega = 0, -2}$$

-   Если $\omega \notin \{-2, 0, 1\}$, то
    $rg\tilde{A} = 2 \Rightarrow RgA = 3$
:::

::: ex
**Ex 5**. $rg\ A =\ ?$ Указать какую либо базисную подсистему столбцов,
строк, невырожденную подматрицу порядка $rg\ A$

-   Совершаем ЭП *строк*: $$A = 
    \begin{pmatrix}
        0 & 0 & 2 & 1 & -1 & 2 \\
        0 & 0 & -4 & -2 & 2 & -4 \\
        3 & -6 & 5 & 1 & 2 & 5 \\
        -1 & 2 & 5 & 3 & -7 & 2 
    \end{pmatrix}
    \rightarrow
    \begin{pmatrix}
    0 & 0 & 2 & 1 & -1 & 2 \\
    0 & 0 & 20 & 10 & -19 & 11 \\
    -1 & 2 & 5 & 3 & -7 & 2 
    \end{pmatrix}
    \rightarrow$$ $$\rightarrow
    \begin{pmatrix}
    0 & 0 & 2 & 1 & -1 & 2 \\
    0 & 0 & 0 & 0 & -9 & -9 \\
    -1 & 2 & 5 & 3 & -7 & 2 
    \end{pmatrix}$$ Столбцы №1, 3, 5 можно принять за базисные (они
    ЛНЗ)\

-   Формируем подматрицу из столбцов №1, 3, 5 и совершаем ЭП *столбцов*:
    $$\tilde{A} =
    \begin{pmatrix}
    0 & 2 & -1 \\
    0 & -4 & 2 \\
    3 & 5 & 2 \\
    -1 & 5 & -7 
    \end{pmatrix}
    \rightarrow
    \begin{pmatrix}
    0 & 0 & -1 \\
    0 & 0 & 2 \\
    3 & 9 & 2 \\
    -1 & -9 & -7
    \end{pmatrix}
    \rightarrow
    \begin{pmatrix}
    0 & 0 & -1 \\
    0 & 0 & 2 \\
    3 & 0 & 2 \\
    -1 & -6 & -7
    \end{pmatrix}$$ Строки №1, 3, 4 - базисные строки А\

-   Невырожденная подматрица: $$\begin{pmatrix}
        0 & 2 & -1 \\
        3 & 5 & 2 \\
        -1 & 5 & -7
    \end{pmatrix}$$
:::

# Скелетное разложение матрицы

::: theorem
**Th 5**. *Любая матрица представляется в виде произведения двух матриц.
Левый множитель - матрица, составленная из столбцов базисного минора,
правй множитель - матрица, составленная из упрощенных строк базисного
минора, когда на его месте находится Е.*
:::

::: ev
*Доказательство 3*. Пусть матрица размера $m\times n$ с минором в левом
верхнем углу. $$A =
\begin{pmatrix}
a_{11} & \dots & a_{1r} & \dots & a_{1n} \\
\vdots & & \vdots & & \vdots \\
a_{r1} & \dots & a_{rr} & \dots & a_{rn}\\
\vdots & & & & \vdots \\
a_{mn} & \dots & \dots & \dots & a_{mn} 
\end{pmatrix}$$

В первом столбце считаем первый элемент ненулевым и с помощью ЭП делаем
его равным 1. Затем, вычитая первую строку, умноженную на
соответствующий коэффициент из остальных строк, получаем первый столбец
единичной матрицы на месте первого столбца базисного минора.

Проделывая аналогичные операции с остальными r столбцами, получаем
единичную подматрицу порядка r на месте базисного минора.
$$\underbrace{E_N \dots E_1}_{T} A =
\left(
\begin{tabular}{c|c}
E & * \\ 
\hline 
0 & 0 \\ 
\end{tabular} 
\right) 
\Rightarrow 
A = T^{-1}
\left(
\begin{tabular}{c|c}
E & * \\ 
\hline 
0 & 0 \\ 
\end{tabular} 
\right)$$ где \* - \"что-то, неважно что\".

Убираем последние m-r строк в преобразованной матрице и последние m-r
столбцов в матрице $T^{-1}$, получая матрицу U: $$A = U(E|*)$$ Заметим,
что $u_{ij} = a_{ij},\ i,j = 1,\dots, r$

::: flushright
[ ч.т.д.]{.underline}
:::
:::

# Системы линейных алгебраических уравнений (СЛАУ)

$$\begin{aligned}
\left\{
\begin{aligned}
a_{11}x_{1} + a_{12}x_{2} + \dots + a_{1n}x_{n} &= b_{1} \\
a_{21}x_{1} + a_{22}x_{2} + \dots + a_{2n}x_{n} &= b_{2} \\
\dots \dots \dots \dots \dots \dots \dots \dots  \\
a_{m1}x_{1} + a_{m2}x_{2} + \dots + a_{mn}x_{n} &= b_{m} 
\end{aligned} \;
\Leftrightarrow
\underbrace{Ax = b}_{\text{матричная форма записи}}
\right. \\
\end{aligned}$$

::: defin
**Def 4**. $$\underset{m \times n}{A} = 
\underbrace{\begin{pmatrix}
    a_{11} & a_{12} & \cdots & a_{1n} \\
    a_{21} & a_{22} & \cdots & a_{2n} \\
    \vdots & \vdots &  & \vdots \\
    a_{m1} & a_{m2} & \cdots & a_{mn}
    \end{pmatrix}}_{\text{основная матрица системы}} ;\
\underbrace{x =
\begin{pmatrix}
x_{1} \\
x_{2} \\
\vdots \\
x_{n}
\end{pmatrix}}_{\text{ст-ц неизв-х}} ;\
\underbrace{b =
    \begin{pmatrix}
    b_{1} \\
    b_{2} \\
    \vdots \\
    b_{m}
    \end{pmatrix}}_{\text{ст-ц своб. членов}}$$
:::

::: defin
**Def 5**. $$\underset{m \times (n+1)}{(A|b)} = 
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} & b_{1}\\
a_{21} & a_{22} & \cdots & a_{2n} & b_{2}\\
\vdots & \vdots &  & \vdots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn} & b_{m}
\end{pmatrix}
- \text{\textbf{расширенная матрица системы}}$$
:::

::: defin
**Def 6**. $x_{0} - \text{\textbf{частные решения}, если: } Ax_{0} = b$
:::

::: defin
**Def 7**. **Общее решение** $Ax = b$ - мн-во всех частных решений
системы.
:::

::: defin
**Def 8**. $Ax = b$ - **совместная**, если у нее $\exists$ хотя бы одно
решение.
:::

::: defin
**Def 9**. Совместные системы $Ax = b$ и $Cx = d$ - **эквивалентные**
если их общие решения совпадают.
:::

::: theorem
**Th 6** (**Кронекера-Капелли**).
:::

::: ev
*Доказательство 4*.

-   Предположим СЛАУ совместна, тогда существуют
    $x_1,\dots x_n:\ a_{1 \bullet}x_1 + \dots + a_{n \bullet}x_n = b$

    Тогда $rg\ (A|b) = rg\ A$, т.к. столбец b является ЛК столбцов
    матрицы А.

-   Пусть $rg\ (A|b) = rg\ A$, тогда базисные миноры обеих матриц будут
    совпадать. Т.к. b - ЛК столбцов базисного минора, то он - ЛК
    столбцов матрицы А. Следовательно его можно разложить с
    коэффициентами $x_1, \dots, x_n$:
    $$a_{1\bullet}x_1 + \dots + a_{n\bullet}x_n = b$$ Следовательно,
    система имеет решение, а значит - совместна.

    ::: flushright
    [ч.т.д.]{.underline}
    :::
:::

::: defin
**Def 10**. $Ax = 0 - \text{\textbf{однородная СЛАУ}}$
:::

::: theorem
**Th 7**. *$x_{1}, \dots, x_{k}$ - частные решения однородной системы
$Ax = 0 \Leftrightarrow \forall \lambda_{i} \in \mathbb{R} \hookrightarrow \sum_{i=1}^{k}\lambda_{i}x_{i}$ -
частные решения $Ax = 0$*
:::

::: ev
*Доказательство 5*.

-   $$\begin{aligned}
    +
    \left\{
    \begin{aligned}
    Ax_{1} &= 0 |\times \lambda_{1} \\
    Ax_{2} &= 0 |\times \lambda_{2} \\
    \cdots &\quad \cdots \\
    Ax_{k} &= 0 |\times \lambda_{k} 
    \end{aligned} \
    \vline
    \Rightarrow
    A\underbrace{(\lambda_{1}x_{1} + \dots + \lambda_{k}x_{k})}_{\text{тоже решения}} = 0 
    \right.
    \end{aligned}$$

-   $$Возьмем\ \lambda_{i} = \left\{ 
    \begin{aligned}
    &0,\ i \ne j \\
    &1,\ i = j
    \end{aligned}
    \Rightarrow x_j - решение.\ Это\ верно\ \forall j = 1, \dots, k
    \right.$$

::: flushright
[ч.т.д.]{.underline}
:::
:::

::: defin
**Def 11**. Упорядоченный набор $x_{1}, \dots, x_{s}$ частных решений
однородной системы $Ax = 0$ - **фундаментальная система решений (ФСР)**,
если:

1.  $x_{1}, \dots, x_{s}$ - ЛНЗ столбцы

2.  $\forall$ частное решение системы $Ax = 0$ выражается через
    $x_{1}, \dots, x_{s}$
:::

::: theorem
**Th 8**. *Общее решение однородной системы $Ax = 0$ имеет вид:\
$\{\sum_{i=1}^{s}\lambda_{i}x_{i}\ |\lambda_{i} \in \mathbb{R}\}$ , где
$x_{1}, \dots, x_{s}$ - образуют ФСР системы.*
:::

::: theorem
**Th 9**. *Общее решение неоднородной системы $Ax = b$ имеет вид:\
$\{x_{0} + \sum_{i=1}^{s}\lambda_{i}x_{i}\ |\lambda_{i} \in \mathbb{R}\}$
, где $x_{0}$ - к.-л. частное решение неоднор. системы, а
$x_{1}, \dots, x_{s}$ - образуют ФСР однородной системы $Ax = 0$.*
:::

## Метод Гаусса решения СЛАУ

::: ex
**Ex 6**. $$\left\{
\begin{aligned}
y + 3z &= -1 \\
2x +3y +5z &= 3 \\
3x +5y + 7z &= 6
\end{aligned}
\right.
\leftrightarrow
\begin{pmatrix}
0 & 1 & 3 & -1 \\
2 & 3 & 5 & 3 \\
3 & 5 & 7 & 6 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
2 & 3 & 5 & 3 \\
0 & 1 & 3 & -1 \\
0 & 1 & -1 & 3 
\end{pmatrix}
\rightarrow$$ $$\rightarrow
\begin{pmatrix}
2 & 3 & 5 & 3 \\
0 & 1 & 3 & -1 \\
0 & 0 & 1 & -1 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
2 & 3 & 0 & 8 \\
0 & 1 & 0 & 2 \\
0 & 0 & 1 & -1 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
2 & 0 & 0 & 2 \\
0 & 1 & 0 & 2 \\
0 & 0 & 1 & -1 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
1 & 0 & 0 & 1 \\
0 & 1 & 0 & 2 \\
0 & 0 & 1 & -1 
\end{pmatrix}$$ Ответ: $x = 1;\ y = 2;\ z = -1$
:::

::: ex
**Ex 7**. $$\begin{pmatrix}
1 & -5 & -6 & 11 & -9 \\
5 & 1 & -4 & 3 & 7 \\
1 & 8 & 7 & -15 & 17 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
1 & -5 & -6 & 11 & -9 \\
0 & 26 & 26 & -52 & 52 \\
0 & 13 & 13 & -26 & 26 
\end{pmatrix}
\rightarrow
\begin{pmatrix}
1 & -5 & -6 & 11 & -9 \\
0 & 1 & 1 & -2 & 2
\end{pmatrix}
\rightarrow$$ $$\rightarrow
\begin{pmatrix}
1 & 0 & -1 & 1 & 1 \\
0 & 1 & 1 & -2 & 2
\end{pmatrix}
=
(E|R|\tilde{b});\quad
R =
\begin{pmatrix}
-1 & 1  \\
1 & -2 
\end{pmatrix},\
\tilde{b} =
\begin{pmatrix}
1  \\
2 
\end{pmatrix}$$ Ответ: $$x = 
\begin{pmatrix}
\tilde{b}  \\
0 \\
\vdots \\
0
\end{pmatrix}
+
\begin{pmatrix}
- R  \\
 E
\end{pmatrix}
\begin{pmatrix}
\lambda_{1}  \\
\vdots \\
\lambda_{n-r}
\end{pmatrix}
= 
\begin{pmatrix}
1  \\
2 \\
0 \\
0
\end{pmatrix}
+
\begin{pmatrix}
1 & -1  \\
-1 & 2  \\
1 & 0 \\
0 & 1 
\end{pmatrix}
\begin{pmatrix}
\lambda_{1}  \\
\lambda_{2}
\end{pmatrix}
,\quad \lambda_{1,2} \in \mathbb{R}$$
:::

::: defin
**Def 12**. $$\Phi = 
\begin{pmatrix}
- R \\
E
\end{pmatrix}
- \text{ \textbf{Фундаментальная матрица (ФМ) системы}}$$
:::

::: obs
*Замечание 4*.
$$x -\ решение\ Ax = b \Leftrightarrow b \text{ раскл. по ст-цам } a_{\bullet 1}, \dots, a_{\bullet n} \text{ с к-тами } x_{1}, \dots, x_{n}$$
:::

::: ex
**Ex 8**. Док-ть: строки $\underset{m\times n}{A}$ ЛНЗ
$\Leftrightarrow Ax = b\ совместна\ \forall \underset{m\times 1}{b}$\
Док-во:

-   {A имеет m ЛНЗ строк} $\Rightarrow$ {А имеет m ЛНЗ столбцов}
    $\Rightarrow \{rg(\underbrace{a_{\bullet 1}, \dots, a_{\bullet n}}_{\text{ст-цы высоты m}}) = m = rg\underset{m\times1}{M} \} \Rightarrow \{\forall b \in \underset{m\times1}{M} \text{ лин. выражается ч-з ст-цы } a_{\bullet 1}, \dots, a_{\bullet n}\} \Rightarrow \{Ax = b\ совместна\ \forall b\}$

-   Если в качестве b (поочередно) взять m первых столбцов (они ЛНЗ)
    единичной матрицы, то они раскладываются по столбцам
    $a_{\bullet 1}, \dots, a_{\bullet n} \Rightarrow rg\underbrace{(a_{\bullet 1}, \dots, a_{\bullet n})}_{\text{обр. м-цу с m стр.}} \geqslant m \Rightarrow$
    строки ЛНЗ.

::: flushright
ч.т.д.
:::
:::

::: obs
*Замечание 5*. Что будет если переставлять местами переменные в ст-це
$x = (x_{1}, \dots, x_{n})^{T}$ ?\
$x_{i}\leftrightarrow x_{j},\ т.е.\ \left\{
\begin{aligned}
\tilde{x_{i}} = x_{j} \\
\tilde{x_{j}} = x_{i}
\end{aligned}
\Rightarrow
a_{\bullet 1}x_{1} + \dots + a_{\bullet i}\tilde{x_{j}} + \dots + a_{\bullet j}\tilde{x_{i}} + \dots + a_{\bullet n}x_{n} = b
\right.$ $$Ax = \tilde{A}\tilde{x} = 
(a_{\bullet 1} \cdots a_{\bullet j} \cdots a_{\bullet i} \cdots a_{\bullet n})
\begin{pmatrix}
x_{1} \\
\vdots \\
\tilde{x_{i}} \\
\vdots \\
\tilde{x_{j}} \\
\vdots \\
x_{n}
\end{pmatrix}
= 
\begin{pmatrix}
b_{1} \\
\vdots \\
b_{m}
\end{pmatrix}$$ Вывод: переобозначение переменных привело к перестановке
столбцов основной м-цы системы (если вдуматься в этот факт, то он
становится очевидным)
:::

::: ex
**Ex 9**. $$\begin{pmatrix}
3 & 1 & 1 & 1 & -2 & 2 \\
6 & 1 & 2 & 3 & -4 & 6 \\
10 & 1 & 3 & 6 & -7 & 11
\end{pmatrix}
\rightarrow
\begin{pmatrix}
3 & 1 & 1 & 1 & -2 & 2 \\
3 & 0 & 1 & 2 & -2 & 4 \\
1 & 0 & 0 & 1 & -1 & 1
\end{pmatrix}
\rightarrow
\begin{pmatrix}
2 & 1 & 1 & 0 & -1 & 1 \\
1 & 0 & 1 & 0 & 0 & 2 \\
1 & 0 & 0 & 1 & -1 & 1
\end{pmatrix}$$ $$\rightarrow
\begin{pmatrix}
1 & 1 & 0 & 0 & -1 & -1 \\
1 & 0 & 1 & 0 & 0 & 2 \\
1 & 0 & 0 & 1 & -1 & 1
\end{pmatrix}$$ Переобозначение:
$\tilde{x_{1}} = x_{2},\ \tilde{x_{2}} = x_{3},\ \tilde{x_{3}} = x_{4},\ \tilde{x_{4}} = x_{1},\ \tilde{x_{5}} = x_{5}$
$$\tilde{A} = 
\begin{pmatrix}
1 & 0 & 0 & 1 & -1 & -1 \\
0 & 1 & 0 & 1 & 0 & 2 \\
0 & 0 & 1 & 1 & -1 & 1
\end{pmatrix};\
\tilde{x} =
\begin{pmatrix}
-1 \\
2 \\
1 \\
0 \\
0 
\end{pmatrix}
+
\begin{pmatrix}
1 & -1 \\
1 & 0 \\
1 & -1 \\
1 & 0 \\
0 & 1 
\end{pmatrix}
\begin{pmatrix}
\lambda_{1} \\
\lambda_{2} 
\end{pmatrix}$$ Совершая **обратную замену** (т.е. меняем строки в
$\tilde{x}$) получаем x: $$x = 
\begin{pmatrix}
0 \\
-1 \\
2 \\
1 \\
0
\end{pmatrix}
+
\begin{pmatrix}
-1 & 0 \\
-1 & 1 \\
-1 & 0 \\
-1 & 1 \\
0 & 1 
\end{pmatrix}
\begin{pmatrix}
\lambda_{1} \\
\lambda_{2}
\end{pmatrix}$$
:::

## Двойственность (нахождение СЛАУ по известной ФМ)

**Задача:** по данной ФМ находим *[одну из]{.underline}* СЛАУ.\
**Идея:** Пусть $\Phi = (x_{\bullet 1} \dots  x_{\bullet s})$ - ФМ
системы (А\|0) $\Rightarrow A\Phi = O = \Phi^{T}A^{T}$\
Т.О.: для СЛАУ $(\Phi^{T}|0)\ \forall$ столбец $А^{T}$ - решение.\
**Алгоритм:**\
1) Решаем систему $(\Phi^{T}|0)$\
2) Транспонируем ФМ данной системы.\
3) Полученная матрица - матрица искомой СЛАУ.

# Линейные (= Векторные) пространства

  --------------------------------------------------------------------------------------
  Перед тем как начать изучение данной темы стоит отметить, что те многомерные
  пространства о которых мы будем говорить можно считать некоторыми
  абстракциями, которые определены ТОЛЬКО АКСИОМАМИ (множества, про
  которые говорится в определении, могут быть совершенно разными:
  числа, матрицы, стулья, конфеты, студенты), которые на каждом
  множестве вводятся принудительным образом.
  В дальнейшем вы встретите много конкретных примеров пространств со
  своими особенностями (метрические пространства, топологические, гильбертовы и т.д.),
  а на данном этапе нужно просто привыкнуть к \"n-мерности\"
  на примере линейных пространств.
  Не нужно себе представлять пространство размерности большей чем 3,
  нужно лишь знать и уметь применять свойства того пространства в котором
  вы решаете задачу.
  Также, для того чтобы легче решить какую либо задачу в n-мерном
  пространстве иногда достаточно решить эту задачу в 2 или 3 мерном
  пространстве и понять геометрический смысл.
  --------------------------------------------------------------------------------------

::: defin
**Def 13**. Множество $\mathscr{L}$ называется **линейным
пространством**, если на нем введены операции сложения и умножения на
число, подчиняющиеся аксиомам:\
1)
$\forall a,b,c \in \mathscr{L} \hookrightarrow (a + b) + c = a + (b + c)$\
2)
$\exists 0 \in \mathscr{L} : \forall x \in \mathscr{L} \hookrightarrow x + 0 = 0 + x = x\quad (0 \text{ - не число, а элемент } \mathscr{L})$\
3)
$\forall a \in \mathscr{L}\ \exists x \in \mathscr{L} : x + a = a + x = 0$\
4) $\forall a, b \in \mathscr{L} \hookrightarrow a + b = b + a$\
5)
$\forall a,b \in \mathscr{L}\ \forall \lambda \in \mathbb{R} \hookrightarrow \lambda(a + b) = \lambda a + \lambda b$\
6)
$\forall a \in \mathscr{L}\ \forall \lambda, \mu \in \mathbb{R} \hookrightarrow (\lambda + \mu)a = \lambda a + \mu a$\
7)
$\forall a \in \mathscr{L} \hookrightarrow 1\times a = a\ (1 \in \mathbb{R})$\
8)
$\forall a \in \mathscr{L}\ \forall \lambda, \mu \in \mathbb{R} \hookrightarrow (\lambda \mu)a = \lambda(\mu a)$
:::

::: obs
*Замечание 6*. $\mathscr{L}$ также называют векторным пространством, а
его элементы - векторами.
:::

::: obs
*Замечание 7*. если $\lambda \in \mathbb{R}$ то: \"ЛП над полем
действительных чисел\"\
если $\lambda \in \mathbb{C}$ то: \"ЛП над полем комплексных чисел\"
:::

**Примеры линейных пространств:**\
1) мн-во векторов геометрического 3-мерного пространства\
2) мн-во векторов, параллельных данной плоскости\
3) мн-во матриц размера $m\times n$\
4) {0} - нулевое пр-во\
5) $P_{n}$ - мн-во многочленов степени не выше n.

::: defin
**Def 14**. $\mathscr{L}$ - ЛП. Непустое подмножество
$\mathscr{L^{'}} \subset \mathscr{L}$ называется **линейным
подпространством**, если:\
1)
$\forall a,b \in \mathscr{L^{'}} \hookrightarrow a + b \in \mathscr{L^{'}}$\
2)
$\forall a \in \mathscr{L^{'}},\ \forall \lambda \in \mathbb{R} \hookrightarrow \lambda a \in \mathscr{L^{'}}$
:::

::: obs
*Замечание 8*. Часто математики говорят, что подмножество является
подпространством если сложение и умножение на число \"не выводит\" из
этого подпространства (т.е. результат суммы и умножения тоже является
элементом подпространства).
:::

::: obs
*Замечание 9*. Подпространство линейного пространства тоже является
линейным пространством.
:::

::: theorem
**Th 10**. *Пусть
$\mathscr{L^{'}}, \mathscr{L^{''}} \subset \mathscr{L}$ -
подпространства. Тогда $\mathscr{L^{'}}\cap \mathscr{L^{''}}$ - тоже
подпространство $\mathscr{L}$.*
:::

::: obs
*Замечание 10*. Даже если
$\mathscr{L^{'}}, \mathscr{L^{''}} \in \mathscr{L}$ подпространства,
$\mathscr{L^{'}} \cup \mathscr{L^{''}}$ - не всегла является
подпространством.
:::

::: theorem
**Th 11**. *Если $\mathscr{L^{'}} \subset \mathscr{L}$ -
подпространство, и $a_{1}, \dots. a_{k} \in \mathscr{L^{'}}$, то
$\forall$ их ЛК
$\lambda_{1}a_{1} + \dots + \lambda_{k}a_{k} \in \mathscr{L^{'}}$*
:::

::: defin
**Def 15**. **Линейная оболочка (ЛО)** векторов
$a_{1}, \dots. a_{k} \in \mathscr{L}$ это множество:\
$\mathscr{L}(a_{1}, \dots. a_{k}) = \left\{\sum_{i=1}^{k}\lambda_{i}a_{i}\ |\ \lambda_{i}\in \mathbb{R}\right\}$

Другими словами, линейная оболочка, образованная на данных векторах -
это множество всех линейных комбинаций этих векторов (например ЛО двух
неколлинеарных векторов в трехмерном пространстве - плоскость).
:::

::: defin
**Def 16**.
$\forall a_{1}, \dots. a_{k} \in \mathscr{L} \hookrightarrow \mathscr{L}(a_{1}, \dots. a_{k})$ -
подпространство $\mathscr{L}$.
:::

**Примеры подпространств:**\
1) Линейная оболочка любых $m \ (n \geqslant m)$ столбцов единичной
матрицы размера n - подпространство в пространстве столбцов высоты n.\
2) Множество решений однородной СЛАУ - подпространство в пространстве
столбцов высоты n. Его можно задать как
$\mathscr{L}(\underbrace{x_{\bullet 1}, \dots, x_{\bullet (n-r)}}_{\text{ФСР}})$

::: obs
*Замечание 11*. Для того чтобы проверить - является ли подмножество
линейным подпространством нужно проверить - \"не выводит, ли\"  сложение
и умножение на число из этого подмножества.
:::

## Линейная зависимость. Ранг. Размерность.

::: defin
**Def 17**. $a_{1}, \dots , a_{k}$ - **Линейно зависимы (ЛЗ)**, если
существует их не тривиальная ЛК равная $0 \in \mathscr{L}$. В противном
случае такой набор - **линейно независимый (ЛНЗ)**.
:::

**Напоминание:**\
1) набор векторов ЛЗ если среди них найдется один, выражающийся через
все остальные.\
2) добавление к ЛЗ набору новых векторов не изменит их линейную
зависимость.\
3) любая подсистема ЛНЗ набора векторов - тоже ЛНЗ.\
4) пусть $b \in \mathscr{L}(a_{1}, \dots , a_{k})$\
5) коэффициенты $\lambda_{1}, \dots, \lambda_{k}$ в разложении
$b = \lambda_{1}a_{1} + \dots + \lambda_{k}a_{k}$ определены однозначно
$\Leftrightarrow a_{1}, \dots , a_{k}$ ЛНЗ.

::: defin
**Def 18**. Пусть $A \subset \mathscr{L}$.\
**Рангом пространства** $A$ называется число $rg\ A = r$, если в $А$
существует r ЛНЗ векторов, а любой набор из r+1 вектора ЛЗ.
:::

::: defin
**Def 19**. **Размерность пространства**
:::

::: obs
*Замечание 12*. Если $dim\ \mathscr{L}$ - конечное целое неотрицательное
число, то $\mathscr{L}$ - конечномерное пространство.
:::

::: obs
*Замечание 13*. Таким образом, из определения сразу же следует, что если
нам захотелось найти размерность какого либо пространства, то необходимо
всего навсего найти максимальное количество ЛНЗ элементов этого
пространства.

Найдите, например, размерность пространства симметричных и
антисимметричных матриц.
:::

::: ex
**Ex 10**. Найти размерность пространства матриц
$\underset{m\times n}{M}$\
Рассмотрим (важный!) вид матриц
$E_{ij}\ (i = 1,\dots,n;\ j = 1,\dots,m)$ у которых на всех позициях
стоят нули кроме ij-го. Всего таких матриц может быть $m\cdot n$ штук.
Они ЛНЗ и определенная их ЛК может дать нам любую матрицу размера
$m\times n$, следовательно - $dim\underset{m\times n}{M} = m\cdot n$
:::

::: theorem
**Th 12**. *Пусть $A \subset \mathscr{L}$ - набор векторов из ЛП,
тогда:\
$rg\ A = rg\ \mathscr{L}(A) = dim\ \mathscr{L}(A)$*
:::

::: defin
**Def 20**. Упорядоченный набор $e_{1},\dots, e_{n} \in \mathscr{L}$ -
**базис пространства** $\mathscr{L}$, если:\
1) $e_{1},\dots, e_{n}$ - ЛНЗ.\
2) $\mathscr{L}(e_{1},\dots, e_{n}) = \mathscr{L}$ (полнота)
:::

::: oboz
*Обозначение 2*. $\textbf{e} = (e_{1} \dots e_{n})$ - строка базисных
векторов
:::

::: defin
**Def 21**. $$\begin{aligned}
x \in \mathscr{L} \\
e_{1}, \dots, e_{n} \text{ - базис } \mathscr{L} \\
x = x_{1}e_{1} + \dots + x_{n}e_{n} 
\end{aligned}\,
\vline 
\Rightarrow 
x_{1}, \dots, x_{n} \text{ - \textbf{координаты вектора} } x \text{ в базисе } \textbf{e}$$
:::

::: obs
*Замечание 14*. Любому вектору пространства в данном базисе сопоставлен
координатный столбец: $$\forall x \in \mathscr{L} \leftrightarrow \xi = 
\begin{pmatrix}
x_{1} \\
\vdots \\
x_{n}
\end{pmatrix}
\in \underset{n\times 1}{M}$$
:::

::: ex
**Ex 11**. Является ли множество $\tilde{M}$ столцов с первой
компонентой равной нулю подпространством $\underset{n \times 1}{M}$?
Если да, то $dim\ \tilde{M} = ?$\
$$\forall x,y \in \tilde{M}:\, 
x = 
\begin{pmatrix}
0 \\
x_{1} \\
\vdots \\
x_{n}
\end{pmatrix} ;\,
y = 
\begin{pmatrix}
0 \\
y_{1} \\
\vdots \\
y_{n}
\end{pmatrix}\,
\Rightarrow
x + y =
\begin{pmatrix}
0 \\
x_{1} + y_{1} \\
\vdots \\
x_{n} + y_{n} 
\end{pmatrix}
\in \tilde{M}$$
$$\forall \lambda \in \mathbb{R} \hookrightarrow \lambda x = 
\begin{pmatrix}
0 \\
\lambda x_{1} \\
\vdots \\
\lambda x_{n}
\end{pmatrix}
\in \tilde{M}$$ Вывод: $\tilde{M}$ - подпространство.\
Рассмотрим столбцы: $$m = 
\underbrace{\begin{pmatrix}
    0 \\
    1 \\
    0 \\
    \vdots \\
    0
    \end{pmatrix},\,
    \begin{pmatrix}
    0 \\
    0 \\
    1 \\
    \vdots \\
    0
    \end{pmatrix}, \dots,\,
    \begin{pmatrix}
    0 \\
    \vdots \\
    0 \\
    0 \\
    1
    \end{pmatrix}}_{\text{n-1 столбец}}
\qquad
\parbox{8cm}{$\mathscr{L}(m) = \tilde{M} \Rightarrow$ m - базис $\Rightarrow dim\ \tilde{M} = n - 1$}$$
:::

::: ex
**Ex 12**. Множество столбцов с какой либо фиксированной компонентой
(например $x_{1} = 1$) не является подпространством пространства
столбцов высоты n, т.к. при умножении на $\lambda \ne 1$ мы получим
столбец, не принадлежащий данному множеству.
:::

::: ex
**Ex 13**. Является ли $\underset{n\times n}{M}^{+}$ - мн-во
симметричных матриц ($A = A^{T}$) подпространством в
$\underset{n\times n}{M}$?\
а)
$A,B \in \underset{n\times n}{M}^{+} \Rightarrow (A + B)^{T} = A^{T} + B^{T} = A + B \Rightarrow A + B \in \underset{n\times n}{M}^{+}$\
б)
$A \in \underset{n\times n}{M}^{+},\ \lambda \in \mathbb{R} \Rightarrow (\lambda A)^{T} = \lambda A^{T} = \lambda A \in \underset{n\times n}{M}^{+}$\
Вывод: $\underset{n\times n}{M}^{+}$ - подпростраство в
$\underset{n\times n}{M}$.

Найдем базис этого подпространство и его размерность.\
Заметим, что если мы определим значение элемента $a_{ij}\, (i \ne j)$,
то мы автоматически определим значение элемента $a_{ji}$, который будет
равен $a_{ij}$. Таким образом, у нас есть $\frac{n(n-1)}{2}$ элементов,
которые мы можем выбрать.

Также мы можем определить какими либо значениями диагональные элементы,
которых n штук.

Таким образом, мы можем выбрать базис из двух групп симметричных
матриц:\
1) матрицы вида $\tilde{E_{ij}}\, (i \ne j)$, у которых на всех позициях
стоят нули кроме ij-той и ji-той, на которых стоят единицы (таких матриц
$\frac{n(n-1)}{2}$ штук)\
2) матрицы вида $E_{ii}$ у которых на всех позициях нули кроме ii-той
(таких матриц n штук).\
Итого у нас получается $\frac{n(n+1)}{2}$ штук ЛНЗ матриц. Линейная
оболочка таких матриц в точности равна множеству симметричных матриц.\
Следовательно: $dim\underset{n\times n}{M}^{+} = \dfrac{n(n + 1)}{2}$
:::

::: ex
**Ex 14**. Найти размерность и базис в:\
$$\mathscr{L} =
\mathscr{L}\left(
\begin{pmatrix}
-3 \\
2 \\
0
\end{pmatrix},
\begin{pmatrix}
-3 \\
6 \\
15
\end{pmatrix},
\begin{pmatrix}
0 \\
-4 \\
-15
\end{pmatrix}
\right)$$ Для того чтобы найти базис необходимо выделить максимальный
набор ЛНЗ в-в среди тех, которые образуют линейную оболочку. Причем
линейная оболочка, построенная на этом ЛНЗ наборе будет равна исходной:
$$\mathscr{L}\left(
\begin{pmatrix}
-3 \\
2 \\
0
\end{pmatrix},
\begin{pmatrix}
-3 \\
6 \\
15
\end{pmatrix},
\begin{pmatrix}
0 \\
-4 \\
-15
\end{pmatrix}
\right)  
=
\mathscr{L}
\underbrace{\left( \begin{pmatrix}
    -3 \\
    2 \\
    0
    \end{pmatrix},
    \begin{pmatrix}
    0 \\
    -4 \\
    -15
    \end{pmatrix}
    \right)}_{\text{Базис}} 
\Rightarrow 
dim\mathscr{L} = 2.$$
:::

## Замена базиса в ЛП.

Пусть: $$\begin{aligned}
&\textbf{e} = (e_{1}, \dots, e_{n}) \text{ - "старый"\ базис } \mathscr{L}\\
&\textbf{e}^{'} = (e_{1}^{'}, \dots, e_{n}^{'}) \text{ - "новый"\ базис } \mathscr{L}
\end{aligned}$$

::: defin
**Def 22**. S - **матрица перехода** от **e** к $\textbf{e}^{'}$, если:
$$\fbox{$\textbf{e}^{'} = \textbf{e}S$}$$
:::

::: obs
*Замечание 15*.
$e_{1}^{'} = e_{1}s_{11} + e_{2}s_{21} + \dots + e_{n}s_{n1} = es_{\bullet 1}$
$$S = 
\begin{pmatrix}
s_{11} & \cdots & s_{1n} \\
\vdots & & \vdots \\
s_{n1} & \cdots & s_{nn}
\end{pmatrix}
=
\begin{pmatrix}
s_{\bullet 1} & \cdots & s_{\bullet n} 
\end{pmatrix}$$
:::

::: theorem
**Th 13**. *$x \in \mathscr{L}$ $$\begin{aligned}
&x \leftrightarrow \xi = 
\begin{pmatrix}
x_{1} \\
\vdots \\
x_{n}
\end{pmatrix} 
\text{ в базисе }
\textbf{e} \\
&x \leftrightarrow \xi^{'} = 
\begin{pmatrix}
x_{1}^{'} \\
\vdots \\
x_{n}^{'}
\end{pmatrix} 
\text{ в базисе }
\textbf{e}^{'} \\
\end{aligned}\,
\vline
\Rightarrow
x = \textbf{e}\xi = \textbf{e}^{'}\xi^{'} = \textbf{e}S\xi^{'}
\Rightarrow 
\fbox{$\xi = S\xi^{'}$}$$*
:::

::: theorem
**Th 14**. *$$\begin{aligned}
&\textbf{e} \stackrel{S}{\rightarrow} \textbf{e}^{'}\\
&\textbf{e}^{'} \stackrel{R}{\rightarrow} \textbf{e}^{''}
\end{aligned}\,
\vline
\Rightarrow
\textbf{e}^{''} = \textbf{e}^{'}R = \textbf{e}SR \Rightarrow
\fbox{$\textbf{e} \stackrel{SR}{\rightarrow} \textbf{e}^{''}$}$$*
:::

::: theorem
**Th 15**. *Матрица перехода всегда не вырожденная, и если
$\textbf{e} \stackrel{S}{\rightarrow} \textbf{e}^{'}$, то
$\textbf{e}^{'} \stackrel{S^{-1}}{\rightarrow} \textbf{e}$*
:::

## Сумма подпространств.

::: defin
**Def 23**. Пусть
$\underbrace{A_{1}, \dots, A_{k}}_{\text{подмножества}} \subset \mathscr{L}$.
Их **суммой** (по Минковскому) называется:
$$A_{1} + \dots + A_{k} \stackrel{def}{=} \{a_{1}+ \dots + a_{k}\ |\ a_{i} \in A_{i},\ i = 1,\dots,k\}$$
:::

::: ex
**Ex 15**. $A, B$ - прямые, $P$ - плоскость, в которой лежат $A, B$.
$A\cup B$ - не подпространство, а $A + B = P$ - подпространство.
:::

::: obs
*Замечание 16*. Если
$U_{1} = \mathscr{L}(A_{1}), \dots, U_{k} = \mathscr{L}(A_{k}) \Rightarrow U = U_{1} + \dots + U_{k} = \mathscr{L}(A_{1}\cup \dots \cup A_{k})\, (U - \text{подпространство})$
:::

::: theorem
**Th 16**. *$$\begin{aligned}
dim\ U_{1} = n_{1} \\
\dots \quad \dots \\
dim\ U_{k} = n_{k}
\end{aligned}\,
\vline
\Rightarrow
n_{1} + \dots + n_{k} \geqslant dim\ (U_{1} + \dots + U_{k})$$*
:::

::: defin
**Def 24**.
$U = \underbrace{U_{1} + \dots + U_{k}}_{\text{подпр-ва } \mathscr{L}}$ -
**прямая сумма**, если\
$\forall x \in U \hookrightarrow x = x_{1} + \dots + x_{k}\, (x_{i} \in U_{i})$
и такое разложение единственно.\
В этом случае пишут: $U = U_{1}\oplus \dots \oplus U_{k}$
:::

::: defin
**Def 25**. Пусть
$U = \underbrace{U_{1} + \dots + U_{k}}_{\text{подпр-ва}}$\
$\tilde{U_{i}} = U_{1} + \dots + U_{i-1} + \dots + U_{k}$ (**сумма всех
подпространств кроме i-го**)
:::

::: theorem
**Th 17** (**Критерий прямой суммы №1**). *Пусть
$U = \underbrace{U_{1} + \dots + U_{k}}_{\text{подпр-ва}}$
$$U = U_{1} \oplus \dots \oplus U_{k} \Leftrightarrow U_{i}\cap \tilde{U_{i}} = 0 \in \mathscr{L}\quad (i = 1, \dots, k)$$*
:::

::: theorem
**Th 18** (**Критерий прямой суммы №2**). *Пусть
$U = \underbrace{U_{1} + \dots + U_{k}}_{\text{подпр-ва}}$,\
$dim\ U_{i} = n_{i};\, \textbf{e}^{(i)}$ - базис $U_{i}$. Тогда:
$$\{U \text{ - прямая сумма } \}\Leftrightarrow \{\textbf{e}^{(1)}\cup \dots \cup \textbf{e}^{(k)} \text{ - базис в U } \}\Leftrightarrow \{dim\ U = n_{1} + \dots + n_{k}\}$$*
:::

::: obs
*Замечание 17*.
$U = \mathscr{L}(\textbf{e}^{(1)}\cup \dots \cup \textbf{e}^{(k)})$ -
выполняется всегда.\
$\textbf{e}^{(1)}\cup \dots \cup \textbf{e}^{(k)}$ - остается ЛНЗ только
в случае прямой суммы подпространств.
:::

::: defin
**Def 26**. Пусть ЛП
$\mathscr{L} = \mathscr{L}^{'}\oplus \mathscr{L}^{''}$. Тогда
$\mathscr{L}^{''}$ - **прямое дополнение** $\mathscr{L}^{'}$ в
$\mathscr{L}$.
:::

::: obs
*Замечание 18*.
$\mathscr{L}^{''} \ne \mathscr{L}\backslash \mathscr{L}^{'}$ (не
путать!)
:::

::: defin
**Def 27**.
$\mathscr{L} = \mathscr{L}^{'}\oplus \mathscr{L}^{''},\ x \in \mathscr{L},\, x^{'} \in \mathscr{L}^{'},\, x^{''} \in \mathscr{L}^{''}.$\
$x = x^{'} + x^{''}$\
$x^{'}$ - проекция $x$ на $\mathscr{L}^{'}$ вдоль $\mathscr{L}^{''}$.
:::

::: ex
**Ex 16**.
$\mathscr{F} = \{f(x)\ |\ f:\mathbb{R} \rightarrow \mathbb{R}\}$ - ЛП
всех функций, определенных на $\mathbb{R}$\
$\mathscr{F}^{+}\subset \mathscr{F}$ - подпространство четных функций\
$\mathscr{F}^{-}\subset \mathscr{F}$ - подпространство нечетных функций\
$\mathscr{F}^{+}\cap \mathscr{F}^{-} = \{0\} \Rightarrow \mathscr{F}^{+} + \mathscr{F}^{-} = \mathscr{F}^{+} \oplus \mathscr{F}^{-}$\
$\forall f(x) \in \mathscr{F} \hookrightarrow \underbrace{\dfrac{f(x)+f(-x)}{2}}_{\in \mathscr{F}^{+}} + \underbrace{\dfrac{f(x)-f(-x)}{2}}_{\in \mathscr{F}^{-}} \Rightarrow$\
Аналогичным образом получается:\
$\left(\underset{n\times n}{M}^{-} \text{ - пространство антисимметричных матриц} \right)$
:::

::: ex
**Ex 17**. Найти проекцию $x = \begin{pmatrix}
2 \\
0 \\
-1
\end{pmatrix}
\in \mathscr{L} = \underset{3\times 1}{M}$ на подпространство
$\mathscr{L}^{'} = \mathscr{L}\left( 
\begin{pmatrix}
4 \\
3 \\
1
\end{pmatrix},
\begin{pmatrix}
1 \\
2 \\
3 
\end{pmatrix},
\begin{pmatrix}
3 \\
1 \\
-2
\end{pmatrix}
\right)$ вдоль $\mathscr{L}^{'} = \mathscr{L}\left( 
\begin{pmatrix}
1 \\
1 \\
1
\end{pmatrix} \right)$\
Решение: $$\mathscr{L}^{'} = \mathscr{L}\left( 
\begin{pmatrix}
    4 \\
    3 \\
    1
\end{pmatrix},
\begin{pmatrix}
    1 \\
    2 \\
    3 
\end{pmatrix},
\begin{pmatrix}
    3 \\
    1 \\
    -2
\end{pmatrix}
\right) 
=
\mathscr{L}^{'} = \mathscr{L}\left( 
\begin{pmatrix}
3 \\
1 \\
-2
\end{pmatrix},
\underbrace{\begin{pmatrix}
    1 \\
    2 \\
    3 
    \end{pmatrix},
    \begin{pmatrix}
    3 \\
    1 \\
    -2
    \end{pmatrix}}_{\text{ЛНЗ - базис } \mathscr{L}^{'}}
\right) 
\Rightarrow 
dim\mathscr{L}^{'} = 2$$
:::

::: theorem
**Th 19** (**формула Грассмана**).
*$\mathscr{L}_{1},\ \mathscr{L}_{2} \subset \mathscr{L}$
$$\fbox{$ dim(\mathscr{L}_{1} + \mathscr{L}_{2}) + dim(\mathscr{L}_{1} \cup \mathscr{L}_{2}) = dim\ \mathscr{L}_{1} + dim\ \mathscr{L}_{2}$}$$*
:::

::: ev
*Доказательство 6*. Пусть
$W \subset \mathscr{L}_2:\ (\mathscr{L}_1 \cap \mathscr{L}_2)\oplus W = \mathscr{L}_2$
$$\Rightarrow \mathscr{L}_1 + \mathscr{L}_2 = \mathscr{L}_1 + ((\mathscr{L}_1 \cap \mathscr{L}_2)+ W) = (\mathscr{L}_1 + (\mathscr{L}_1 \cap \mathscr{L}_2)) + W = \mathscr{L}_1 + W$$
Кроме того, т.к.
$(\mathscr{L}_1 \cap \mathscr{L}_2)\oplus W = \mathscr{L}_2$, то
$$W + \mathscr{L}_1 = W \oplus \mathscr{L}_1 \Rightarrow \text{dim }W = \text{dim }\mathscr{L}_2 - \text{dim }(\mathscr{L}_1\cap \mathscr{L}_2) = \text{dim }(\mathscr{L}_1 + \mathscr{L}_2) - \text{dim }\mathscr{L}_1$$

::: flushright
[ч.т.д.]{.underline}
:::
:::

# Линейные отображения и преобразования.

::: defin
**Def 28**. **Отображение** из множества А в множество В - это правило
по которому каждому элементу из А сопоставлен элемент или множество
элементов из В.
:::

::: defin
**Def 29**. Если
$\varphi: \mathscr{L} \rightarrow \tilde{\mathscr{L}}:$\
1)
$\forall x,y \in \mathscr{L} \hookrightarrow \varphi(x + y) = \varphi(x) + \varphi(y)$\
2)
$\forall x \in \mathscr{L},\, \forall \lambda \in \mathbb{R(C)} \hookrightarrow \varphi(\lambda x) = \lambda \varphi(x)$\
то $\varphi$ - **линейное отображение** из пространства $\mathscr{L}$ в
$\tilde{\mathscr{L}}$.
:::

::: defin
**Def 30**. Если $\mathscr{L} = \tilde{\mathscr{L}}$, то линейное
отображение называется **линейным преобразованием**.
:::

::: defin
**Def 31**. Пусть $A \subset \mathscr{L}$ - набор векторов из
$\mathscr{L}$.
$$\fbox{$ \varphi(A) = \{\varphi(x)\,|\, x \in A\}$} \text{ - \textbf{образ} } A$$
:::

::: defin
**Def 32**.
$$\fbox{$ Im\ \varphi = \varphi(\mathscr{L}) = \{\varphi(x)\, |\, x \in \mathscr{L}\}$} \text{ - \textbf{образ отображения} } \varphi.$$
(т.е. это все векторы \"конечного\"  пространства (включая 0), которые
имеют прообраз в \"исходном\" пространстве)
:::

::: defin
**Def 33**.
$$\fbox{$Ker\ \varphi = \{x \in \mathscr{L}\, | \, \varphi(x) = 0\}$} \text{ - \textbf{ядро отображения} } \varphi$$
(т.е. это те векторы из \"исходного\"  пространства, которые при
действии на них отображения переходят в 0)
:::

::: obs
*Замечание 19*. Для лучшего понимания понятий образ и ядро полезно
представлять себе вот такую картинку:

![image](limage1.jpg)

где $\mathscr{L}_1$ - \"исходное\" пространство, $\mathscr{L}_2$ -
\"конечное\" пространство.
:::

::: obs
*Замечание 20*. $$\begin{aligned}
&\varphi: \mathscr{L} \rightarrow \tilde{\mathscr{L}}  \text{ - нулевое отображение} \\
&\forall x \in \mathscr{L} \hookrightarrow \varphi(x) = 0 \in \tilde{\mathscr{L}}\\
\end{aligned}\,
\vline
\Rightarrow
\begin{aligned}
Im\ \varphi = 0\\
Ker\ \varphi = \mathscr{L}
\end{aligned}$$
:::

**Свойства линейного отображения:**

1.  $\varphi(0) = 0$

2.  $\varphi\left( \sum\limits_{i=1}^{k}\lambda_{i}x_{i}\right)  = \sum\limits_{i=1}^{k}\lambda_{i} \varphi(x_{i})$

3.  Если $\mathscr{L}^{'} \subset \mathscr{L}$ - подпространство, то:
    $\varphi(\mathscr{L}^{'})$ - подпространство в
    $\tilde{\mathscr{L}}$.

4.  $Im\ \varphi$ - подпространство.

5.  $Ker\ \varphi$ - подпространство.

6.  ЛЗ вектора переходят в ЛЗ.

7.  $rg\ A \geqslant rg\ \varphi(A)$

8.  $dim\ \mathscr{L}^{'} \geqslant dim\ \varphi(\mathscr{L}^{'})$

::: defin
**Def 34**.
$$\fbox{$rg\ \varphi \stackrel{def}{=} dim\ Im\ \varphi$} \text{ - \textbf{ранг отображения}.}$$
:::

::: defin
**Def 35**. $\varphi$ - **инъекция**, если
$x \ne y \Rightarrow \varphi(x) \ne \varphi(y)$\
(разные вектора переходят в разные)
:::

::: obs
*Замечание 21*. $\varphi$ - инъективное $\Rightarrow Ker\ \varphi = 0$
:::

::: obs
*Замечание 22*. $\varphi$ - инъективное $\Rightarrow$ ЛНЗ векторы
переходят в ЛНЗ.
:::

::: defin
**Def 36**. $\varphi$ - **сюръекция**, если
$Im\ \varphi = \tilde{\mathscr{L}}$
:::

::: theorem
**Th 20** (**Критерий сюръективности**).
*$$\fbox{$\varphi$ - сюръекция $\Leftrightarrow dim\ Im\ \varphi = m$}$$*
:::

::: ex
**Ex 18** (23.8(4)). Даны
$\vec{a},\ \vec{n} \ne \vec{0}:\, (\vec{a},\vec{n}) \ne 0$\
$\mathscr{L}_{1}$ - прямая, параллельная $\vec{a}$\
$\mathscr{L}_{2}$ - плоскость, перпендикулярная $\vec{n}$\
$\varphi$ - проекция на $\mathscr{L}_{1}$ вдоль $\mathscr{L}_{2}$\
Найти формулу для $\varphi$, проверить его линейность, найти
$Ker\ \varphi,\ Im\ \varphi,\ rg\ \varphi$.

*Решение:*

-   $\mathscr{L} = \mathscr{L}_{1} \oplus \mathscr{L}_{2}$\
    Выберем базис в
    $\mathscr{L}:\ \underbrace{\vec{a}}_{\in \mathscr{L}_{1}},\ \underbrace{[\vec{a},\vec{n}],\ [\vec{a},[\vec{a},\vec{n}]]}_{\in \mathscr{L}_{2}}$\
    Любой вектор из $\mathscr{L}$ можно разложить по базису:\
    $\vec{x} = \underbrace{\alpha \vec{a}}_{\text{пр-я на }\mathscr{L}_{1} \text{ вдоль }\mathscr{L}_{2}} + \beta[\vec{a},\vec{n}] + \gamma[\vec{a},[\vec{a},\vec{n}]]\ | \cdot \vec{n}\ $
    (скалярно)\
    $(\vec{x}, \vec{n}) = \alpha(\vec{a}, \vec{n}) \Rightarrow \alpha = \dfrac{(\vec{x}, \vec{n})}{(\vec{a}, \vec{n})} \Rightarrow$
    Ответ:
    $\varphi(\vec{x}) = \dfrac{(\vec{x}, \vec{n})}{(\vec{a}, \vec{n})} \vec{a}$\

-   Линейность следует из линейности скалярного произведения:\
    $$\forall \vec{x},\vec{y} \in \mathscr{L} \hookrightarrow \varphi(\vec{x} + \vec{y}) = \dfrac{(\vec{x} + \vec{y}, \vec{n})}{(\vec{a}, \vec{n})} \vec{a} = 
    \dfrac{(\vec{x}, \vec{n})}{(\vec{a}, \vec{n})}\vec{a} + \dfrac{(\vec{y}, \vec{n})}{(\vec{a}, \vec{n})}\vec{a} = \varphi(\vec{x}) + \varphi(\vec{y})$$
    $$\forall \vec{x} \in \mathscr{L},\ \forall \lambda \in \mathbb{R} \hookrightarrow \varphi(\lambda \vec{x}) = \lambda \varphi(\vec{x})$$

-   $Ker\ \varphi = \{\vec{x}\ |\ \underbrace{(\vec{x},\vec{n}) = 0}_{\text{Ур-е пл-ти } \perp \vec{n}}\} = \mathscr{L}_{2} \qquad Im\ \varphi = \{\lambda \vec{a}\ |\ \lambda \in \mathbb{R}\} = \mathscr{L}_{1}$\
    $$rg\ \varphi = dim\ Im\ \varphi = 1$$
:::

## Координатная запись отображений

Очень важным является то, что каждому линейному отображению в некоторых
базисах (в исходном и конечном пространствах) сопоставлена некоторая
матрица размера $m\times n$, где количество строк m - это размерность
пространства В КОТОРОЕ отображают, а количество столбцов n - это
размерность пространства ОТКУДА отображают.

Столбцы этой матрицы имеют важный смысл, который определяет действие
отображения на каждый базисный вектор исходного пространства.

Интуитивно понятно, что если мы знаем действие отображения на каждый
базисный вектор данного пространства, то мы также знаем его действие на
любой вектор из этого пространства.

Покажем это, отыскав связь между координатным столбцом любого вектора из
исходного пространства с координатным столбцом образа этого вектора в
конечном пространстве, зная как действует отображение на базисные
вектора (координатные столбцы в конечном пространстве).

  ------------------------------------------------------------------------------------------------------------- --------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------
                        $\underline{\mathscr{L}^{n},\ \textbf{e} = (e_{1} \dots e_{n})}$                                                                                  $\underline{\tilde{\mathscr{L}^{m}},
                                                                                                                                                                          \ \textbf{f} = (f_{1} \dots f_{m})}$
                                    $x = \xi^{1}e_{1} + \dots + \xi^{n}e_{n}$                                                                                             $\varphi(x) = \xi^{1}\varphi(e_{1}) + \dots + \xi^{n}\varphi(e_{n})$
                                                                                                                                                                          $\varphi(e_{i}) = \alpha_{i}^{1}f_{1} + \dots + \alpha_{i}^{m}f_{m}\ (i = 1,\dots,n)$
                                                                                                                                                                          $\varphi(x) = \eta^{1}f_{1} + \dots + \eta^{m}f_{m}$
                                                                                                                                                                          
                                                                                                                                                                          
   $\sum\limits_{p=1}^{m}\eta^{p}f_{p} = \sum\limits_{i=1}^{n}\xi^{i}\sum\limits_{p=1}^{m}\alpha_{i}^{p}f_{p}$                             $=$                            $\sum\limits_{i=1}^{n}\sum\limits_{p=1}^{m}\alpha_{i}^{p}\xi^{i}f_{p} = \sum\limits_{p=1}^{m}f_{p}\sum\limits_{i=1}^{n}\alpha_{i}^{p}\xi^{i}$
                                                                                                                                      $\Downarrow$                        
                                                                                                                 $\eta^{p} = \sum\limits_{i=1}^{n}\alpha_{i}^{p}\xi^{i}$  
  ------------------------------------------------------------------------------------------------------------- --------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------

$$\begin{pmatrix}
\eta^{1} \\
\vdots \\
\eta^{m} 
\end{pmatrix}
=
\begin{pmatrix}
\alpha_{1}^{1} & \cdots & \alpha_{n}^{1} \\
\vdots & & \vdots \\
\alpha_{1}^{m}& \cdots & \alpha_{n}^{m}
\end{pmatrix}
\begin{pmatrix}
\xi^{1} \\
\vdots \\
\xi^{n}
\end{pmatrix}
\Rightarrow 
\fbox{$\boldsymbol{\eta} = \textbf{A}\boldsymbol{\xi}$}$$

::: defin
**Def 37**. **Матрицей ЛО**
$\varphi: \mathscr{L}^{n} \rightarrow \tilde{\mathscr{L}^{m}}$ в базисах
**e, f** называется: $$\underset{m\times n}{A} = 
\begin{pmatrix}
\alpha_{1}^{1} & \cdots & \alpha_{n}^{1} \\
\vdots & & \vdots \\
\alpha_{1}^{m}& \cdots & \alpha_{n}^{m}
\end{pmatrix}
=
\begin{pmatrix}
a_{\bullet 1} \cdots a_{\bullet n} \\
\end{pmatrix}
\quad (обозначение:\ \varphi \underset{e,f}{\rightarrow} A)$$
:::

::: obs
*Замечание 23*.
$$\boldsymbol{\eta} = \textbf{A}\boldsymbol{\xi} \Rightarrow
\begin{aligned}
Ker\ \varphi = \{x \leftrightarrow \boldsymbol{\xi}\ |\ \textbf{A}\boldsymbol{\xi} = 0\}\\
Im\ \varphi = \mathscr{L}(a_{\bullet 1}, \dots, a_{\bullet n})
\end{aligned}$$ (если в исходном пространстве базис
$e_{1},\dots, e_{n}$, то
$Im\ \varphi = \mathscr{L}(\varphi(e_{1}),\dots, \varphi(e_{n})$))
:::

::: theorem
**Th 21**. *Ранг матрицы линейного отображения равен рангу этого
отображения: $$rg\ \varphi = rg\ A$$*
:::

::: theorem
**Th 22**. *$$\fbox{$dim\ Im\ \varphi + dim\ Ker\ \varphi = n$}$$*
:::

::: obs
*Замечание 24*.
$$\fbox{$ Ker\ \varphi = 0 \Leftrightarrow dim\ Im\ \varphi = n $}$$
:::

::: obs
*Замечание 25*. О сюръективности или инъективности ЛО также можно
судить, зная его матрицу:

-   столбцы м-цы ЛО ЛНЗ $\Leftrightarrow$ ЛО - инъекция

-   строки м-цы ЛО ЛНЗ $\Leftrightarrow$ ЛО - сюръекция
:::

::: defin
**Def 38**. Отображение - **биекция**, если каждому
$y \in \tilde{\mathscr{L}^{m}}$ соответствует прообраз одного и только
одного вектора из $\mathscr{L}^{n}$, т.е. ЛО и сюръекция и инъекция.
:::

::: obs
*Замечание 26*. $$\begin{aligned}
Для\ инъекции: rg\ \varphi = n\\
Для\ сюръекции: rg\ \varphi = m 
\end{aligned}\
\vline
\Rightarrow
\fbox{ $n = m = rg\ \varphi \Leftrightarrow \varphi$ - биекция}$$
:::

## Изменение матрицы ЛО при замене базисов

Так как матрица ЛО зависит от базисов в исходном и конечном
пространствах, то при их замене она изменится.

Найдем связь матрицы ЛО, записанной в новом базисе с матрицей,
записанной в старом базисе, зная матрицы переходов от старых базисов к
новым.

$\varphi:\mathscr{L}\rightarrow \tilde{\mathscr{L}}$, **e, f** - базисы
в $\mathscr{L}$ и $\tilde{\mathscr{L}}$ $$\begin{aligned}
\textbf{e}^{'}= \textbf{e}S \\
\textbf{f}^{'} = \textbf{f}P
\end{aligned}\
\vline 
\Rightarrow 
\varphi \underset{e^{'},f^{'}}{\rightarrow} A^{'}$$

$Пусть\ x\in \mathscr{L}, y = \varphi(x) \in \tilde{\mathscr{L}}$
$$\begin{aligned}
x \stackrel{\textbf{e}}{\leftrightarrow} \xi \\
x \stackrel{\textbf{e}^{'}}{\leftrightarrow} \xi^{'}\\
\xi = S\xi^{'}
\end{aligned}\quad
\begin{aligned}
y \stackrel{\textbf{f}}{\leftrightarrow} \eta \\
y \stackrel{\textbf{f}^{'}}{\leftrightarrow} \eta^{'}\\
\eta = P\eta^{'}
\end{aligned}\
\vline
\Rightarrow 
P\eta^{'} = AS\xi^{'} 
\Rightarrow
\begin{aligned}
\eta^{'} = P^{-1}AS\xi^{'}
\eta^{'} = A^{'}\xi^{'}
\end{aligned}
\Rightarrow
\fbox{$ A^{'} = P^{-1}AS $}$$ В случае преобразования:

## Сумма и произведение отображений

$\varphi,\ \psi: \mathscr{L} \rightarrow \tilde{\mathscr{L}},\ \lambda \in \mathbb{R}$

::: defin
**Def 39**.
$$(\varphi + \psi)(x) \stackrel{def}{=} \varphi(x) + \psi(x)\qquad 
(\lambda \varphi)(x) \stackrel{def}{=} \lambda \varphi(x)$$
:::

::: obs
*Замечание 27*. $$\begin{aligned}
\varphi \underset{e,f}{\rightarrow} A \\
\psi \underset{e,f}{\rightarrow} B
\end{aligned}\
\vline
\Rightarrow
\begin{aligned}
(\varphi + \psi) \underset{e,f}{\rightarrow} A + B\\
(\lambda \varphi) \underset{e,f}{\rightarrow} \lambda A
\end{aligned}$$
:::

::: defin
**Def 40**. $$\begin{aligned}
\varphi: \mathscr{L} \rightarrow \tilde{\mathscr{L}} \\
\psi: \tilde{\mathscr{L}} \rightarrow \tilde{\tilde{\mathscr{L}}}
\end{aligned}\
\vline
\Rightarrow
\forall x \in \mathscr{L} \hookrightarrow ( \psi \varphi)(x) \stackrel{def}{=} \psi(\varphi(x)) \in \tilde{\tilde{\mathscr{L}}}
\Rightarrow
\psi \varphi: \mathscr{L} \rightarrow \tilde{\tilde{\mathscr{L}}}$$
:::

::: defin
**Def 41**. $\varphi: \mathscr{L}\rightarrow \mathscr{L}$\
$\varphi^{0} \stackrel{def}{=} Id$ (**единичное преобразование** -
$Id(x) = x$)\
$\varphi^{1} \stackrel{def}{=} \varphi$\
$\cdots$\
$\varphi^{k} \stackrel{def}{=} \underbrace{\varphi \cdot \varphi \dots \varphi}_{k\ раз}$
:::

::: defin
**Def 42**. $\varphi: \mathscr{L}\rightarrow \mathscr{L}$\
$p(t) = a_{0} + a_{1}t + a_{2}t^{2} + \dots + a_{n}t^{n}$\
$p(\varphi) = a_{0}Id + a_{1}\varphi + a_{2}\varphi^{2} + \dots + a_{n}\varphi^{n}$
:::

::: obs
*Замечание 28*.
$\varphi \underset{e}{\rightarrow} A \Rightarrow  p(\varphi) \underset{e}{\rightarrow} p(A) =  a_{0}E + a_{1}A + a_{2}A^{2} + \dots + a_{n}A^{n}$
:::

## Изоморфизм линейных пространств

::: defin
**Def 43**. **Изоморфизм** - биекция с сохранением операций.
:::

::: defin
**Def 44**. Если существует изоморфизм
$\mathscr{L}\rightarrow \tilde{\mathscr{L}}$, то ЛП $\mathscr{L}$ и
$\tilde{\mathscr{L}}$ - изоморфны.
:::

::: oboz
*Обозначение 3*. $\mathscr{L} \cong \tilde{\mathscr{L}}$
:::

::: ex
**Ex 19**. Выбор базиса в n-мерном ЛП определяет изоморфизм этого ЛП на
n-мерное арифметическое пространство (пространство столбцов -
координат), сопостовляющий каждому вектору его координатный столбец. Это
**координатный изоморфизм**.
:::

::: theorem
**Th 23** (**Теорема об изоморфизме**).
:::

::: obs
*Замечание 29* (**Значение теоремы об изоморфизме** (**!!!**)). ЛП могут
состоять из чего угодно - столбцов, многочленов, чисел, направленных
отрезков, функций - природа их элементов роли не играет, когда изучаются
их свойства, связанные с линейными операциями.

Все эти свойства у двух изоморфных пространств совершенно одинаковые.
Если мы условимся не различать между собой изоморфные пространства, *то
для каждой размерности существует только одно линейное пространство*.

Иными словами, мы можем изучать свойства связанные с линейными
операциями у обычных арифметических пространств, а не у всевозможных
абстрактных линейных пространств.
:::

## Инвариантные подпространства

::: obs
*Замечание 30*. Начиная с этого момента под $\varphi$ и другими
обозначениями ЛО мы будем понимать линейное преобразование, если не
оговорено противное.

В связи с этим следует обратить внимание на то, что образ и ядро
преобразования будут находиться в одном ЛП. В дальнейшем мы сможем
определить те условия, при которых образ и ядро могут совпадать, быть
вложенными друг в друга или не иметь общих векторов.
:::

::: defin
**Def 45**. Подпространство $\tilde{\mathscr{L}} \subset \mathscr{L}$
**инвариантно** относительно преобразования $\varphi$. если
$\varphi(\tilde{\mathscr{L}}) \subset \tilde{\mathscr{L}}$ (т.е.:
$\forall x \in \tilde{\mathscr{L}} \hookrightarrow \varphi(x) \in \tilde{\mathscr{L}}$).\
Переводя на русский язык - подпространство инвариантно относительно
преобразования, если после действия преобразования на каждый вектор
данного подпространства ни один из этих векторов \"не выпрыгнул\" из
этого подпространства.
:::

В качестве упражнения советую вам доказать следующие замечания:

::: obs
*Замечание 31*. $\forall \varphi \hookrightarrow$

-   $Im\ \varphi$ - инвариантное подпространство
    $(\varphi(Im\ \varphi) \subset Im\ \varphi)$

-   $\forall \tilde{\mathscr{L}} \supset Im\ \varphi \hookrightarrow \tilde{\mathscr{L}}$ -
    инвариантное подпространство.

-   $Ker\ \varphi$ - инвариантное подпространство.

-   $\forall \tilde{\mathscr{L}} \subset Ker \hookrightarrow \tilde{\mathscr{L}}$ -
    инвариантное подпространство.

Отсюда можно сделать вывод, что $\mathscr{L}$ и 0 всегда инвариантные
подпространства.
:::

::: obs
*Замечание 32*. $\mathscr{L}_{1}, \dots, \mathscr{L}_{k}$ - инвариантные
подпространства относительно преобразования, то:

-   $\mathscr{L}_{1} \cap \dots \cap \mathscr{L}_{k}$ - инвариантное
    подпространство

-   $\mathscr{L}_{1} + \dots + \mathscr{L}_{k}$ - инвариантное
    подпространство.
:::

::: proposition
**Утверждение 1**. *$e = (e_{1},\dots, e_{n})$ - базис в $\mathscr{L}$\
$$1)\
\tilde{\mathscr{L}} = \mathscr{L}(e_{1},\dots, e_{k}) - инвариантно\ относительно\ \varphi \Leftrightarrow 
A = 
\begin{pmatrix}
\underset{k\times k}{A} & \bullet \\
0 & \bullet 
\end{pmatrix}$$ $$2) 
\begin{aligned}
\mathscr{L}_{1} = \mathscr{L}(e_{1},\dots, e_{k_{1}}) - инвариантно\\
\mathscr{L}_{2} = \mathscr{L}(e_{k_{1} + 1},\dots, e_{k_{1} + k_{2}}) - инвариантно\\
\mathscr{L}_{3} = \mathscr{L}(e_{k_{1} + k_{2} + !},\dots, e_{k_{1} + k_{2} + k_{3}}) - инвариантно\\
\end{aligned}
\Leftrightarrow \varphi \underset{e}{\rightarrow} A = 
\begin{pmatrix}
\underset{k_{1}\times k_{1}}{\tilde{A}} & 0 & 0 \\
0 & \underset{k_{2}\times k_{2}}{\tilde{B}} & 0 \\
0 & 0 & \underset{k_{3}\times k_{3}}{\tilde{C}}
\end{pmatrix}$$ $k_{1} + k_{2} + k_{3} = n$*
:::

::: obs
*Замечание 33*. Если $e = (e_{1} \dots e_{n})$ -
базис пространства $\mathscr{L}$ и $\mathscr{L}(e_{1}),\dots, \mathscr{L}(e_{n})$ -
инвариантные подпространства относительно $\varphi$, то действие линейного
преобразования на базисные векторы будет следующим:
$\varphi(e_{i}) = \lambda_{i}e_{i}$ и: $$A = 
\begin{pmatrix}
\lambda_{1} & 0 & \cdots & 0 \\
0 & \lambda_{2} & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots\\
0 & \cdots & \cdots & \lambda_{n}
\end{pmatrix}$$
:::

::: defin
**Def 46**. $\varphi^{'}$ - **ограничение (сужение) преобразования**
$\varphi\ если\ \varphi^{'}: \mathscr{L}^{'} \rightarrow \mathscr{L}^{'},\quad \mathscr{L}^{'}$ -
подпространство (инвариантное)

::: obs
*Замечание 34*. В случае утверждения выше матрицами сужения
преобразования с матрицей А являются:
$\underset{k_{1}\times k_{1}}{\tilde{A}},\ \underset{k_{2}\times k_{2}}{\tilde{B}},\ \underset{k_{3}\times k_{3}}{\tilde{C}}.$
:::
:::

::: theorem
**Th 24**. *Если преобразования $\varphi\ и\ \psi$ перестановочны, то
ядро и множество значений одного из них инвариантно относительно
другого.*
:::

::: ev
*Доказательство 7*. В два пункта:

-   Если
    $x \in Ker\ \varphi,\ то\ \varphi(x) = 0 \Rightarrow \psi(\varphi(x)) = 0 \Rightarrow \varphi(\psi(x)) = 0 \Rightarrow \psi(x) \in Ker\ \varphi$

-   Если
    $x \in Im\ \varphi,\ то\ \exists z:\ x = \varphi(z) \Rightarrow \psi(x) = \psi(\varphi(z)) = \varphi(\psi(x)) \Rightarrow \psi(x) \in Im\ \varphi$

::: flushright
[ч.т.д.]{.underline}
:::
:::

### Характеристический многочлен

::: defin
**Def 47**. $\varphi \underset{e}{\rightarrow} A$\
$$\fbox{$ \chi_{\varphi}(\lambda) = |A - \lambda E| $}$$ -
**характеристический многочлен преобразования** $\varphi$
:::

::: proposition
**Утверждение 2**. *$\chi_{\varphi}(\lambda)$ не зависит от базиса
**е**.*
:::

::: defin
**Def 48**. Уравнение $\chi_{\varphi}(\lambda) = 0$ -
**характеристическое уравнение** (ХУ) $\varphi$. Его корни -
**характеристические числа** (ХЧ) $\varphi$.
:::

### Общий вид характеристического многочлена (отсутствует)

## Собственные подпространства 

::: defin
**Def 49**. $\mathscr{L}$ - вещественное (комплексное) ЛП. Число
$\lambda \in \mathbb{R(C)}$ - **собственное значение (СЗ)** линейного
преобразования, если: $$\exists x \ne o:\ \varphi(x) = \lambda x.$$

При этом $x$ - **собственный вектор (СВ)**, отвечающий собственному
значению $\lambda$.
:::

::: obs
*Замечание 35*. (вспомните предыдущие 2 замечания)

-   $x - СВ\ \Leftrightarrow \mathscr{L}(x)$ - одномерное инвариантное
    подпространство $\varphi$

-   Если $\lambda$ - СЗ, то хотя бы один СВ ему принадлежащий
    существует.
:::

::: theorem
**Th 25**. *(**О связи СЗ и ХЧ**)*

-   *В комплексном ЛП:\
    $\lambda$ - ХЧ $\Leftrightarrow \lambda$ - СЗ*

-   *В действительном ЛП:\
    $\lambda \in \mathbb{R} \Leftrightarrow \lambda$ - СЗ*
:::

::: defin
**Def 50**. $\lambda - СЗ\ \varphi$. **Собственным подпространством**
отвечающим СЗ $\lambda$ называется $$Ker(\varphi - \lambda \cdot Id)$$
![image](limage2.jpg)

::: obs
*Замечание 36*. Данное определение легко понять, установив простую
логическую цепочку:
$$x \in Ker\ (\varphi - \lambda\cdot Id) \Leftrightarrow (\varphi - \lambda \cdot Id)(x) = 0 \Leftrightarrow \varphi(x) - \lambda \cdot Id(x) = 0 \Leftrightarrow \varphi(x) = \lambda x$$
:::
:::

::: obs
*Замечание 37*. $\lambda_{1},\ \lambda_{2}$ - различные СЗ $\varphi$

-   Тогда:
    $Ker\ (\varphi - \lambda_{1}\cdot Id) \cap Ker\ (\varphi - \lambda_{2}\cdot Id) = 0$
    (собственные подпространства, отвечающие различным СЗ, пересекаются
    тривиальным образом)

-   Если
    $\lambda = 0\ СЗ\ \varphi \Rightarrow Ker\ \varphi \ne 0 \Rightarrow \varphi - не\ инъекция.$
:::

::: theorem
**Th 26**. *{В i-ом столбце матрицы линейного преобразования все
элементы вне главной диагонали равны нулю} $\Leftrightarrow$ {i-ый
базисный вектор собственный.}*

*Вывод: диагональный элемент [такого]{.underline} столбца - СЗ.*
:::

::: theorem
**Th 27**. *{Матрица линейного преобразования в некотором базисе
диагональная} $\Leftrightarrow$ {Все базисные векторы собственные}*
:::

### Традиционный алгоритм нахождения собственных подпространств

1.  Находим СЗ преобразования из уравнения: $|A-\lambda E| = 0$

2.  Составляем СЛАУ: $(A - \lambda E)\xi = 0$

3.  ФСР системы за исключением нулевого решения - состоит из
    координатных столбцов векторов, составляющих базис собственного
    подпространства

### Алгоритм Бурмистрова нахождения собственных подпространств

Используя алгоритм выше, вы гарантированно придете к правильному ответу.
Но бывают ситуации, когда можно пропустить некоторые действия этого
алгоритма, заменив их более простыми.

Например, если дана матрица размера от 2 до 5-6, а также в ней все
элементы меньше $\sim$`<!-- -->`{=html}15, то можно просто угадать СЗ,
при котором детерминант матрицы из 1 пункта обнулится.

Короче говоря, мы просто подбираем n-1 СЗ из n штук, а последнее можно
найти, заметив что след матрицы есть сумма СЗ.

Если мы видим, что матрица \"супер вырожденная\" - т.е. у нас
получилось, например 2 или 3 ЛЗ строки (которые можно обнулить), то и
собственному значению будет отвечать СП, размерности 2 или 3
соответственно.

Далее, когда мы нашли собственные значения, мы подставляем их в основную
матрицу СЛАУ из 2 пункта. А затем, мы также угадываем такие векторы,
которые, при перемножении с данной матрицей, давали бы нулевой столбец.
Это тоже довольно не сложно делается с матрицами небольшого размера и
небольшими элементами.

Линейная оболочка полученных СВ и есть СП.

### Комплексные характеристические числа

Находимся в комплексном пространстве. Дано линейное преобразование,
заданное своей матрицей. $$|A - \lambda E| = 0$$
$\lambda_{0} = \alpha + i\beta$ - комплексное ХЧ.\
$$A\xi = \lambda_{0} \xi \Leftrightarrow (A - \lambda_{0} E)\xi = 0$$
где $\xi = \gamma + i \eta$ - комплексный координатный столбец
собсвенного вектора, отвечающего СЗ $\lambda_{0}$.
$$A(\gamma + i\eta) = (\alpha + i\beta)(\gamma + i\eta)$$ Отделяем
вещественные и мнимые части: $$\left\{
    \begin{aligned}
    A\gamma = \alpha \gamma - \beta \eta \\
    A\eta = \beta \gamma + \alpha \eta
    \end{aligned}
\right.$$ Докажем что $\gamma$ и $\eta$ ЛНЗ (т.е.
$\exists \mathscr{L}(\gamma,\eta)$)\
Предположим противное: $$\eta = \sigma \gamma \Rightarrow 
+
\left\{
\begin{aligned}
A\gamma &= \alpha \gamma - \beta \sigma \gamma\ |\cdot (-\sigma)\\
\sigma A \gamma &= \beta \gamma + \alpha \sigma \gamma 
\end{aligned}
\right.
\Rightarrow 
0 = - \beta \sigma^{2}\gamma - \beta \gamma$$ Получили:
$\beta {(\sigma^{2} + 1)}\gamma = 0 \Rightarrow \beta \gamma = 0$\
$\gamma \ne 0\ (иначе\ \eta = 0 \Rightarrow \xi = 0) \Rightarrow \beta = 0$ -
противоречие (т.к. $\lambda_{0} \in \mathbb{C}$)\
$\Rightarrow \gamma,\ \eta$ - ЛНЗ.

::: flushright
[ч.т.д.]{.underline}
:::

::: obs
*Замечание 38*. (**Смысл существования** $\mathbb{R/C}$ ХЧ)

-   Смысл существования действительного ХЧ - есть инвариантное
    одномерное пространство.

-   Смысл существования комплексного ХЧ - есть инвариантная плоскость.\
    $\mathscr{L}(\gamma,\eta)$ - двумерная линейная оболочка, задающая
    ее. $$\left\{
    \begin{aligned}
    \varphi(\gamma) = A\gamma = \alpha \gamma - \beta \eta \\
    \varphi(\eta) = A\eta = \beta \gamma + \alpha \eta
    \end{aligned}
    \Rightarrow A = 
    \begin{pmatrix}
    \alpha & \beta \\
    - \beta & \alpha 
    \end{pmatrix} 
    \right.$$ A - матрица сужения линейного преобразования на
    инвариантную плоскость.

    Подводя итог можно сказать, что если у нас имеется комплексное ХЧ,
    то существует инвариантная плоскость, на которой матрица сужения
    линейного преобразования - есть матрица поворота и растяжения
    (поворотная гомотетия)
:::

## Приведение матрицы преобразования к диагональному виду

::: defin
**Def 51**. $\varphi: \mathscr{L}\rightarrow \mathscr{L}$ -
**диагонализуемое**, если в $\mathscr{L}\ \exists$ базис **e**:
$\varphi \underset{e}{\rightarrow} А$, где А - диагональная матрица.
:::

::: theorem
**Th 28**. *{$\varphi$ - диагонализуемо} $\Rightarrow$ {в
$\mathscr{L}\ \exists$ базис из СВ} $\Rightarrow$ {Размерность любого СП
равна кратности соответствующего корня ХУ}$\Rightarrow$ {все
пространство можно представить:
$\mathscr{L} = \underbrace{\mathscr{L}_{\lambda_{1}} \oplus \dots \oplus \mathscr{L}_{\lambda_{k}}}_{все\ СП}$}*
:::

::: defin
**Def 52**. **Геометрическая кратность СЗ** - это размерность
пространства, отвечающего данному СЗ.
:::

::: obs
*Замечание 39*.
$$\fbox{Алгебраическая кратность $\geqslant$ Геометрическая кратность $>$ 0}$$
:::

::: obs
*Замечание 40*. Пусть $\varphi$ - диагонализуемое.

Возьмем в $\mathscr{L}$ базис
$e = (\underbrace{e^{(1)}_{1}, \dots,e^{(1)}_{s_{1}}}_{базис\ \mathscr{L}_{\lambda_{1}}}, \underbrace{e^{(2)}_{1}, \dots, e^{(2)}_{s_{2}}}_{базис\ \mathscr{L}_{\lambda_{2}}}, \dots, \underbrace{e^{(k)}_{1}, \dots, e^{(k)}_{s_{k}}}_{базис\ \mathscr{L}_{\lambda_{k}}})$\
Тогда: $$\varphi \rightarrow A = 
\begin{pmatrix}
\lambda_{1} & \cdots & \cdots & \cdots & \cdots & \cdots & \cdots & 0\\
\vdots & \ddots & & & & & & \vdots \\
\vdots & & \lambda_{1} & & & & & \vdots \\
\vdots & & & \ddots & & & & \vdots \\
\vdots & & & & \ddots & & & \vdots \\
\vdots & & & & & \lambda_{k} & & \vdots \\
\vdots & & & & & & \ddots & \vdots \\
0 &\cdots & \cdots & \cdots & \cdots & \cdots & \cdots& \lambda_{k}
\end{pmatrix}$$
:::

::: obs
*Замечание 41*. $\lambda_{0}$ - СЗ.
$\quad x_{1}, \dots, x_{s} \in \lambda_{0}$\
$$\begin{aligned}
\varphi(x_{1}) = \lambda_{0} x_{1} \\
\qquad \cdots \\
\varphi(x_{s}) = \lambda_{0} x_{s} \\
ЛК:\ \beta_{1}x_{1} + \dots + \beta_{s}x_{s} = y
\end{aligned}\
\vline
\Rightarrow 
\varphi(y) = \beta_{1}\lambda_{0}x_{1} + \dots + \beta_{s}\lambda_{0}x_{s} = \lambda_{0}(\beta_{1}x_{1} + \dots + \beta_{s}x_{s}) = \lambda_{0}y$$
Имеется 2 пути: $$\begin{aligned}
y = 0\\
y = СВ
\end{aligned}\
\vline
\Rightarrow
\text{ЛК СВ-в - либо 0, либо СВ}$$
:::

::: theorem
**Th 29**. *$\lambda_{1}, \dots, \lambda_{s}$ - различные СЗ\
$x^{1}_{1}, \dots, x^{1}_{k_{1}}$ - ЛНЗ СВ-ры $\in \lambda_{1}$\
$\cdots$\
$x^{s}_{1}, \dots, x^{s}_{k_{s}}$ - ЛНЗ СВ-ры $\in \lambda_{s}$\
Вся эта куча СВ-в - ЛНЗ.*
:::

::: ev
*Доказательство 8*. Пусть $y_i,\ i = 1,\dots, s$ - не тривиальная
линейная комбинация собственных векторов, принадлежащих i-му СЗ.

Предположим, что $y_1 + \dots + y_s = 0$. Мы знаем что $y_i$ либо 0,
либо СВ, но так как $y_i$ - не тривиальная ЛК СВ-в, то остается лишь то,
что $y_i$ - СВ.

А не тривиальная комбинация СВ-в $y_i$ (с коэффицентами 1),
принадлежащих различным СЗ, не может быть равна нулю. следовательно вся
кучка векторов ЛНЗ.

::: flushright
[ч.т.д.]{.underline}
:::
:::

# Евклидовы пространства

::: defin
**Def 53**. $\mathscr{L}$ - **евклидово конечномерное пространство**,
если на нем определена скалярная функция двух аргументов (элементов
этого пространства), называемая **скалярным произведением** и
подчиняющаяся аксиомам:\
1) $(x, y) = (y, x)$\
2) $(x + y, z) = (x, z) + (y, z)$\
3) $(\alpha x, y) = \alpha (x, y)$\
4) $(x, x) \geqslant 0$ или $(x, x) = 0 \Leftrightarrow x = 0$
:::

::: oboz
*Обозначение 4*. $\mathscr{E}^{n}$ - n-мерное евклидово пространство.
:::

::: defin
**Def 54**.
$$\fbox{$ |a| = \sqrt{(a,a)}$} - \textbf{длина\ вектора } a.$$
:::

::: defin
**Def 55**. $a\perp b ,\ если: (a,b) = 0$
:::

::: proposition
**Утверждение 3**. *Нулевой вектор перпендикулярен всем остальным
векторам из $\mathscr{E}$*
:::

::: proposition
**Утверждение 4**. *Если в наборе все векторы попарно перпендинулярны и
не 0, то они ЛНЗ.*
:::

::: proposition
**Утверждение 5**. *$$\begin{aligned}
x = x_{1} + \dots + x_{k} \\
x_{i} \perp x_{j}\ (i,j = 1, \dots, k;\ i \ne j)
\end{aligned}\ 
\vline 
\Rightarrow 
|x|^{2} = |x_{1}|^{2} + \dots + |x_{k}|^{2}$$*
:::

::: defin
**Def 56**. Базис $e_{1}, \dots, e_{n}$ - **ортогональный**, если
вектора попарно $\perp$.
:::

::: defin
**Def 57**. Базис $e_{1}, \dots, e_{n}$ - **ортонормированный (ОНБ)**,
если $(e_{i}, e_{j}) = \delta_{ij}$.
:::

::: defin
**Def 58**. $\mathscr{E}^{'}, \mathscr{E}^{''} \subset \mathscr{E}$\
$\mathscr{E}^{'}\perp \mathscr{E}^{''}\ (\perp \ подпространства), если\ \forall x \in \mathscr{E}^{'},\ \forall y \in \mathscr{E}^{''} \hookrightarrow x\perp y$.
:::

## Ортогонализация методом Грамма-Шмидта

-   1\) $f_{1} = e_{1}$\
    2) $f_{2} = e_{2} - \alpha_{21}f_{1}$\
    3) $f_{3} = e_{3} - \alpha_{31}f_{1} - \alpha_{32}f_{2}$\
    $\vdots$\
    k)
    $f_{k} = e_{k} - \alpha_{k1}f_{1} - \dots - \alpha_{k(k-1)}f_{k-1}$\
    $\vdots$\
    n)
    $f_{n} = e_{n} - \alpha_{n1}f_{1} - \dots - \alpha_{n(n-1)}f_{n-1}$

-   Покажем, что на к)-м шаге мы не получим $f_{k} = 0$:

    Видно, что
    $\mathscr{L}(e_{1}) \supset  \mathscr{L}(f_{1}); \dots; \mathscr{L}(e_{1}, \dots, e_{k-1}) \supset \mathscr{L}(f_1,\dots, f_{k-1})$

    Предположим, что
    $f_{k} = e_{k} - \underbrace{\alpha_{k1}f_{1} - \dots - \alpha_{k(k-1)}f_{k-1}}_{\in \mathscr{L}(e_{1}, \dots, e_{k-1})} = 0$

    Т.к. мы показали, что $e_{1}, \dots, e_{k-1}$ взаимно
    перпендикулярны и $f_{i} \ne 0,\ i=1, \dots, k-1$, то они ЛНЗ
    $\Rightarrow$ их не тривиальная ЛК не 0.

    Но:

    $\underbrace{e_{k}}_{\in \mathscr{L}(e_{k})} \perp - \underbrace{(\alpha_{k1}f_{1} + \dots + \alpha_{k(k-1)}f_{k-1})}_{\in \mathscr{L}(e_{1}, \dots, e_{k-1})} \quad (\mathscr{L}(e_{1}, \dots, e_{k-1}) \cap \mathscr{L}(e_{k}) = 0)$\
    $\Rightarrow f_{k} \ne 0$

-   Подбираем $\alpha_{ij}$ так, чтобы
    $f_{k}\perp f_{l} \quad (k,l = 1, \dots, n, \ k \ne l)$:\
    $0 = (f_{2}, f_{1}) = (e_{2},f_{1}) - \alpha_{21}|f_{1}|^{2} \Rightarrow \alpha_{21} = \dfrac{(e_{2}, f_{1})}{|f_{1}|^{2}}$

    $0 = (f_{3}, f_{1}) = (e_{3}, f_{1}) - \alpha_{31} |f_{1}|^{2} \Rightarrow \alpha_{31} = \dfrac{(e_{3}, f_{1})}{|f_{1}|^{2}}$

    $\Rightarrow \alpha_{kj} = \dfrac{(e_{k}, f_{j})}{|f_{j}|^{2}}$

### Геометрический смысл ортогонализации

-   В 2-D пространстве:\
    Сохраняется площадь, построенного на векторах параллелограмма
    (сохраняется векторное произведение)

-   В 3-D пространстве:\
    Сохраняется объем.

**Вывод**: Доказали, что любой базис в евклидовом пространстве можно
ортогонализовать.

::: ex
**Ex 20**. Пусть есть некоторые векторы n-мерного евклидового
пространства. Взяв один вектор за первый и ортогонализуя базис методом
Грамма-Шмидта получим некий ОНБ. Вопрос - взяв за первый в
ортогонализации другой базисный вектор получим ли мы такой же базис или
другой?

Иначе говоря - зависит ли получаемый в результате ортогонализации базис
от выбора первого вектора?
:::

## Матрица Грамма

::: defin
**Def 59**. $x_{1}, \dots, x_{k} \in \mathscr{E}$
$$\Gamma(x_{1}, \dots, x_{k}) = 
\begin{pmatrix}
(x_{1}, x_{1}) & \cdots & (x_{1}, x_{k})\\
\vdots & & \vdots \\
(x_{k}, x_{1}) & \cdots & (x_{k}, x_{k})
\end{pmatrix}
- \text{\textbf{матрица Грамма} системы векторов}$$
:::

::: obs
*Замечание 42*. Матрица Грамма - симметричная.
:::

::: proposition
**Утверждение 6**. *$e = (e_{1}, \dots, e_{n})$ - базис евклидова
пространства. $$\begin{aligned}
x \leftrightarrow \xi = 
\begin{pmatrix}
x_{1} \\
\vdots \\
x_{n}
\end{pmatrix};\
y \leftrightarrow \eta =
\begin{pmatrix}
y_{1} \\
\vdots \\
y_{n}
\end{pmatrix}\\
\Gamma = 
\begin{pmatrix}
(e_{1}, e_{1}) & \cdots & (e_{1}, e_{n})\\
\vdots & & \vdots \\
(e_{n}, e_{1}) & \cdots & (e_{n}, e_{n})
\end{pmatrix}
\end{aligned}\
\vline 
\Rightarrow 
\fbox{$ (x, y) = \xi^{T}\Gamma \eta $}$$*
:::

::: obs
*Замечание 43*. В ОНБ $\Gamma = E \Rightarrow$
:::

::: ex
**Ex 21**. Как из линейного пространства сделать евклидово?\
Ответ: Ввести единичную матрицу Грамма базиса (тем самым ввели скалярное
произведение) ((можно было вводить совершенно любую другую МГ, но
единичная - самая простая))
:::

### Матрица Грамма при замене базиса

$\mathscr{E}^n,\ e = (e_{1}, \dots, e_{n}),\ e \stackrel{S}{\rightarrow} e^{'}$
$$\begin{aligned}
x \stackrel{e}{\leftrightarrow} \xi \\
y \stackrel{e}{\leftrightarrow} \eta 
\end{aligned} \quad
\begin{aligned}
x \stackrel{e^{'}}{\leftrightarrow} \xi^{'} \\
y \stackrel{e^{'}}{\leftrightarrow} \eta^{'} 
\end{aligned} \quad 
\begin{aligned}
\xi = S\xi^{'} \\
\eta = S\eta^{'}
\end{aligned} \
\vline
\Rightarrow 
\begin{aligned}
&(x, y) = \xi^{T}\Gamma \eta = (S\xi^{'})^{T}\Gamma S\eta^{'} 
= (\xi^{'})^{T}\underline{S^{T}\Gamma S} \eta^{'} \\
&(x, y) = (\xi^{'})^{T}\underline{\Gamma^{'}} \eta^{'}
\end{aligned}$$ Вывод:

::: obs
*Замечание 44*.  - определитель матрицы Грамма [базиса]{.underline}
строго положителен.
:::

::: proposition
**Утверждение 7**. *В процессе ортогонализации $|\Gamma| = const$.*
:::

::: ev
*Доказательство 9*. Представим переход
$e_1,\dots, e_n \rightarrow f_1,\dots, f_n$ в виде процедуры:

-   $e_1,\dots, e_n \rightarrow f_1,e_2,\dots, e_n\ (f_{1} = e_{1})$

-   $f_1,e_2,\dots, e_n \rightarrow f_1,f_2, e_{3},\dots, e_n\ (f_{2} = e_{2} - \alpha_{21}f_{1})$

-   

-   $f_1,\dots, f_{k-1}, e_{k},\dots, e_n \rightarrow f_1,\dots, f_k, e_{k+1},\dots, e_n\ (f_{k} = e_{k} - \alpha_{k1}f_{1} - \dots - \alpha_{k(k-1)}f_{k-1})$

-   

-   $f_1,\dots,f_{n-1}, e_n \rightarrow f_1,\dots, f_n\ (f_{n} = e_{n} - \alpha_{n1}f_{1} - \dots - \alpha_{n(n-1)}f_{n-1})$

Рассмотрим матрицу перехода от одного базиса к другому на k-м шаге:
$$S = \begin{pmatrix}
1 & 0 & \cdots & 0 & -\alpha_{k1} & 0 & \cdots & 0 \\
0 & 1 & & 0 & \vdots & \vdots & & 0 \\
\vdots & 0 &\ddots & \vdots & \vdots & \vdots & & \vdots \\
\vdots & \vdots &  & 1 & -\alpha_{k(k-1)} & 0 & & \vdots \\
\vdots & \vdots & & 0 & 1 & 0 & & \vdots \\
\vdots & \vdots & & \vdots & 0 & 1 & & \vdots \\
\vdots & \vdots & & \vdots & \vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & 0 & 0 & 0 & \cdots & 1 \\
\end{pmatrix}$$ (здесь единички только на диагонали)
$$|S| = 1 \Rightarrow |\Gamma^{'}| = |S^T||\Gamma||S| = |S|^2|\Gamma| = |\Gamma|$$

::: flushright
[ч.т.д.]{.underline}
:::
:::

::: proposition
**Утверждение 8**. *$x_{1}, \dots, x_{k} \in \mathscr{E}$*
:::

::: ev
*Доказательство 10*. Для доказательства достаточно показать, что
определитель матрицы Грамма от ЛЗ векторов равен нулю, так как ранее мы
уже получили, что от ЛНЗ векторов (т.е. от базиса) матрица Грамма строго
положительная.

Пусть вектора ЛЗ. Возьмем их [нетривиальную]{.underline} ЛК равную нулю
и домножим ее последовательно на каждый из этих векторов. Получим
систему из k уравнений: $$\left\{
\begin{aligned}
\alpha_1(x_1,x_1) + \dots + \alpha_k(x_1,x_k) = 0 \\
\vdots \\
\alpha_1(x_k,x_1) + \dots + \alpha_k(x_k,x_k) = 0
\end{aligned}
\right.$$ В матричном виде это выглядит так:
$$\Gamma(x_1,\dots, x_k)\begin{pmatrix}
\alpha_1 \\
\vdots \\
\alpha_k 
\end{pmatrix} = 0 \Rightarrow |\Gamma(x_1,\dots, x_k)| = 0$$
:::

::: obs
*Замечание 45*.
$|\Gamma(x_{1}, \dots, x_{k})| = 0 \Leftrightarrow x_{1}, \dots, x_{k}$ -
ЛЗ.
:::

*Следствие.* $x, y \in \mathscr{E}$ $$|\Gamma(x, y)| = 
\begin{pmatrix}
(x, x) & (x, y) \\
(x, y) & (y, y)
\end{pmatrix}
=
(x, x)(y, y) - (x, y)^{2} \geqslant 0$$ $$\Rightarrow 
\fbox{$ |x||y| \geqslant|(x, y)| $}\ - \text{\textbf{неравенство\ Коши-Буняковского}}$$

*Следствие.*\
$(x + y, x + y) = (x, x) + 2(x, y) + (y, y) \leq |x|^{2} + 2|x||y| + |y|^{2} = (|x| + |y|)^{2}$\
$$\Rightarrow \fbox{$ |x + y|^{2} \leq (|x| + |y|)^{2} $}$$

::: obs
*Замечание 46*. Базис ортогонален $\Leftrightarrow \Gamma$ векторов
этого базиса диагональная
:::

## Ортогональное проецирование вектора на подпространство

::: proposition
**Утверждение 9**.
*$\mathscr{E}^{'} \subset \mathscr{E}:\ \forall x \in \mathscr{E}\ \exists x^{'} \in \mathscr{E}^{'} \wedge \exists x^{''} \perp \mathscr{E}^{'}:$
$$\fbox{$ x = x^{'} + x^{''} $} 
\qquad
\parbox{4cm}{$x^{'}$ - \textbf{проекция} на $\mathscr{E}^{'}$ $x^{''}$ - \textbf{ортогональная составляющая}}$$
Такое представление единственно.*
:::

::: ev
*Доказательство 11*. От противного. $$\begin{aligned}
x = \tilde{x^{'}} + \tilde{x^{''}} \\
x = x^{'} + x^{''}
\end{aligned}\
\vline
\Rightarrow
\underbrace{x^{'}-\tilde{x^{'}}}_{\in \mathscr{E}^{'}} = \underbrace{x^{''}-\tilde{x^{''}}}_{\in \mathscr{E}^{''}} = y  \Rightarrow \begin{aligned}
y \perp \mathscr{E}^{'} \\
y \in \mathscr{E}^{'}
\end{aligned}\
\vline
\Rightarrow
y = 0$$

::: flushright
[ч.т.д.]{.underline}
:::
:::

### Методы нахождения ортогональной проекции

-   1.  Строим ОНБ в $\mathscr{E}^{'}$

    2.  Используем формулу для проекции:
        $x^{'} = (x, e_{1})e_{1} + \dots + (x, e_{k})e_{k}$

-   $\mathscr{E},\ \mathscr{E}^{'} = \mathscr{L}(a_{1}, \dots, a_{s})$.
    Пусть $a_{1}, \dots, a_{s}$ - ЛНЗ (к-тные ст-цы в некотором ОНБ из
    $\mathscr{E}$)

    $\Rightarrow x^{'} = \alpha_{1}a_{1} + \dots + \alpha_{s}a_{s}$
    $$\begin{aligned}
    A = (a_{1}| \dots | a_{s}) \\
    \alpha = 
    \begin{pmatrix}
    \alpha_{1} \\
    \vdots \\
    \alpha_{s}
    \end{pmatrix}
    \end{aligned}\
    \vline 
    \Rightarrow
    x^{'} = A\alpha$$ Чтобы найти $x^{'}$ найдем $\alpha$:
    $$\begin{aligned}
    x = A\alpha + x^{''}\ |\cdot A^{T} \\
    x^{''} \perp \mathscr{L}(a_{1}, \dots, a_{s})
    \end{aligned}\
    \vline
    \Rightarrow 
    A^{T}x = \underbrace{A^{T}A}_{= \Gamma}\alpha$$
    $\alpha = (A^{T}A)^{-1}A^{T}x \Rightarrow$

::: obs
*Замечание 47*. Матрица перехода от одного ОБ к другому ОБ -
ортогональная ($S^{T} = S^{-1}$)
:::

## Ортогональное дополнение подпространства

::: defin
**Def 60**.
$\mathscr{E}^{'}_{\perp} = \{x \in \mathscr{E}\ |\ x \perp \mathscr{E}^{'}\}$ -
**ортогональное дополнение** $\mathscr{E}^{'}$ до $\mathscr{E}$.
:::

::: proposition
**Утверждение 10**. *$\mathscr{E}^{'}_{\perp}$ - подпространство.
(выполнены все аксиомы)*
:::

::: proposition
**Утверждение 11**.
:::

::: ev
*Доказательство 12*.

1.  Докажем сначала, что
    $\mathscr{E} = \mathscr{E}^{'} + \mathscr{E}^{''}$
    $$\forall x \in \mathscr{E} \ \exists x^{'}\in \mathscr{E}^{'} \wedge x^{''}\in \mathscr{E}^{'}_{\perp}:\ x = x^{'} + x^{''}$$
    Множество всевозможных сумм $x^{'} + x^{''}$ - это сумма
    подпространств. $$\begin{aligned}
    \Rightarrow \mathscr{E} \subset \mathscr{E}^{'} + \mathscr{E}^{'}_{\perp}\\
    \mathscr{E} \supset \mathscr{E}^{'} + \mathscr{E}^{'}_{\perp}\ (т.к.\ все\ векторы\ \in \mathscr{E})
    \end{aligned}\
    \vline
    \Rightarrow
    \mathscr{E} = \mathscr{E}^{'} + \mathscr{E}^{'}_{\perp}$$

2.  Докажем, что
    $\mathscr{E}^{'} + \mathscr{E}^{'}_{\perp} = \mathscr{E}^{'} \oplus \mathscr{E}^{'}_{\perp}$

    Если вектор лежит и в ортогональной проекции и в ортогональном
    дополнении, то он ортогонален сам себе, следовательно он нуль.

::: flushright
[ч.т.д.]{.underline}
:::
:::

::: proposition
**Утверждение 12**.
:::

::: ev
*Доказательство 13*.

1.  $dim\ \mathscr{E}^{'} = k \Rightarrow dim\ \mathscr{E}^{'}_{\perp} = n-k \Rightarrow dim\ (\mathscr{E}^{'}_{\perp})_{\perp} = k$

2.  Докажем, что
    $\mathscr{E}^{'} \subset (\mathscr{E}^{'}_{\perp})_{\perp}$
    $$\forall x \in \mathscr{E}^{'} \Rightarrow x \perp \mathscr{E}^{'}_{\perp} \Rightarrow x \in (\mathscr{E}^{'}_{\perp})_{\perp} \Rightarrow \mathscr{E}^{'} \subset (\mathscr{E}^{'}_{\perp})_{\perp}$$

::: flushright
[ч.т.д.]{.underline}
:::
:::

::: proposition
**Утверждение 13**. *Подпространство часто задается СЛАУ:
$$\mathscr{E}^{'} = \left\{ x:\ \left\{ 
\begin{aligned}
(a_{1}, x) = 0\\
\dots \\
(a_{k}, x) = 0
\end{aligned}
\right.
\right\}
\Rightarrow 
\mathscr{E}^{'}_{\perp} = \mathscr{L}(a_{1}, \dots, a_{k})$$*
:::

## Расстояние от вектора до подпространства и угол между вектором и подпространством

$\mathscr{E}^{'} \subset \mathscr{E}^{n},\ x \in \mathscr{E}^{n}$

::: defin
**Def 61**. **Расстояние** от $x$ до $\mathscr{E}^{'}$: 
:::

::: proposition
**Утверждение 14**.
:::

::: defin
**Def 62**. **Угол между вектором и подпространством** - это угол между
вектором и его проекцией на это подпространство.
($x \ne 0,\ x^{'} \ne 0$)
$$cos\ \varphi = \dfrac{(x,x^{'})}{|x||x^{'}|} = \dfrac{(x^{'} + x^{''},x^{'})}{|x||x^{'}|} = \dfrac{|x^{'}|^{2}}{|x||x^{'}|} = \dfrac{|x^{'}|}{|x|} > 0 
    \Rightarrow \varphi \in \left[0, \dfrac{\pi}{2}\right]$$
:::

## Объем параллелепипеда

::: defin
**Def 63**. $a_{1}, \dots, a_{n}$ - ЛНЗ.
$$\fbox{$ \Pi(a_{1}, \dots, a_{n}) \stackrel{def}{=} \{ a = t_{1}a_{1} + \dots + t_{n}a_{n}\ |\ t_{i} \in [0,1],\ i = 1, \dots, n\}$}$$ -
**параллелепипед**, образованный на векторах $a_{1}, \dots, a_{n}$
:::

::: defin
**Def 64**.
$V(a_{1}, \dots, a_{n}) = V(a_{1}, \dots, a_{n-1})\cdot \rho(a_{n}, \mathscr{L}(a_{1}, \dots, a_{n-1}))$

$\rho(a_{n}, \mathscr{L}(a_{1}, \dots, a_{n-1})) = |a_{n}^{''}|$ -
ортогональная составляющая относительно
$\mathscr{L}(a_{1}, \dots, a_{n-1})$.

$\Rightarrow V(a_{1}, \dots, a_{n}) = V(a_{1}, \dots, a_{n-2})|a^{''}_{n-1}||a^{''}_{n} = \dots = \underbrace{|a^{''}_{1}|\cdot \dots \cdot |a^{''}_{n}|}$
$$\fbox{$ V(a_{1}, \dots, a_{n}) \stackrel{def}{=} |a^{''}_{1}|\cdot \dots \cdot |a^{''}_{n}| $}$$ -
**объем параллелепипеда**
:::

::: proposition
**Утверждение 15**.
:::

::: obs
*Замечание 48*.
$$\dfrac{V(a_{1}, \dots, a_{k}, x)}{V(a_{1}, \dots, a_{k})} = \dfrac{V(a_{1}, \dots, a_{k})|x^{''}|}{V(a_{1}, \dots, a_{k})} = |x^{''}|$$
:::

### Дополнительная формула объема параллелепипеда (отсутствует)

# Линейные преобразования в евклидовом пространстве

::: obs
*Замечание 49* (№0). Все свойства ЛП в евклидовом пространстве остаются
как и в линейных, но с некоторыми добавлениями.
:::

::: obs
*Замечание 50*. Далее мы заметим, что чем больше мы вводим ограничений в
виде определений новых типов преобразований, тем интереснее и обширнее
их свойства.
:::

## Сопряженные преобразования

::: defin
**Def 65**.
$\mathscr{E}^{n},\ \varphi: \mathscr{E} \rightarrow \mathscr{E}$\
$\varphi^{*}: \mathscr{E} \rightarrow \mathscr{E}$ - **сопряженное к
$\varphi$ преобразование**, если:
$$\fbox{$\forall x, y \in \mathscr{E} \hookrightarrow (x, \varphi(y)) = (\varphi^{*}(x), y)$}$$
:::

::: defin
**Def 66**. $e - базис, \Gamma$ $$\begin{aligned}
\varphi \stackrel{e}{\leftrightarrow} A\\
\varphi^{*} \stackrel{e}{\leftrightarrow} A^{*}
\end{aligned}\quad
\begin{aligned}
x \stackrel{e}{\leftrightarrow} \xi \\
y \stackrel{e}{\leftrightarrow} \eta
\end{aligned} \quad
\begin{aligned}
\varphi(x) \stackrel{e}{\leftrightarrow} A\xi\\
\varphi^{*}(y) \stackrel{e}{\leftrightarrow} A^{*}\eta
\end{aligned}$$ $$\begin{aligned}
(A\xi)^{T}\Gamma \eta = \xi^{T}\Gamma A^{*} \eta \\
(A\xi)^{T}\Gamma \eta = \xi^{T}A^{T} \Gamma \eta
\end{aligned}\
\vline
\Rightarrow 
\fbox{$ A^{*} = \Gamma^{-1}A^{T}\Gamma $}\text{ - \textbf{матрица сопряженного преобразования}}$$
:::

::: obs
*Замечание 51*. В ОНБ: $A^{*} = A^{T}$
:::

**Свойства сопряженного преобразования:**

1.  $(\varphi^{*})^{*} = \varphi$

2.  $(\varphi \psi)^{*} = \psi^{*} \varphi^{*}$

3.  $\chi_{\varphi}(\lambda) = \chi_{\varphi^{*}}(\lambda)$

## Самосопряженные преобразования

::: defin
**Def 67**. $\varphi$ - **самосопряженное** (ССП), если
$\varphi = \varphi^{*}$
:::

::: ex
**Ex 22**. $\mathscr{E}^{'} \subset \mathscr{E}^{n},\ \varphi$ -
ортогональное проецирование на $\mathscr{E}^{'}$ $$\begin{aligned}
x = x^{'} + x^{''} \\
y = y^{'} + y^{''} \\
\varphi(x) = x^{'}
\end{aligned}\
\vline
\Rightarrow
(\varphi(x), y) = (x^{'}, y^{'} + y^{''}) = (x^{'}, y^{'}) = (x^{'} + x^{''}, y^{'}) = (x, \varphi(y))$$
Следовательно - ОП - самосопряженное преобразование.
:::

**Свойства самосопряженного преобразования:**

1.  Характеристические числа вещественные

2.  СВ, принадлежащие разным СЗ - ортогональны друг другу

3.  $\mathscr{E}^{'}$ - инвар. относительно
    $\varphi \Rightarrow \mathscr{E}^{'}_{\perp}$ - тоже инвариантно

4.  У ССП существует ОНБ из СВ

5.  ССП - диагонализуемо

::: obs
*Замечание 52*. $$\begin{aligned}
\text{У ССП существует ОНБ из СВ} \\
\text{ССП - диагонализуемо}
\end{aligned}\
\vline
\Rightarrow
\exists S: A^{'} = \Lambda = S^{-1}AS = S^{T}AS$$ $\Lambda$ -
диагональная матрица
:::

::: obs
*Замечание 53*. С геометрической точки зрения ССП - это набор растяжений
и сжатий к взаимно перпендикулярным осям.
:::

## Изоморфизм евклидовых пространств

::: defin
**Def 68**. Два евклидовых пространства - **изоморфны**, если существует
взаимно однозначное линейное отображение, при котором:
$$(\varphi(x), \varphi(y)) = (x, y)$$ т.е. $\varphi$ - *сохраняет
скалярное произведение.*
:::

::: proposition
**Утверждение 16**.
*$$\fbox{$ \mathscr{E}^{'} \cong \mathscr{E}^{''} \Leftrightarrow dim\ \mathscr{E}^{'} = dim\ \mathscr{E}^{''} $}$$*
:::

## Ортогональные преобразования

::: defin
**Def 69**. Преобразование - ортогональное (ОП), если оно сохраняет
скалярное произведение: $$\fbox{$(\varphi(x), \varphi(y)) = (x, y)$}$$
:::

::: proposition
**Утверждение 17**. *ОП - линейное*
:::

**Свойства ортогонального преобразования:**

1.  $\varphi$ - ОП $\Rightarrow \varphi^{*} = \varphi^{-1}$

2.  [В ОНБ]{.underline} у ОП матрица ортогональная

3.  $\varphi$ - ОП $\Rightarrow \varphi$ - биекция

    ::: obs
    *Замечание 54*. В бесконечномерных пространствах ОП не обязательно
    биекция.\
    Пример: $\varphi: e_{n} \rightarrow e_{n+1}$ (тогда $e_{1}$ не
    соответствует никакой вектор)
    :::

4.  ХЧ по модулю равны 1

5.  Сохраняет длины и углы между векторами

6.  **e** - ОНБ$\varphi$ - ОП
    $\Leftrightarrow \varphi(e_{1}), \dots, \varphi(e_{n})$ - ОНБ

7.  $\underset{ОНБ}{\textbf{e}} \stackrel{S}{\rightarrow} \underset{ОНБ}{\textbf{f}} \Rightarrow S$ -
    ортогональная матрица

### Матрица сужения ОП на $\mathbb{C}$ (отсутствует доказательство)

::: proposition
**Утверждение 18**. *Существует ОНБ в котором матрица ОП имеет вид
блочно-диагональной, на диагонали которой находятся либо $\pm1$ либо
матрица вида: $$\begin{pmatrix}
cos\ \mu & -sin\ \mu \\
sin\ \mu & cos\ \mu
\end{pmatrix}$$*
:::

# Унитарные пространства

::: defin
**Def 70**. Линейное пространство над полем $\mathbb{C}$ называется
**унитарным (УП)**, если на нем введено скалярное произведение,
подчиняющееся аксиомам:\
1) $(x, y) = \overline{(y, x)}$\
(не $(x, y) = (y, x)$ как в ЛП над $\mathbb{R}$, т.к.
$(ix, ix) = -(x, x) < 0$, что невозможно, т.к. длина вектора
неотрицательна)\
2) $(x + y, z) = (x, z) + (y, z)$\
3)
$(\alpha x, y) = \alpha(x, y),\ но:\ (x, \beta y) = \overline{\beta}(x, y)$\
(т.к.
$(x, \beta y) = \overline{(\beta y, x)} = \overline{\beta(y, x)} = \overline{\beta}(x, y)$)
:::

::: defin
**Def 71**. Матрица называется **эрмитовой**, если
:::

## Матрица Грамма в УП

$e_{1}, \dots, e_{n}$ - базис $$\Gamma = 
\begin{pmatrix}
(e_{1}, e_{1}) & \cdots & (e_{1}, e_{n}) \\
\vdots & & \vdots \\
(e_{n}, e_{1}) & \cdots & (e_{n}, e_{n})
\end{pmatrix}
\stackrel{В\ УП}{\Longrightarrow} \fbox{$\Gamma = \overline{\Gamma^{T}}$}$$

### Изменение МГ при переходе к новому базису

$\mathscr{E}^n,\ e = (e_{1}, \dots, e_{n}),\ e \stackrel{S}{\rightarrow} e^{'}$
$$\begin{aligned}
x \stackrel{e}{\leftrightarrow} \xi \\
y \stackrel{e}{\leftrightarrow} \eta 
\end{aligned} \quad
\begin{aligned}
x \stackrel{e^{'}}{\leftrightarrow} \xi^{'} \\
y \stackrel{e^{'}}{\leftrightarrow} \eta^{'} 
\end{aligned} \quad 
\begin{aligned}
\xi = S\xi^{'} \\
\eta = S\eta^{'}
\end{aligned} \
\vline
\Rightarrow 
\begin{aligned}
\xi^{T}\Gamma \overline{\eta} = (\xi^{'})^{T}\Gamma^{'} \overline{\eta^{'}}\\
(S\xi^{'})^{T}\Gamma(\overline{S\eta^{'}}) = (\xi^{'})^{T}\Gamma^{'} \overline{\eta^{'}}
\end{aligned}\ 
\vline
\Rightarrow
\fbox{$ \Gamma^{'} = S^{T}\Gamma \overline{S} $}$$

## Неравенство Коши-Буняковского в УП

$x, y$ - любые векторы $\alpha \in \mathbb{R},\ \beta \in \mathbb{C}$\
$(\alpha x + \beta y, \alpha x + \beta y) = \alpha^{2}(x, x) + \alpha \overline{\beta} (x, y) + \beta \underbrace{\overline{\alpha}}_{= \alpha}\overline{(x, y)} + |\beta|^{2}(y, y) \geqslant 0$\
$(\overline{\beta}(x, y) + \beta \overline{(x, y)})^{2} - 4(x, x)|\beta|^{2}(y, y) \le 0 \Rightarrow |(x, y)|^{2}(|(x, y)|^{2} - (x, x)(y, y)) \le 0$\
1 случай:
$(x, y) \ne 0 \Rightarrow |x|^{2}|y|^{2} \geqslant|(x, y)|^{2}$\
2 случай: $(x, y) = 0 \Rightarrow 0 \equiv 0$

## Скалярное произведение в УП

::: proposition
**Утверждение 19**. *В УП:*
:::

## Сопряженные (= эрмитовы) преобразования в УП

$$\begin{aligned}
(\varphi(x), y) = (x, \varphi^{*}(y))\\
\varphi \stackrel{e}{\rightarrow} A_{\varphi} \\
\varphi^{*} \stackrel{e}{\rightarrow} A_{\varphi^{*}}
\end{aligned}\
\vline
\Rightarrow
\begin{aligned}
(A_{\varphi}\xi)^{T}\Gamma \overline{\eta} = \xi^{T}\Gamma (\overline{A_{\varphi^{*}}\eta})\\
\xi^{T} A^{T}_{\varphi}\Gamma \overline{\eta} = \xi^{T}\Gamma \overline{A_{\varphi^{*}}}\overline{\eta}
\end{aligned}\
\vline
\Rightarrow
\fbox{$ A^{T}_{\varphi}\Gamma = \Gamma \overline{A_{\varphi^{*}}} $}$$

# Линейные функционалы

::: defin
**Def 72**. **Линейный функционал** (= линейная функция)(ЛФ) - это
линейное отображение: $$f: \mathscr{L} \rightarrow \mathbb{R}$$ Иначе
говоря, это самое обычное линейное отображение, у которого
\"конечное\" пространство - это одномерное пространство действительных
чисел (переводит точки n-мерного пространства в чиселки).
:::

## Координатная запись ЛФ

::: obs
*Замечание 55*. Матрица ЛФ будет строкой $1 \times n$, где n -
размерность \"исходного\" пространства, а 1 - размерность числовой
прямой:
$$\boldsymbol{\chi} = (f(e_{1}) \dots f(e_{n})), \text{ где } f(e_{i}) \in \mathbb{R}$$
:::

::: proposition
**Утверждение 20**. *Значение ЛФ на любом векторе определяется абсолютно
также как и для ЛО: $$f(x) = 
\begin{pmatrix}
f(e_{1}) & \dots & f(e_{n}) 
\end{pmatrix}
\begin{pmatrix}
\xi^{1} \\
\vdots \\
\xi^{n}
\end{pmatrix}
= \boldsymbol{\chi} \boldsymbol{\xi} \quad (\varphi(x) = A\boldsymbol{\xi} - для\ ЛО)$$*
:::

## Строка ЛФ при замене базиса

$$\begin{aligned}
\mathscr{L}^{n},\ \textbf{e},\ \textbf{e} \stackrel{S}{\rightarrow} \textbf{e}^{'}\\
f: \mathscr{L} \rightarrow \mathbb{R} \\
\boldsymbol{\chi} = (f(e_{1}) \dots f(e_{n})) \\
x \stackrel{e}{\leftrightarrow} \boldsymbol{\xi} \quad x \stackrel{e^{'}}{\leftrightarrow} \boldsymbol{\xi}^{'}
\end{aligned}\
\vline
\Rightarrow
f(x) = f(\xi^{i}e_{i}) = \xi^{i} f(e_{i}) = \boldsymbol{\chi \xi} = \boldsymbol{\chi} S \boldsymbol{\xi}^{'} = \boldsymbol{\chi^{'}}\boldsymbol{\xi}^{'}$$
$\Rightarrow$

## Сопряженное пространство

::: proposition
**Утверждение 21**. *Если строки двух ЛФ равны, то и ЛФ равны.*
:::

::: proposition
**Утверждение 22**. *Между функционалами и строками длины n - биекция.*
:::

::: proposition
**Утверждение 23**. *$$\begin{aligned}
\mathscr{L}^{n},\ e \\
f \stackrel{e}{\leftrightarrow} \chi_{f} \\
g \stackrel{e}{\leftrightarrow} \chi_{g}
\end{aligned}\
\vline
\Rightarrow
\begin{aligned}
(f + g) \stackrel{e}{\leftrightarrow} \chi_{f} + \chi_{g} \\
\alpha f \stackrel{e}{\leftrightarrow} \alpha \chi_{f}
\end{aligned}$$*
:::

**Вывод:**

Между строками ЛФ и строками длины n биекция, а также сохраняются
операции с ЛФ. Следовательно, можно говорить о линейном пространстве
линейных функционалов $\mathscr{L}^{*}$ - **сопряженное пространство**
по отношению к $\mathscr{L}\ (dim\ \mathscr{L}^{*} = n)$

::: obs
*Замечание 56*. Сопряженное пространство можно также считать некоторой
абстракцией и не нужно пытаться представить пространство функций, ведь
мы изучаем свойства этого ЛП. Поэтому, говоря о пространстве ЛФ мы имеем
ввиду самое обычное пространство строк длины n (т.к. мы установили
изоморфизм между ним и пространством ЛФ)
:::

### Биортогональный базис (ББ)

Выберем в $\mathscr{L}$ ОНБ $e = (e_{1} \dots e_{n})$. Выберем
$p_{1}, \dots, p_{n} \in \mathscr{L}^{*}:\ p_{i}(x) = x_{i}$, где
$x_{i}$ - i-ая координата вектора $x$. Очевидно, что $$\begin{aligned}
p_{1} = (1\ 0 \dots 0)\\
\dots \\
p_{n} = (0 \dots 0\ 1)
\end{aligned}\
\vline 
\Rightarrow 
они\ ЛНЗ\ \Rightarrow базис$$

Базис $(p_{1} \dots p_{n})$ называется **биортогональным** к
$(e_{1} \dots e_{n})$.

### Матрица перехода от одного ББ к другому

::: obs
*Замечание 57*. Для того чтобы лучше понять, как происходит замена ББ,
вспомните как происходит замена базиса в ЛП.
:::

$$\begin{aligned}
&f \stackrel{e}{\leftrightarrow} \chi = (\chi_{1} \dots \chi_{n}) = \chi_{1}p_{1} + \dots + \chi_{n} p_{n} = \textbf{p}\chi^{T} \text{ - строка ЛФ в базисе е} \\
&f \stackrel{p}{\leftrightarrow} \chi^{T} \text{ - к-тный ст-ц элемента сопряженного пространства - ЛФ-ии в базисе р}
\end{aligned}$$ $$\textbf{p} = 
\begin{pmatrix}
p_{1} \\
\vdots \\
p_{n}
\end{pmatrix}$$ Теперь покажем, что зная матрицу перехода от одного
базиса к другому в ЛП, можно получить ББ к новому базису.
$$\begin{aligned}
e \stackrel{s}{\rightarrow} e^{'} \\
f \stackrel{p}{\leftrightarrow} \chi^{T} \\
f \stackrel{p^{'}}{\leftrightarrow} \chi^{' T}
\end{aligned}\
\vline
\Rightarrow
\chi^{'} = \chi S 
\Rightarrow 
\chi^{'T} = S^{T} \chi^{T}
\Rightarrow 
\chi^{T} = (S^{T})^{-1}\chi^{'T}$$ Вывод: матрица $(S^{T})^{-1}$ -
матрица перехода от старого ББ (который соответствует старому базису
**e**) к новому (который соответствует $\textbf{e}^{'}$)

::: obs
*Замечание 58*. Сопряженное пространство $\mathscr{L}^{*}$ - такое же
ЛП, как и любое другое, и, следовательно, имеет сопряженное пространство
$\mathscr{L}^{**}$, элементы которого - линейные функции на
$\mathscr{L}^{*}$.
:::

::: proposition
**Утверждение 24**.
:::

## Линейные функционалы в евклидовых пространствах (отсутствует)

::: obs
*Замечание 59*. Выбор базиса в ЛП $\mathscr{L}$ устанавливает изоморфизм
между $\mathscr{L}$ и $\mathscr{L}^{*}$. Покажем, что для n-мерного
евклидова пространства $\mathscr{E}$ существует такой изоморфизм,
независящий от базиса.
:::

::: proposition
**Утверждение 25**.
:::

# Билинейные функции

::: defin
**Def 73**. Отображение
$\beta:\mathscr{L}\times\mathscr{L} \rightarrow \mathbb{R}$ -
**билинейная функция (форма) (БФ)**, если выполнены 3 аксиомы:\
1) $\beta(a, b + c) = \beta(a, b) + \beta(a, c)$\
2) $\beta(a + b, c) = \beta(a, c) + \beta(b, c)$\
3) $\beta(\lambda a, \mu b) = \lambda \mu (a, b)$
:::

::: defin
**Def 74**. $e = (e_{1} \dots e_{n})$ - базис в $\mathscr{L}$\
$\beta:\mathscr{L}\times\mathscr{L} \rightarrow \mathbb{R}$ - билинейная
форма. $$B = 
\begin{pmatrix}
b_{11} & \cdots & b_{1n} \\
\vdots & & \vdots \\
b_{n1} & \cdots & b_{nn}
\end{pmatrix} \quad
b_{ij} = \beta(e_{i}, e_{j})$$ - **матрица билинейной формы**
:::

::: oboz
*Обозначение 5*. $\beta \underset{e}{\rightarrow} B$
:::

::: theorem
**Th 30**. *$$\begin{aligned}
\beta \underset{e}{\rightarrow} B \\
x \stackrel{e}{\leftrightarrow} \xi \\
y \stackrel{e}{\leftrightarrow} \eta 
\end{aligned}\
\vline 
\Rightarrow
\fbox{$ \beta(x, y) = \xi^{T}B\eta $}$$*
:::

::: obs
*Замечание 60*. $\mathscr{B}$ - ЛП билинейных форм.
$\mathscr{B} \cong \underset{n \times n}{M} \Rightarrow dim\ \mathscr{B} = n^{2}$
:::

::: theorem
**Th 31**. *При переходе к новому базису:
$$\fbox{$ B^{'} = S^{T}BS $}$$*
:::

*Следствие 1.* Знак $|B|$ не зависит от базиса:
$|B^{'}| = |S^{T}||B||S| = |S|^{2}|B|$

*Следствие 2.* rg B не зависит от базиса

::: defin
**Def 75**. **Ранг билинейной формы** - ранг ее матрицы
:::

::: defin
**Def 76**. БФ - симметричная, если
$\forall x, y \in \mathscr{L} \hookrightarrow \beta(x, y) = \beta(y, x)$
:::

::: theorem
**Th 32**. *БФ - симметричная $\Leftrightarrow B^{T} = B$*
:::

## Квадратичные формы

::: defin
**Def 77**. **Квадратичная форма** - отображение
$k: \mathscr{L} \rightarrow \mathbb{R}:$\
$k(x) = \beta(x, x)\quad (\underline{\beta - симметричная})$
:::

::: ex
**Ex 23**. Скалярное произведение векторов - симметричная БФ.
Соответствующая квадратичная форма сопоставляет вектору квадрат его
длины.
:::

::: obs
*Замечание 61*. По заданной квадратичной форме k однозначно определяется
соответствующая симметричная БФ:
$$k(x + y) = \beta(x + y, x + y) = \beta(x, x) + \beta(y, x) + \beta(y, y)$$
$$\Rightarrow \beta(x, y) = \dfrac{1}{2}(k(x + y) - k(x) - k(y))$$
:::

::: defin
**Def 78**. Матрицей квадратичной формы является матрица соответствующей
ей БФ.
:::

::: defin
**Def 79**. На диагонали матрицы квадратичной формы стоят ее значения на
базисных векторах.
:::

## Приведение квадратичной формы к диагональному виду

::: theorem
**Th 33**. *$\forall$ КФ существует базис в котором она имеет
диагональный вид.*
:::

::: defin
**Def 80**. $k(x)$ - **положительно определенная**, если
$\forall x \ne 0 \hookrightarrow k(x) > 0$ (полуопределенной, если
$k(x) \geqslant 0$)
:::

::: defin
**Def 81**. $k(x)$ - **отрицательно определенная**, если
$\forall x \ne 0 \hookrightarrow k(x) < 0$
:::

::: defin
**Def 82**. БФ - **положительно определенная**, если она порождает
положительно определенную КФ.
:::

::: theorem
**Th 34** (**Критерий Сильвестра**).
*$$БФ - положительно\ определенная \Leftrightarrow \Delta_{k} > 0$$*
:::

::: defin
**Def 83**. Матрица КФ имеет канонический вид, если на диагонали стоят
{-1, 0, 1}
:::

::: defin
**Def 84**. Количество $d_{i} > 0$ в диагональном виде k(x) -
положительный индекс инерции КФ и обозначается p(k)
:::

::: defin
**Def 85**. Количество $d_{i} < 0$ в диагональном виде k(x) -
отрицательный индекс инерции КФ и обозначается q(k)
:::

::: defin
**Def 86**. сингатура $= p(k) - q(k)$
:::

::: defin
**Def 87**. $rg\ k = p(k) + q(k)$
:::

::: theorem
**Th 35** (**Закон инерции КФ**). *Количество положительных и
отрицательных индексов инерции одно и то же в любом базисе*
:::

::: ex
**Ex 24** (Вопрос с экзамена). Дана положительно полуопределенная БФ.
Доказать: 1) сумма элементов матрицы данной БФ неотрицательна, 2) сумма
элементов матрицы, с коэффициентами $\{+1, -1\}$ взятыми в шахматном
порядке (если представить матрицу как шахматную доску), данной БФ
неотрицательна.
:::

::: ev
*Доказательство 14*. В данной задаче в первом пункте нужно лишь знать,
что сумма элементов матрицы не зависит от того, на какие вектора мы
собираемся подействовать этой БФ. Поэтому, зная что мы имеем дело с
положительно полуопределенной БФ:

-   $\beta(x, y) = \xi^{T}B\eta = \beta(e_{i}, e_{j})\xi^{i}\eta^{j}$
    $$Говорим,\ что\ \xi = \begin{pmatrix}
    \xi^{1} \\
    \vdots \\
    \xi^{n}
    \end{pmatrix}
    =
    \begin{pmatrix}
    1 \\
    \vdots \\
    1
    \end{pmatrix};\
    \eta = 
    \begin{pmatrix}
    \eta^{1} \\
    \vdots \\
    \eta^{n}
    \end{pmatrix}
    =
    \begin{pmatrix}
    1 \\
    \vdots \\
    1
    \end{pmatrix}$$ Тогда:
    $\beta(x, y) = \beta(e_{i}, e_{j}) \geqslant 0$

-   $$Говорим,\ что\ \xi^{i} = (-1)^{i+1},\ \eta^{j} = (-1)^{j+1}$$
    Тогда:
    $\beta(x, y) = \underbrace{\beta(e_{i}, e_{j})(-1)^{i+1}(-1)^{j+1}}_{\text{тот самый шахматный порядок}} \geqslant 0$

    ::: flushright
    ч.т.д.
    :::
:::

## Преобразование, присоединенное билинейной форме

::: defin
**Def 88**.
$\varphi: \mathscr{E} \rightarrow \mathscr{E}: \beta(x, y) = (x, \varphi(x))$ -
присоединенное преобразование.
:::

::: proposition
**Утверждение 26**. *$\forall$ БФ $\exists !$ присоединенное
преобразование:
$$(x, \varphi(y)) = \xi^{T} \Gamma A \eta - билинейная\ форма\ B = \Gamma A \Rightarrow A = \Gamma^{-1}B$$*
:::

## Приведение пары квадратичных форм к диагональному виду

::: theorem
**Th 36**.
*$\mathscr{E}^{n} \Rightarrow \forall k(x)\ \exists \textbf{e} \text{ - \underline{ОНБ}}:\ k \underset{e}{\rightarrow} \begin{pmatrix}
d_{1} & & 0\\
 & \ddots & \\
 0 & & d_{n} 
\end{pmatrix} \text{ - диагональный вид}$*
:::

::: theorem
**Th 37**. *$$\begin{aligned}
\mathscr{L} \text{ - ЛП} \\
f \text{ - любая КФ} \\
g \text{ - полож. опр. КФ}
\end{aligned}\ 
\vline
\Rightarrow
\exists e:\ f \underset{e}{\rightarrow} \begin{pmatrix}
d_{1} & & 0\\
& \ddots & \\
0 & & d_{n} 
\end{pmatrix},\
g \underset{e}{\rightarrow} \underbrace{\begin{pmatrix}
    \tilde{d_{1}} & & 0\\
    & \ddots & \\
    0 & & \tilde{d_{n}} 
    \end{pmatrix}}_{\text{канонический вид}}$$*
:::

### Метод №1

$$\begin{aligned}
K, H - матрицы\ КФ\ в\ e \\
H - матрица\ Грамма\ в\ e 
\end{aligned}\
\vline
\Rightarrow
A = H^{-1}K \text{ - присоединенное преобр. к форме К}$$
$|H^{-1}K - \lambda E| = 0$ - ХУ $\Rightarrow |K - \lambda H| = 0$

$\forall$ корня ур-я $|K - \lambda H| = 0$ решения системы (К -
$\lambda$H \| 0) нужно нормировать используя скалярное произведение с
$\Gamma = H$.

Объединяя получившиеся базисы получим тот, в котором К имеет
диагональный вид, а Н = Е - канонический (т.к. это м-ца положительно
опр. КФ, которая является МГ в ОНБ).

### Метод №2 (метод Бурмистрова - отсутствует)

# Полярное разложение преобразований

::: defin
**Def 89**. $\varphi$ - **положительное преобразование**, если оно ССП и
$\forall x \hookrightarrow (\varphi(x), x) \geqslant 0$
:::

::: obs
*Замечание 62*.
$\varphi(x) = \lambda x \Rightarrow (\lambda x, x) \geqslant 0 \Rightarrow \lambda (x, x) \geqslant 0 \Rightarrow$ -
СЗ неотрицательные.
:::

::: proposition
**Утверждение 27**. *$\varphi \varphi^{*}$ - положительное*
:::

::: proposition
**Утверждение 28**.
*$\exists \varphi \underset{e}{\rightarrow} A:\ \exists|A| \Rightarrow \exists h \text{ - положительное: } h^{2} = \varphi^{*}\varphi$*
:::

::: theorem
**Th 38** (**О полярном разложении**).
*$$\varphi - \ невырожденное\ \Rightarrow \exists \underbrace{h}_{\text{полож.}}, \underbrace{g}_{\text{ортогон.}}:\ \varphi = gh$$*
:::

# Поверхности II порядка (отсутствует)

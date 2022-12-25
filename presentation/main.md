---
marp: true
theme: uncover
class: invert
style: |
    * {
        font-family: Times New Roman;
    }
    footer {
        border-top: 1px solid #999;
        font-size: small;
        opacity: 0.8; 
    }
    header {
        margin-top: 0px;
        border-bottom: 1px solid #999;
        font-size: 66px;
        opacity: 0.9; 
    }
    .head {
        font-size: 26px
    }
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    }
    .left{
        text-align: left 
    }
---

<div class="head">
 МОСКОВСКИЙ ГОСУДАРСТВЕННЫЙ ТЕХНИЧЕСКИЙ УНИВЕРСИТЕТ ИМЕНИ Н.Э. БАУМАНА (НАЦИОНАЛЬНЫЙ ИССЛЕДОВАТЕЛЬСКИЙ УНИВЕРСИТЕТ)
</div>

# «Классификация методов модификации ядра Linux» 


<div class="left">
<b>Студент:</b> Романов Семен Константинович

<b>Группа:</b> ИУ7-55Б
<b>Руководитель:</b> Оленев Антон Александрович

</div>

---
<style scoped>
    .left {
        margin-top: 0px;
    }
    li {
        font-size: 34px;
    }
</style>
    
# <header>Цель и задачи
</header>

<div class="left"><b>Цель</b> – классифицировать методы модификации ядра Linux.</div>

##### <div class="left">Задачи:
* Провести обзор существующих методов модификации ядра Linux;
* Провести анализ методов модификации ядра Linux;
* Сформулировать критерии классификации методов модификации ядра;
* Классифицировать существующие методы модификации ядра.
</div>

---

# <header>Термины предметной области
</header>

<div class="left">
Ядро Linux — это основной компонент ОС Linux.
</div>

<div class="left">Ядро должно в первую очередь выполнять две основные задачи:
</div>

* Взаимодействие с аппаратными компонентами, обслуживая все низкоуровневые элементы, входящие в состав аппаратной платформы.
* Обеспечить среду выполнения для программ, которые будут выполняться в операционной системе.

---
<style scoped>
    header {
        margin-top: 0px;
        font-size: 44px;
    }
    .left {
        font-size: 32px;
    }
</style>
    

# <header>Термины предметной области
</header>

![bg left fit](../research/inc/img/virt_mem2.png)


<div class="left">
Виртуальная память - это способ организации памяти, при котором процессору предоставляется не физические адреса, а виртуальные адреса, которые
в дальнейшем переводятся в физические адреса с помощью таблиц страниц.
</div>

---

<style scoped>
    header {
        margin-top: 0px;
        font-size: 44px;
    }
    .left {
        font-size: 32px;
    }
</style>
    

# <header>Термины предметной области
</header>

![bg fit right](../research/inc/img/rings.png)


<div class="left">
Идея колец защиты заключается в том, что каждое кольцо имеет собственный набор инструкций, которые процесс на данном кольце защиты может выполнять, и чем ближе кольцо к нулевому, тем больше прав имеет процесс.
</div>

---

<style scoped>
    .left {
        margin-top: 0px;
        font-size: 34px;
    }
    li {
        font-size: 30px;
    }
</style>

# <header>Задачи модификации ядра Linux
</header>


<div class="left">
Примеры некоторых задач, которые должны быть решены на уровне ядра:
</div>

* Написание приложений с доступом к низкоуровневым ресурсам, которые не могут быть предоставлены другими способами.
* Реализация алгоритмов, которые должны быть выполнены с высокой точностью по времени и/или пространству
* Написание программ, которые должны быть доступны всем пользователям системы.
* Также следует перейти в пространство ядра, где накладные расходы, такие как смена пространств пользователь-ядро, становится неприемлемыми для эффективной или корректной работы программы.

---
<style scoped>
    header {
        margin-top: 0px;
        font-size: 60px;
    }
    .marg {
        margin-top: 80px;
        font-size: 60px;
    }
    .left {
        font-size: 32px;
    }
</style>

# <header>Обзор методов модификации ядра Linux
</header>

## <div class="marg">Перекомпиляция ядра</div>

<div class="columns">
    <div>
        Преимущества:
        <ul style="list-style-type: '+ '">
            <li> Скорость работы системы.
            <li> Универсальность
            <li> Начиная c версии 6.1 нативная поддержка Rust
        </lu>
    </div>
    <div>
        Недостатки:
        <ul style="list-style-type: '- '">
            <li> Необходимость перекомпиляции ядра для каждого нового модуля. 
            <li> Сложность добавления кода в ядро Linux.
            <li> Серьезный риск повредить систему
        </lu>
    </div>
</div>

---
<style scoped>
    header {
        margin-top: 0px;
        font-size: 60px;
    }
    .marg {
        margin-top: 80px;
        font-size: 60px;
    }
    .left {
        font-size: 32px;
    }
</style>

# <header>Обзор методов модификации ядра Linux
</header>

## <div class="marg">Loadable Kernel Module</div>

<div class="columns">
    <div>
        Преимущества:
        <ul style="list-style-type: '+ '">
            <li> Динамическая загрузка
            <li> Экономия оперативной памяти
            <li> Облегченный способ отладки
        </lu>
    </div>
    <div>
        Недостатки:
        <ul style="list-style-type: '- '">
            <li> Увеличение времени загрузки системы
            <li> Проблемы со совместимостью
            <li> Штраф за фрагментацию
            <li> Риск повредить систему
        </lu>
    </div>
</div>

---
<style scoped>
    header {
        margin-top: 0px;
        font-size: 60px;
    }
    .marg {
        margin-top: 80px;
        font-size: 60px;
    }
    .left {
        font-size: 32px;
    }
</style>

# <header>Обзор методов модификации ядра Linux
</header>

## <div class="marg">Kernel Live Patching</div>

<div class="columns">
    <div>
        Преимущества:
        <ul style="list-style-type: '+ '">
            <li> Обновление без перезагрузки системы.
            <li> Возможность автоматизации процесса
            <li> Обновления проходят быстро
        </lu>
    </div>
    <div>
        Недостатки:
        <ul style="list-style-type: '- '">
            <li> Сложность реализации
            <li> Ограниченность
            <li> Не все ядра поддерживают Live Patching
        </lu>
    </div>
</div>

---
<style scoped>
    header {
        margin-top: 0px;
        font-size: 60px;
    }
    .marg {
        margin-top: 80px;
        font-size: 60px;
    }
    .left {
        font-size: 32px;
    }
</style>

# <header>Обзор методов модификации ядра Linux
</header>

## <div class="marg">extended Berkeley Packet Filter</div>

<div class="columns">
    <div>
        Преимущества:
        <ul style="list-style-type: '+ '">
            <li> Не изменяет исходный код ядра
            <li> Поддержка высокоуровневых языков
            <li> Динамическая загрузка
        </lu>
    </div>
    <div>
        Недостатки:
        <ul style="list-style-type: '- '">
            <li> Ограниченность
            <li> Проблемы с безопасностью
            <li> Развивающаяся технология
        </lu>
    </div>
</div>


---
<style scoped>
    * {
        font-size: 25px;
    }
    header {
        margin-top: 0px;
        font-size: 48px;
    }
    .marg {
        margin-top: 20px;
        font-size: 40px;
    }
    .left {
        font-size: 32px;
    }
</style>

# <header>Классификация методов модификации ядра Linux
</header>

## <div class="marg">Критерии сравнения методов модификации ядра</div>


Критерий                |   Описание 
:-----                  |   :------
Производительность      |   Производительность программ
Безопасность            |   Наличие гарантии, что внесенный код не вызовет остановку системы
Скорость разработки     |   Является ли метод быстрым в разработке
Гибкость                |   Возможность метода подстроиться под любые поставленные задачи
Простота отладки        |   Является ли описанная модификация простой в отладке
Поддержка               |   Поддержка метода разработчиками ядра при его написании
Простота развёртывания  |   Является ли описанный метод простым в развёртывании на большом количестве машин

---
<style scoped>
    * {
        font-size: 25px;
    }
    header {
        margin-top: 0px;
        font-size: 48px;
    }
    .marg {
        margin-top: 20px;
        font-size: 40px;
        margin-bottom: 20px;
    }
    .left {
        font-size: 32px;
    }
</style>

# <header>Классификация методов модификации ядра Linux
</header>

## <div class="marg">Критерии сравнения методов модификации ядра</div>


Критерий                |   Рекомпиляция    |   LKM     |   Live Patching   |   eBPF
:-----                  |   :------:        |   :------:|   :------:        |   :------:
Производительность      | :white_check_mark:  | :white_check_mark: | :white_check_mark: | :white_check_mark:
Безопасность            | :x:  | :x: | :x: | :white_check_mark: 
Скорость разработки     | :x:  | :white_check_mark: | :x: | :white_check_mark:
Гибкость                | :white_check_mark:  | :white_check_mark: | :x: | :x:
Простота отладки        | :x:  | :white_check_mark:/:x: | :x: | :white_check_mark:
Поддержка               | :white_check_mark:  | :white_check_mark: | :white_check_mark: | :x:
Простота развёртывания  | :x:  | :white_check_mark: | :white_check_mark: | :white_check_mark:


---
<style scoped>
    * {
        font-size: 30px;
    }
    header {
        margin-top: 0px;
        font-size: 48px;
    }
    .marg {
        margin-top: 20px;
        font-size: 40px;
        text-align: left;
    }
    /* .left {
        font-size: 32px;
    } */
</style>

# <header>Выводы
</header>

## <div class="marg">В ходе данной работы были изучены:</div>

- методы модификации ядра Linux;
- критерии сравнения методов модификации ядра;
- основные принципы работы и преимущества каждого из методов.

<div class="left">
Был выполнен обзор существующих методов модификации ядра Linux, проведен анализ их преимуществ и недостатков.
</div>

<div class="left">
Были сформулированы критерии классификации методов модификации ядра Linux.
Была проведена классификация методов модификации ядра Linux по критериям, сформулированным в ходе работы.
</div>

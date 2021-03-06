# Term Frequency, Inverse Document Frequency (TF/IDF)

## Инвертированный индекс

Индекс в ES на самом деле называется **"инвертированный индекс"**(*inverted index*). Это механизм, по которому все поисковые движки работают. Предположим, есть два документа:

- **Document 1**: "Space: The final frontier. These are the voyages..."
- **Document 2**: "He's bad, he's number one. He's the space cowboy with the laser gun!"

Инвертированный индекс не будет хранить эти строки в чистом виде. Поисковый движок, такой как ES, разбивает каждый документ на индивидуальные **поисковые термины** (*term*). В этом примере мы разобьем строки по словам и сконвертируем к нижнему регистру. Затем мы сопоставим эти термины с документами, в которых они возникают:

| Слово        |    Документ        |
| ------------- |:-------------:|
|   space   | 1,2 |
|    the  | 1,2 |
|    final  | 1 |
|   frontier   | 1 |
|he|2|
|bad|2|

На деле инвертированный индекс хранит не только документ, в котором встречается слово, но и позицию, на которой слово расположено. 

## Релевантность

TF-IDF означает `Term Frequency * Inverse Document Frequency`, где:

- `Term Frequency` - частота встречи термина в некотором документе;
- `Document Frequency` - частота встречи термина во всех документах;
- `Inverse Document Frequency (IDF)` - инверсия частоты встречи во всех документах. Учёт IDF уменьшает вес широкоупотребительных слов (вроде The и прочего).

`Term Frequency / Document Frequency` это то же самое, что `Term Frequency * Inverse Document Frequency`. Эта величина позволяет определить релевантность документа запросу.

Если поделить частоту встречаемости термина в документе на частоту встречи термина во всех документах - можно определить, насколько этот термин "особенный" для некоторого документа. Если слово в данном документе встречается намного чаще, чем в других - он более релевантен. 

> Большой вес в TF-IDF получат слова с высокой частотой в пределах конкретного документа и с низкой частотой употреблений в других документах. - Википедия






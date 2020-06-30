# Набор данных MovieLens 

Это свободный набор данных из рейтингов фильмов. Этот набор данных позволит нам поиграть с разными данными, которые представляют из себя не только плоские записи, но и структурированные свойства вроде рейтинга, даты релиза.

Нам не нужен самый большой сет, ведь мы работаем всего на одной машине. Мы возьмем набор "recommended for education". На момент прохождения курса он был из 100.000 записей и весил 1 MB: [https://grouplens.org/datasets/movielens/latest/](https://grouplens.org/datasets/movielens/latest/)

Состоит он из csv-записей в нескольких файлах:

- movies;

```csv
movieId,title,genres
1,Toy Story (1995),Adventure|Animation|Children|Comedy|Fantasy
```

- links;

```csv
movieId,imdbId,tmdbId
1,0114709,862
```

- ratings;

```csv
userId,movieId,rating,timestamp
1,1,4.0,964982703
```

- tags.

```csv
userId,movieId,tag,timestamp
2,60756,funny,1445714994
2,60756,Highly quotable,1445714996
```





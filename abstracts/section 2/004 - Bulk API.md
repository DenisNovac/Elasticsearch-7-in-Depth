# Пакетная вставка данных

Теперь нужно импортировать все фильмы разом. 

ES использует формат импорта bulk:

```json
curl -XPUT 192.168.88.242:9200/_bulk -d '

{ "create": { "_index": "movies", "_id": "135569" } }
{ "id": "135569", "title": "Star Trek Beyond", "year": 2016, "genre": ["Action", "Adventure", "Sci-Fi"] }
{ "create": { "_index": "movies", "_id": "122886" } }
{ "id": "122886", "title": "Star Wars: Episode VII - The Force Awakens", "year": 2015, "genre": ["Action", "Adventure", "Fantasy", "Sci-Fi", "IMAX"] }
`
```

В Кибане тоже так можно:

```json
PUT _bulk 
{ "create": { "_index": "movies", "_id": "135569" } }
{ "id": "135569", "title": "Star Trek Beyond", "year": 2016, "genre": ["Action", "Adventure", "Sci-Fi"] }
{ "create": { "_index": "movies", "_id": "122886" } }
{ "id": "122886", "title": "Star Wars: Episode VII - The Force Awakens", "year": 2015, "genre": ["Action", "Adventure", "Fantasy", "Sci-Fi", "IMAX"] }
```

Формат коротких строк вместо одного большого JSON использован для экономии памяти и ускорения индексации. В таком формате ES не требуется постоянно держать в памяти, в какой индекс нужно отправлять каждый из документов и в какой части массива он находится сейчас.

Загрузка:

```bash
hcurl -XPUT 192.168.88.242:9200/_bulk?pretty --data-binary @movies.json
```

Если какие-то из документов уже есть в индексе, может прийти ошибка:

```json
{
    "create" : {
        "_index" : "movies",
        "_type" : "_doc",
        "_id" : "135569",
        "status" : 409,
        "error" : {
            "type" : "version_conflict_engine_exception",
            "reason" : "[135569]: version conflict, document already exists (current version [1])",
            "index_uuid" : "76FZgebZSY-mrLvmNGe_zg",
            "shard" : "0",
            "index" : "movies"
        }
    }
}
```



# Импорт в индекс


Альяс hcurl для curl (размещён в ~/.local/bin и назначен исполняемым через `chmod +x`):

```bash
#!/bin/bash
/usr/bin/curl -H "Content-Type: application/json" "$@"
```

Командой `source .profile` можно сразу загрузить обновленный файл.

Воспользуемся маппингом для создания индекса:

```json
hcurl -XPUT 192.168.88.242:9200/movies -d '
{
    "mappings": {
        "properties": {
            "year": {"type": "date"}
        }
    }
}
'
```

А затем импортируем фильм в индекс:

```json
hcurl -XPUT 192.168.88.242:9200/movies/_doc/109487 -d '
{
    "genre": ["IMAX", "Sci-Fi"],
    "title": "Interstellar",
    "year": 2014
}
'
```

Как видно, в маппингах мы указали лишь `year`, остальные поля определятся эластиком сами.

При поиске можно использовать год так же, как он был вписан:

```json
GET movies/_search
{
  "query": {
    "match_phrase": {
      "year": "2014"
    }
  }
}

//или напрямую

GET movies/_doc/109487
```

Ответ:

```json
{
    "_index" : "movies",
    "_type" : "_doc",
    "_id" : "109487",
    "_score" : 1.0,
    "_source" : {
        "genre" : [
        "IMAX",
        "Sci-Fi"
        ],
        "title" : "Interstellar",
        "year" : 2014
    }
}
```

Вывести всё содержимое индкса:

```json
GET movies/_search?pretty
```

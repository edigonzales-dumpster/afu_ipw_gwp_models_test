# gwp-models

```
docker run --rm --name edit-db -p 54321:5432 --hostname primary \
-e PG_DATABASE=edit -e PG_LOCALE=de_CH.UTF-8 -e PG_PRIMARY_PORT=5432 -e PG_MODE=primary \
-e PG_USER=admin -e PG_PASSWORD=admin \
-e PG_PRIMARY_USER=repl -e PG_PRIMARY_PASSWORD=repl \
-e PG_ROOT_PASSWORD=secret \
-e PG_WRITE_USER=gretl -e PG_WRITE_PASSWORD=gretl \
-e PG_READ_USER=ogc_server -e PG_READ_PASSWORD=ogc_server \
sogis/oereb-db:latest
```

## Ein Modell

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin --defaultSrsCode 2056 --nameByTopic --models Sonderbauwerke --modeldir ".;http://models.geo.admin.ch" --dbschema sonderbauwerke --schemaimport
```

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin --defaultSrsCode 2056 --nameByTopic --models Sonderbauwerke --modeldir ".;http://models.geo.admin.ch" --dbschema sonderbauwerke --export fubar.xtf
```

```
java -jar /Users/stefan/apps/ilivalidator-1.11.8/ilivalidator-1.11.8.jar fubar.xtf
```

## Zwei Modelle

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin --defaultSrsCode 2056 --nameByTopic --models SBW --modeldir ".;http://models.geo.admin.ch" --dbschema sbw --schemaimport
```

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin --defaultSrsCode 2056 --nameByTopic --models LK --modeldir ".;http://models.geo.admin.ch" --dbschema lk --schemaimport
```

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin --defaultSrsCode 2056 --nameByTopic --models SBW --modeldir ".;http://models.geo.admin.ch" --dbschema sbw --export sbw.xtf
```

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin --defaultSrsCode 2056 --nameByTopic --models LK --modeldir ".;http://models.geo.admin.ch" --dbschema lk --export lk.xtf
```

```
java -jar /Users/stefan/apps/ilivalidator-1.11.8/ilivalidator-1.11.8.jar lk.xtf sbw.xtf
```

```
Error: line 25: SBW.Sonderbauwerke.Sonderbauwerk: tid 2: The value of the attribute egrid of SBW.Sonderbauwerke.Sonderbauwerk was not found in the condition class.
```

## Zwei Modell mit View
```
java -jar /Users/stefan/apps/ilivalidator-1.11.8/ilivalidator-1.11.8.jar --config config.toml lk.xtf sbw.xtf
```

```
Error: line 25: SBW.Sonderbauwerke.Sonderbauwerk: tid 2: The value of the attribute egrid of SBW.Sonderbauwerke.Sonderbauwerk was not found in the condition class.
```
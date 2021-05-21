# adozona-couchbase-import-export-service

Az Adózóna Couchbase import-export szolgáltatás éles környezetben futó példányának a kódja. <br/>

A tényleges forráskód a `hvghu solution`-ben található:

- [https://git.hvg.hu/projects/HVG/repos/hvghu/browse/src/CouchbaseImportExport](https://git.hvg.hu/projects/HVG/repos/hvghu/browse/src/CouchbaseImportExport)

A szolgáltatás célja az, hogy az **A** `couchbase`-ből átmozgasson adatok a **B** `couchbase`-be.
<br><br>


----------


### Adózóna kalkulátor admin
Az Adózóna kalkulátor admin minden bucket esetén egységes szervereket használ.

**couchbase szerverek:**

- `http://192.168.1.221:8091`
- `http://192.168.1.222:8091`

**bucketek:**

- `api-data`
- `cms-data`
- `hvg-article`
- `default`


----------


### Adózóna kalkulátor site
Az Adózóna kalkulátor oldal viszont bucket-enként külön szervert

**api-data bucket:**

- `http://taxcb-01.hvgonline.hu:8091`
- `http://taxcb-02.hvgonline.hu:8091`
- `http://taxcb-03.hvgonline.hu:8091`

**cms-data bucket**

- `http://192.168.1.221:8091`
- `http://192.168.1.222:8091`
- `http://192.168.1.223:8091`
- `http://192.168.1.224:8091`

... (a teljes lista a kalkulátor projekt configjaiban látható ([ITT](https://git.hvg.hu/projects/TAX/repos/adozona/browse/src/Adozona.Site)))

A lényeg, hogy ezáltal az `api-data bucket` szervere a két alkalmazás esetén eltér, márpedig az a `bucket` tartalmazza a kalkulátorokat. Ezért van szükség, hogy a `http://192.168.1.221 - 222`-ről átmozgassa a `http://taxcb-01-02-03.hvgonline.hu`-ra az adatokat, mert a `site`-nál az `api-data bucket` ott található.
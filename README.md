# dlfa-188_v1-indexer-http-requests-xml

See [DLFA-188: v1 indexer: set up a GitHub repo containing all Solr HTTP requests for a full indexing job](https://jira.nyu.edu/browse/DLFA-188)

---

## How this repo was created

At the root of [dlfa\-188\_v1\-indexer\-http\-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests), `TARGET_DIR` was set to the absolute path to the root of this repo, and then this for-loop was run:

```shell
for f in $( cat index.txt )
do 
        repository=$( dirname $( dirname $f ) )
        eadid=$( basename $( dirname $f ) )
        filename=$( basename $f | sed 's/\.txt$/.xml/' )
        targetDirectory=$TARGET_DIR/$repository/$eadid/
        mkdir -p $targetDirectory
        targetFile=$TARGET_DIR/$repository/$eadid/$filename
        perl -0pe 's/^POST.*\r\n\r\n//ms' $f | xmllint --format - > $targetFile
done
```

---

## [dlfa-188\_v1-indexer-http-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/) commit

[dlfa-188\_v1-indexer-http-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/) commit used: [206386a464e2b1280021571cbd4e73218990c26c](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/commit/206386a464e2b1280021571cbd4e73218990c26c)

## How _index.txt_ was created

```shell
find http-requests -type f | sort > index.txt
```

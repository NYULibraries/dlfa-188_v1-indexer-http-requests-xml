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

[dlfa-188\_v1-indexer-http-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/) commit used: n/a because this batch has to be committed and pushed in pieces to work around the GitHub 2GB push limit.  The batch is based on [f4ef0e201f8514f5461f4e973f97477da8d0fbfc](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/commit/f4ef0e201f8514f5461f4e973f97477da8d0fbfc).  Once everything has been committed, this README.md will be updated to reflect that the two repos are fully sync'ed.

## How _index.txt_ was created

```shell
find http-requests -type f | sort > index.txt
```

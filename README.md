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

[dlfa-188\_v1-indexer-http-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/) commit used: [95cba332e358281ce682d48472a0d35e36214ea0](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests/commit/95cba332e358281ce682d48472a0d35e36214ea0)

Note that this is not the exact commit that the generation job was run with, but it is equivalent.  Originally the entire set of HTTP request files were added to [dlfa\-188\_v1\-indexer\-http\-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests) in a single commit, and the generation job for this repo was run off of that.  Due to GitHub limits, it was necessary to start over and break up adding of the HTTP requests into smaller commits.  The commit identified above should be equivalent in terms of the state of _http-requests/_ in [dlfa\-188\_v1\-indexer\-http\-requests](https://github.com/NYULibraries/dlfa-188_v1-indexer-http-requests) when the generation job ran.

## How _index.txt_ was created

```shell
find http-requests -type f | sort > index.txt
```

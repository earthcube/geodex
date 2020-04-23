# Running the Geodex / GeoCODES services

## Prerequisits
* Assumes Ubuntu LTS
* Go (`apt-get install golang`)
* Docker


## Checkout source
```
mkdir -p ~/go/src/earthcube.org/Project418/
cd go/src/earthcube.org/Project418
git clone https://github.com/craig-willis/gleaner -b eco
git clone https://github.com/craig-willis/services -b eco
git clone https://github.com/craig-willis/webui -b eco
git clone https://github.com/craig-willis/webUI2 -b eco
```


## Building 


```
cd gleaner
make gleaner
docker build -t you/gleaner -f build/Dockerfile .
```

```
cd services
make linux
docker build -t you/p418services -f build/Dockerfile .
```

```
cd webui
make webui
docker build -t you/p418webui -f build/Dockerfile .
```

```
cd webUI2
docker build -t you/p418webui2 .
```


## Running 

For Gleaner, see the ECO [README](https://github.com/craig-willis/gleaner/blob/eco/docs/starterpack/README.md).

Create /etc/hosts entry for `geodex.local.earthcube.org`:
```
127.0.0.1  geodex.local.earthcube.org
``` 

To run the web services in this repo:
```
docker-compose up
```

If running on a VM, forward ports 8080 and 80:
```
ssh -L 8080:localhost:8080 -L 80:localhost:80  you@vm
```

Test the following URLs:
* http://geodex.local.earthcube.org/ Geodex main landing page
* http://geodex.local.earthcube.org/geocodes/ Geocodes text/spatial search
* http://geodex.local.earthcube.org/geocodes/textSearch.html Text search for IEDA only. Search for "coral" ([api call](http://geodex.local.earthcube.org/api/v1/textindex/search?q=coral&s=0&i=ieda&n=10))
* http://geodex.local.earthcube.org/geocodes/spatialSearch.html Search for [-125.40664,44.4617] ([api call](* http://geodex.local.earthcube.org/api/v1/spatial/search/object?geowithin={%22type%22:%22FeatureCollection%22,%22features%22:[{%22type%22:%22Feature%22,%22geometry%22:{%22type%22:%22Point%22,%22coordinates%22:[-125.40664,44.4617]},%22properties%22:{}}]}))



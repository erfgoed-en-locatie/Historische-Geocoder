#API calls

##user story 1: plaatsnamen standaardiseren

###urls en parameters:

`api/search/q=Aelst%20by%20Eyndoven`

Zoek PiTs met naam 'Aelst by Eyndoven'

`api/search/q=Milligen&type=place`

Zoek PiTs met naam 'Milligen' van het type 'place'. Er is ook een gemeente waarvoor die naam gebruikt werd, maar die willen we niet.

`api/search/q=Milligen&type=municipality`

Zoek PiTs met naam 'Milligen' van het type 'municipality'. Er is ook een plaats met die naam, maar die willen we niet - we standaardiseren dit keer een lijst met gemeenten.

`api/search/q=Weerd&liesIn=Limburg`

Zoek PiTs waarvoor de naam 'Weerd' gebruikt werd en die binnen de provincie Limburg liggen. Voor 1700 werd het Brabantse Valkenswaard nog 'Weerd' genoemd.

`api/search/q=Weerd&year=1600`

Zoek PiTs waarvoor de naam 'Weerd' gebruikt werd in 1600. Na 1700 ging het Brabantse Weerd zich Valkenswaard noemen om zich te onderscheiden van het Limburgse Weert.

`api/search/q=Broek&source=verdwenen-dorpen`

We willen alleen binnen verdwenen dorpen zoeken, en dus wel het verdwenen Broek bij Strijen vinden, maar niet Broek in Waterland of Broek 

#JSON output

- Als GeoJSON
- Elke Feature is een __klont__, d.w.z. een concept als bijv. de plaats 'Naarden'
- Een klont kan verschillende pits hebben
- Pits en relaties zijn opgenomen in properties
- De Geometry van een Feature is een GeometryCollection die meerdere geometrieën kan bevatten
- Bij elke pit is aangegeven of die een geometrie heeft en zo ja, welke geometrie in de GeometryCollection dat dan wel niet mag zijn

Onderstaande JSON is (deel van) het antwoord op een zoekactie naar 'Naarden'. Gevonden zijn de klont 'plaats Bussum' vanwege het toponiem 'Bussem bij Naarden' en de klont 'gemeente Naarden'.

De klont 'plaats Bussum' bevat een geonames, een tgn en een simon hart pit. De klont 'gemeente Naarden' bevat twee gemeentegeschiedenis pits, eentje met de grenzen tot 1817 en eentje met de grenzen van daarna.


```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "type": "hg:Place",
        "pits": [
          {
            "source": "geonames",
            "name": "Bussum",
            "type": "hg:Place",
            "id": "geonames/2758064",
            "uri": "http://www.geonames.org/2758064/",
            "geometryIndex": 0
          },
          {
            "source": "simon-hart",
            "name": "Bussem bij Naarden",
            "usedFrom": ["1600","1800"],
            "usedUntil": ["1600","1800"],
            "type": "hg:Place",
            "id": "simon-hart/3185",
            "matchedQuery": true  ,
            "geometryIndex": -1
          },
          {
            "source": "tgn",
            "name": "Bussum",
            "type": "hg:Place",
            "id": "tgn/1047690",
            "uri": "http://vocab.getty.edu/tgn/1047690",
            "geometryIndex": 1
          }
        ],
        "relations": [
          {
            "from": "simon-hart/3185",
            "to": "geonames/2758064",
            "label": "hg:isUsedFor"
          },
          {
            "from": "geonames/2758064",
            "to": "tgn/1047690",
              "label": "hg:sameAs"
          }
        ]
      },
      "geometry": {
        "type": "GeometryCollection",
        "geometries": [
          {
            "type": "Point",
            "coordinates": [5.161111, 52.273333]
          },
          {
            "type": "Point",
            "coordinates": [5.2, 52.283333]
          }
        ]
      }
    },
    {
      "type": "Feature",
      "properties": {
        "type": "hg:Municipality",
        "pits": [
          {
            "source": "gemeentegeschiedenis",
            "name": "Naarden",
            "startDate": [null,null],
            "endDate": [1817,1817],
            "type": "hg:Municipality",
            "id": "gemeentegeschiednis/453",
            "uri": "http://www.gemeentegeschiedenis.nl/gemeentenaam/Naarden",
            "matchedQuery": true  ,
            "geometryIndex": 0
          },
          {
            "source": "gemeentegeschiedenis",
            "name": "Naarden",
            "startDate": [1817, 1817],
            "endDate": [null,null],
            "type": "hg:Municipality",
            "id": "gemeentegeschiednis/453",
            "uri": "http://www.gemeentegeschiedenis.nl/gemeentenaam/Naarden",
            "matchedQuery": true,
            "geometryIndex": 1
          }
        ],
        "relations": [
          {
            "from": "simon-hart/3185",
            "to": "geonames/2758064",
            "label": "hg:isUsedFor"
          },
          {
            "from": "geonames/2758064",
            "to": "tgn/1047690",
              "label": "hg:sameAs"
          }
        ]
      },
      "geometry": {
        "type": "GeometryCollection",
        "geometries": [
          {"type":"Polygon","coordinates":[[[5.164649,52.302723],[5.170513,52.302644],[5.207283,52.309896],[5.225614,52.309652],[5.228434,52.300129],[5.213642,52.296334],[5.209966,52.299114],[5.192818,52.298099],[5.187431,52.290001],[5.194482,52.286238],[5.193484,52.279765],[5.187336,52.278406],[5.183096,52.276422],[5.159284,52.274755],[5.158122,52.270148],[5.169415,52.263021],[5.187173,52.266203],[5.18547,52.264079],[5.176964,52.253463],[5.160784,52.25544],[5.149797,52.255958],[5.139676,52.258813],[5.143277,52.269785],[5.141492,52.274815],[5.144695,52.278507],[5.146728,52.281926],[5.141443,52.283623],[5.137375,52.277323],[5.124772,52.277565],[5.106421,52.283185],[5.103339,52.283807],[5.095244,52.28918],[5.097426,52.291612],[5.107803,52.29649],[5.098567,52.296468],[5.094262,52.304726],[5.098203,52.307432],[5.105272,52.302596],[5.120035,52.31009],[5.113407,52.314839],[5.12641,52.323047],[5.134659,52.316953],[5.158921,52.304689],[5.164649,52.302723]]]
          },
          {"type":"Polygon","coordinates":[[[5.098203,52.307432],[5.105272,52.302596],[5.120035,52.31009],[5.113407,52.314839],[5.12641,52.323047],[5.134659,52.316953],[5.158921,52.304689],[5.164649,52.302723],[5.170513,52.302644],[5.207283,52.309896],[5.225614,52.309652],[5.228434,52.300129],[5.213642,52.296334],[5.209966,52.299114],[5.192818,52.298099],[5.187431,52.290001],[5.194482,52.286238],[5.193484,52.279765],[5.187336,52.278406],[5.183096,52.276422],[5.181464,52.280643],[5.176917,52.281624],[5.170036,52.280263],[5.16196,52.283484],[5.158457,52.280871],[5.144695,52.278506],[5.146728,52.281926],[5.141443,52.283623],[5.137375,52.277323],[5.124772,52.277565],[5.106421,52.283185],[5.103339,52.283807],[5.095244,52.28918],[5.097426,52.291612],[5.107803,52.29649],[5.098567,52.296468],[5.094262,52.304726],[5.098203,52.307432]]]}
        ]
      }
    }
  ]
}

```



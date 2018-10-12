# ReconKB
ReconKB aims to develop a recon tool for pentesting which will automatically search the web for information about a target. 
The tool will then try to receive as much information about the target as possible and create a RDF knowledge base (see. RDF and SPARQL) which further on can be questioned on the fly of the further pentest. 

## KB scheme
The knowledge base scheme will be mostly generic, but will aim to use the following predefined schmes:

* FOAF
* DBpedia
* Dublin Core
* rdfs
* owl

The initial information scheme will look like the following for a company :

```rdf
@prefix rkbr : <http://reconkb.org/resource/>
@prefix rkbp : <http://reconkb.org/property/>

rkbr:target rkbp:label targetNameOrSuch; 
            rkbp:term additionalTermToSearch; 
            rkbp:website website;
            rdfs:class dbp:company.
```

## How does ReconKB work
ReconKB will receive initial information (such as the company name). 
The input will be `ReconKB` for example then reconKB will search for ReconKB and tries to receive a website, social media etc. Afterwards it will check all available meta data. Further on it will parse all documents, news etc. available and uses NLP on it to gather these informations. 

the output may look like
```rdf
@prefix rkbr : <http://reconkb.org/resource/>
@prefix rkbp : <http://reconkb.org/property/>

...

rkbr:ReconKB rkbp:label ReconKB; 
            rkbp:term "recon tool";
            rkbp:term "nlp";
            rkbp:website https://github.com/TortugaAttack/ReconKB;
            rdfs:class dbr:software.
            rkbp:developer rkbr:TortugaAttack;
            rkpb:startDate "12.10.2018";
            rkbp:document rkbr:doc1;
            ... # all information/triples gathered through the document
            
rkbr:doc1   rkbp:label ....
            rkbp:origin http://reconkb.org/docs/doc1;
            rkbp:text "...";
            rkbp:terms ["term1", "term2",...].
            
rkbr:TortugAttack rkbp:label ...
            rkbp:twitter ....
            ...
``` 

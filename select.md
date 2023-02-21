#### PREFIX
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX m: <http://www.semanticweb.org/lihekun/SANGUO#>

##### hasAncestor 有祖先
```
sanguo:hasAncestor(?a, ?b) -> sqwrl:select(?b, ?a)
```

##### hasAncestor 曹操的老婆们
```
sanguo:Person(sanguo:CaoCao) ^ sanguo:isSpouseOf(sanguo:CaoCao, ?b) -> sqwrl:select(?b)
```

##### 

##### Age
```
SELECT ?v ?y
 WHERE {
?v m:birthYear ?y .
FILTER(?y > 0)
 } ORDER BY ?y
```

##### Leader
```
SELECT ?leader ?subordinate
 WHERE {
?leader m:hasVassal ?subordinate .
 }
```

##### 
```
SELECT ?name ?birthYear
	WHERE { ?x sg:familyName ?name .
	?x sg:birthYear ?birthYear . 
	FILTER(?name = 'Cao')
 }
```
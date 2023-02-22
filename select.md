#### PREFIX
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX m: <http://www.semanticweb.org/lihekun/SANGUO#>

1. hasAncestor 有祖先
```
sanguo:hasAncestor(?a, ?b) -> sqwrl:select(?b, ?a)
```

2. hasVassal 曹操的老婆们
```
sanguo:Person(sanguo:CaoCao) ^ sanguo:isSpouseOf(sanguo:CaoCao, ?b) -> sqwrl:select(?b)
```

3. Leader
```
SELECT ?leader ?subordinate
 WHERE {
?leader sg:hasVassal ?subordinate .
 }
```

4. 所有和曹操有关系的人
```
SELECT ?e ?r
 WHERE {
?e ?r sg:CaoCao .
 }
```

5. birthYear
```
SELECT ?v ?y
 WHERE {
?v m:birthYear ?y .
FILTER(?y > 0)
 } ORDER BY ?y
```

6. 姓曹的人
```
SELECT ?name ?birthYear
	WHERE { ?x sg:familyName ?name .
	?x sg:birthYear ?birthYear . 
	FILTER(?name = 'Cao')
 }
```

7. 有儿子的人
```
sanguo:hasChild(?father, ?son) ^ sanguo:isFatherOf(?son, ?c) -> sqwrl:select(?father, ?son)
```
8. 谁是谁的叔叔
```

```
9. 超过一个子嗣的人
10. 有过1个以上老公的人
11. 和曹操有血缘关系又是下属的人
12. 有多个老婆的
13. 所有的母亲
14. 曹操和曹真有几种关系
15. 谁是谁的爷爷
16. fatherInLaw的人
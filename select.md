#### PREFIX
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX m: <http://www.semanticweb.org/lihekun/SANGUO#>

1. hasAncestor 有祖先
```
sg:hasAncestor(?a, ?b) -> sqwrl:select(?b, ?a)
```

2. hasVassal 曹操的老婆们
```
sg:Person(sanguo:CaoCao) ^ sg:isSpouseOf(sanguo:CaoCao, ?b) -> sqwrl:select(?b)
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
sg:hasParent(?a, ?b) ^ sg:hasBrother(?b, ?c) -> sqwrl:select(?a, ?c)
```
9. 超过一个孩子的人
```
SELECT ?object (COUNT(?child) AS ?c)
	WHERE {
?object sg:hasChild ?child .

} GROUP BY ?object
HAVING (?c > 1)
```
10. 有过1个以上老公的人
```
sg:Woman(?a) ^ sg:hasSpouse(?a, ?b)  .  sqwrl:makeSet(?g, ?b) ^ sqwrl:groupBy(?g, ?a)  .  sqwrl:size(?n, ?g) ^ swrlb:greaterThan(?n, 1) -> sqwrl:select(?a, ?b)
```
11. 和曹操有血缘关系又是下属的人
```
sg:hasVassal(sg:CaoCao, ?x) ^ sg:hasBloodrelation(?x, sg:CaoCao) -> sqwrl:select(?x)
```
12. 有多个老婆的
```
sg:Man(?a) ^ sg:hasSpouse(?a, ?b)  .  sqwrl:makeSet(?g, ?b) ^ sqwrl:groupBy(?g, ?a)  .  sqwrl:size(?n, ?g) ^ swrlb:greaterThan(?n, 1) -> sqwrl:select(?a, ?b)
```
13. 所有的母亲
```
sg:isMotherOf(?a, ?b) -> sqwrl:select(?a)
```
14. 谁是谁的爷爷
```
sg:hasParent(?a, ?b) ^ sg:hasParent(?b, ?c) ^ sg:Man(?c) -> sqwrl:select(?c, ?a)
```
15. FatherInLaw
```
sg:hasSpouse(?a, ?b) ^ sg:hasParent(?b, ?p) ^ sg:Man(?p) -> sqwrl:select(?a, ?p)
```

16. 按年龄排序
```
SELECT ?object ?t
WHERE
{
?object sg:birthYear ?year .
?object sg:dieYear ?die .
BIND (
(?die - ?year) AS ?t
)
} ORDER BY DESC (?t)
```
# Gallica-Onstage

Taks for the Onstage Working Group to link Gallica URIs to Onstage ones. 

(Run `pip install -U -r requirements.txt`)


## BNF SPARQL Endpoint
<https://data.bnf.fr/sparql>

### QUERIES

Gallica URIs where Moliere has a role (creator or contributor)

```bash
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdarelationships: <http://rdvocab.info/RDARelationshipsWEMI/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT DISTINCT(?URLGallica) WHERE { 
  	?w  rdarelationships:electronicReproduction ?URLGallica;
       ?p ?o.
  ?o ?r <http://data.bnf.fr/ark:/12148/cb11916418p#about>.
  
} 

```

Gallica URIs where Moliere has a role (creator or contributor) with tiles, lables and dates 

```bash
PREFIX dcterm: <http://purl.org/dc/terms/>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdarelationships: <http://rdvocab.info/RDARelationshipsWEMI/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT DISTINCT ?role ?URLGallica ?title ?label ?date 
WHERE { 
  	?rdf_URI  rdarelationships:electronicReproduction ?URLGallica;
       ?p ?bnf_URI.
   ?bnf_URI ?role <http://data.bnf.fr/ark:/12148/cb11916418p#about>.
  
  OPTIONAL {?rdf_URI dcterms:title ?title.} 
  OPTIONAL {?bnf_URI dcterms:title ?title.} 
  OPTIONAL {?rdf_URI rdfs:label ?label .}
  OPTIONAL {?bnf_URI rdfs:label ?label .}
  OPTIONAL {?rdf_URI dcterms:date ?date.} 
  OPTIONAL {?bnf_URI dcterms:date ?date.} 
     
  
} #limit 100
```


## Ontology Named Graph

version 2020Q4: </br> <<https://data.goldenagents.org/datasets/ufab7d657a250e3461361c982ce9b38f3816e0c4b/ga_ontology_20201216>>

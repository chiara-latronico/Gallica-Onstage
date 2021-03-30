# Gallica-Onstage

Task for the Onstage Working Group - </br>
Linking the Gallica's URIs where Molière is creator or contributor to the Onstage's URIs  

### BNF SPARQL Endpoint
<https://data.bnf.fr/sparql>

### QUERIES

Gallica URIs where Molière has a role

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

Gallica URIs where Molière has a role with tiles, lables and dates 

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

CONSTRUCT RDF dataset where the Gallica URIs (where Molière has a role) have type CreativeWork and contains titles, labels and dates


```bash
PREFIX dcterm: <http://purl.org/dc/terms/>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdarelationships: <http://rdvocab.info/RDARelationshipsWEMI/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX schema: <http://schema.org/>
CONSTRUCT {
?URLGallica rdf:type schema:CreativeWork ;
            dcterms:title ?title ; 
            rdfs:label ?label ;
            dcterms:date ?date.} 

WHERE { 
  	?rdf_URI  rdarelationships:electronicReproduction ?URLGallica;
        ?p ?bnf_URI.
        ?bnf_URI ?role <http://data.bnf.fr/ark:/12148/cb11916418p#about>.
  
  OPTIONAL {?bnf_URI dcterms:title ?title.} 
  OPTIONAL {?bnf_URI rdfs:label ?label .}
  OPTIONAL {?bnf_URI dcterms:date ?date.} 
  
  OPTIONAL {?rdf_URI dcterms:title ?title.} 
  OPTIONAL {?rdf_URI rdfs:label ?label .}
  OPTIONAL {?rdf_URI dcterms:date ?date.}  
  
} #limit 100
```

### CONSTRUCT DATASET 

The RDF dataset made out of the CONSTRCT query can be found here: </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/Moliere-in-Gallica.ttl> 


### Lenticular Lens 
Link to the Lenticular Lens job where the Gallica URIs are matched against the Onstage ones based on different algorithms: </br>
<https://recon.diginfra.net/?job_id=929b6be5c54024773a9c0b29f3206861>

## FOLLOW UP
Anlysis of LENS #1, with label "UNION 2:: TITLES + EXACT DATES" 


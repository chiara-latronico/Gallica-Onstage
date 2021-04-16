# Golden Agents- Linking Gallica to Onstage

Golden Agents task for the Onstage Working Group - </br>
Linking the Gallica's URIs where the author Molière has the role of creator or contributor, to the Onstage's URIs  

### BNF SPARQL Endpoint
<https://data.bnf.fr/sparql>

### Queries

1. Gallica URIs where Molière has a role. (Molière URI: <<http://data.bnf.fr/ark:/12148/cb11916418p#about>> ) 

```bash
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdarelationships: <http://rdvocab.info/RDARelationshipsWEMI/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT DISTINCT ?URLGallica 
WHERE { 
  	?rdf_URI  rdarelationships:electronicReproduction ?URLGallica;
        ?p ?bnf_URI.
        ?bnf_URI ?role <http://data.bnf.fr/ark:/12148/cb11916418p#about>.
} 

```

2. Gallica URIs where Molière has a role with tiles, lables and dates 

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
  
  OPTIONAL {?bnf_URI dcterms:title ?title.} 
  OPTIONAL {?bnf_URI rdfs:label ?label .}
  OPTIONAL {?bnf_URI dcterms:date ?date.} 
  
  OPTIONAL {?rdf_URI dcterms:title ?title.} 
  OPTIONAL {?rdf_URI rdfs:label ?label .}
  OPTIONAL {?rdf_URI dcterms:date ?date.}     
} 
```

3. CONSTRUCT RDF dataset where the Gallica URIs (where Molière has a role) have type CreativeWork and contain titles, labels and dates


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
} 
```

### CONSTRUCT Dataset  

The Gallica subset in RDF (made from the CONSTRUCT query) can be found here: </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/Moliere-in-Gallica.ttl> 


### Lenticular Lens 
Link to the Lenticular Lens job where the Gallica URIs are matched against the Onstage URIs using different algorithms: </br>
<https://recon.diginfra.net/?job_id=929b6be5c54024773a9c0b29f3206861>

### Follow up
1. [X] Validation of linkset LENS #1, labelled "UNION 2:: TITLES + EXACT DATES" ; {ongoing} </br>
2. [ ] Export of linkset LENS #1 ; </br>
3. [ ] Publish linkset LENS #1 in Timbuctoo ;  </br>
4. [ ] Data integration form linkset LENS #1 to the Onstage database . </br>



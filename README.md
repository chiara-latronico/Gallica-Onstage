# Golden Agents- Linking Gallica to Onstage

Golden Agents task for the Onstage Working Group - </br>
Linking the Gallica's URIs where the author Molière has the role of creator or contributor, to the Onstage URIs  

### BNF SPARQL Endpoint
<https://data.bnf.fr/sparql>

### Queries

1. Gallica URIs where Molière has a role. (Molière URI: <<http://data.bnf.fr/ark:/12148/cb11916418p#about>> ) 

```SPARQL
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

2. Gallica URIs where Molière has a role with titles, labels, dates and publishers

```SPARQL
PREFIX dcterm: <http://purl.org/dc/terms/>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdarelationships: <http://rdvocab.info/RDARelationshipsWEMI/>
PREFIX dcterms: <http://purl.org/dc/terms/>
SELECT DISTINCT ?role ?URLGallica ?title ?label ?date ?publisher ?publishersName
WHERE { 
  	?rdf_URI  rdarelationships:electronicReproduction ?URLGallica;
        ?p ?bnf_URI.
        ?bnf_URI ?role <http://data.bnf.fr/ark:/12148/cb11916418p#about>.
  
  OPTIONAL {?bnf_URI dcterms:title ?title.} 
  OPTIONAL {?bnf_URI rdfs:label ?label .}
  OPTIONAL {?bnf_URI dcterms:date ?date.} 
  OPTIONAL {?bnf_URI dcterms:publisher ?publisher.} 
  OPTIONAL {?bnf_URI <http://rdvocab.info/Elements/publishersName> ?publishersName.}
  
  OPTIONAL {?rdf_URI dcterms:title ?title.} 
  OPTIONAL {?rdf_URI rdfs:label ?label .}
  OPTIONAL {?rdf_URI dcterms:date ?date.}   
  OPTIONAL {?rdf_URI dcterms:publisher ?publisher.} 
  OPTIONAL {?rdf_URI <http://rdvocab.info/Elements/publishersName> ?publishersName.} 
} 
```

3. CONSTRUCT RDF dataset where the Gallica URIs (where Molière has a role) have type CreativeWork and contain titles, labels, dates and publishers


```SPARQL
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
            dcterms:date ?date ;
            dcterms:publisher ?publisher ;
    	    <http://rdvocab.info/Elements/publishersName> ?publishersName.} 

WHERE { 
  	?rdf_URI  rdarelationships:electronicReproduction ?URLGallica;
        ?p ?bnf_URI.
        ?bnf_URI ?role <http://data.bnf.fr/ark:/12148/cb11916418p#about>.
  
  OPTIONAL {?bnf_URI dcterms:title ?title.} 
  OPTIONAL {?bnf_URI rdfs:label ?label .}
  OPTIONAL {?bnf_URI dcterms:date ?date.} 
  OPTIONAL {?bnf_URI dcterms:publisher ?publisher.} 
  OPTIONAL {?bnf_URI <http://rdvocab.info/Elements/publishersName> ?publishersName.}
  
  OPTIONAL {?rdf_URI dcterms:title ?title.} 
  OPTIONAL {?rdf_URI rdfs:label ?label .}
  OPTIONAL {?rdf_URI dcterms:date ?date.} 
  OPTIONAL {?rdf_URI dcterms:publisher ?publisher.} 
  OPTIONAL {?rdf_URI <http://rdvocab.info/Elements/publishersName> ?publishersName.} 

}  
```

### CONSTRUCT Dataset  

The Gallica subset in RDF (made from the CONSTRUCT query) can be found here: </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/CONSTRUCT-Moliere-in-Gallica-titles-labels-dates-publishers.ttl>


### Lenticular Lens 
Link to the Lenticular Lens job where the Gallica URIs are matched against the Onstage URIs using different algorithms: </br>
<https://recon.diginfra.net/?job_id=929b6be5c54024773a9c0b29f3206861>

### LinkSets
1. Linksets in CSV exported directly from Lenticular Lens can be found here: </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/skos_close_match_LL.csv> </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/skos_related_match_LL.csv>

2. Linksets in Excell (enriched and normalized with names of publishers) can be found here: </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/Skos_close_match.xlsx> </br>
<https://github.com/chiara-latronico/Gallica-Onstage/blob/main/Skos_related_match.xlsx>

### Follow up
1. [X] Validation of linkset #8 </br>
2. [ ] Export of linkset in RDF linkset #8 ; </br>
3. [ ] Publish linkset #8 in Timbuctoo ;  </br>
4. [ ] Syc linkset #8 in Virtuoso .  </br>




# Football Domain Ontology

## Domain Description
This ontology models the football (soccer) domain, representing key concepts such as players, teams, matches, competitions, venues, and officials. The ontology enables semantic querying and reasoning about football-related information.

## Namespaces Used

- **RDF**: http://www.w3.org/1999/02/22-rdf-syntax-ns# - Used for basic RDF constructs
- **RDFS**: http://www.w3.org/2000/01/rdf-schema# - Used for class hierarchies and property domains/ranges
- **OWL**: http://www.w3.org/2002/07/owl# - Used for advanced ontology features
- **XSD**: http://www.w3.org/2001/XMLSchema# - Used for data types
- **DC**: http://purl.org/dc/elements/1.1/ - Used for document metadata
- **FOAF**: http://xmlns.com/foaf/0.1/ - Used for person and organization concepts
- **SKOS**: http://www.w3.org/2004/02/skos/core# - Used for concept classification

## Classes and Subclasses

### Person
- Player
  - Goalkeeper
  - Defender
  - Midfielder
  - Forward
- Coach
- Referee
- TeamStaff

### Organization
- Team
  - ClubTeam
  - NationalTeam
- Federation

### Event
- Match
- Tournament
- Training

### Place
- Stadium
- TrainingGround

### FootballObject
- Ball
- Goal
- Card
  - YellowCard
  - RedCard

## Properties

### Object Properties
- playsFor (domain: Player, range: Team)
- coaches (domain: Coach, range: Team)
- participatesIn (domain: Team, range: Tournament)
- playedAt (domain: Match, range: Stadium)
- hasHomeTeam (domain: Match, range: Team)
- hasAwayTeam (domain: Match, range: Team)
- refereesMatch (domain: Referee, range: Match)
- isPartOf (domain: Match, range: Tournament)
- hasPlayer (domain: Team, range: Player)
- performsAction (domain: Player, range: Action)
- receivesCard (domain: Player, range: Card)

### Data Properties
- playerNumber (domain: Player, range: xsd:integer)
- playerPosition (domain: Player, range: xsd:string)
- birthDate (domain: Person, range: xsd:date)
- teamName (domain: Team, range: xsd:string)
- matchDate (domain: Match, range: xsd:dateTime)
- goalsScored (domain: Player, range: xsd:integer)
- stadiumCapacity (domain: Stadium, range: xsd:integer)
- nationality (domain: Person, range: xsd:string)

## SPARQL Queries

### Query 1: Find all forwards who scored more than 10 goals
```sparql
PREFIX fb: <http://www.semanticweb.org/football-ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?player ?name ?goals ?team
WHERE {
  ?player rdf:type fb:Forward .
  ?player fb:playerName ?name .
  ?player fb:goalsScored ?goals .
  ?player fb:playsFor ?team .
  ?team fb:teamName ?teamName .
  FILTER (?goals > 10)
}
ORDER BY DESC(?goals)
```
This query finds all forward players who have scored more than 10 goals, ordered by goal count descending.

### Query 2: Find stadiums with capacity over 50,000 and the teams that play there
```sparql
PREFIX fb: <http://www.semanticweb.org/football-ontology#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?stadium ?name ?capacity ?team ?teamName
WHERE {
  ?stadium rdf:type fb:Stadium .
  ?stadium fb:stadiumName ?name .
  ?stadium fb:stadiumCapacity ?capacity .
  ?team fb:homeStadium ?stadium .
  ?team fb:teamName ?teamName .
  FILTER (?capacity > 50000)
}
ORDER BY DESC(?capacity)
```
This query retrieves all stadiums with a capacity over 50,000, along with the teams that use them as their home stadium.

## OWL Features

The ontology uses the following OWL features:
- Class hierarchies and inheritance
- Property restrictions (domain and range)
- Property characteristics (functional, inverse functional)
- Equivalence relationships
- Disjointness between classes

## SWRL Rules

### Rule 1: Identify experienced players
```
Player(?p) ^ goalsScored(?p, ?g) ^ swrlb:greaterThan(?g, 100) -> ExperiencedPlayer(?p)
```
This rule classifies any player who has scored more than 100 goals as an experienced player.

### Rule 2: Identify derby matches
```
Match(?m) ^ hasHomeTeam(?m, ?ht) ^ hasAwayTeam(?m, ?at) ^ 
baseLocation(?ht, ?loc) ^ baseLocation(?at, ?loc) -> DerbyMatch(?m)
```
This rule identifies derby matches when both teams are from the same location.

### Rule 3: Calculate player efficiency
```
Player(?p) ^ goalsScored(?p, ?g) ^ matchesPlayed(?p, ?m) ^ 
swrlb:divide(?e, ?g, ?m) ^ swrlb:greaterThan(?e, 0.5) -> EfficientStriker(?p)
```
This rule identifies efficient strikers as players with a goal-to-match ratio greater than 0.5.

### Rule 4: Identify potential transfers
```
Player(?p) ^ playsFor(?p, ?t1) ^ contractEndsIn(?p, ?year) ^ 
swrlb:equal(?year, 2023) ^ Team(?t2) ^ needsPosition(?t2, ?pos) ^ 
playerPosition(?p, ?pos) -> PotentialTransfer(?p, ?t2)
```
This rule identifies potential transfers by matching players whose contracts are ending with teams that need players in their positions.

## Conclusion

This football domain ontology demonstrates how semantic web technologies can be leveraged to model complex sporting domains. The ontology provides several advantages over traditional relational databases:

1. **Flexible schema evolution**: The ontology can be easily extended with new concepts without breaking existing queries.
2. **Inference capabilities**: Using OWL and SWRL, new knowledge can be inferred from existing data.
3. **Integration of heterogeneous data**: The ontology can easily integrate data from multiple sources using shared vocabularies.
4. **Complex relationships**: The ontology can represent complex relationships between entities that are difficult to model in relational databases.

The ontology can be used for various applications such as match analysis, player scouting, tournament management, and fan engagement platforms.

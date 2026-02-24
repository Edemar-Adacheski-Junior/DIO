# MODELAGEM DE DADOS EM GRAFOS DE UM SERVIÇO DE STREAMING

## Problema
Você foi contratado por um novo serviço de streaming de filmes e séries e sua primeira tarefa é projetar o banco de dados.
Diferente dos sistemas tradicionais, a empresa quer focar nos relacionamentos para criar um sistema de recomendação poderoso.

## Desafio
Modele e crie um pequeno grafo de conhecimento para este serviço.
O modelo deve incluir:
- **Entidades (Nós):** User, Movie, Series, Genre, Actor, Director
- **Conexões (Relacionamentos):** WATCHED (com propriedade rating), ACTED_IN, DIRECTED, IN_GENRE

## Entrega
1. Um diagrama ou esboço do seu modelo de grafo.
2. Um script Cypher (.cypher) que cria constraints para os nós (ex: UNIQUE para IDs) e popula o banco com pelo menos 10 usuários, 10 filmes / séries e seus respectivos relacionamentos.

## DIAGRAMA DE MODELO DE GRAFO

<img width="1377" height="708" alt="LogicaDeGrafos" src="https://github.com/user-attachments/assets/c4b3f6ca-4463-46be-9ae9-13aef80e4610" />

<img width="2221" height="1216" alt="Untitled graph" src="https://github.com/user-attachments/assets/1acab6ea-db3c-49f0-af33-552b2bbefcdd" />

## SCRIPT CYPHER

CREATE (`Ação`:Genre)<-[:IN_GENRE]-(`Alien vs. Predador: Requiem (2007)`:Movie)-[:IN_GENRE]->(Terror:Genre)<-[:IN_GENRE]-(`Alien vs. Predador (2004)`:Movie)-[:IN_GENRE]->(`Ação`)<-[:IN_GENRE]-(`Alien: A Ressurreição (1997)`:Movie)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien³ (1992)`:Movie)-[:IN_GENRE]->(`Ficção científica`:Genre)<-[:IN_GENRE]-(`Aliens: O Resgate (1986)`:Movie)<-[:ACTED_IN]-(`Sigourney Weaver`:Actor)-[:ACTED_IN]->(`Alien: O Oitavo Passageiro (1979)`:Movie)<-[:DIRECTED]-(`Ridley Scott`:Director)-[:DIRECTED]->(`Prometheus (2012)`:Movie)<-[:ACTED_IN]-(:Actor)-[:ACTED_IN]->(`Alien Covenant (2017)`:Movie)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: Earth (2025)`:Series)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien: Isolation - The Digital Series (2019)`:Series)-[:IN_GENRE]->(:Genre),
(`Charles Bishop Weyland`:User)-[:WATCHED {rating: 6.3}]->(`Alien: A Ressurreição (1997)`)<-[:WATCHED {rating: 5.4}]-(`H.R. Giger`:User)-[:WATCHED {rating: 4.6}]->(`Alien³ (1992)`)<-[:WATCHED {rating: 6.4}]-(`Ellen Ripley`:User)-[:WATCHED {rating: 8.4}]->(`Aliens: O Resgate (1986)`)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien: O Oitavo Passageiro (1979)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: A Ressurreição (1997)`)<-[:WATCHED {rating: 6.2}]-(`Ellen Ripley`),
(`Ellen Ripley`)-[:WATCHED {rating: 8.5}]->(`Alien: O Oitavo Passageiro (1979)`)-[:IN_GENRE]->(Suspense:Genre)<-[:IN_GENRE]-(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.4}]-(`H.R. Giger`)-[:WATCHED {rating: 7.1}]->(`Alien: Earth (2025)`),
(:Director)-[:DIRECTED]->(`Aliens: O Resgate (1986)`)-[:IN_GENRE]->(`Ação`),
(:Director)-[:DIRECTED]->(`Alien³ (1992)`)<-[:ACTED_IN]-(`Sigourney Weaver`),
(:User)-[:WATCHED {rating: 6}]->(`Alien³ (1992)`)-[:IN_GENRE]->(:Genre),
(:Director)-[:DIRECTED]->(`Alien: A Ressurreição (1997)`),
(:Director)-[:DIRECTED]->(`Alien vs. Predador (2004)`)<-[:ACTED_IN]-(:Actor),
(:User)-[:WATCHED {rating: 8}]->(`Alien: Isolation - The Digital Series (2019)`)<-[:WATCHED {rating: 7.5}]-(`H.R. Giger`)-[:WATCHED {rating: 5.6}]->(`Alien vs. Predador (2004)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien vs. Predador: Requiem (2007)`)<-[:WATCHED {rating: 4.7}]-(`H.R. Giger`)-[:WATCHED {rating: 7}]->(`Prometheus (2012)`)<-[:WATCHED {rating: 7.3}]-(:User)-[:WATCHED {rating: 6.5}]->(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.5}]-(:User),
(:Director)-[:DIRECTED]->(`Alien vs. Predador: Requiem (2007)`)<-[:ACTED_IN]-(:Actor),
(:Genre)<-[:IN_GENRE]-(`Prometheus (2012)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: Isolation - The Digital Series (2019)`),
(`Elizabeth Shaw`:User)-[:WATCHED {rating: 7}]->(`Prometheus (2012)`)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.4}]-(`Elizabeth Shaw`),
(`Ridley Scott`)-[:DIRECTED]->(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.5}]-(David:User),
(:Director)-[:DIRECTED]->(`Alien: Earth (2025)`)<-[:ACTED_IN]-(:Actor),
(`Alien: Earth (2025)`)-[:IN_GENRE]->(Suspense),
(:Director)-[:DIRECTED]->(`Alien: Isolation - The Digital Series (2019)`)<-[:ACTED_IN]-(:Actor),
(:User)-[:WATCHED {rating: 9}]->(`Aliens: O Resgate (1986)`)<-[:WATCHED {rating: 9.7}]-(`H.R. Giger`)-[:WATCHED {rating: "9,4"}]->(`Alien: O Oitavo Passageiro (1979)`),
(`Aliens: O Resgate (1986)`)<-[:WATCHED {rating: 8.4}]-(`Charles Bishop Weyland`)-[:WATCHED {rating: 2.1}]->(`Alien vs. Predador (2004)`),
(David)-[:WATCHED {rating: 6.5}]->(`Prometheus (2012)`),
(`Charles Bishop Weyland`)-[:WATCHED {rating: 5.9}]->(`Alien³ (1992)`)

MATCH path0 = (`Ação`:Genre)<-[:IN_GENRE]-(`Alien vs. Predador: Requiem (2007)`:Movie)-[:IN_GENRE]->(Terror:Genre)<-[:IN_GENRE]-(`Alien vs. Predador (2004)`:Movie)-[:IN_GENRE]->(`Ação`)<-[:IN_GENRE]-(`Alien: A Ressurreição (1997)`:Movie)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien³ (1992)`:Movie)-[:IN_GENRE]->(`Ficção científica`:Genre)<-[:IN_GENRE]-(`Aliens: O Resgate (1986)`:Movie)<-[:ACTED_IN]-(`Sigourney Weaver`:Actor)-[:ACTED_IN]->(`Alien: O Oitavo Passageiro (1979)`:Movie)<-[:DIRECTED]-(`Ridley Scott`:Director)-[:DIRECTED]->(`Prometheus (2012)`:Movie)<-[:ACTED_IN]-(:Actor)-[:ACTED_IN]->(`Alien Covenant (2017)`:Movie)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: Earth (2025)`:Series)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien: Isolation - The Digital Series (2019)`:Series)-[:IN_GENRE]->(:Genre),
path1 = (`Charles Bishop Weyland`:User)-[:WATCHED {rating: 6.3}]->(`Alien: A Ressurreição (1997)`)<-[:WATCHED {rating: 5.4}]-(`H.R. Giger`:User)-[:WATCHED {rating: 4.6}]->(`Alien³ (1992)`)<-[:WATCHED {rating: 6.4}]-(`Ellen Ripley`:User)-[:WATCHED {rating: 8.4}]->(`Aliens: O Resgate (1986)`)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien: O Oitavo Passageiro (1979)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: A Ressurreição (1997)`)<-[:WATCHED {rating: 6.2}]-(`Ellen Ripley`),
path2 = (`Ellen Ripley`)-[:WATCHED {rating: 8.5}]->(`Alien: O Oitavo Passageiro (1979)`)-[:IN_GENRE]->(Suspense:Genre)<-[:IN_GENRE]-(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.4}]-(`H.R. Giger`)-[:WATCHED {rating: 7.1}]->(`Alien: Earth (2025)`),
path3 = (:Director)-[:DIRECTED]->(`Aliens: O Resgate (1986)`)-[:IN_GENRE]->(`Ação`),
path4 = (:Director)-[:DIRECTED]->(`Alien³ (1992)`)<-[:ACTED_IN]-(`Sigourney Weaver`),
path5 = (:User)-[:WATCHED {rating: 6}]->(`Alien³ (1992)`)-[:IN_GENRE]->(:Genre),
path6 = (:Director)-[:DIRECTED]->(`Alien: A Ressurreição (1997)`),
path7 = (:Director)-[:DIRECTED]->(`Alien vs. Predador (2004)`)<-[:ACTED_IN]-(:Actor),
path8 = (:User)-[:WATCHED {rating: 8}]->(`Alien: Isolation - The Digital Series (2019)`)<-[:WATCHED {rating: 7.5}]-(`H.R. Giger`)-[:WATCHED {rating: 5.6}]->(`Alien vs. Predador (2004)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien vs. Predador: Requiem (2007)`)<-[:WATCHED {rating: 4.7}]-(`H.R. Giger`)-[:WATCHED {rating: 7}]->(`Prometheus (2012)`)<-[:WATCHED {rating: 7.3}]-(:User)-[:WATCHED {rating: 6.5}]->(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.5}]-(:User),
path9 = (:Director)-[:DIRECTED]->(`Alien vs. Predador: Requiem (2007)`)<-[:ACTED_IN]-(:Actor),
path10 = (:Genre)<-[:IN_GENRE]-(`Prometheus (2012)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: Isolation - The Digital Series (2019)`),
path11 = (`Elizabeth Shaw`:User)-[:WATCHED {rating: 7}]->(`Prometheus (2012)`)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.4}]-(`Elizabeth Shaw`),
path12 = (`Ridley Scott`)-[:DIRECTED]->(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.5}]-(David:User),
path13 = (:Director)-[:DIRECTED]->(`Alien: Earth (2025)`)<-[:ACTED_IN]-(:Actor),
path14 = (`Alien: Earth (2025)`)-[:IN_GENRE]->(Suspense),
path15 = (:Director)-[:DIRECTED]->(`Alien: Isolation - The Digital Series (2019)`)<-[:ACTED_IN]-(:Actor),
path16 = (:User)-[:WATCHED {rating: 9}]->(`Aliens: O Resgate (1986)`)<-[:WATCHED {rating: 9.7}]-(`H.R. Giger`)-[:WATCHED {rating: "9,4"}]->(`Alien: O Oitavo Passageiro (1979)`),
path17 = (`Aliens: O Resgate (1986)`)<-[:WATCHED {rating: 8.4}]-(`Charles Bishop Weyland`)-[:WATCHED {rating: 2.1}]->(`Alien vs. Predador (2004)`),
path18 = (David)-[:WATCHED {rating: 6.5}]->(`Prometheus (2012)`),
path19 = (`Charles Bishop Weyland`)-[:WATCHED {rating: 5.9}]->(`Alien³ (1992)`)
RETURN path0, path1, path2, path3, path4, path5, path6, path7, path8, path9, path10, path11, path12, path13, path14, path15, path16, path17, path18, path19

MERGE (`Ação`:Genre)<-[:IN_GENRE]-(`Alien vs. Predador: Requiem (2007)`:Movie)-[:IN_GENRE]->(Terror:Genre)<-[:IN_GENRE]-(`Alien vs. Predador (2004)`:Movie)-[:IN_GENRE]->(`Ação`)<-[:IN_GENRE]-(`Alien: A Ressurreição (1997)`:Movie)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien³ (1992)`:Movie)-[:IN_GENRE]->(`Ficção científica`:Genre)<-[:IN_GENRE]-(`Aliens: O Resgate (1986)`:Movie)<-[:ACTED_IN]-(`Sigourney Weaver`:Actor)-[:ACTED_IN]->(`Alien: O Oitavo Passageiro (1979)`:Movie)<-[:DIRECTED]-(`Ridley Scott`:Director)-[:DIRECTED]->(`Prometheus (2012)`:Movie)<-[:ACTED_IN]-(:Actor)-[:ACTED_IN]->(`Alien Covenant (2017)`:Movie)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: Earth (2025)`:Series)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien: Isolation - The Digital Series (2019)`:Series)-[:IN_GENRE]->(:Genre)
MERGE (`Charles Bishop Weyland`:User)-[:WATCHED {rating: 6.3}]->(`Alien: A Ressurreição (1997)`)<-[:WATCHED {rating: 5.4}]-(`H.R. Giger`:User)-[:WATCHED {rating: 4.6}]->(`Alien³ (1992)`)<-[:WATCHED {rating: 6.4}]-(`Ellen Ripley`:User)-[:WATCHED {rating: 8.4}]->(`Aliens: O Resgate (1986)`)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien: O Oitavo Passageiro (1979)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: A Ressurreição (1997)`)<-[:WATCHED {rating: 6.2}]-(`Ellen Ripley`)
MERGE (`Ellen Ripley`)-[:WATCHED {rating: 8.5}]->(`Alien: O Oitavo Passageiro (1979)`)-[:IN_GENRE]->(Suspense:Genre)<-[:IN_GENRE]-(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.4}]-(`H.R. Giger`)-[:WATCHED {rating: 7.1}]->(`Alien: Earth (2025)`)
MERGE (:Director)-[:DIRECTED]->(`Aliens: O Resgate (1986)`)-[:IN_GENRE]->(`Ação`)
MERGE (:Director)-[:DIRECTED]->(`Alien³ (1992)`)<-[:ACTED_IN]-(`Sigourney Weaver`)
MERGE (:User)-[:WATCHED {rating: 6}]->(`Alien³ (1992)`)-[:IN_GENRE]->(:Genre)
MERGE (:Director)-[:DIRECTED]->(`Alien: A Ressurreição (1997)`)
MERGE (:Director)-[:DIRECTED]->(`Alien vs. Predador (2004)`)<-[:ACTED_IN]-(:Actor)
MERGE (:User)-[:WATCHED {rating: 8}]->(`Alien: Isolation - The Digital Series (2019)`)<-[:WATCHED {rating: 7.5}]-(`H.R. Giger`)-[:WATCHED {rating: 5.6}]->(`Alien vs. Predador (2004)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien vs. Predador: Requiem (2007)`)<-[:WATCHED {rating: 4.7}]-(`H.R. Giger`)-[:WATCHED {rating: 7}]->(`Prometheus (2012)`)<-[:WATCHED {rating: 7.3}]-(:User)-[:WATCHED {rating: 6.5}]->(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.5}]-(:User)
MERGE (:Director)-[:DIRECTED]->(`Alien vs. Predador: Requiem (2007)`)<-[:ACTED_IN]-(:Actor)
MERGE (:Genre)<-[:IN_GENRE]-(`Prometheus (2012)`)-[:IN_GENRE]->(`Ficção científica`)<-[:IN_GENRE]-(`Alien: Isolation - The Digital Series (2019)`)
MERGE (`Elizabeth Shaw`:User)-[:WATCHED {rating: 7}]->(`Prometheus (2012)`)-[:IN_GENRE]->(Terror)<-[:IN_GENRE]-(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.4}]-(`Elizabeth Shaw`)
MERGE (`Ridley Scott`)-[:DIRECTED]->(`Alien Covenant (2017)`)<-[:WATCHED {rating: 6.5}]-(David:User)
MERGE (:Director)-[:DIRECTED]->(`Alien: Earth (2025)`)<-[:ACTED_IN]-(:Actor)
MERGE (`Alien: Earth (2025)`)-[:IN_GENRE]->(Suspense)
MERGE (:Director)-[:DIRECTED]->(`Alien: Isolation - The Digital Series (2019)`)<-[:ACTED_IN]-(:Actor)
MERGE (:User)-[:WATCHED {rating: 9}]->(`Aliens: O Resgate (1986)`)<-[:WATCHED {rating: 9.7}]-(`H.R. Giger`)-[:WATCHED {rating: "9,4"}]->(`Alien: O Oitavo Passageiro (1979)`)
MERGE (`Aliens: O Resgate (1986)`)<-[:WATCHED {rating: 8.4}]-(`Charles Bishop Weyland`)-[:WATCHED {rating: 2.1}]->(`Alien vs. Predador (2004)`)
MERGE (David)-[:WATCHED {rating: 6.5}]->(`Prometheus (2012)`)
MERGE (`Charles Bishop Weyland`)-[:WATCHED {rating: 5.9}]->(`Alien³ (1992)`)

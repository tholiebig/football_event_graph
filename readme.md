# Football match events in a graph database
This repo contains example processing code to convert .csv files into 
the appropriate format for importing into the neo4j graph database.

## Data
The example data contains the on-pitch events for football matches as 
described here; https://www.kaggle.com/secareanualin/football-events.  
The data is remapped to ensure unique nodeIds and relationship types.  
TODO: description of graph connectivity

## How to use
* install Neo4j 5.x (https://neo4j.com/docs/operations-manual/current/installation/)
* install requirements.txt
* `cd football_event_graph/scripts`
* `python process_files_for_neo4j_import.py <matchMetadataFilepath> <matchEventsFilepath> <processedFileSaveDir>`
* `./build_new_database_neo4j_v5.sh <processedFileSaveDir>`
* `./start_neo4j.sh` (requires Docker)
* database should then be running on localhost:7474

### Set indexes (optional)
```
CREATE RANGE INDEX matchEvtm FOR (n:MATCH_EVENT) ON n.matchEventTime;
CREATE RANGE INDEX matchEvso FOR (n:MATCH_EVENT) ON n.sortOrder;
CREATE RANGE INDEX matchEvtg FOR (n:MATCH_EVENT) ON n.isGoal;
CREATE RANGE INDEX matchEvtf FOR (n:MATCH_EVENT) ON n.isFastBreak;
CREATE TEXT INDEX playertxt FOR (n:PLAYER) ON n.text;
CREATE TEXT INDEX matchEvttxt FOR (n:MATCH_EVENT) ON n.text;
```

### Example
![graph_example](https://user-images.githubusercontent.com/22633509/97285861-ac21d400-183a-11eb-897e-7e41f3068666.png)

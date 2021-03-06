Cartographier-des-flux-Twitter
==============================

==> Démonstration : http://maps.esrifrance.fr/twitterStreamlayer.html <==

Cette application permet de cartographier le flux twitter récupéré par <a href="http://www.esrifrance.fr/arcgis-geoevent-processor-for-server.aspx" target='_blank'>ArcGIS GeoEvent Processor for Server</a> dans une Streamlayer de l'API ArcGIS Javascript.

L'architecture mise en place pour cette application est : Twitter => ArcGIS Server/GeoEvent Processor => Application Javascript

Le connecteur Twitter pour ArcGIS GeoEvent Processor est téléchargeable sur le <a href="https://github.com/Esri/twitter-for-geoevent" target='_blank'>Github Esri</a>  ou sur <a href="http://www.arcgis.com/home/item.html?id=041138094e5348eb902f4b71175eeb6f" target='_blank'>ArcGIS Online</a> 

  
Instructions
============
  <b>1</b>- Après installation du connecteur Twitter, vous devez créer une nouvelle définition pour la sortie afin de simplifier le message Twitter entrant qui est créé automatiquement. 
La défintion des champs utilisée en sortie dans l'application est la suivante :

  <i>MyTweetDefinition</i>

  Name: <i>date<br></i>
  Type: Date<br>
  Cardinality: One<br>
  Tags:TIME_START<br>

  Name: <i>nom</i><br>
  Type: String<br>
  Cardinality: One<br>
  Tags:<br>
  
  Name: <i>lieu<br></i>
  Type: String<br>
  Cardinality: One<br>
  Tags:<br>
  
  Name: <i>texte<br></i>
  Type: String<br>
  Cardinality: One<br>
  Tags:<br>
  
  Name: <i>shape<br></i>
  Type: Geometry<br>
  Cardinality: One<br>
  Tags:GEOMETRY<br>
 
  Name: <i>ID<br></i>
  Type: Integer<br>
  Cardinality: One<br>
  Tags:TRACK_ID<br>
  
  <b>2</b>- Créer l'Input "Receive Tweets"
  
  <b>3</b>- Créer l'Output "Publish JSON to a Web Socket"
  <br>URL WebSocket par défaut : <i>http://localhost:6180/ws
  </i>
  
  <b>4</b>- Créer le service GeoEvent Processor "Twitter"
  <br>Ajouter un filtre avec la condition attributaire <i>geolocated=true</i>
  <br>Ajouter un processus de type Mappage de champs et faire correspondre la définition en entrée (TweetStatus) avec la définition créée pour la sortie (MyTweetDefinition) :
  <i><br>$RECEIVED_TIME = date<br>
  user.name = nom <br>
  place.full_name = lieu <br>
  text = texte <br>
  coordinates = shape <br>
  id_str = ID</i>
  
  <b>5</b>- Editer le fichier <i>twitterStreamlayer.html</i> et assurez-vous que l'URL ligne 318 correspond à votre WebSocket en sortie de GeoEvent Processor

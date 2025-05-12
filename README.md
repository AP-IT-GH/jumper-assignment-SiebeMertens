JumpAgent - Unity Setup Documentatie Inleiding Deze documentatie beschrijft hoe je een Unity-scene correct opzet om succesvol de JumpAgent-opdracht uit te voeren met behulp van ML-Agents. De taak betreft een lineaire movement challenge waarbij de agent moet leren springen over bewegende obstakels.

Doel van de Opdracht Taak: Laat de agent succesvol over bewegende obstakels springen.

Omgeving: Bevat één agent in een eenvoudige lineaire omgeving.

Acties:

0 = Stil blijven

1 = Springen

Reward Functie:

+1.0 voor succesvol springen over een obstakel

-0.2 voor onnodig springen

-0.01 voor stil blijven staan wanneer een obstakel arriveert

Vereisten Unity (aanbevolen versie compatibel met ML-Agents)

ML-Agents package (importeer via Unity Package Manager of GitHub)

Scene Setup

Maak een nieuwe scene aan en importeer ML-Agents package.
Voeg de volgende 3D-objecten toe: Plane: De ondergrond voor de agent en obstakels.
Cube (Agent): Dient als de agent.

Cube (Obstacle Detector): Dient als de detectiezone voor obstakels.

Obstacle Prefab: Maak een lege GameObject aan.
Voeg een cube als child toe.

Pas de afmetingen aan (bijvoorbeeld smal en hoog).

Sla deze op als prefab in de Prefabs-map.

Componenten per Object Plane: Mesh Renderer

Mesh Collider

ObstacleSpawner script

Agent (Cube) Mesh Renderer

Box Collider

Rigidbody

Freeze Position: X, Z

Freeze Rotation: X, Y, Z

Behavior Parameters

Behavior Name: AgentJump

Vector Observation Size: 50

Action Type: Discrete

Branches: 1

Branch 0 Size: 2

AgentJump script (koppel de ObstacleDetector)

Decision Requester

Extra Box Collider met Is Trigger aangevinkt

Obstacle Detector (2e Cube op dezelfde positie als de agent) Box Collider (Is Trigger: aan)

Rigidbody

ObstacleDetector script

Scripts AgentJump.cs Verwerkt observaties: obstakels, locatie van de agent.

Bepaalt rewards op basis van:

Contact met obstakel (negatieve reward)

Raycast-controle onder de agent (verhindert ongewenste sprongen op obstakels)

Positieve of negatieve actie volgens de detectiezone

ObstacleDetector.cs Detecteert objecten tijdens het springen via trigger.

Als de agent springt:

En er wordt geen obstakel gedetecteerd → negatieve reward

En er wordt wel een obstakel gedetecteerd → positieve reward

Als de agent stil blijft en een obstakel nadert → negatieve reward

ObstacleMove.cs Obstakels bewegen richting agent.

Obstakels worden vernietigd zodra ze de plane verlaten.

ObstacleSpawner.cs Bepaalt spawnlocatie en spawninterval van obstakels.

Spawnt prefab-obstakels op willekeurige of geplande tijdstippen.

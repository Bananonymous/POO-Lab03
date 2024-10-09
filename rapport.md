# Rapport Labo 03: Fédération Internationale de Gymnastique

##### Par Nicolet Victor et Surbeck Léon

### Diagramme UML

Le diagramme UML ci-dessous illustre la structure des classes représentant les fédérations nationales, les gymnastes, les juges, les disciplines, les catégories et les événements sportifs.

![Diagramme UML Fédération Internationale de Gymnastique](./imgs/Schéma.png)

### Explication des choix de modélisation

1. **Personne** :

   - _Attributs_ : La classe `Personne` factorise les attributs communs entre les gymnastes et les juges, tels que le nom, le prénom, la date de naissance et le numéro de téléphone.
   - _Héritage_ : Les classes `Gymnaste` et `Juge` héritent de `Personne`, centralisant ainsi les informations partagées entre ces deux types d'individus.

2. **Fédération Nationale** :

   - _Attributs_ : Chaque fédération nationale est définie par son nom et peut participer à plusieurs événements. La méthode `getEventParticipation()` permet de retourner la liste des événements où la fédération a participé.
   - _Associations_ : Une fédération nationale est composée de plusieurs gymnastes et juges (cardinalité "2..\*"), et elle peut s'inscrire à plusieurs événements. La fédération est représentée par une relation de composition avec ses gymnastes et juges.

3. **Gymnaste** :

   - _Attributs_ : Un gymnaste est défini par son genre, son poids, et sa taille, en plus des attributs hérités de `Personne`. La méthode `getVictoires()` permet de calculer le nombre de victoires du gymnaste dans une catégorie donnée.
   - _Associations_ : Un gymnaste est associé à aucune ou plusieurs catégories via la relation "Concours dans", avec une limite maximale de 16 gymnastes par catégorie.

4. **Juge** :

   - _Attributs_ : Les juges héritent de la classe `Personne` et sont rattachés à une fédération nationale. Ils participent aux événements pour noter les gymnastes.
   - _Associations_ : Une fédération nationale est composée d'au moins deux juges (cardinalité "2..\*"), qui participent aux événements auxquels la fédération est inscrite.

5. **Discipline** :

   - _Attributs_ : Chaque discipline est caractérisée par un nom et le genre des gymnastes qui peuvent y participer. Une discipline regroupe plusieurs catégories.
   - _Associations_ : Une discipline est composée d'une ou plusieurs catégories (cardinalité "1..\*"). Elle est également liée aux événements auxquels elle est présentée.

6. **Catégorie** :

   - _Attributs_ : Une catégorie est définie par son nom et est associée à une discipline. Elle est liée à plusieurs gymnastes qui y participent, avec une limite maximale de 16 participants par catégorie.
   - _Associations_ : Chaque catégorie appartient à une discipline (cardinalité "1") et est liée aux gymnastes par la relation "Concours dans".

7. **Événement Sportif** :

   - _Attributs_ : Un événement est défini par son nom et sa date. Il est également associé à plusieurs disciplines et conserve une méthode `getPodium()` pour retourner les trois meilleurs gymnastes dans une catégorie donnée.
   - _Associations_ : Un événement est composé de une ou plusieurs disciplines (cardinalité "0..\*"), chacune étant elle-même composée de catégories. Les fédérations s'inscrivent à des événements, incluant leurs gymnastes et juges.

8. **Inscription à un événement** :

   - _Attributs_ : L'entité `S'inscrit à` représente l'inscription d'une fédération nationale à un événement. Elle est caractérisée par la date de modification de l'inscription.
   - _Associations_ : Cette entité relie une fédération à un événement, avec l'obligation de spécifier les juges et gymnastes participants lors de l'inscription (cardinalité "1..\*").
   - _Contraintes d'intégrité_ : Lorsqu'une fédération s'inscrit à un événement, elle doit fournir la liste des juges et des gymnastes participants, et chaque juge et gymnaste doit appartenir à la fédération qui les inscrit.

9. **Notes et Podium** :
   - _Attributs_ : Chaque gymnaste reçoit une note sous forme de réel pour sa participation dans une catégorie. La méthode `getPodium()` retourne les trois meilleurs gymnastes dans une catégorie donnée lors d'un événement spécifique.

### Méthodes nécessaires

1. `getEvenementsParticipe(FederationNationale) -> List<Evenement>` :

   - Retourne la liste des événements où une fédération nationale a participé.

2. `getPodium(Categorie, Evenement) -> List<Gymsnaste>` :

   - Retourne le podium (les trois premiers gymnastes) pour une catégorie lors d'un événement donné.

3. `getNbVictoires(Gymnaste, Categorie) -> int` :
   - Retourne le nombre de victoires d'un gymnaste dans une catégorie donnée.

### Contraintes d'intégrité

1. Une fédération nationale doit avoir au moins deux gymnastes et deux juges pour s'inscrire à un événement (selon la donnée)
2. Le genre du gymnaste doit correspondre à celui requis par la discipline pour qu'il puisse concourir.
3. Un événement qui inclut une discipline inclut nécessairement toutes les catégories de cette discipline.

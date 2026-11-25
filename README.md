# Projet-POO

import numpy as np
import random
from abc import ABC, abstractmethod 

class De:
    def __init__(self, seed=None): #le hasard est différent à chaque lancer puisque seed=None
        self._hasard= random.Random(seed)
        self._resultat = 0 

    @property 
    def resultat (self):
        return self._resultat
    
    def lancer(self, nombre_des):
        """Lance 1 ou 2 dés à 6 faces et renvoie la liste des résultats."""
        self._resultat = 0
        self._Tour_bonus = False
        if nombre_des not in (1, 2):
            raise ValueError("Le nombre de dés doit être 1 ou 2.")
        if nombre_des == 2 and "Gare" not in self.Joueur._liste_monuments_acquis:
            raise ValueError("Vous ne possedez pas la Gare")
        for _ in range(nombre_des):
            d = self._hasard.randint(1, 6)
            if self._resultat == d : 
                self._Tour_bonus = True 
            self._resultat += d
        return [self._resultat]
    
class Monuments:
    def __init__(self,nom:str,cout:int):
        self._nom:str=nom
        self._cout:int=cout
   
    @property
    def nom(self):
      return self._nom

    @property
    def cout(self):
      return self._cout
  
    def obtenu(self, joueur: 'Joueur'):
        if self._nom in joueur._list_monuments:
            return(True)

class Gare (Monuments):
    def __init__(self):
        super().__init__("Gare",4)
        
class Centre_commercial (Monuments):
    def __init__(self):
        super().__init__("Centre commercial",10)

class Parc_dattraction (Monuments):
    def __init__(self):
        super().__init__("Parc d'attraction",16)
        
class Tour_radio (Monuments):
    def __init__(self):
        super().__init__("Tour radio",22)    

class Joueur:
    def __init__(self,nom:str,IA:bool):
        self._nom:str=nom
        self._argent:int=3
        self._list_monuments_acquis:list=[]
        self._list_etablissements_acquis:list=[]  #rajouter deux établissements de base
        self._nombre_dés:int=1
        self._IA:bool=IA
   
   
    @property
    def nom(self):
        return(self._nom)
   
   
    @property
    def argent(self):
        return(self._argent)
   
   
    def gagnant(self): #renvoie True si le joueur a gagné la partie, False sinon
        return len(self._list_monuments_acquis==4)
   
    @property
    def list_monuments_acquis(self):
        return self._list_monuments_acquis
   
    @property
    def list_etablissements_acquis(self):
        return self._list_etablissements_acquis
    
    def possede_monuments(self, monuments :Monuments ):
        if monuments is in self._list_monuments_acquis:
        
    def acheter (self, nom : str, plateau : 'Plateau'):
        etab = plateau.etablissement(nom)
        if self._argent < etab.cout :
            raise ValueError ("Pas assez d'argent")
        elif etab.nombre_exemp==0:
            raise ValueError("Cet établissement n'est plus disponible")
        elif etab._couleur == "violet" and etab in self._list_etablissements_acquis:
            raise ValueError ("Vous ne pouvez avoir qu'un exemplaire")
        else:
            self._argent -= etab._valeur
            self._nombre_ex-=1
            if self.nom not in self.Joueur._list_etablissements_acquis:
                self.Joueur._list_etablissements_acquis.append([etab,1])
            else:
                for i in range(len(self._list_etablissements_acquis)):
                    if self.Joueur._list_etablissements_acquis[i][0]==self._nom:
                        self.Joueur._list_etablissements_acquis[i][1]+=1

    def acheter_monuments(self, monuments: Monuments):
       if possede_monuments(monuments.nom) :
           raise ValueError("")
           raise ValueError ("Vous n'avez pas assez d'argent")
           
    def paie (self,montant : int):
        self._argent += montant 

    def payer (self, montant : int) :
        if self._argent < montant :
            raise ValueError("pas assez d'argent")
        else :
            self._argent -= montant
            
    def payer_limite(self, montant : int) :
        pay_max = min(self._argent, montant)
        self._argent-= pay_max
        return pay_max
                       
class Etablissement:
    liste_couleur = ["bleu","vert","rouge","violet"]
    liste_categorie = ["champs","ferme","magasin","cafe","nature","usine","marche","ville"]
    def __init__(self,nom:str,cout:int,valeur:int,couleur:str,categorie:str,rapport:int,nombre_ex:int):
        self._nom:str = nom
        self._cout:int = cout
        self._valeur:int = valeur
        self._couleur:str = couleur
        self._categorie:str = categorie
        self._rapport:int = rapport
        self._nombre_ex:int = nombre_ex

    @property
    def nom(self,nombre_ex):
        return self._nom
    
    @property
    def cout(self):
        return(self._cout)

    @property
    def valeur(self):
        return(self._valeur)

    @property
    def couleur(self):
        return(self._couleur)
    
    @property
    def categorie(self):
        return(self._categorie)

    @property
    def rapport(self):
        return(self._rapport)

    @property
    def nombre_exemp(self):
        return(self._nombre_ex)
    
    def gain (self , proprietaire: Joueur):
        montant = self._rapport
        if self._categorie in ("magasin", "cafe") and proprietaire.possede_monument("CentreCommercial"):
            montant +=1
        return montant

    
    def activer(self, proprietaire: Joueur, joueur_actif: Joueur, plateau: "Plateau", resultat_de: int):
        if self.couleur == "vert" and proprietaire is joueur_actif:
            for i in range (len(self.valeur)):
                if self._valeur[i] == self.Des._resultat :
                    montant = self.gain(proprietaire)
                    self.gain
                    joueur_actif.paie(montant)
    
        if self.couleur == "bleu"  :
            for i in range (len(self.valeur)):
                if self._valeur[i] == self.Des._resultat :
                    montant = self._gain(proprietaire)
                    proprietaire._argent += montant
    
        if self.couleur == "rouge" and proprietaire is not joueur_actif:
            for i in range (len(self.valeur)):
                if self._valeur[i] == self.Des._resultat :
                    montant = joueur_actif._paye_limite(self._gain(proprietaire))
                    proprietaire._argent += montant
                    
        elif self._couleur == "violet" and proprietaire is joueur_actif :
            self._activer_violet(proprietaire,plateau)

     def activer_violet(self, propriétaire : "Joueur",plateau: 'Plateau'):
        pass
        
class Champs_de_ble(Etablissement):
    def __init__(self):
        super().__init__("Champsdeble",1,[1],"bleu","champs",1,6)

class Ferme(Etablissement):
    def __init__(self):
        super().__init__("Ferme",1,[2],"bleu","ferme",1,6)
        
class Boulangerie(Etablissement):
    def __init__(self):
        super().__init__("Boulangerie",1,[2,3],"vert","magasin",1,6)
        
class Cafe(Etablissement):
    def __init__(self):
        super().__init__("Cafe",2,[3],"rouge","cafe",1,6)
        
class Superette(Etablissement):
    def __init__(self):
        super().__init__("Superette",2,[4],"vert","magasin",3,6)
        
class Foret(Etablissement):
    def __init__(self):
        super().__init__("Foret",3,[5],"bleu","nature",1,6)
        
class Fromagerie(Etablissement):
    def __init__(self):
        super().__init__("Fromagerie",5,[7],"vert","usine",3,6)
        
class Fabrique_de_meubles(Etablissement):
    def __init__(self):
        super().__init__("Fabriquedemeubles",3,[8],"vert","usine",3,6)
        
class Mine(Etablissement):
    def __init__(self):
        super().__init__("Mine",6,[9],"bleu","nature",5,6)
        
class Restaurant(Etablissement):
    def __init__(self):
        super().__init__("Restaurant",3,[9,10],"rouge","cafe",2,6)

class Verger(Etablissement):
    def __init__(self):
        super().__init__("Verger",3,[10],"bleu","champs",3,6)

class Marche_de_fruits_et_legumes(Etablissement):
    def __init__(self):
        super().__init__("Marchedefruitsetlegumes",2,[11,12],"vert","marche",2,6)

class Centre_d_affaires(Etablissement):
    def __init__(self):
        super().__init__("Centred'affaires",8,[6],"violet","ville",0,4)
   
    def activer_violet(self, propriétaire : "Joueur",plateau: 'Plateau'):
        # question choix joueur et etablissement avec vérification
        if joueur._nom not in Plateau._liste_joueur :
            raise ValueError ("Ce Joueur n'est pas dans la partie")
        if etablissment.nom not in joueur._liste_etablissements_acquis :
            raise ValueError (f"{joueur._nom} ne possède pas {etablissment._nom}")

class Stade(Etablissement):
    def __init__(self):
        super().__init__("Stade",6,[6],"violet","ville",2,4)

class Chaine_de_Television(Etablissement):
    def __init__(self):
        super().__init__("ChainedeTelevision",7,[6],"violet","ville",5,4)
    
    def activer_violet(self, proprietaire : "Joueur",plateau: 'Plateau'):
        #cible question avec vérification
        for autre in plateau.joueurs :
            if autre is not proprietaire :
                montant = autre._payer_limite(self._rapport)
                proprietaire.gagner(montant)
        

                    
class OrdreJoueurs:
    def __init__(self,joueurs:list[str]):
        if not 2<= len(joueurs)<=4:
            raise ValueError("Il faut entre 2 et 4 joueurs")
        self._joueurs:list[str]=joueurs
        self._scores:dict[str,int]={}
        self._ordre:list[str]=[]
        
    def lancer_des(self):
        """Chaque joueur lance un dé"""
        for joueur in self._joueurs:
            score=random.randint(1,6)
            self._scores[joueur]=score
            print (f" {joueur} obtient {score}")
            
    def a_des_egalites(self)->bool:
        """Renvoie True si au moins deux joueurs ont le meme score"""
        scores= list(self._scores.values())
        for score in scores:
            if scores.count(score)>1:
                return True
        return False
        
    def determiner_ordre(self)->list[str]:
        """Classe les joueurs par ordre décroissant; tout le monde relance en cas d'égalité"""
        self.lancer_des()
        while self.a_des_egalites():
            print("Egalité! Tout le monde relance")
            self.lancer_des()
        tries=sorted(self._scores.items(), key=lambda item: item[1], reverse=True)
        self._ordre= [joueur for joueur, _ in tries]
        return self._ordre
  
class Plateau:
    def __init__(self,ordre_joueurs: OrdreJoueurs |None=None):
        self._list_monuments=[]
        self._list_etablissements=[]
        self._catalogue = {}
        if ordre_joueurs is not None:
            self._list_joueur=ordre_joueurs.determiner_ordre()
        else:
            self._list_joueur=[]
            print("Joueurs dans l'ordre de jeu: {self._list_joueur}")
        
    def ajouter_joueur(self,nom:str,IA:bool):
        for joueur in self._list_joueur:
            if joueur.nom == nom:
                raise ValueError("Ce nom est déjà utilisé.")
        self._list_joueur.append(Joueur(nom,IA))
    
    def etablissment (self, nom : str):
        if nom not in self._catalogue :
            raise ValueError(f"{nom} n'est pas dans le jeu ")
        else :
            return (self._catalogue[nom])
   
    def partie_terminee(self):
        for joueur in self._list_joueur:
            if joueur.gagnant():
                return True
        return False

    def demarrer_jeu(self):
        list_ordre=[] #COMPLETER LISTE ORDRE RAMY
        tour=list_ordre[0]

        while not partie_terminee(self):
            jouer_action(self,tour)
            if tour==len(list_ordre-1):
                tour=0
            else:
                tour=tour+1

    def etablissements_effet(self,joueur,lancer_de):
        list_effets=[]
        for etablissement in joueur.list_etablissements_acquis:
            if etablissement[0].valeur==lancer_de:
                list_effets.append(etablissement)
        return(list_effets)
        



Plateau=Plateau()

# Michel=Joueur("Michel",False)
# Michel.acheter_etablissement(Plateau._list_etablissements[0])

for i in range(4):
    print(Plateau._list_monuments[i]._nom)

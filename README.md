# Projet-POO

import numpy as np
import random
from abc import ABC, abstractmethod 

class De:
    def __init__(self, seed=None): #le hasard est différent à chaque lancer puisque seed=None
        self._hasard= random.Random(seed)

    def lancer(self, nombre_des=1):
        """Lance 1 ou 2 dés à 6 faces et renvoie la liste des résultats."""
        if nombre_des not in (1, 2):
            raise ValueError("Le nombre de dés doit être 1 ou 2.")
        return [self._hasard.randint(1, 6) for _ in range(nombre_des)]
    

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

    def acheter_monument(self,monument:Monuments):
        if self._argent< monument._cout :
            raise ValueError("Pas assez d'argent")
        elif monument in self._list_monuments_acquis:
            raise ValueError("Tu possèdes déjà ce monument")
        else:
            self._list_monuments_acquis.append(monument)

    def acheter_etablissement(self,etablissement:Etablissement):
        if self._argent< etablissement._cout :
            raise ValueError("Pas assez d'argent")
        elif etablissement.nombre_ex==0:
            raise ValueError("Cet établissement n'est plus disponible")
        else:
            etablissement.nombre_ex(etablissement.nombre_exemp-1)
            if etablissement not in self._list_etablissements_acquis:
                self._list_etablissements_acquis.append([etablissement,1])
            else:
                for i in range(len(self._list_etablissements_acquis)):
                    if self._list_etablissements_acquis[i][0]==etablissement._nom:
                        self._list_etablissements_acquis[i][1]+=1

    @property
    def list_monuments_acquis(self):
        return self._list_monuments_acquis

    @property
    def list_etablissements_acquis(self):
        return self._list_etablissements_acquis


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
    def nombre_exemp(self):
        return(self._nombre_ex)


    def nombre_ex(self,nombre_ex):
        self._nombre_ex=nombre_ex

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

class Stade(Etablissement):
    def __init__(self):
        super().__init__("Stade",6,[6],"violet","ville",2,4)

class Chaine_de_Television(Etablissement):
    def __init__(self):
        super().__init__("ChainedeTelevision",7,[6],"violet","ville",5,4)
        

class Monuments:
    def __init__(self,nom:str,cout:int):
        self._nom:str=nom
        self._cout:int=cout

    def obtenu(self,joueur:Joueur):
        if self._nom in joueur._list_monuments:
            return(True)


class Plateau:
    def __init__(self):
        self._list_monuments=[]
        self._list_etablissements=[]
        self._list_joueur=[]


    @property
    def list_monuments(self):
        return(self._list_monuments)

    @property
    def list_etablissements(self):
        return(self._list_etablissements)

    def ajouter_monuments(self,nom:str,prix:int):
        self._list_monuments.append(Monuments(nom,prix))


    def ajouter_etablissements(self,nom:str,cout:int,valeur:int,couleur:str,categorie:str,rapport:int,nombre_ex:int):
        if categorie not in Etablissement.liste_categorie:
            raise ValueError("Mauvaise catégorie")
        elif couleur not in Etablissement.liste_couleur:
            raise ValueError("Mauvaise couleur")
        else:
            self._list_etablissements.append(Etablissement(nom,cout,valeur,couleur,categorie,rapport,nombre_ex))

    def ajouter_joueur(self,nom:str,IA:bool):
        for joueur in self._list_joueur:
            if joueur.nom == nom:
                raise ValueError("Ce nom est déjà utilisé.")
        self._list_joueur.append(Joueur(nom,IA))

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
    
    def jouer_action(self,joueur):
        pass


Plateau=Plateau()
Plateau.ajouter_monuments("Gare",4)
Plateau.ajouter_monuments("CentreCommercial",10)
Plateau.ajouter_monuments("ParcAttraction",16)
Plateau.ajouter_monuments("TourRadio",22)

# Michel=Joueur("Michel",False)
# Michel.acheter_etablissement(Plateau._list_etablissements[0])

for i in range(4):
    print(Plateau._list_monuments[i]._nom)

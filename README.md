# Projet-POO

import numpy as np
import random
from abc import ABC, abstractmethod 


class Joueur:
    def __init__(self,nom:str,IA:bool):
        self._nom:str=nom
        self._argent:int=3
        self._list_monuments_acquis:list=[]
        self._list_etablissements:list=[]  #rajouter deux établissements de base
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
        elif etablissement._nombre_ex==0:
            raise ValueError("Cet établissement n'est plus disponible")
        else:
            self._list_etablissements_acquis.append(etablissement)

class Etablissement:
    def __init__(self,nom:str,cout:int,valeur:int,couleur:str,categorie:str,rapport:int,nombre_ex:int):
        self._nom:str = nom
        self._cout:int = cout
        self._valeur:int = valeur
        self._couleur:str = couleur
        self._categorie:str = categorie
        self._rapport:int = rapport
        self._nombre_ex:int = nombre_ex
    

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

    @property
    def list_monuments(self):
        return(self._list_monuments)

    @property
    def list_etablissements(self):
        return(self._list_etablissements)

    def ajouter_monuments(self,nom:str,prix:int):
        self._list_monuments.append(Monuments(nom,prix))


    def ajouter_etablissements(self,nom:str,cout:int,valeur:int,couleur:str,categorie:str,rapport:int,nombre_ex:int): #changer les attributs
        self._list_etablissements.append(Etablissement(self,nom,cout,valeur,couleur,categorie,rapport,nombre_ex))


Plateau=Plateau()
Plateau.ajouter_monuments("Gare",4)
Plateau.ajouter_monuments("CentreCommercial",10)
Plateau.ajouter_monuments("ParcAttraction",16)
Plateau.ajouter_monuments("TourRadio",22)
Plateau.ajouter_etablissements("Champsdeble",1,1,"bleu","champs",1,6)
Plateau.ajouter_etablissements("Ferme",1,2,"bleu","ferme",1,6)
Plateau.ajouter_etablissements("Boulangerie",1,(2,3),"vert","magasin",1,6)
Plateau.ajouter_etablissements("Cafe",2,3,"rouge","cafe",1,6)


for i in range(4):
    print(Plateau._list_monuments[i]._nom)

# Projet-POO

import numpy as np
import random
from abc import ABC, abstractmethod 


class Joueur:
    def __init__(self,nom,IA:bool):
        self._nom=nom
        self._argent=3
        self._list_monuments_acquis=[]
        self._list_etablissements=[]  #rajouter deux établissements de base
        self._nombre_dés=1
        self._IA=IA


    @property
    def nom(self):
        return(self._nom)


    @property
    def argent(self):
        return(self._argent)


    def gagnant(self): #renvoie True si le joueur a gagné la partie, False sinon
        return len(self._list_monuments_acquis==4)

    def acheter_monument(self,monument):
        if self._argent< monument._cout :
            raise ValueError("Pas assez d'argent")
        elif monument in self._list_monuments_acquis:
            raise ValueError("Tu possèdes déjà ce monument")
        else:
            self._list_monuments_acquis.append(monument)

    def acheter_etablissement(self,etablissement):
        if self._argent< etablissement._cout :
            raise ValueError("Pas assez d'argent")
        elif etablissement._nombre_ex==0:
            raise ValueError("Cet établissement n'est plus disponible")
        else:
            self._list_etablissements_acquis.append(etablissement)

class Etablissement:
    def __init__(self,nom,cout,valeur,couleur,categorie,rapport,nombre_ex):
        self._nom = nom
        self._cout = cout
        self._valeur = valeur
        self._couleur = couleur
        self._categorie = categorie
        self._rapport = rapport
        self._nombre_ex = nombre_ex
    

class Monuments:
    def __init__(self,nom,cout):
        self._nom=nom
        self._cout=cout

    def obtenu(self,Joueur):
        if self._nom in Joueur._list_monuments:
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

    def ajouter_monuments(self,nom,prix):
        self._list_monuments.append(Monuments(nom,prix))


    def ajouter_etablissements(self,nom,cout,valeur,couleur,categorie,rapport,nombre_ex): #changer les attributs
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

# Projet-POO

import numpy as np
import random
from abc import ABC, abstractmethod 


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


    def ajouter_etablissements(self,nom:str,cout:int,valeur:int,couleur:str,categorie:str,rapport:int,nombre_ex:int):
        self._list_etablissements.append(Etablissement(nom,cout,valeur,couleur,categorie,rapport,nombre_ex))


Plateau=Plateau()
Plateau.ajouter_monuments("Gare",4)
Plateau.ajouter_monuments("CentreCommercial",10)
Plateau.ajouter_monuments("ParcAttraction",16)
Plateau.ajouter_monuments("TourRadio",22)
Plateau.ajouter_etablissements("Champsdeble",1,[1],"bleu","champs",1,6)
Plateau.ajouter_etablissements("Ferme",1,[2],"bleu","ferme",1,6)
Plateau.ajouter_etablissements("Boulangerie",1,[2,3],"vert","magasin",1,6)
Plateau.ajouter_etablissements("Cafe",2,[3],"rouge","cafe",1,6)
Plateau.ajouter_etablissements("Superette",2,[4],"vert","magasin",3,6)
Plateau.ajouter_etablissements("Foret",3,[5],"bleu","nature",1,6)
Plateau.ajouter_etablissements("Fromagerie",5,[7],"vert","usine",3,6)
Plateau.ajouter_etablissements("Fabriquedemeubles",3,[8],"vert","usine",3,6)
Plateau.ajouter_etablissements("Mine",6,[9],"bleu","nature",5,6)
Plateau.ajouter_etablissements("restaurant",3,[9,10],"rouge","cafe",2,6)
Plateau.ajouter_etablissements("Verger",3,[10],"bleu","champs",3,6)
Plateau.ajouter_etablissements("Fabriquedemeubles",2,[11,12],"vert","marche",2,6)
Plateau.ajouter_etablissements("Centred'affaires",8,[6],"violet","ville",0,4)
Plateau.ajouter_etablissements("Stade",6,[6],"violet","ville",2,4)
Plateau.ajouter_etablissements("ChainedeTelevision",7,[6],"violet","ville",5,4)

# Michel=Joueur("Michel",False)
# Michel.acheter_etablissement(Plateau._list_etablissements[0])

for i in range(4):
    print(Plateau._list_monuments[i]._nom)

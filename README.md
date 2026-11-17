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
        elif
        elif monument in self._list_monuments_acquis:
            raise ValueError("Tu possèdes déjà ce monument")
        else:
            self._list_monuments_acquis.append(monument)


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


    def ajouter_etablissements(self,nom,prix): #changer les attributs
        self._list_etablissements.append("quelque chose")


Plateau=Plateau()
Plateau.ajouter_monuments("Gare",4)
Plateau.ajouter_monuments("CentreCommercial",10)
Plateau.ajouter_monuments("ParcAttraction",16)
Plateau.ajouter_monuments("TourRadio",22)



for i in range(4):
    print(Plateau._list_monuments[i]._nom)

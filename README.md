# Raonament Basat en Casos per a la Generació Intel·ligent de Menús

Sistema de **Raonament Basat en Casos (CBR) híbrid** dissenyat per a la generació i recomanació personalitzada de menús gastronòmics per a esdeveniments, combinant coneixement simbòlic (ontologies) i subsimbòlic (espais vectorials latents).

Projecte realitzat per a l'assignatura **Sistemes Basats en el Coneixement (SBC)** del **Grau en Intel·ligència Artificial (UPC)**.

## Autores

* **Blanca Mira Fradera**
* **Laida Queral Llopart**
* **Olga Obiols Fuentes**

## Idea del problema

L'objectiu és resoldre el problema de la planificació de menús per a l'empresa de càtering fictícia **RicoRico**. El sistema ha de proposar menús coherents que s'ajustin a una gran varietat de factors:

* **Restriccions dures**: Al·lèrgies (15 categories normalitzades) i dietes estrictes (vegà, halal, celiac, etc.).
* **Objectius qualitatius**: Estil culinari preferit (japonès, fumat, tropical, etc.), formalitat de l'acte i temporada.
* **Limitacions logístiques**: Nombre de comensals i pressupost objectiu.

A diferència dels sistemes basats en regles rígides, aquest model utilitza la creativitat algorísmica per **adaptar** casos previs a noves realitats, garantint sempre la seguretat alimentària.

## Cicle CBR implementat

El projecte implementa completament el cicle de les 4 R's del Raonament Basat en Casos:

1. **Retrieve (Recuperació)**: Selecciona els casos més útils mitjançant una funció de similitud global ponderada i l'estratègia *Adaptation-Guided Retrieval*, que prioritza casos fàcilment adaptables a les restriccions del nou usuari.
2. **Reuse (Reutilització i Adaptació)**:
* **Adaptació Simbòlica**: Gestió de restriccions i "Parelles Vetades" (ingredients que l'usuari rebutja junts).
* **Adaptació Subsimbòlica**: Ús de **FlavorGraph** i tècniques de *Vector Steering* per realitzar substitucions creatives d'ingredients basades en perfils moleculars i de sabor.
* **Mòdul de Tècniques**: Selecció i assignació de tècniques de cuina (estàndard o alta cuina) amb un mecanisme de *Rollback* per ajustar-se al pressupost.
* **Mòdul de Begudes**: Maridatge dinàmic basat en afinitat estructural i aromàtica.


3. **Revise (Revisió)**: Avaluació multidimensional (satisfacció global, gust, originalitat). Implementa una **Arquitectura de Memòria Dual** que distingeix entre preferències personals (Canal A) i regles globals de domini apreses per consens (Canal B).
4. **Retain (Retenció)**: Política de retenció selectiva que aprèn nous casos si són prou útils, nous i segurs.

## Tecnologies

* **Python**: Nucli de la lògica i orquestració del cicle CBR.
* **FlavorGraph**: Embeddings vectorials pre-entrenats per al càlcul de distàncies semàntiques i químiques entre ingredients.
* **Gemini API (LLM)**: Utilitzat exclusivament com a capa de formalització per generar la redacció final de la carta i les presentacions dels plats.
* **Hugging Face**: Generació d'imatges dels menús per a una experiència visual completa.

## Estructura del repositori

* `/src`: Implementació de les fases del cicle (`Retriever.py`, `Revise.py`, `Retain.py`) i operadors especialitzats (ingredients, begudes, tècniques).
* `/data`: Base de coneixement (ingredients, begudes, estils) i memòria del sistema (base de casos, regles apreses).
* `/models`: Representació matemàtica del *FlavorGraph* (`.pickle`).

## Com executar

1. Instal·la les dependències de Python necessàries.
2. Configura la teva clau d'API per a Gemini (opcional, per a la generació de text avançada).
3. Executa l'orquestrador principal:

```bash
python src/main.py

```

## Resultats i Explicabilitat (XCBR)

El sistema destaca per la seva transparència i capacitat d'aprenentatge:

* **Explicabilitat**: Totes les decisions (maridatges, substitucions per al·lèrgia) es justifiquen a l'usuari final en llenguatge natural.
* **Aprenentatge Actiu**: Quan diversos usuaris rebutgen una combinació (ex: llobarro amb tòfona), el sistema genera automàticament una **Regla de Restricció Global**.
* **Robustesa**: Validat mitjançant jocs de prova complexos que inclouen des de sopars informals fins a banquets corporatius massius amb múltiples restriccions dietètiques simultànies.
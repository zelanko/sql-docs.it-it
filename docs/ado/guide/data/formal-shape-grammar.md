---
title: Grammatica forma formale | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: rothja
ms.author: jroth
ms.openlocfilehash: ce65f6961502a5bfe43278e4a29a11c4210d4af8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758257"
---
# <a name="formal-shape-grammar"></a>Grammatica formale per Shape
Si tratta della grammatica formale per la creazione di qualsiasi comando Shape:  
  
-   I termini grammaticali richiesti sono stringhe di testo delimitate da parentesi angolari ("<>").  
  
-   I termini facoltativi sono delimitati da parentesi quadre ("[]").  
  
-   Le alternative sono indicate da un rovesciata ("&#124;").  
  
-   Le alternative ripetute sono indicate da puntini di sospensione ("...").  
  
-   *Alfa* indica una stringa di lettere alfabetiche.  
  
-   *Digit* indica una stringa di numeri.  
  
-   *Unicode-digit* indica una stringa di cifre Unicode.  
  
 Tutti gli altri termini sono valori letterali.  
  
|Termine|Definizione|  
|----------|----------------|  
|\<Shape-comando>|SHAPE [ \< Table-exp> [[As] \< alias>]] [ \< shape-Action>]|  
|\<tabella-> exp|{ \< provider-comando-testo>} &#124;<br /><br /> ( \< Shape-command>) &#124;<br /><br /> TABELLA con \< virgolette-nome> &#124;<br /><br /> \<nome tra virgolette>|  
|\<forma-azione>|ACCODAre gli \< alias-field-list> &#124;<br /><br /> Compute \< Aliased-field-list> [by \< field-list>]|  
|\<con alias-Field-List>|\<con alias-Field> [, con \< alias-Field... >]|  
|\<con alias-Field>|\<Field-exp> [[AS] \< alias>]|  
|\<campo-> exp|( \< relazione-exp>) &#124;<br /><br /> \<calcolato-exp> &#124;<br /><br /> \<aggregazione-> &#124; exp<br /><br /> \<nuovo-> exp|  
|<relation_exp>|\<Table-exp> [[AS] \< alias>]<br /><br /> CORRELAre \< Relation-cond-list>|  
|\<relazione-cond-list>|\<relation-cond> [, \< relazione-cond>...]|  
|\<relazione-> cond|\<Nome-campo> al \<> di riferimento figlio|  
|\<> di riferimento figlio|\<Nome campo> &#124;<br /><br /> PARAMETRO \< param-ref>|  
|\<> param-Ref|\<numero>|  
|\<> elenco campi|\<Nome-campo> [, \< nome-campo>]|  
|\<aggregazione-> exp|SUM ( \< Qualified-Field-name>) &#124;<br /><br /> MEDIA ( \< Qualified-Field-name>) &#124;<br /><br /> MIN ( \< Qualified-Field-name>) &#124;<br /><br /> MAX ( \< Qualified-Field-name>) &#124;<br /><br /> COUNT ( \< qualified-alias> &#124; \< Qualified-Name>) &#124;<br /><br /> STDEV ( \< Qualified-Field-name>) &#124;<br /><br /> ANY ( \< Qualified-Field-name>)|  
|\<calcolato-exp>|CALCOLO ( \< espressione>)|  
|\<Qualified-Field-Name>|\<> alias. [ \< alias>...] \< Nome campo>|  
|\<> alias|\<nome tra virgolette>|  
|\<Nome campo>|\<nome tra virgolette> [[AS] \< alias>]|  
|\<nome tra virgolette>|" \< string>" &#124;<br /><br /> ' \< string>' &#124;<br /><br /> [ \< string>] &#124;<br /><br /> \<nome>|  
|\<nome qualificato>|alias [. alias...]|  
|\<nome>|alfa [alpha &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<numero>|digit [digit...]|  
|\<nuovo-> exp|NUOVO \< tipo di campo> [( \< numero> [, \< numero>])]|  
|\<> di tipo campo|Tipo di dati OLE DB o ADO.|  
|\<> stringa|Unicode-char [Unicode-char...]|  
|\<> espressione|Espressione Visual Basic, Applications Edition i cui operandi sono altre colonne non di calcolo nella stessa riga.|  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso alle righe in un recordset gerarchico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Cenni preliminari sulla data shaping](../../../ado/guide/data/data-shaping-overview.md)   
 [Provider richiesti per la definizione dei dati](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Clausola APPEND della forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandi per la forma in generale](../../../ado/guide/data/shape-commands-in-general.md)   
 [SHAPE COMPUTE-clausola](../../../ado/guide/data/shape-compute-clause.md)   
 [Funzioni di Visual Basic, Applications Edition](../../../ado/guide/data/visual-basic-for-applications-functions.md)

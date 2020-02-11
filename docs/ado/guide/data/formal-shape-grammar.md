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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91bdf0cfbfe87075d2c9484bca7edd835a950ee6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925345"
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
|\<Shape-comando>|SHAPE [\<Table-exp> [[As] \<alias>]] [\<Shape-Action>]|  
|\<tabella-> exp|{\<provider-comando-testo>} &#124;<br /><br /> (\<Shape-Command>) &#124;<br /><br /> TABELLA \<con virgolette-nome> &#124;<br /><br /> \<nome tra virgolette>|  
|\<forma-azione>|ACCODAre \<gli alias-Field-List> &#124;<br /><br /> Compute \<Aliased-Field-List> [by \<Field-List>]|  
|\<con alias-Field-List>|\<con alias-Field> [, \<con alias-Field... >]|  
|\<con alias-Field>|\<Field-exp> [[AS] \<alias>]|  
|\<campo-> exp|(\<relazione-exp>) &#124;<br /><br /> \<calcolato-exp> &#124;<br /><br /> \<aggregazione-> &#124; exp<br /><br /> \<nuovo-> exp|  
|<relation_exp>|\<Table-exp> [[AS] \<alias>]<br /><br /> CORRELAre \<relation-cond-list>|  
|\<relazione-cond-list>|\<relation-cond> [, \<relazione-cond>...]|  
|\<relazione-> cond|\<Nome-campo> al \<> di riferimento figlio|  
|\<> di riferimento figlio|\<Nome campo> &#124;<br /><br /> PARAMETRO \<param-Ref>|  
|\<> param-Ref|\<numero>|  
|\<> elenco campi|\<Nome-campo> [, \<nome-campo>]|  
|\<aggregazione-> exp|SUM (\<Qualified-Field-Name>) &#124;<br /><br /> MEDIA (\<Qualified-Field-Name>) &#124;<br /><br /> MIN (\<Qualified-Field-Name>) &#124;<br /><br /> MAX (\<Qualified-Field-Name>) &#124;<br /><br /> COUNT (\<qualified-alias> &#124; \<Qualified-Name>) &#124;<br /><br /> STDEV (\<Qualified-Field-Name>) &#124;<br /><br /> ANY (\<Qualified-Field-Name>)|  
|\<calcolato-exp>|CALCOLO (\<espressione>)|  
|\<Qualified-Field-Name>|\<> alias. [\<alias>...] \<nome campo>|  
|\<> alias|\<nome tra virgolette>|  
|\<Nome campo>|\<nome tra virgolette> [[AS] \<alias>]|  
|\<nome tra virgolette>|"\<String>" &#124;<br /><br /> '\<String>' &#124;<br /><br /> [\<String>] &#124;<br /><br /> \<nome>|  
|\<nome qualificato>|alias [. alias...]|  
|\<nome>|alfa [alpha &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<numero>|digit [digit...]|  
|\<nuovo-> exp|NUOVO \<tipo di campo> [(\<numero> [, \<numero>])]|  
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

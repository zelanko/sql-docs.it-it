---
title: Forma clausola APPEND | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e09113b42f655a3b94ab3877ff81f2553a363931
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924187"
---
# <a name="shape-append-clause"></a>Clausola APPEND di Shape
Clausola APPEND forma comando aggiunge una o più colonne a un **Recordset**. Spesso, queste colonne sono le colonne a capitoli, che fanno riferimento a un elemento figlio **Recordset**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Descrizione  
 Come indicato di seguito sono riportate le parti di questa clausola:  
  
 *parent-command*  
 Zero o uno dei seguenti (è possibile omettere il *comando padre* completamente):  
  
-   Un comando del provider racchiuso tra parentesi graffe ("{}") che restituisce un **Recordset** oggetto. Viene eseguito il comando per il provider di dati sottostante e la relativa sintassi dipende dai requisiti del provider. Si tratterà in genere il linguaggio SQL, anche se ADO non richiede alcun linguaggio di query specifico.  
  
-   Un altro comando shape incorporati racchiuso tra parentesi.  
  
-   La parola chiave nella tabella, seguita dal nome di una tabella nel provider di dati.  
  
 *parent-alias*  
 Alias facoltativo che fa riferimento all'elemento padre **Recordset**.  
  
 *column-list*  
 Uno o più delle operazioni seguenti:  
  
-   Una colonna aggregata.  
  
-   Una colonna calcolata.  
  
-   Una nuova colonna creata utilizzando la nuova clausola.  
  
-   Una colonna del capitolo. Definizione di una colonna capitolo è racchiuso tra parentesi ("()"). Vedere la sintassi seguente.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>Note  
 *child-recordset*  
 -   Un comando del provider racchiuso tra parentesi graffe ("{}") che restituisce un **Recordset** oggetto. Viene eseguito il comando per il provider di dati sottostante e la relativa sintassi dipende dai requisiti del provider. Si tratterà in genere il linguaggio SQL, anche se ADO non richiede alcun linguaggio di query specifico.  
  
-   Un altro comando shape incorporati racchiuso tra parentesi.  
  
-   Il nome di un oggetto esistente data shaping **Recordset**.  
  
-   La parola chiave nella tabella, seguita dal nome di una tabella nel provider di dati.  
  
 *child-alias*  
 Un alias che fa riferimento all'elemento figlio **Recordset**.  
  
 *parent-column*  
 Una colonna nel **Recordset** restituiti dai *comando padre.*  
  
 *child-column*  
 Una colonna nel **Recordset** restituiti dai *comando figlio*.  
  
 *param-number*  
 Visualizzare [funzionamento dei comandi con parametri](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *chapter-alias*  
 Un alias che fa riferimento alla colonna del capitolo aggiunta all'elemento padre.  
  
> [!NOTE]
>  Il *"-la colonna padre* TO *colonna figlio"* clausola è effettivamente un elenco, in cui ogni relazione definita è separato da una virgola  
  
> [!NOTE]
>  La clausola dopo la parola chiave accodamento è effettivamente un elenco, in cui ogni clausola è separato da una virgola e definisce un'altra colonna da aggiungere all'elemento padre.  
  
## <a name="remarks"></a>Note  
 Quando si costruisce i comandi del provider dall'input dell'utente come parte di un comando SHAPE, SHAPE li considererà il fornito dall'utente un comando del provider come una stringa opaca e passarle fedele al provider. Ad esempio, nel comando seguente, forma  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 FORMA eseguirà due comandi: `select * from t1` e (`select * from t2 RELATE k1 TO k2)`. Se l'utente fornisce un comando composto costituita da più provider comandi separati da punti e virgola, forma non è in grado di distinguere la differenza. Quindi, il comando seguente di forma,  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 FORMA viene eseguita `select * from t1; drop table t1` e (`select * from t2 RELATE k1 TO k2),` senza rendersi conto che `drop table t1` è separato e nel comando in questo caso, pericoloso, provider. Le applicazioni devono sempre convalidare l'input dell'utente per impedire attacchi di questo tipo potenziali pirati informatici.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Funzionamento dei comandi senza parametri](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Funzionamento dei comandi con parametri](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Comandi ibridi](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Clausole COMPUTE intermedie di Shape](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)

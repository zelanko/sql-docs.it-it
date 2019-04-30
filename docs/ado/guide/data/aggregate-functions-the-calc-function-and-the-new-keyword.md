---
title: Aggregazione di funzioni, funzione CALC e parola chiave NEW | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76fbb95117b1aae982242f24dc2cb1e815bc2356
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063097"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>Funzioni di aggregazione, funzione CALC e parola chiave NEW
Il data shaping supporta le funzioni seguenti. Il nome assegnato al capitolo contenente la colonna da utilizzare è il *capitolo-alias*.  
  
 Un capitolo-alias può essere completo, costituito da ogni nome di colonna per il capitolo contenente le *-nome della colonna,* tutti separati da punti. Ad esempio, se il capitolo di padre, Cap1, include un capitolo figlio, Cap2, che dispone di una colonna amount amt, quindi il nome completo sarebbe chap1.chap2.amt.  
  
|Funzioni di aggregazione|Descrizione|  
|-------------------------|-----------------|  
|SUM (*capitolo-alias*. *nome della colonna*)|Calcola la somma di tutti i valori nella colonna specificata.|  
|AVG (*capitolo-alias*. *nome della colonna*)|Calcola la media di tutti i valori nella colonna specificata.|  
|MAX (*capitolo-alias*. *nome della colonna*)|Calcola il valore massimo nella colonna specificata.|  
|MIN (*capitolo-alias*. *nome della colonna*)|Calcola il valore minimo nella colonna specificata.|  
|CONTEGGIO (*capitolo-alias*[. *nome della colonna*])|Conta il numero di righe nell'alias specificato. Se viene specificata una colonna, solo le righe per cui tale colonna è diverso da Null vengono incluse nel conteggio.|  
|STDEV(*chapter-alias*.*column-name*)|Calcola la deviazione standard della colonna specificata.|  
|QUALSIASI (*capitolo-alias*. *nome della colonna*)|Valore della colonna specificata. QUALSIASI ha un valore stimabile solo quando il valore della colonna è uguale per tutte le righe nel capitolo.<br /><br /> **Nota** se la colonna non contiene lo stesso valore per tutte le righe nel capitolo, il comando SHAPE arbitrariamente restituisce uno dei valori come il valore della funzione ANY.|  
  
|espressione calcolata|Descrizione|  
|---------------------------|-----------------|  
|CALC (*espressione*)|Calcola un'espressione arbitraria, ma solo sulla riga del **Recordset** contenente la funzione CALC. Qualsiasi espressione usando queste [Visual Basic for Applications (VBA) funzioni](../../../ado/guide/data/visual-basic-for-applications-functions.md) è consentito.|  
  
|NUOVA parola chiave|Descrizione|  
|-----------------|-----------------|  
|NUOVE *-tipo di campo* [(*larghezza* &#124; *scala* &#124; *precisione* &#124; *errore*[, *scalabilità* &#124; *errore*])]|Aggiunge una colonna vuota del tipo specificato per il **Recordset**.|  
  
 Il *-tipo di campo* passato con la nuova parola chiave può essere uno dei seguenti tipi di dati.  
  
|Tipi di dati OLE DB|Equivalenti di tipi di dati ADO|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary, AdVarBinary, adLongVarBinary|  
|DBTYPE_STR|adChar, adVarChar, adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 Quando il nuovo campo è di tipo decimale (in OLE DB DBTYPE_DECIMAL, o in ADO, adDecimal), è necessario specificare i valori di precisione e scala.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)

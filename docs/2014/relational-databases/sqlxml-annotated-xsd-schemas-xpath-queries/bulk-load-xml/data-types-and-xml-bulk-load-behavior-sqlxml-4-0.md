---
title: Tipi di dati e comportamento del caricamento bulk XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 34b03423f3bb88166d0d9ce5b0df450d4455e7ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068171"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipi di dati e comportamento del caricamento bulk XML (SQLXML 4.0)
  I tipi di dati specificati nello schema di mapping (tipo XSD o XDR e `sql:datatype`) vengono in genere ignorati ad eccezione dei casi seguenti:  
  
 In XSD:  
  
-   Se il tipo è `dateTime` o `time`, è necessario specificare `sql:datatype` in quanto il caricamento bulk XML esegue la conversione dei dati prima di inviare i dati a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando si esegue il caricamento bulk in una colonna di `uniqueidentifier` tipo in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e il valore XSD è un GUID che include parentesi graffe ({e}), è necessario specificare **SQL: DataType = "uniqueidentifier"** per rimuovere le parentesi graffe prima che il valore venga inserito nella colonna. Se non si specifica `sql:datatype`, il valore viene inviato con le parentesi graffe e l'inserimento non viene  eseguito.  
  
 Per ulteriori informazioni su `sql:datatype` , vedere [coercizione del tipo di dati e l'annotazione sql: DataType &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 In XDR:  
  
-   Se `dt:type` è `datetime`, `time`, `dateTime.tz` o `time.tz`, è necessario specificare i tipi di dati `dt:type` e `sql:datatype`, in quanto il caricamento bulk XML esegue la conversione dei dati prima di inviarli a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se i dati XML sono di tipo `uuid` , è `sql:datatype` necessario specificare. è necessario anche **DT: Type = "UUID"** , a meno che i dati non siano dati di tipo stringa. Se non si specifica `dt:uuid`, il caricamento bulk XML accetta stringhe con parentesi graffe e le rimuove, se necessario.  
  
-   Se i dati XML sono di tipo `bin.base64` o `bin.hex`, è necessario specificare il tipo di dati XML con `dt:type`. Il caricamento bulk XML carica quindi i dati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come rappresentazione esadecimale dei dati.  
  
  

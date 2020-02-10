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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d2eb9af2b353760f5b195b95d6a9f9d5d1efc9b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013421"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipi di dati e comportamento del caricamento bulk XML (SQLXML 4.0)
  I tipi di dati specificati nello schema di mapping (tipo XSD o XDR e `sql:datatype`) vengono in genere ignorati ad eccezione dei casi seguenti:  
  
 In XSD:  
  
-   Se il tipo è `dateTime` o `time`, è necessario specificare `sql:datatype` in quanto il caricamento bulk XML esegue la conversione dei dati prima di inviare i dati a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando si esegue il caricamento bulk in una colonna `uniqueidentifier` di tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in e il valore XSD è un GUID che include parentesi graffe ({e}), è necessario specificare **SQL: DataType = "uniqueidentifier"** per rimuovere le parentesi graffe prima che il valore venga inserito nella colonna. Se non si specifica `sql:datatype`, il valore viene inviato con le parentesi graffe e l'inserimento non viene  eseguito.  
  
 Per ulteriori informazioni su `sql:datatype`, vedere [coercizione del tipo di dati e l'annotazione sql: datatype &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 In XDR:  
  
-   Se `dt:type` è `datetime`, `time`, `dateTime.tz` o `time.tz`, è necessario specificare i tipi di dati `dt:type` e `sql:datatype`, in quanto il caricamento bulk XML esegue la conversione dei dati prima di inviarli a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se i dati XML sono di tipo `uuid`, `sql:datatype` è necessario specificare. è necessario anche **DT: Type = "UUID"** , a meno che i dati non siano dati di tipo stringa. Se non si specifica `dt:uuid`, il caricamento bulk XML accetta stringhe con parentesi graffe e le rimuove, se necessario.  
  
-   Se i dati XML sono di tipo `bin.base64` o `bin.hex`, è necessario specificare il tipo di dati XML con `dt:type`. Il caricamento bulk XML carica quindi i dati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come rappresentazione esadecimale dei dati.  
  
  

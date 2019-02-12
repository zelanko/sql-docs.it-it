---
title: Tipi di dati e XML in blocco il comportamento di caricamento (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3c4f77d06c8beca3c9da7e885a839883f70ec41
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012732"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipi di dati e comportamento del caricamento bulk XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  I tipi di dati specificati nello schema di mapping (tipo XSD o XDR e **SQL: DataType**) vengono in genere ignorate, tranne nei casi seguenti:  
  
 In XSD:  
  
-   Se il tipo è **data/ora** oppure **ora**, è necessario specificare la **SQL: DataType** perché il caricamento Bulk XML esegue la conversione dei dati prima di inviare i dati a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando si esegue un caricamento bulk in una colonna di **uniqueidentifier** digitare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e il valore XSD è un GUID che include parentesi graffe ({e}), è necessario specificare **SQL: DataType = "uniqueidentifier"** a rimuovere le parentesi graffe prima che il valore viene inserito nella colonna. Se **SQL: DataType** non viene specificato, il valore viene inviato con le parentesi graffe e l'inserimento ha esito negativo.  
  
 Per altre informazioni sulle **SQL: DataType**, vedere [coercizioni dei tipi di dati e annotazione SQL: DataType &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 In XDR:  
  
-   Se il **dt: Type** viene **datetime**, **ora**, **dateTime.tz**, o **time.tz**, è necessario specificare sia il **dt: Type** e **SQL: DataType** tipi di dati perché il caricamento Bulk XML esegue la conversione dei dati prima di inviare i dati da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se i dati XML sono di tipo **uuid**, **SQL: DataType** specificare; **dt: Type = "uuid"** anche è obbligatorio, a meno che i dati sono dati di tipo stringa. Se non si specifica **dt:uuid**, il caricamento Bulk XML accetta stringhe con parentesi graffe (e rimuove, se necessario).  
  
-   Se i dati XML **bin.base64** oppure **hex**, è necessario specificare il tipo di dati XML con **dt: Type**. Il caricamento bulk XML carica quindi i dati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come rappresentazione esadecimale dei dati.  
  
  

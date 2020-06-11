---
title: Tipi di dati e comportamento del caricamento bulk XML (SQLXML)
description: Informazioni sui tipi di dati e sul comportamento del caricamento bulk XML in SQLXML 4,0.
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e77e4ca789a2abf5bb664221adb8911dd5a1bae5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529747"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipi di dati e comportamento del caricamento bulk XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  I tipi di dati specificati nello schema di mapping (XSD o XDR e **SQL: DataType**) vengono generalmente ignorati, tranne nei casi seguenti:  
  
 In XSD:  
  
-   Se il tipo è **DateTime** o **Time**, è necessario specificare **SQL: DataType** perché il caricamento bulk XML esegue la conversione dei dati prima di inviare i dati a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Quando si esegue il caricamento bulk in una colonna di tipo **uniqueidentifier** in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e il valore XSD è un GUID che include parentesi graffe ({e}), è necessario specificare **SQL: DataType = "uniqueidentifier"** per rimuovere le parentesi graffe prima che il valore venga inserito nella colonna. Se **SQL: DataType** non è specificato, il valore viene inviato con le parentesi graffe e l'inserimento ha esito negativo.  
  
 Per ulteriori informazioni su **SQL: DataType**, vedere [coercizione del tipo di dati e l'annotazione sql: datatype &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 In XDR:  
  
-   Se **DT: Type** è **DateTime**, **Time**, **DateTime.TZ**o **time.TZ**, è necessario specificare entrambi i tipi di dati **DT: Type** e **SQL: DataType** perché il caricamento bulk XML esegue la conversione dei dati prima di inviare i dati a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Se i dati XML sono di tipo **UUID**, è necessario specificare **SQL: DataType** ; è necessario anche **DT: Type = "UUID"** , a meno che i dati non siano dati di tipo stringa. Se non si specifica **DT: UUID**, il caricamento bulk XML accetta stringhe con parentesi graffe (e le rimuove se necessario).  
  
-   Se i dati XML sono **bin. Base64** o **bin. Hex**, è necessario specificare il tipo di dati XML con **DT: Type**. Il caricamento bulk XML carica quindi i dati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come rappresentazione esadecimale dei dati.  
  
  

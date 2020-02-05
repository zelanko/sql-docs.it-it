---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 404f414a1f4bfe75c3476e0954e810c4b36ddaa3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68002896"
---
# <a name="mssqlserver_12329"></a>MSSQLSERVER_12329
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|12329|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|Testo del messaggio|Tipi di dati char(n) e varchar(n) che usano regole di confronto con una tabella codici diversa da 1252 non supportati con *construct*.|  
  
## <a name="explanation"></a>Spiegazione  
Non utilizzare i tipi di dati char(n) e varchar(n) in cui vengono utilizzate le regole di confronto con una tabella codici diversa da 1252.  
  
## <a name="user-action"></a>Azione dell'utente  
Una situazione imprevista in grado di generare questo errore è:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
Da utilizzare in alternativa:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  

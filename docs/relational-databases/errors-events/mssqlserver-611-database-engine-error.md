---
description: MSSQLSERVER_611
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33076c77372ac62f154fbe5d3c60273447be99e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470963"
---
# <a name="mssqlserver_611"></a>MSSQLSERVER_611
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|611|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|VAR_SIZE_TOO_BIG|  
|Testo del messaggio|Impossibile inserire o aggiornare una riga perché le dimensioni di colonna variabili totali, incluso l'overhead, superano il limite di %d byte.|  
  
## <a name="explanation"></a>Spiegazione  
Le dimensioni di colonna variabili totali sono maggiori del limite consentito dallo schema. L'errore 611 viene restituito quando la colonna variabili supera il limite nel case fisso, se il formato di archiviazione vardecimal è abilitato, o quando le dimensioni della colonna variabili superano il limite consentito in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per un record di dati compresso.  
  
## <a name="user-action"></a>Azione dell'utente  
Ridurre le dimensioni del record.  
  

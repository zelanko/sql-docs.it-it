---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ee98c0144d492b74e8ddc2785b21b76a363eb92
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915935"
---
# <a name="mssqlserver1105"></a>MSSQLSERVER_1105
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1105|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NO_MORE_SPACE_IN_FG|  
|Testo del messaggio|Impossibile allocare spazio per l'oggetto '%.*ls'%.\*ls nel database'%.\*ls'. Il filegroup '%.\*ls' è pieno. Liberare spazio su disco eliminando i file non necessari, eliminando oggetti dal filegroup, aggiungendo file al filegroup oppure attivando l'aumento automatico delle dimensioni per i file esistenti nel filegroup.|  
  
## <a name="explanation"></a>Spiegazione  
 Nel filegroup indicato non vi è spazio disponibile su disco.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire le azioni seguenti per tentare di liberare spazio sufficiente nel filegroup:  
  
-   Attivare l'aumento automatico delle dimensioni dei file.  
  
-   Aggiungere altri file al gruppo di file.  
  
-   Liberare spazio su disco eliminando indici o tabelle che non sono più necessari.  
  
-   Per ulteriori informazioni, vedere "Risoluzione dei problemi relativi a spazio su disco insufficiente" nella documentazione online di SQL Server.  
  
> [!NOTE]  
>  Se un indice si trova in diversi file, `ALTER INDEX REORGANIZE` può restituire un errore 1105 quando uno dei file è pieno. Il processo di riorganizzazione viene bloccato quando il processo prova a spostare le righe nel file pieno. Per risolvere questo problema relativo a tale limitazione, eseguire `ALTER INDEX REBUILD` anziché `ALTER INDEX REORGANIZE` o modificare il limite di aumento delle dimensioni dei file pieni.  
  
  

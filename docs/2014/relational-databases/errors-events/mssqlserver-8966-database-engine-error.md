---
title: MSSQLSERVER_8966 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dee5b45aac6518517434595b0f26ce18d219866b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913163"
---
# <a name="mssqlserver_8966"></a>MSSQLSERVER_8966
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8966|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|Testo del messaggio|Impostare leggere e impostare un latch nella pagina P_ID con tipo di latch TYPE. Impossibile eseguire OPERATION.|  
  
## <a name="explanation"></a>Spiegazione  
 L'operazione di lettura della pagina non è stata eseguita oppure non è stato possibile impostare un latch in una pagina PFS o GAM. È possibile che nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siano segnalati timeout del latch o altri messaggi associati.  
  
## <a name="user-action"></a>Azione dell'utente  
 Controllare il log degli errori di SQL Server per esaminare i messaggi contenuti e risolvere gli errori.  
  
  

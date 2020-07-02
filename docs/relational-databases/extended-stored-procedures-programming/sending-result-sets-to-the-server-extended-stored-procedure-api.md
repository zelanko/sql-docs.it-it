---
title: Invio di set di risultati al server (API delle stored procedure estese)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: c0ba957f0cde17f7accfeee66952fe2488a854bd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767751"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Invio di set di risultati al server (API delle stored procedure estese)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 Quando si invia un set di risultati a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il stored procedure esteso deve chiamare l'API appropriata come indicato di seguito:  
  
-   La funzione **srv_sendmsg** può essere chiamata in qualsiasi ordine prima o dopo l'invio di tutte le righe, se presenti, con **srv_sendrow**. Tutti i messaggi devono essere inviati al client prima dell'invio dello stato di completamento con **srv_senddone**.  
  
-   La funzione **srv_sendrow** viene chiamata una volta per ogni riga inviata al client. Tutte le righe devono essere inviate al client prima dell'invio di qualsiasi messaggio, valore di stato o stato di completamento con **srv_sendmsg**, l'argomento **srv_status** di **srv_pfield**o **srv_senddone**.  
  
-   Quando si invia una riga in cui non sono state definite tutte le colonne con **srv_describe** , l'applicazione genera un messaggio di errore informativo e restituisce FAIL al client. In questo caso, la riga non viene inviata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di stored procedure estese](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  

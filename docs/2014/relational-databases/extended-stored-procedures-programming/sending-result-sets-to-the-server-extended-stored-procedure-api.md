---
title: Invio di set di risultati al server (API stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a58c8eca585bbbe2c935c524840bc465992d45c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62511846"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Invio di set di risultati al server (API delle stored procedure estese)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Usare invece l'integrazione con CLR.  
  
 Quando si invia un set di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]risultati a, il stored procedure esteso deve chiamare l'API appropriata come indicato di seguito:  
  
-   La funzione **srv_sendmsg** può essere chiamata in qualsiasi ordine prima o dopo l'invio di tutte le righe, se presenti, con **srv_sendrow**. Tutti i messaggi devono essere inviati al client prima dell'invio dello stato di completamento con **srv_senddone**.  
  
-   La funzione **srv_sendrow** viene chiamata una volta per ogni riga inviata al client. Tutte le righe devono essere inviate al client prima dell'invio di qualsiasi messaggio, valore di stato o stato di completamento con **srv_sendmsg**, l'argomento **srv_status** di **srv_pfield**o **srv_senddone**.  
  
-   Quando si invia una riga in cui non sono state definite tutte le colonne con **srv_describe** , l'applicazione genera un messaggio di errore informativo e restituisce FAIL al client. In questo caso, la riga non viene inviata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di stored procedure estese](creating-extended-stored-procedures.md)  
  
  

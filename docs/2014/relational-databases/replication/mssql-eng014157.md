---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4120808754eb4b76d8b81d2342a49ebc2e4f9dba
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049175"
---
# <a name="mssql_eng014157"></a>MSSQL_ENG014157
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14157|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|La sottoscrizione creata dal Sottoscrittore '%s' della pubblicazione '%s' è scaduta ed è stata eliminata.|  
  
## <a name="explanation"></a>Spiegazione  
 Un Sottoscrittore deve eseguire la sincronizzazione con il server di pubblicazione durante l'intervallo di tempo specificato nel periodo di memorizzazione della pubblicazione. Se la sincronizzazione non viene eseguita in tale intervallo, la sottoscrizione scade. Per altre informazioni, vedere [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
## <a name="user-action"></a>Azione dell'utente  
 La sottoscrizione deve essere ricreata e inizializzata prima che il Sottoscrittore possa iniziare a ricevere nuovamente le modifiche ai dati:  
  
-   Per informazioni sulla creazione di sottoscrizioni, vedere [Sottoscrivere le pubblicazioni](subscribe-to-publications.md).  
  
-   Per informazioni sull'inizializzazione delle sottoscrizioni, vedere [Inizializzare una sottoscrizione](initialize-a-subscription.md).  
  
 Se nel database di sottoscrizione sono contenute modifiche che non sono state sincronizzate con il server di pubblicazione, è possibile utilizzare la [tablediff Utility](../../tools/tablediff-utility.md) per determinare quali righe sono diverse nei database di pubblicazione e sottoscrizione.  
  
 Per evitare che le sottoscrizioni scadano, è possibile incrementare il periodo di memorizzazione della pubblicazione. Prestare attenzione quando si imposta un valore elevato poiché può determinare la memorizzazione di una quantità maggiore di dati e metadati, con una conseguente riduzione delle prestazioni. Per altre informazioni, vedere [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  

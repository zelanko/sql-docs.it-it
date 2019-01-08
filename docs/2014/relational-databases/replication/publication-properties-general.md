---
title: Proprietà pubblicazione, Generale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.general.f1
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9b04098ad26cd4cf539fde4f1f826e4e6d1ce5c0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786173"
---
# <a name="publication-properties-general"></a>Proprietà pubblicazione, Generale
  La pagina **Generale** della finestra di dialogo **Proprietà pubblicazione** contiene informazioni di base sulla pubblicazione, tra cui il nome, la descrizione e i criteri di scadenza della sottoscrizione.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Nome del database della pubblicazione (informazione di sola lettura).  
  
 **Database**  
 Nome del database di pubblicazione (informazione di sola lettura).  
  
 **Descrizione**  
 Descrizione della pubblicazione.  
  
 **Tipo**  
 Tipo di pubblicazione (informazione di sola lettura).  
  
 **Scadenza sottoscrizione**  
 Selezionare una delle opzioni per la scadenza della sottoscrizione: **Le sottoscrizioni non scadono mai** oppure **le sottoscrizioni scadono**, con un periodo di tempo esplicito (**intervallo**).  
  
 Per le pubblicazioni snapshot e transazionali, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di accettare l'impostazione predefinita **Le sottoscrizioni non hanno scadenza**.  
  
 Per la replica di tipo merge, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di accettare l'impostazione predefinita **Le sottoscrizioni scadono** e di impostare il valore più basso possibile per **Intervallo**. Più è alto il valore del periodo di tempo di scadenza, maggiore è la quantità di metadati archiviati, con conseguenti possibili effetti negativi sulle prestazioni. Raggiungere un equilibrio tra la necessità di disconnettere i Sottoscrittori o semplicemente di non consentire ai Sottoscrittori di eseguire la sincronizzazione per un periodo di tempo esteso e i potenziali problemi di prestazioni derivanti dall'archiviazione e dall'elaborazione di grandi quantità di metadati.  
  
 Per altre informazioni, vedere [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
 **Livello di compatibilità**  
 Solo per[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Solo per le pubblicazioni di tipo merge. Consente di selezionare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] minima richiesta per i Sottoscrittori che eseguono la sincronizzazione con la pubblicazione. Il livello di compatibilità viene determinato da una serie di regole associate.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)  
  
  

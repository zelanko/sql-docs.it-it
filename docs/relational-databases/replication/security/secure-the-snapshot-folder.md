---
title: Proteggere la cartella snapshot | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], security
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 30e0f800477af8305f64b617aa3af543e789bdc1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051887"
---
# <a name="secure-the-snapshot-folder"></a>Sicurezza della cartella snapshot
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La cartella snapshot è una directory in cui vengono archiviati i file di snapshot. È consigliabile dedicare questa directory esclusivamente all'archiviazione degli snapshot. Concedere all'agente snapshot l'autorizzazione di scrittura per la cartella e verificare che l'autorizzazione di lettura sia concessa solo all'account di Windows utilizzato dall'agente di merge o dall'agente di distribuzione per accedere alla cartella. L'account di Windows associato all'agente deve essere un account di dominio per poter accedere a una cartella snapshot posizionata in un computer remoto.  
  
> [!NOTE]  
>  Controllo account utente consente agli amministratori di gestire i propri diritti utente elevati (detti anche *privilegi*). Quando l'esecuzione avviene in sistemi operativi con Controllo account utente abilitato, gli amministratori non utilizzano i propri diritti amministrativi, ma eseguono la maggior parte delle azioni come utenti standard (non amministrativi), assumendo temporaneamente i diritti di amministratore solo se necessario. Controllo account utente può impedire l'accesso amministrativo alla condivisione snapshot. Le autorizzazioni per la condivisione snapshot devono pertanto essere concesse in modo esplicito agli account di Windows utilizzati dall'agente snapshot, dall'agente di distribuzione e dall'agente di merge. È necessario eseguire questa operazione anche se gli account di Windows sono membri del gruppo Administrators.  
  
 Se si configura un server di distribuzione tramite Configurazione guidata distribuzione o Creazione guidata pubblicazione, la cartella snapshot viene configurata per impostazione predefinita su un percorso locale: X:\Programmi\Microsoft SQL Server\\ *\<istanza>* \MSSQL\ReplData. Se si usano un server di distribuzione remoto o sottoscrizioni pull, è necessario specificare una condivisione di rete UNC (ad esempio \\\\<*nomecomputer>* \snapshot) anziché un percorso locale.  
  
 Quando si concedono le autorizzazioni di accesso alla cartella snapshot, è necessario valutare il tipo di accesso che verrà utilizzato per la cartella. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2003 vengono utilizzate le schede di finestre di dialogo seguenti:  
  
-   Se si specifica un percorso locale, concedere le autorizzazioni mediante la scheda **Sicurezza** della finestra di dialogo **Proprietà** per la cartella.  
  
-   Se si specifica una condivisione di rete, concedere le autorizzazioni mediante la scheda **Condivisione** della finestra di dialogo **Proprietà** per la cartella.  
  
    > [!NOTE]  
    >  Se l'agente di replica viene eseguito nel server di distribuzione, utilizzare la scheda **Sicurezza** della finestra di dialogo **Proprietà** della cartella per concedere autorizzazioni all'account di Windows utilizzato per l'esecuzione dell'agente. Eseguire questa operazione anche in caso di utilizzo di una condivisione di rete. Ciò è applicabile all'agente di merge e all'agente di distribuzione per una sottoscrizione push e all'agente snapshot quando il server di pubblicazione e il server di distribuzione risiedono nello stesso computer.  
  
 Per ulteriori informazioni sull'impostazione di autorizzazioni per i percorsi locali e le condivisioni di rete, vedere la documentazione di Windows.  
  
> [!NOTE]  
>  Se una pubblicazione viene rimossa, la replica tenta di rimuovere la cartella snapshot nel contesto di sicurezza dell'account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se questo account non dispone di privilegi sufficienti, accedere con un account che dispone di privilegi adeguati e rimuovere manualmente la cartella. Per rimuovere una cartella, è necessario il privilegio **Modifica** se la cartella si trova in un percorso locale oppure il privilegio **Controllo completo** se la cartella è una condivisione di rete.  
  
## <a name="delivering-snapshots-through-ftp"></a>Recapito di snapshot tramite FTP  
 Sebbene sia consigliabile dal punto di vista della sicurezza archiviare gli snapshot in una condivisione UNC, gli snapshot possono essere archiviati in una condivisione FTP e quindi recapitati a un Sottoscrittore tramite FTP. Quando si configura il server FTP, verificare che la directory virtuale esponga una condivisione UNC sottostante che consente l'accesso in scrittura all'agente snapshot per la pubblicazione.  
  
 Per configurare un Sottoscrittore in modo che recuperi lo snapshot tramite FTP, impostare innanzitutto un server FTP con un account di accesso e password per l'FTP che consenta ai Sottoscrittori l'accesso in lettura per poter scaricare i file di snapshot.  
  
 Per recapitare uno snapshot tramite FTP, vedere [Recapitare uno snapshot tramite FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 Per informazioni sull'impostazione e la modifica delle password per l'accesso agli snapshot tramite FTP, vedere la sezione relativa al recapito degli snapshot tramite FTP in [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le opzioni snapshot](../../../relational-databases/replication/snapshot-options.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Trasferire snapshot tramite FTP](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)  
  
  

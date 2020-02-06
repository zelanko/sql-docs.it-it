---
title: Inizializzare una sottoscrizione con uno snapshot | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3624d1eef64f10ae93802c4a7514fd54edcc0e74
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287928"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inizializzazione di una sottoscrizione con uno snapshot
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Al termine della creazione di una pubblicazione, uno snapshot iniziale viene in genere creato e copiato nella cartella snapshot. Per impostazione predefinita, queste operazioni vengono eseguite per le pubblicazioni di tipo merge create mediante la Creazione guidata nuova pubblicazione. Viene quindi applicato al Sottoscrittore dall'agente di distribuzione (per le pubblicazioni transazionali e snapshot) o dall'agente di merge (per le pubblicazioni di tipo merge) durante la sincronizzazione iniziale della sottoscrizione. Il processo di snapshot dipende dal tipo di pubblicazione:  
  
-   Se lo snapshot è per una pubblicazione snapshot, una pubblicazione transazionale o una pubblicazione di tipo merge che non utilizza filtri con parametri, lo snapshot contiene lo schema e i dati nei file di programma per la copia bulk, nonché vincoli, proprietà estese, indici, trigger e le tabelle di sistema necessarie per la replica. Per altre informazioni sulla creazione e l'applicazione dello snapshot, vedere [Creare e applicare lo snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
-   Se lo snapshot è per una pubblicazione di tipo merge che utilizza filtri con parametri, verrà creato utilizzando un processo a due fasi. Viene innanzitutto creato uno snapshot dello schema contenente gli script di replica e lo schema degli oggetti pubblicati, ma non i dati. Ogni sottoscrizione viene quindi inizializzata con uno snapshot che include gli script e lo schema copiati dallo snapshot dello schema e i dati appartenenti alla partizione della sottoscrizione. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Lo snapshot è costituito da file diversi a seconda del tipo di replica e degli articoli contenuti nella pubblicazione. Tali file vengono copiati nella cartella snapshot predefinita specificata al momento della configurazione del server di distribuzione o in quella alternativa specificata al momento della creazione della pubblicazione.  
  
|Tipo di replica|File di snapshot comuni|  
|-------------------------|---------------------------|  
|Replica snapshot o transazionale|schema (sch), dati (bcp), vincoli e indici (dri), vincoli (idx), trigger (trg) solo per l'aggiornamento dei Sottoscrittori, file di snapshot compressi (cab)|  
|Replica di tipo merge|schema (sch), dati (bcp), vincoli e indici (dri), trigger (trg), dati di tabelle di sistema (sys), tabelle dei conflitti (cft), file di snapshot compressi (cab)|  
  
 Se il trasferimento dello snapshot viene interrotto in un punto, verrà ripreso automaticamente senza rinviare i file il cui trasferimento è stato completato. L'unità di recapito per l'agente snapshot è il file con estensione bcp per ogni articolo della pubblicazione e pertanto i file recapitati solo in parte devono essere recapitati nuovamente per intero. Il ripristino dello snapshot, tuttavia, può comportare una riduzione significativa della quantità di dati trasmessi e garantire il recapito dello snapshot in tempo utile anche se la connessione non è affidabile.  
  
## <a name="snapshot-options"></a>Opzioni per gli snapshot  
 Quando si inizializza una sottoscrizione con uno snapshot È possibile:  
  
-   Specificare una posizione alternativa per la cartella snapshot in aggiunta a quella predefinita o al posto di questa. Per altre informazioni, vedere [Modificare le opzioni snapshot](../../relational-databases/replication/snapshot-options.md).  
  
-   Comprimere gli snapshot per l'archiviazione sui supporti rimovibili o il trasferimento su una rete lenta. Per altre informazioni, vedere [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots). 

-   Eseguire gli script Transact-SQL prima o dopo aver applicato lo snapshot. Per altre informazioni, vedere [Eseguire gli script prima e dopo l'applicazione dello snapshot](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Trasferire i file di snapshot mediante il protocollo FTP (File Transfer Protocol). Per altre informazioni, vedere [Trasferire snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione](../../relational-databases/replication/initialize-a-subscription.md)   
 [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  

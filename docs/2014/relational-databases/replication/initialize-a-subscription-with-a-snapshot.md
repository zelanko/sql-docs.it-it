---
title: Inizializzare una sottoscrizione con uno snapshot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: df9cfb95144bbc7db16ff0bb72f96ff3e4465f89
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043220"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inizializzazione di una sottoscrizione con uno snapshot
  Al termine della creazione di una pubblicazione, uno snapshot iniziale viene in genere creato e copiato nella cartella snapshot. Per impostazione predefinita, queste operazioni vengono eseguite per le pubblicazioni di tipo merge create mediante la Creazione guidata nuova pubblicazione. Viene quindi applicato al Sottoscrittore dall'agente di distribuzione (per le pubblicazioni transazionali e snapshot) o dall'agente di merge (per le pubblicazioni di tipo merge) durante la sincronizzazione iniziale della sottoscrizione. Il processo di snapshot dipende dal tipo di pubblicazione:  
  
-   Se lo snapshot è per una pubblicazione snapshot, una pubblicazione transazionale o una pubblicazione di tipo merge che non utilizza filtri con parametri, lo snapshot contiene lo schema e i dati nei file di programma per la copia bulk, nonché vincoli, proprietà estese, indici, trigger e le tabelle di sistema necessarie per la replica. Per altre informazioni sulla creazione e l'applicazione dello snapshot, vedere [Creare e applicare lo snapshot](create-and-apply-the-snapshot.md).  
  
-   Se lo snapshot è per una pubblicazione di tipo merge che utilizza filtri con parametri, verrà creato utilizzando un processo a due fasi. Viene innanzitutto creato uno snapshot dello schema contenente gli script di replica e lo schema degli oggetti pubblicati, ma non i dati. Ogni sottoscrizione viene quindi inizializzata con uno snapshot che include gli script e lo schema copiati dallo snapshot dello schema e i dati appartenenti alla partizione della sottoscrizione. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Lo snapshot è costituito da file diversi a seconda del tipo di replica e degli articoli contenuti nella pubblicazione. Tali file vengono copiati nella cartella snapshot predefinita specificata al momento della configurazione del server di distribuzione o in quella alternativa specificata al momento della creazione della pubblicazione.  
  
|Tipo di replica|File di snapshot comuni|  
|-------------------------|---------------------------|  
|Replica snapshot o transazionale|schema (sch), dati (bcp), vincoli e indici (dri), vincoli (idx), trigger (trg) solo per l'aggiornamento dei Sottoscrittori, file di snapshot compressi (cab)|  
|Replica di tipo merge|schema (sch), dati (bcp), vincoli e indici (dri), trigger (trg), dati di tabelle di sistema (sys), tabelle dei conflitti (cft), file di snapshot compressi (cab)|  
  
 Se il trasferimento dello snapshot viene interrotto in un punto, verrà ripreso automaticamente senza rinviare i file il cui trasferimento è stato completato. L'unità di recapito per l'agente snapshot è il file con estensione bcp per ogni articolo della pubblicazione e pertanto i file recapitati solo in parte devono essere recapitati nuovamente per intero. Il ripristino dello snapshot, tuttavia, può comportare una riduzione significativa della quantità di dati trasmessi e garantire il recapito dello snapshot in tempo utile anche se la connessione non è affidabile.  
  
## <a name="snapshot-options"></a>Opzioni per gli snapshot  
 Quando si inizializza una sottoscrizione con uno snapshot È possibile:  
  
-   Specificare una posizione alternativa per la cartella snapshot in aggiunta a quella predefinita o al posto di questa. Per altre informazioni, vedere [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md).  
  
-   Comprimere gli snapshot per l'archiviazione sui supporti rimovibili o il trasferimento su una rete lenta. Per altre informazioni, vedere [Compressed Snapshots](compressed-snapshots.md).  
  
-   Eseguire gli script Transact-SQL prima o dopo aver applicato lo snapshot. Per altre informazioni, vedere [Eseguire gli script prima e dopo l'applicazione dello snapshot](snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Trasferire i file di snapshot mediante il protocollo FTP (File Transfer Protocol). Per altre informazioni, vedere [Trasferire snapshot tramite FTP](transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione](initialize-a-subscription.md)   
 [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md)  
  
  

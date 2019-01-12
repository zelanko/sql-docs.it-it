---
title: Snapshot compressi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 873a16f8e6dcc73b4f2b3da5727d49207252ca63
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124281"
---
# <a name="compressed-snapshots"></a>Snapshot compressi
  È consigliabile comprimere i file di snapshot quando vengono trasferiti in una rete lenta o salvati su supporti rimovibili in cui lo spazio disponibile non è sufficiente per contenere uno snapshot non compresso. La compressione, pur essendo utile in queste situazioni, richiede più tempo per generare e applicare lo snapshot.  
  
 I file di snapshot compressi vengono scritti nel formato di file [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB, che consente di comprimere file di 2 GB o di dimensione inferiore. La compressione non è invece possibile per file di dimensione superiore a 2 GB. Per comprimere i file, è necessario scriverli in una cartella snapshot alternativa, in quanto non è possibile comprimere i file scritti nella cartella predefinita. Per altre informazioni sui percorsi alternativi delle cartelle snapshot, vedere [Posizioni alternative della cartella snapshot](alternate-snapshot-folder-locations.md).  
  
 I file vengono decompressi nella posizione di esecuzione dell'agente di distribuzione o dell'agente di merge. Con gli snapshot compressi vengono in genere utilizzate sottoscrizioni pull, in modo che i file vengano decompressi nel Sottoscrittore. Quando il Sottoscrittore riceve un file compresso, quest'ultimo viene scritto inizialmente in un percorso temporaneo. Dopo che il file compresso è stato copiato nel Sottoscrittore, i file di snapshot nel file compresso vengono decompressi, in ordine e uno alla volta, tramite l'utilità CAB. Lo spazio necessario nel Sottoscrittore equivale alla somma della dimensione del file compresso e della dimensione del file non compresso più grande.  
  
> [!NOTE]  
>  Gli snapshot compressi, in alcuni casi, consentono di migliorare le prestazioni relative al trasferimento di file di snapshot in rete. La compressione dello snapshot richiede, tuttavia, un'ulteriore elaborazione da parte dell'agente snapshot per la generazione dei file di snapshot e da parte dell'agente di distribuzione o dell'agente di merge per l'applicazione di tali file. Questo può rallentare il processo di generazione degli snapshot e, in alcuni casi, aumentare il tempo necessario per applicarli. Inoltre, poiché non è possibile riprendere gli snapshot compressi in caso di errore della rete, tali snapshot non sono adatti per le reti non affidabili. Quando si utilizzano snapshot compressi in rete, è necessario considerare tutti i pro e contro.  
  
 **Per comprimere e recapitare file di snapshot**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Comprimere i file di snapshot &#40;SQL Server Management Studio&#41;](snapshot-options.md#compress-snapshot-files)  
  
-   Programmazione [!INCLUDE[tsql](../../includes/tsql-md.md)] della replica: [Configurare le proprietà dello snapshot &#40;programmazione Transact-SQL della replica&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Opzioni per gli snapshot](snapshot-options.md)  
  
  

---
title: Posizioni alternative della cartella snapshot | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff65f1f4d5042e3b7c401a47e7c9df795dd681b4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777866"
---
# <a name="alternate-snapshot-folder-locations"></a>Posizioni alternative della cartella snapshot
  Le posizioni alternative della cartella snapshot consentono di archiviare i file di snapshot in una posizione aggiuntiva o diversa da quella predefinita, in genere inclusa nel database di distribuzione. Una posizione alternativa può essere un altro server, un'unità di rete oppure un supporto rimovibile, ad esempio un CD-ROM o un disco rimovibile.  
  
 Le posizioni alternative della cartella snapshot vengono archiviate come proprietà della pubblicazione. Dato che la posizione alternativa della cartella snapshot è una proprietà della pubblicazione, l'agente di distribuzione e l'agente di merge sono in grado di individuare la cartella snapshot corretta durante il processo di sincronizzazione.  
  
 Se si desidera specificare una posizione alternativa della cartella snapshot o comprimere i file di snapshot senza creare immediatamente lo snapshot iniziale, è possibile impostare le proprietà della pubblicazione relative alla posizione dello snapshot e quindi eseguire l'agente snapshot per tale pubblicazione. Se tuttavia si modifica la posizione alternativa dopo avere creato lo snapshot iniziale, è possibile che gli snapshot generati per la pubblicazione non vengano ricollocati nella nuova posizione alternativa. In questo caso, a seconda delle impostazioni di pubblicazione, l'agente di merge o l'agente di distribuzione potrebbero non essere in grado di trovare i file di snapshot nella nuova posizione alternativa.  
  
> [!NOTE]  
>  Evitare di specificare una posizione alternativa che corrisponde alla posizione predefinita della cartella snapshot utilizzando la finestra di dialogo **Proprietà pubblicazione** o [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql).  
  
> [!CAUTION]  
>  Non utilizzare contemporaneamente sia WebSync sia percorsi alternativi della cartella snapshot.  
  
 **Per specificare posizioni alternative della cartella snapshot**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Specificare un percorso alternativo per la cartella snapshot &#40;SQL Server Management Studio&#41;](publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md) 
  
-   Programmazione [!INCLUDE[tsql](../../includes/tsql-md.md)] della replica: [Configurare le proprietà dello snapshot &#40;programmazione Transact-SQL della replica&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Opzioni per gli snapshot](snapshot-options.md)  
  
  

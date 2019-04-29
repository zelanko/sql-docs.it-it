---
title: Configurare FILESTREAM in un cluster di failover | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca95e56a965cb2dd967a673fb33688fd09981960
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920035"
---
# <a name="set-up-filestream-on-a-failover-cluster"></a>Configurazione di FILESTREAM in un cluster di failover
  In questo argomento viene descritto come abilitare FILESTREAM in un cluster di failover. Prima di eseguire questa procedura, è consigliabile acquisire familiarità con il [clustering di failover](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) e abilitare FILESTREAM. Per informazioni su come abilitare FILESTREAM, vedere [Abilitare e configurare FILESTREAM](enable-and-configure-filestream.md).  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>Per configurare FILESTREAM in un cluster di failover  
  
1.  Configurare il nodo primario per il cluster di failover.  
  
     Al termine della configurazione, abilitare FILESTREAM nel nodo primario usando **Gestione configurazione SQL Server**. Verranno abilitate le impostazioni per cui è necessario disporre dei privilegi di amministratore di Windows. Se è necessario usare l'accesso remoto, selezionare **Consenti ai client remoti l'accesso tramite flusso ai dati FILESTREAM**. Verrà creata una risorsa cluster di condivisione file.  
  
2.  Configurare un nodo passivo.  
  
     Al termine della configurazione, abilitare FILESTREAM nel nodo passivo usando **Gestione configurazione SQL Server**. Il nome specificato per **Nome condivisione di Windows** deve essere lo stesso in tutti i nodi del cluster.  
  
3.  Per aggiungere più nodi passivi, ripetere il passaggio 2.  
  
4.  Una volta aggiunti tutti i nodi, completare il processo eseguendo la stored procedure sp_configure in ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Per aggiungere e abilitare nodi aggiuntivi nel cluster in qualsiasi momento, ripetere i passaggi 2, 3 e 4.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [Rimuovere un'istanza del cluster di failover di SQL Server &#40;programma di installazione&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  

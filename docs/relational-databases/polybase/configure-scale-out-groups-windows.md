---
title: Configurare gruppi con scalabilità orizzontale PolyBase in Windows | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: tutorial
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 81bfb5f4e2a69b065d8995823ee87fe9b913d11b
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710619"
---
# <a name="configure-polybase-scale-out-groups-on-windows"></a>Configurare gruppi con scalabilità orizzontale PolyBase in Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive come configurare un [gruppo con scalabilità orizzontale PolyBase](polybase-scale-out-groups.md) in Windows. Questa funzionalità consente di creare un cluster di istanze di SQL Server per elaborare set di dati di grandi dimensioni da origini dati esterne, ad esempio Hadoop o Archiviazione BLOB di Azure, in una soluzione di scalabilità orizzontale che consente di migliorare le prestazioni delle query.

## <a name="prerequisites"></a>Prerequisites
  
- Più di un computer nello stesso dominio  
  
- Un account utente di dominio per l'esecuzione dei servizi PolyBase  
  
## <a name="process-overview"></a>Panoramica del processo

I passaggi seguenti riepilogano il processo per la creazione di un gruppo con scalabilità orizzontale PolyBase. La prossima sezione offre una procedura guidata più dettagliata di ogni passaggio.
  
1. Installare la stessa versione di SQL Server con PolyBase su N computer.
  
2. Selezionare un'istanza di SQL Server come nodo head. Un nodo head può essere definito solo in un'istanza di SQL Server Enterprise.
  
3. Aggiungere le istanze rimanenti di SQL Server come nodi di calcolo usando [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).

4. Monitorare i nodi nel gruppo usando [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).

5. Facoltativo. Rimuovere un nodo di calcolo usando [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="example-walk-through"></a>Procedura dettagliata di esempio

Di seguito vengono illustrati i passaggi per configurare un gruppo di PolyBase con:  
  
1. Due macchine nel dominio *PQTH4A* . I nomi computer sono:  
  
   - PQTH4A-CMP01  
  
   - PQTH4A-CMP02  
  
2. Account di dominio: *PQTH4A\PolyBaseUser*  

## <a name="install-sql-server-with-polybase-on-all-machines"></a>Installare SQL Server con PolyBase in tutti i computer

1. Eseguire setup.exe.
  
2. Nella pagina Selezione funzionalità scegliere **Servizio query PolyBase per i dati esterni**.
  
3. Nella pagina Configurazione server usare l'**account di dominio** PQTH4A\PolyBaseUser per il motore di ricerca PolyBase di SQL Server e SQL Server PolyBase Data Movement Service.
  
4. Nella pagina di configurazione di PolyBase selezionare l'opzione **Usare questa istanza di SQL Server come parte del gruppo PolyBase con scalabilità orizzontale**. Verrà aperto il firewall per consentire le connessioni in ingresso ai servizi di PolyBase.
  
5. Al termine dell'installazione, eseguire **services.msc**. Verificare che SQL Server, il motore PolyBase e PolyBase Data Movement Service siano in esecuzione.
  
   ![Servizi PolyBase](../../relational-databases/polybase/media/polybase-services.png "Servizi PolyBase")  
  
## <a name="select-one-sql-server-as-head-node"></a>Selezionare un'istanza di SQL Server come nodo head  
  
Al termine dell'installazione, entrambi i computer possono fungere da nodi head del gruppo di PolyBase. In questo esempio, si sceglierà "MSSQLSERVER" in PQTH4A-CMP01 come nodo head.
  
## <a name="add-other-sql-server-instances-as-compute-nodes"></a>Aggiungere altre istanze di SQL Server come nodi di calcolo  
  
1. Connettersi a SQL Server su PQTH4A-CMP02.
  
2. Eseguire la stored procedure [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).

   ```sql
   -- Enter head node details:
   -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';
   ```  

3. Eseguire services.msc sul nodo di calcolo, PQTH4A-CMP02.
  
4. Arrestare il motore PolyBase e riavviare PolyBase Data Movement Service.
  
## <a name="optional-remove-a-compute-node"></a>Facoltativo: Rimuovere un nodo di calcolo  
  
1. Connettersi al nodo di calcolo PQTH4A-CMP02 per SQL Server.
  
2. Eseguire la stored procedure sp_polybase_leave_group.
  
    ```sql  
    EXEC sp_polybase_leave_group;  
    ```  
  
3. Eseguire services.msc sul nodo di calcolo da rimuovere, PQTH4A-CMP02.
  
4. Avviare il motore PolyBase. Riavviare PolyBase Data Movement Service.
  
5. Verificare che il nodo sia stato rimosso eseguendo la DMV sys.dm_exec_compute_nodes su PQTH4A-CMP01. A questo punto, PQTH4A-CMP02 funzionerà come un nodo head autonomo  
  
## <a name="next-steps"></a>Passaggi successivi  

Per la risoluzione dei problemi, vedere [PolyBase troubleshooting with dynamic management views](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).
  
Per altre informazioni su PolyBase, vedere la [panoramica di PolyBase](../../relational-databases/polybase/polybase-guide.md).

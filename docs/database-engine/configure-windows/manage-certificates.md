---
title: Gestione dei certificati (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88e35bc2589f30a0fa3d6b707d66aa25325dc89e
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/28/2019
ms.locfileid: "55088991"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>Gestione dei certificati (Gestione configurazione SQL Server)

Questo argomento descrive come distribuire e gestire i certificati in una topologia con gruppi di disponibilità o cluster di failover Always On di SQL Server.

I certificati SSL/TLS sono molto usati per proteggere l'accesso a SQL Server. Con le versioni precedenti di SQL Server le organizzazioni con grandi quantità di SQL Server dovevano compiere sforzi considerevoli per gestire la propria infrastruttura di certificati per SQL Server, spesso sviluppando script ed eseguendo comandi manuali. In SQL Server 2019 la gestione dei certificati è integrata in Gestione configurazione SQL Server e questo semplifica varie attività comuni, ad esempio: 

* Visualizzazione e convalida di certificati installati in un'istanza di SQL Server. 
* Identificazione dei certificati prossimi alla scadenza. 
* Distribuzione dei certificati ai computer appartenenti a gruppi di disponibilità dal nodo che contiene la replica primaria. 
* Distribuzione dei certificati ai computer appartenenti a un'istanza del cluster di failover dal nodo attivo.

> [!NOTE]
> È possibile usare la gestione dei certificati in Gestione configurazione SQL Server con versioni precedenti di SQL Server, a partire da SQL Server 2008.

##  <a name="provision-single-server-cert"></a> Per installare un certificato per una singola istanza di SQL Server  
  
1. Nel riquadro della console di Gestione configurazione SQL Server espandere **Configurazione di rete SQL Server**.  
  
2. Fare clic con il pulsante destro del mouse su **Protocolli per** *&lt;nome istanza&gt;* quindi selezionare **Proprietà**.  
  
3. Scegliere la scheda **Certificato** e quindi selezionare **Importa**.  
  
4. Selezionare **Sfoglia** e quindi selezionare il file del certificato.  
  
5. Selezionare **Avanti** per convalidare il certificato. Se non ci sono errori, selezionare **Avanti** per importare il certificato nell'istanza locale.  
  
 
##  <a name="provision-failover-cluster-cert"></a> Per installare un certificato in una configurazione cluster di failover  
  
1. Nel riquadro della console di Gestione configurazione SQL Server espandere **Configurazione di rete SQL Server**.
  
2. Fare clic con il pulsante destro del mouse su **Protocolli per** *&lt;nome istanza&gt;* quindi scegliere **Proprietà**. 

3. Scegliere la scheda **Certificato** e quindi selezionare **Importa**.

4. Selezionare il tipo di certificato e indicare se l'importazione riguarda solo il nodo corrente oppure ogni singolo nodo del cluster.

5. Se l'installazione riguarda un nodo singolo, scegliere **Sfoglia** e selezionare il file del certificato. Andare al passaggio 8.

6. Se l'installazione del certificato riguarda ogni nodo, selezionare **Avanti** per visualizzare l'elenco dei nodi dei possibili proprietari. I possibili proprietari dell'istanza del cluster di failover corrente di SQL Server sono preselezionati.

7. Scegliere **Avanti** per selezionare il certificato da importare.

8. Immettere la password quando richiesto. Cercare eventuali avvisi o errori dopo la convalida.

9. Selezionare **Avanti** per importare i certificati selezionati.

> [!NOTE]
> Completare questi passaggi nel nodo attivo dell'istanza del cluster di failover di SQL Server. L'utente deve avere autorizzazioni amministratore per tutti i nodi del cluster.

##  <a name="provision-availability-group-cert"></a>Per installare un certificato in una configurazione del gruppo di disponibilità  
  
1. Nel riquadro della console di Gestione configurazione SQL Server espandere **Configurazione di rete SQL Server**.
  
2. Fare clic con il pulsante destro del mouse su **Protocolli per** *&lt;nome istanza&gt;* quindi selezionare **Proprietà**.  
  
3. Scegliere la scheda **Certificato** e quindi selezionare **Importa**.  
  
4. Scegliere il tipo di certificato e **Avanti** per selezionare dall'elenco dei gruppi di disponibilità noti.  

5. Selezionare **Avanti** per scegliere i certificati per ogni nodo di replica. Il nome di file dei certificati deve corrispondere al nome NetBIOS dei nodi.

6. Selezionare **Avanti** per importare il certificato in ogni nodo.


> [!NOTE]
> Completare questi passaggi dal nodo che contiene la replica primaria del gruppo di disponibilità. L'utente deve avere autorizzazioni amministratore per tutti i nodi del cluster.


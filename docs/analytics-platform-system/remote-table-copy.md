---
title: Copia di tabelle remote - Parallel Data Warehouse | Microsoft Docs
description: Utilizzo di copia della tabella remota in Analitica Platform System Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678561"
---
# <a name="remote-table-copy"></a>Copia della tabella remota
Viene descritto come usare la funzionalità di copia della tabella remota per copiare tabelle da database di SQL Server PDW per i database di SQL Server SMP remoti (non appliance). Usare la copia di tabelle remote a rende possibili scenari di hub e spoke per SQL Server PDW.  
  
## <a name="BasicsPDE"></a>Comprendere copia di tabelle Remote per SQL Server PDW  
Copia della tabella remota è una funzionalità di SQL Server PDW che rende possibili scenari di Hub e Spoke copiando i risultati di un'istruzione SQL SELECT in una tabella in un database SMP. Copia della tabella remota è stata avviata con il [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) istruzione.  
  
## <a name="BasicsPrerequisites"></a>Requisiti per l'utilizzo di copia della tabella remota  
È possibile usare le tabelle di copia per copiare tabella remota di SQL Server PDW in un database di SQL Server quando vengono soddisfatte queste condizioni:  
  
-   Il database di destinazione deve essere un'istanza di Microsoft® SQL Server® in esecuzione in un sistema Microsoft Windows® che può connettersi all'appliance di SQL Server PDW ma non risiede in un server all'interno dell'appliance. Remota di SQL Server possono essere connessi a SQL Server PDW con rete InfiniBand o attraverso la rete Ethernet.  
  
-   I dati da copiare devono essere selezionabili con un singolo SQL Server PDW validi [seleziona](../t-sql/queries/select-transact-sql.md) istruzione.  
  
-   Il server di destinazione deve essere un server non appliance. Impossibile copiare i dati direttamente da un'appliance a un'altra usando le istruzioni riportate in questo argomento.  
  
-   Il server di destinazione deve essere accessibile a tutti i nodi nella rete Infiniband dell'appliance.  
  
## <a name="ConfigureRemote"></a>Configurare una copia della tabella remota  
Per usare una copia della tabella remota, è necessario acquistare e configurare un server di Windows, configurare SQL Server nel server di Windows e configurare SQL Server PDW. Usare i collegamenti seguenti per eseguire questi tre passaggi di configurazione.  
  
1.  [Configurare un sistema Windows esterno per ricevere copie di una tabella remota usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurare un Server SQL SMP esterno per ricevere copie di una tabella remota](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurare SQL Server PDW per copie di una tabella remota](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Eseguire una copia della tabella remota  
Per eseguire una copia della tabella remota, usare il [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) istruzione SQL. Gli esempi sono inclusi con l'argomento CREATE REMOTE TABLE.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

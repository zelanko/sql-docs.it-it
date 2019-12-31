---
title: Copia di tabelle remote
description: Uso della copia della tabella remota nella piattaforma Analytics System Parallel data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400485"
---
# <a name="remote-table-copy"></a>Copia della tabella remota
Viene descritto come utilizzare la funzionalità di copia della tabella remota per copiare tabelle da database SQL Server PDW ai database SQL Server SMP (non Appliance) remoti. Usare la copia della tabella remota per abilitare gli scenari Hub e spoke per SQL Server PDW.  
  
## <a name="BasicsPDE"></a>Informazioni sulla copia della tabella remota per SQL Server PDW  
La copia della tabella remota è una funzionalità di SQL Server PDW che consente scenari Hub e spoke copiando i risultati di un'istruzione SQL SELECT in una tabella di un database SMP. La copia della tabella remota viene avviata con l'istruzione [Create Remote table As Select](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) .  
  
## <a name="BasicsPrerequisites"></a>Requisiti per l'utilizzo della copia della tabella remota  
È possibile utilizzare la copia della tabella remota per copiare tabelle da SQL Server PDW a un database SQL Server quando vengono soddisfatte queste condizioni:  
  
-   Il database di destinazione deve essere un'istanza di Microsoft® SQL Server® in esecuzione in un sistema® Microsoft Windows in grado di connettersi al dispositivo SQL Server PDW ma non si trova su un server all'interno dell'appliance. Il SQL Server remoto può essere connesso al SQL Server PDW tramite la rete InfiniBand o tramite la rete Ethernet.  
  
-   È necessario che i dati da copiare siano selezionabili utilizzando una singola istruzione SQL Server PDW [Select](../t-sql/queries/select-transact-sql.md) valida.  
  
-   Il server di destinazione deve essere un server non appliance. I dati non possono essere copiati direttamente da un appliance a un altro seguendo le istruzioni riportate in questo argomento.  
  
-   Il server di destinazione deve essere accessibile a tutti i nodi nella rete InfiniBand dell'appliance.  
  
## <a name="ConfigureRemote"></a>Configurare la copia della tabella remota  
Per usare la copia della tabella remota, è necessario acquistare e configurare un server Windows, configurare SQL Server in Windows Server e configurare SQL Server PDW. Usare i collegamenti seguenti per eseguire questi tre passaggi di configurazione.  
  
1.  [Configurare un sistema Windows esterno per ricevere copie della tabella remota tramite InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurare un SQL Server SMP esterno per ricevere copie di tabella remota](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurare SQL Server PDW per le copie della tabella remota](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Eseguire una copia della tabella remota  
Per eseguire una copia della tabella remota, usare l'istruzione [Create Remote table As Select](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL. Gli esempi sono inclusi nell'argomento creare una tabella remota.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

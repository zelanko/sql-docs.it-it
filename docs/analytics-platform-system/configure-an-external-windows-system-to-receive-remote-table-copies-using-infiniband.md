---
title: Configurare Windows per la ricezione di copie della tabella remota
description: Viene descritto come acquistare e configurare un sistema Windows non Appliance connesso tramite la rete InfiniBand da usare con la funzionalità di copia della tabella remota in Parallel data warehouse. Il sistema di Windows ospiterà il database di SQL Server che riceve la copia della tabella remota da un database SQL Server PDW. Viene acquistata separatamente dal dispositivo ed è connessa alla rete InfiniBand dell'appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401311"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>Configurare un sistema Windows esterno per ricevere copie della tabella remota tramite InfiniBand-Parallel data warehouse
Viene descritto come acquistare e configurare un sistema Windows non Appliance connesso tramite la rete InfiniBand da usare con la funzionalità di copia della tabella remota in SQL Server PDW. Il sistema di Windows ospiterà il database di SQL Server che riceve la copia della tabella remota da un database SQL Server PDW. Viene acquistata separatamente dal dispositivo ed è connessa alla rete InfiniBand dell'appliance.  
  
> [!NOTE]  
> La connessione tramite la rete InfiniBand non è necessaria per l'utilizzo della copia della tabella remota. La connessione tramite la rete Ethernet può essere eseguita se la larghezza di banda Ethernet soddisfa le esigenze.  
  
Questo argomento descrive uno dei passaggi di configurazione per la configurazione della copia di una tabella remota. Per un elenco di tutti i passaggi di configurazione, vedere copia di una [tabella remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Prima di configurare il sistema Windows esterno, è necessario:  
  
1.  Acquistare o fornire un sistema Windows che riceverà le copie remote.  
  
2.  Rack del sistema Windows nel rack di controllo (se lo spazio è sufficiente) o sufficientemente vicino al dispositivo, in modo che sia possibile connetterlo alla rete InfiniBand dell'appliance.  
  
3.  Acquistare cavi InfiniBand e una scheda di rete InfiniBand dal fornitore hardware del dispositivo. Si consiglia di acquistare una scheda di rete con due porte per la tolleranza di errore durante la ricezione dei dati esportati. È consigliabile usare una scheda di rete a due porte, ma non è un requisito.  
  
## <a name="configure-an-external-windows-system-to-receive-remote-table-copies"></a><a name="HowToWindows"></a>Configurare un sistema Windows esterno per la ricezione di copie di tabella remota  
Per configurare il sistema Windows esterno, attenersi alla procedura seguente:  
  
1.  Installare la scheda di rete InfiniBand nel sistema Windows.  
  
2.  Connettere la scheda di rete InfiniBand al comportatore InfiniBand principale nel rack di controllo usando cavi InfiniBand.  
  
3.  Installare e configurare il driver Windows appropriato per la scheda di rete InfiniBand.  
  
    I driver InfiniBand per Windows sono sviluppati da OpenFabrics Alliance, un consorzio di settore di fornitori InfiniBand.  Il driver corretto potrebbe essere stato distribuito con la scheda InfiniBand. In caso contrario, il driver può essere scaricato da www.openfabrics.org.  
  
4.  Configurare l'indirizzo IP per ogni porta sulla scheda. Per usare gli indirizzi IP statici di un intervallo di indirizzi riservati a questo scopo, sono necessari sistemi SMP. Configurare la prima porta in base ai parametri seguenti:  
  
    -   Indirizzo di rete IP: 172.16.132. x  
  
    -   Subnet mask IP: 255.255.128.0  
  
    -   Intervallo host IP: 1-254  
  
    Per le schede di rete InfiniBand con due porte, configurare la seconda porta in base ai parametri seguenti:  
  
    -   Indirizzo di rete IP: 172.16.132. x  
  
    -   Subnet mask IP: 255.255.128.0  
  
    -   Intervallo host IP: 1-254  
  
5.  Se viene usato un adattatore a due porte o più sistemi Windows esterni sono connessi a un'appliance, assegnare a ogni sistema un numero host diverso all'interno di ogni subnet IP.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

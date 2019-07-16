---
title: Configurare Windows per ricevere copie di una tabella remota - Parallel Data Warehouse | Microsoft Docs
description: Descrive come acquistare e configurare un sistema di Windows non appliance connesso tramite la rete InfiniBand per l'uso con la funzionalità di copia tabella remota in Parallel Data Warehouse. Il sistema di Windows ospiterà il database di SQL Server che riceve la copia della tabella remota da un database di SQL Server PDW. È acquistato separatamente dall'appliance e connesso alla rete InfiniBand appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 428dc5b4edda91f60a09a52c0326f881f257b32c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961304"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>Configurare un sistema Windows esterno per ricevere copie di una tabella remota usando InfiniBand - Parallel Data Warehouse
Descrive come acquistare e configurare un sistema di Windows non appliance connesso tramite la rete InfiniBand per l'uso con la funzionalità di copia tabella remota in SQL Server PDW. Il sistema di Windows ospiterà il database di SQL Server che riceve la copia della tabella remota da un database di SQL Server PDW. È acquistato separatamente dall'appliance e connesso alla rete InfiniBand appliance.  
  
> [!NOTE]  
> La connessione tramite la rete InfiniBand non è necessaria per l'utilizzo di copia della tabella remota. La connessione attraverso la rete Ethernet può essere eseguita se la larghezza di banda Ethernet soddisfa le proprie esigenze.  
  
In questo argomento descrive uno dei passaggi di configurazione per la configurazione di copia della tabella remota. Per un elenco di tutti i passaggi di configurazione, vedere [copia della tabella remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Prima di configurare il sistema Windows esterno, è necessario:  
  
1.  Acquisto o fornire un sistema di Windows che riceverà la copia remota.  
  
2.  Installare in rack il sistema di Windows nel rack controllo (se è disponibile spazio sufficiente) o abbastanza ravvicinati per l'appliance in modo che è possibile connetterla alla rete InfiniBand appliance.  
  
3.  Acquistare una scheda di rete InfiniBand e dei cavi InfiniBand dal fornitore dell'hardware dell'appliance. È consigliabile acquistare una scheda di rete con due porte per la tolleranza di errore quando si ricevono i dati esportati. Una scheda di rete due porte è consigliabile, ma non è un requisito.  
  
## <a name="HowToWindows"></a>Configurare un sistema Windows esterno per ricevere copie di una tabella remota  
Per configurare il sistema Windows esterno, usare la procedura seguente:  
  
1.  Installare la scheda di rete InfiniBand nel sistema di Windows.  
  
2.  Connettere la scheda di rete InfiniBand al commutatore InfiniBand principale nel rack controllo tramite cavi InfiniBand.  
  
3.  Installare e configurare il driver di Windows appropriato per la scheda di rete InfiniBand.  
  
    I driver InfiniBand per Windows sono sviluppati dal team di OpenFabrics Alliance, un consorzio di settore di fornitori InfiniBand.  Può avere il driver corretto sia stato distribuito con l'adattatore InfiniBand. In caso contrario, il driver può essere scaricato da www.openfabrics.org.  
  
4.  Configurare l'indirizzo IP per ogni porta nella scheda. I sistemi SMP sono necessarie per usare gli indirizzi IP statici da un intervallo di indirizzi riservati per questo scopo. Configurare la prima porta in base ai parametri seguenti:  
  
    -   Indirizzo IP: 172.16.132.x  
  
    -   Subnet mask IP: 255.255.128.0  
  
    -   Intervallo IP host: 1-254  
  
    Per le schede di rete InfiniBand con due porte, configurare la seconda porta in base ai parametri seguenti:  
  
    -   Indirizzo IP: 172.16.132.x  
  
    -   Subnet mask IP: 255.255.128.0  
  
    -   Intervallo IP host: 1-254  
  
5.  Se viene usato un adattatore due porta o più sistemi Windows esterni connessi a un'appliance, assegnare un numero di host diversi all'interno di ogni subnet IP ogni sistema.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  

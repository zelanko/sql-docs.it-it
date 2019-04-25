---
title: Configurare Parallel Data Warehouse per copie di una tabella remota | Microsoft Docs
description: Viene descritto come configurare Parallel Data Warehouse, per usare la funzionalità di copia della tabella remota per copiare le tabelle nei database di SQL Server SMP nei server non appliance.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fdac0b6ed211e223c3fad7ba15ac79a282c61303
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509523"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Configurare Parallel Data Warehouse per copie di una tabella remota
Viene descritto come configurare SQL Server PDW per usare la funzionalità di copia della tabella remota per copiare le tabelle nei database di SQL Server SMP nei server non appliance.  
  
In questo argomento descrive uno dei passaggi di configurazione per la configurazione di copia della tabella remota. Per un elenco di tutti i passaggi di configurazione, vedere [copia di tabelle Remote](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Per configurare SQL Server PDW per l'utilizzo di copia della tabella remota, è necessario:  
  
-   Dispone di un account di amministratore di sistema di piattaforma Analitica con la possibilità di accedere direttamente al  <strong>*appliance_domain*-AD01</strong> e  <strong>*appliance_domain*-AD02</strong> nodi.  
  
-   Conoscere il nome host o nome IP del server di destinazione.  
  
## <a name="HowToPDW"></a>Configurare SQL Server PDW per la copia della tabella remota: Aggiornare i nomi Host nel DNS  
Il **CREATE REMOTE TABLE** istruzione utilizzata per le copie di tabelle remote, specifica il server di destinazione usando l'indirizzo IP o il nome IP del sistema Windows SMP. Per usare il nome dell'IP, è necessario aggiungere le voci per la risoluzione dei nomi corretta per il server DNS.  
  
I passaggi seguenti illustrano la procedura per aggiornare il server DNS.  
  
1.  Accedere al nodo AD attivo (in genere  <strong>*appliance_domain*-AD01</strong>).  
  
2.  Aprire Gestore DNS. È disponibile nella **strumenti di amministrazione** nel **avviare** menu.  
  
3.  Utilizzare il gestore DNS per aggiungere il nome dell'IP.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Usare un server d'inoltro DNS per risolvere i nomi DNS Non Appliance](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  

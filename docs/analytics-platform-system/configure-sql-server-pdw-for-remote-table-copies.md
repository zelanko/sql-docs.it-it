---
title: Copie della tabella remota
description: Viene descritto come configurare Parallel data warehouse per utilizzare la funzionalità di copia della tabella remota per copiare tabelle in database SMP SQL Server su server non Appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401259"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Configurare data warehouse parallele per le copie della tabella remota
Viene descritto come configurare SQL Server PDW per utilizzare la funzionalità copia tabella remota per copiare tabelle in database SMP SQL Server su server non Appliance.  
  
Questo argomento descrive uno dei passaggi di configurazione per la configurazione della copia di una tabella remota. Per un elenco di tutti i passaggi di configurazione, vedere la pagina relativa alla [copia remota della tabella](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Prima di iniziare  
Per configurare SQL Server PDW per l'utilizzo della copia della tabella remota, è necessario:  
  
-   Disporre di un account amministratore di sistema della piattaforma di analisi con la possibilità di accedere direttamente ai nodi <strong> *appliance_domain*-ad01</strong> e <strong> *appliance_domain*-ad02</strong> .  
  
-   Conosce il nome host o il nome IP del server di destinazione.  
  
## <a name="HowToPDW"></a>Configurare SQL Server PDW per la copia della tabella remota: aggiornare i nomi host in DNS  
L'istruzione **Create Remote Table** , utilizzata per le copie della tabella remota, specifica il server di destinazione utilizzando l'indirizzo IP o il nome IP del sistema Windows SMP. Per usare il nome IP, è necessario aggiungere voci per la corretta risoluzione dei nomi al server DNS.  
  
La procedura seguente illustra come aggiornare il server DNS.  
  
1.  Accedere al nodo Active Directory (in genere <strong> *appliance_domain*-ad01</strong>).  
  
2.  Aprire il gestore DNS. Si trova in **strumenti di amministrazione** nel menu **Start** .  
  
3.  Utilizzare il gestore DNS per aggiungere il nome IP.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Usare un server d'invio DNS per risolvere i nomi DNS non Appliance](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  

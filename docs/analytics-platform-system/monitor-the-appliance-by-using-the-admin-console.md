---
title: Monitorare con la console di amministrazione
description: Per il sistema di piattaforma di analisi, la console di amministrazione è un'applicazione Web che copre le informazioni sullo stato dell'appliance, sull'integrità e sulle prestazioni. Gli utenti si connettono alla console di amministrazione tramite un browser Internet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 977e38016fbb58356d22ccfc5f783539e5f852d5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400938"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Monitorare l'appliance con la console di amministrazione-sistema della piattaforma di analisi
La console di amministrazione è un'applicazione Web SQL Server PDW che presenta le informazioni sullo stato, l'integrità e le prestazioni dell'appliance. Gli utenti si connettono alla console di amministrazione tramite Internet Explorer.  
  
## <a name="About"></a>Informazioni sulla console di amministrazione  
![Home console dello strumento](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Appliance**  
Home  
Fornisce un riepilogo rapido dello stato dell'appliance.  
  
Integrità  
Visualizza la topologia del dispositivo con indicatori che mostrano l'integrità di ogni componente monitorato all'interno di ciascun nodo. Consente di visualizzare lo stato corrente dei singoli nodi e delle proprietà dei componenti del nodo.  
  
Visualizza gli avvisi hardware e software.  
  
Monitoraggio delle prestazioni  
Visualizza i grafici di performance monitor.  
  
**Parallel Data Warehouse**  
Home  
Fornisce un riepilogo rapido dello stato PDW.  
  
Sessioni  
Visualizza le sessioni utente di PDW attive. Questo può essere utile per il monitoraggio della contesa di risorse.  
  
Query  
Visualizza un elenco di query in esecuzione e query completate di recente. Vengono visualizzati gli eventuali errori correlati. Consente inoltre di visualizzare i dettagli del piano di esecuzione della query e le informazioni sull'esecuzione del nodo.  
  
Operazioni di caricamento  
Consente di visualizzare i piani di carico, lo stato corrente dei carichi PDW e gli eventuali errori correlati.  
  
Backup/ripristini  
Visualizza un log delle operazioni di backup e ripristino di PDW.  
  
Integrità  
Visualizza la topologia PDW con indicatori che mostrano l'integrità di ogni componente monitorato all'interno di ciascun nodo. Consente di visualizzare lo stato corrente dei singoli nodi e delle proprietà dei componenti del nodo.  
  
Visualizza gli avvisi hardware e software.  
  
Risorse  
Visualizza un elenco di blocchi di risorse PDW e il relativo stato corrente.  
  
Archiviazione  
Riepiloga l'utilizzo dello spazio di archiviazione PDW.  
  
Monitoraggio delle prestazioni  
Visualizza i grafici di performance monitor PDW.  
 
> [!NOTE]  
> La console di amministrazione ha una risoluzione dello schermo 1024x768. La console di amministrazione Visualizza i risultati migliori con una risoluzione dello schermo di 1280 X 1024 o superiore.  
  
## <a name="Connect"></a>Connettersi alla console di amministrazione  
Per connettersi alla console di amministrazione, è necessario:  
  
-   Almeno Internet Explorer versione 10.  
  
-   Autorizzazioni per accedere alla console di amministrazione. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Indirizzo IP del cluster del nodo di controllo.  Ottenere questo dal SQL Server PDW amministratore.  
  
Per connettersi alla console di amministrazione, usare Internet Explorer e HTTPS per passare all'indirizzo IP del cluster del nodo di controllo. Ad esempio, se l'indirizzo IP del cluster del nodo di controllo `10.192.63.102`è, `https://10.192.63.102` immettere nella barra degli indirizzi del browser. La prima schermata richiederà l' **account di accesso** e la **password**. Specificare un account di accesso e una password per l'autenticazione SQL Server oppure un account di accesso con autenticazione di Windows e una password di Windows. Se si utilizza un account di accesso con autenticazione di Windows, la console di amministrazione utilizzerà la rappresentazione.  
  
## <a name="RelatedTasks"></a>Attività della console di amministrazione  
La console di amministrazione consente di monitorare gli elementi seguenti:  
  
|||  
|-|-|  
|**Information Type**|**Come accedere alla console di amministrazione**|  
|Stato generale dell'appliance|Fare clic su **stato dell'appliance** nel menu superiore oppure **Home**.|  
|Avvisi|Fare clic su **Avvisi**. Per ulteriori informazioni, vedere informazioni sugli [avvisi della console di amministrazione &#40;&#41;piattaforma di strumenti analitici ](understanding-admin-console-alerts.md).|  
|Componenti del dispositivo e relativo stato|Fare clic su **stato dell'appliance** nel menu superiore oppure **Home**.|  
|Monitorare le richieste (incluse query, caricamenti, backup e ripristini)|Fare clic su **sessioni** per visualizzare le sessioni attualmente attive o recenti.<br /><br />Fare clic su **query** per visualizzare le query attualmente attive o recenti. Le informazioni visualizzate per le query includono carichi, backup e ripristini.<br /><br />Fare clic su **blocchi** per visualizzare i blocchi attivi.|  
|Monitorare informazioni aggiuntive per carichi, backup e ripristini.|Fare clic su **caricamenti** o **backup/ripristini**.|  
|Informazioni sulle prestazioni|Fare clic su **Performance Monitor**.|  
  
## <a name="see-also"></a>Vedere anche  
[Monitoraggio Appliance &#40;sistema piattaforma di analisi&#41;](appliance-monitoring.md)  
  

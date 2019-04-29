---
title: Monitoraggio con Console di Amministrazione - sistema di piattaforma Analitica | Microsoft Docs
description: Per il sistema di piattaforma Analitica, la Console di amministrazione è un'applicazione web che espone le informazioni di stato, l'integrità e prestazioni dell'appliance. Gli utenti di connettersi alla Console di amministrazione tramite un browser internet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d094f809052222238806e679e38c6578422fd9aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027542"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Monitorare l'appliance con la Console di Amministrazione - sistema di piattaforma Analitica
La Console di amministrazione è un'applicazione web di SQL Server PDW che copre le informazioni di stato, l'integrità e prestazioni dell'appliance. Gli utenti di connettersi alla Console di amministrazione tramite Internet Explorer.  
  
## <a name="About"></a>Sulla Console di amministrazione  
![Appliance Console Home](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Appliance**  
Home  
Offre un breve riepilogo dello stato del dispositivo.  
  
Integrità  
Consente di visualizzare la topologia dello strumento con gli indicatori che mostra l'integrità di ogni componente monitorato all'interno di ogni nodo. Consente di visualizzare lo stato corrente dei singoli nodi e le proprietà dei componenti di nodo.  
  
Visualizza gli avvisi di hardware e software.  
  
Performance Monitor  
Consente di visualizzare i grafici di monitoraggio delle prestazioni.  
  
**Parallel Data Warehouse**  
Home  
Fornisce un riepilogo rapido dello stato di PDW.  
  
Sessioni  
Visualizza sessioni attive di utente PDW. Questo può consentire per il monitoraggio di contesa delle risorse.  
  
Query  
Visualizza un elenco di esecuzione di query e query completate di recente. Visualizza gli errori correlati, se presente. Offre inoltre la possibilità di visualizzare i dettagli dei query nodo e piano di esecuzione informazioni sull'esecuzione.  
  
Caricamenti  
Consente di visualizzare caricare i piani, lo stato corrente di PDW carichi e gli errori correlati, se presente.  
  
Backup/ripristini  
Consente di visualizzare un log di PDW backup e le operazioni di ripristino.  
  
Integrità  
Consente di visualizzare la topologia PDW con gli indicatori che mostra l'integrità di ogni componente monitorato all'interno di ogni nodo. Consente di visualizzare lo stato corrente dei singoli nodi e le proprietà dei componenti di nodo.  
  
Visualizza gli avvisi di hardware e software.  
  
Risorse  
Visualizza un elenco di blocchi risorse PDW e il relativo stato corrente.  
  
Archiviazione  
Riepiloga l'uso di archiviazione PDW.  
  
Performance Monitor  
Consente di visualizzare i grafici di monitoraggio delle prestazioni di PDW.  
 
> [!NOTE]  
> La console di amministrazione ha una risoluzione dello schermo 1024 x 768. La console di amministrazione consente di visualizzare migliore con una risoluzione dello schermo di 1280 X 1024 o superiore.  
  
## <a name="Connect"></a>Connettersi alla Console di amministrazione  
Per connettersi alla Console di amministrazione, è necessario:  
  
-   Almeno Internet Explorer versione 10.  
  
-   Autorizzazioni per accedere alla Console di amministrazione. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   L'indirizzo IP del cluster di nodo di controllo.  Ottenere queste informazioni dall'amministratore di SQL Server PDW.  
  
Per connettersi alla Console di amministrazione, usare Internet Explorer e https per passare all'indirizzo IP del cluster di nodo di controllo. Ad esempio, se l'indirizzo IP del cluster di nodo di controllo è `10.192.63.102`, immettere `https://10.192.63.102` nella barra degli indirizzi del browser. La prima schermata richiederà il **account di accesso** e **PASSWORD**. Specificare un account di accesso di autenticazione di SQL Server e password, o un accesso con autenticazione di Windows e password di Windows. Se si usa un account di accesso di autenticazione di Windows, la Console di amministrazione userà la rappresentazione.  
  
## <a name="RelatedTasks"></a>Attività della Console di amministrazione  
La Console di amministrazione consente di controllare quanto segue:  
  
|||  
|-|-|  
|**Tipo di informazioni**|**Come l'accesso nella Console di amministrazione**|  
|Stato complessivo dell'appliance|Fare clic su **lo stato di Appliance** nel menu in alto, o **Home**.|  
|Avvisi|Fare clic su **avvisi**. Per altre informazioni, vedere [Understanding avvisi della Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](understanding-admin-console-alerts.md).|  
|I componenti di Appliance e il relativo stato|Fare clic su **lo stato di Appliance** nel menu in alto, o **Home**.|  
|Richieste di monitoraggio (incluse le query, caricamenti, i backup e ripristini)|Fare clic su **sessioni** per visualizzare le sessioni attualmente attive o recenti.<br /><br />Fare clic su **query** per visualizzare le query attualmente attive o recenti. Le informazioni visualizzate per query includono carichi, backup e ripristini.<br /><br />Fare clic su **blocchi** per visualizzare i blocchi attivi.|  
|Monitorare le informazioni aggiuntive per caricamenti, i backup e ripristino.|Fare clic su **caricamenti** oppure **backup/ripristini**.|  
|Informazioni sulle prestazioni|Fare clic su **Performance Monitor**.|  
  
## <a name="see-also"></a>Vedere anche  
[Monitoraggio dell'Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-monitoring.md)  
  

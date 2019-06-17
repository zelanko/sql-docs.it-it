---
title: Imposta valori soglia avvisi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbmmonitor.setwarningthreshold.f1
ms.assetid: 17f93147-e7d9-4092-b4c2-c11b38051171
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9f1c7c05a02c67fda968ea26bd114d16b0b73925
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65805165"
---
# <a name="set-warning-thresholds"></a>Imposta valori soglia avvisi
  Usare questa finestra di dialogo per abilitare e configurare una o più soglie degli avvisi per il database selezionato nell'albero di navigazione della finestra di dialogo **Monitoraggio mirroring del database** .  
  
 La finestra di dialogo tenta di connettersi a entrambe le istanze del server. Queste connessioni vengono stabilite in modo asincrono. Nella finestra di dialogo viene visualizzato lo stato di connessione di ogni partner. Se il partner non è connesso, fare clic su **Connetti**.  
  
 **Per utilizzare SQL Server Management Studio per il monitoraggio del mirroring del database**  
  
-   [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Opzioni  
 *Istanza del server e relativo stato di connessione*  
 Nome di un'istanza del server partner nel formato _SYSTEM_ **\\** _INSTANCE_NAME_. Per un'istanza del server predefinita, viene visualizzato solo il nome di sistema.  
  
 Il campo indica inoltre se il monitoraggio è attualmente connesso all'istanza del server. I possibili stati di connessione sono i seguenti:  
  
-   **Non connesso a**  *nome_istanza_server*  
  
-   **Tentativo di connessione a**  *nome_istanza_server*  
  
-   **Connesso a**  *nome_istanza_server*  
  
    > [!NOTE]  
    >  Se non si è membri del ruolo predefinito del server **sysadmin** , lo stato è impostato su **Connesso a** *nome_istanza_server* **(autorizzazioni limitate)** .  
  
 Il nome di ogni istanza del server partner è visualizzato in un campo *Istanza del server e relativo stato di connessione* separato. Il campo in alto indica il server principale all'avvio dell'esecuzione del monitoraggio.  
  
 **Connetti**/**Annulla**  
 Un pulsante **Connetti**/**Annulla** è associato a ogni *istanza del server e al relativo stato di connessione* . Lo stato del pulsante dipende dallo stato di connessione:  
  
-   Se non è presente alcuna connessione all'istanza del server, il testo del pulsante è **Connetti**. Fare clic sul pulsante per connettersi all'istanza del server.  
  
-   Quando è in corso un tentativo di connessione, il testo del pulsante è **Annulla**. Fare clic sul pulsante per annullare il tentativo di connessione.  
  
-   Se il server è connesso, il testo del pulsante è **Connesso**e il pulsante è disattivato.  
  
 **Thresholds**  
 Nella griglia **Valori soglia** sono visualizzate le impostazioni degli avvisi per le due istanze del server.  
  
> [!NOTE]  
>  Se un'istanza del server non è connessa, le relative colonne sono visualizzate con celle vuote e uno sfondo grigio. Quando viene stabilita la connessione, nella griglia viene visualizzato automaticamente il contenuto dell'istanza.  
  
 La griglia include le colonne seguenti:  
  
 **Avvisi**  
 Elenca gli avvisi supportati:  
  
|Avviso|Descrizione|  
|-------------|-----------------|  
|**Avvisa se il log non inviato supera la soglia**|La soglia indica il numero di kilobyte (KB), del log non inviato nella coda di invio sull'istanza del server principale.|  
|**Avvisa se il log non ripristinato supera la soglia**|La soglia indica il numero di KB della coda di rollforward sull'istanza del server mirror.|  
|**Avvisa se il tempo di memorizzazione della transazione non inviata meno recente è superiore alla soglia**|La soglia indica il numero di minuti delle transazioni non ancora inviate dalla coda di invio all'istanza del server mirror. Questo valore consente di misurare la potenziale perdita di dati in termini di tempo.|  
|**Avvisa se l'overhead di commit del mirror supera la soglia**|La soglia indica il numero di millisecondi di ritardo per transazione (rilevante solo in modalità a protezione elevata). Questo ritardo rappresenta la quantità di overhead generato mentre l'istanza del server principale è in attesa che l'istanza del server mirror scriva il record di log della transazione nella coda di rollforward.|  
  
 **Abilitato su '** *\<istanza server>* **'**  
 Una casella di controllo deselezionata indica che l'avviso è attualmente disabilitato sull'istanza del server. Per abilitare un avviso, selezionare la relativa casella di controllo.  
  
 **Valore di soglia su '** *\<istanza server>* **'**  
 Quando un avviso è abilitato, impostare la soglia nella parte sinistra della colonna. Un evento si verifica se la soglia specificata viene raggiunta all'aggiornamento della tabella dello stato. Se si disabilita una soglia dopo aver configurato un valore, il valore configurato rimane nel campo e verrà utilizzato in caso di riabilitazione dell'avviso.  
  
 Quando un avviso non è abilitato, il campo non è attivo.  
  
 **OK**  
 Se si fa clic su **OK** , questa finestra di dialogo viene chiusa e vengono visualizzati i valori attualmente specificati per le soglie degli avvisi nella griglia **Valori di soglia** della pagina a schede **Avvisi**.  
  
## <a name="remarks"></a>Note  
 Una soglia è applicabile solo a un partner per volta, ma è consigliabile impostare una soglia per un determinato evento su entrambi i partner per assicurare che l'avviso venga mantenuto in caso di failover del database. La soglia appropriata per ogni partner dipende dalle capacità in termini di prestazioni del sistema di tale partner.  
  
 Un evento viene scritto nel log eventi per una prestazione solo se il relativo valore è uguale o superiore alla relativa soglia quando la tabella dello stato è in fase di aggiornamento. Se un valore di picco raggiunge la soglia solo temporaneamente tra gli aggiornamenti di stato, tale picco non viene segnalato.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Monitoraggio del mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Avviare la Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
  

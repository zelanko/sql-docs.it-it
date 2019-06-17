---
title: Usare dettagli Esplora oggetti per monitorare i gruppi di disponibilità (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.OEdetails.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: 84affc47-40e0-43d9-855e-468967068c35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5545b36aba250a04744b66abad5434f8573c053e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788324"
---
# <a name="use-the-object-explorer-details-to-monitor-availability-groups-sql-server-management-studio"></a>Utilizzare Dettagli Esplora oggetti per monitorare Gruppi di disponibilità (SQL Server Management Studio)
  In questo argomento viene illustrato come utilizzare il riquadro **Dettagli Esplora oggetti** di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] per monitorare e gestire i database di disponibilità AlwaysOn, le repliche di disponibilità e i gruppi di disponibilità esistenti.  
  
> [!NOTE]  
>  Per informazioni sull'uso del riquadro Dettagli Esplora oggetti, vedere [Riquadro Dettagli di Esplora oggetti](../../../ssms/object/object-explorer-details-pane.md).  
  
-   **Prima di iniziare:**  [Prerequisiti](#Prerequisites)  
  
-   **Per monitorare un gruppo di disponibilità utilizzando:**  [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Dettagli Esplora oggetti:**  
  
     [Dettagli del gruppo di disponibilità](#AvGroupsDetails)  
  
     [Dettagli replica di disponibilità](#AvReplicaDetails)  
  
     [Dettagli database di disponibilità](#AvDbDetails)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario essere connessi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (istanza del server) che ospita la replica primaria o una replica secondaria.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per monitorare i gruppi di disponibilità, le repliche di disponibilità e i database di disponibilità**  
  
1.  Scegliere **Dettagli Esplora oggetti**dal menu Visualizza o premere **F7** .  
  
2.  In Esplora oggetti connettersi all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui si desidera monitorare un gruppo di disponibilità, quindi fare clic sul nome del server per espandere il relativo albero.  
  
3.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
4.  Nel riquadro **Dettagli Esplora oggetti** viene visualizzato ogni gruppo di disponibilità per il quale l'istanza del server connesso ospita una replica. Per ogni gruppo di disponibilità, la colonna **Istanza primaria del server** contiene il nome dell'istanza del server che attualmente ospita la replica primaria.  Per visualizzare ulteriori informazioni su un determinato gruppo di disponibilità, selezionarlo in Esplora oggetti.  
  
5.  Nel riquadro **Dettagli Esplora oggetti** vengono visualizzati i nodi **Repliche di disponibilità** e **Database di disponibilità** per questo gruppo di disponibilità:  
  
    -   Quando si espande il nodo **Gruppo di disponibilità** in Esplora oggetti e si seleziona il nodo **Repliche di disponibilità** , nel riquadro **Dettagli Esplora oggetti** vengono visualizzate informazioni su ogni replica di disponibilità nel gruppo. Per ulteriori informazioni, vedere [Dettagli replica di disponibilità](#AvReplicaDetails), più avanti in questo argomento.  
  
         Per eseguire operazioni su più repliche di disponibilità, selezionarle e fare clic con il pulsante destro del mouse su di esse per aprire un menu di scelta rapida in cui sono elencati i comandi disponibili.  
  
    -   Quando si espande il nodo **Gruppo di disponibilità** in Esplora oggetti e si seleziona il nodo **Database di disponibilità** , nel riquadro **Dettagli Esplora oggetti** vengono visualizzate informazioni su ogni database di disponibilità nel gruppo. Per ulteriori informazioni, vedere [Dettagli database di disponibilità](#AvDbDetails), più avanti in questo argomento.  
  
         Per eseguire operazioni su più database di disponibilità, selezionarli e fare clic con il pulsante destro del mouse su di essi per aprire un menu di scelta rapida in cui sono elencati i comandi disponibili.  
  
##  <a name="AvGroupsDetails"></a> Dettagli gruppo di disponibilità  
 Nella schermata dei dettagli **Gruppi di disponibilità** vengono visualizzate le colonne seguenti:  
  
 **Name**  
 Elenca le cartelle **Repliche di disponibilità**, **Database di disponibilità**e **Listener gruppo disponibilità** del gruppo di disponibilità selezionato.  
  
##  <a name="AvReplicaDetails"></a> Dettagli replica di disponibilità  
 Nella schermata dei dettagli **Replica di disponibilità** vengono visualizzate le colonne seguenti:  
  
 **Istanza del server**  
 Contiene il nome dell'istanza del server che ospita la replica di disponibilità, insieme a un'icona che indica lo stato di connessione corrente dell'istanza del server all'istanza del server locale.  
  
 **Ruolo**  
 Indica il ruolo corrente della replica di disponibilità, ovvero **Primario** o **Secondario**. Per informazioni sui ruoli di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
 **Modalità di connessione nel ruolo secondario**  
 Indica se i database di una determinata replica di disponibilità che detiene il ruolo secondario, ovvero che agisce come replica secondaria, possono accettare connessioni dai client.  
  
 I valori possibili sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Non consentire connessioni**|Le connessioni dirette ai database di disponibilità non sono consentite quando questa replica di disponibilità agisce come una replica secondaria. I database secondari non sono disponibili per l'accesso in lettura.|  
|**Consenti solo connessioni con finalità di lettura**|Sono consentite solo connessioni dirette in sola lettura quando questa replica agisce come una replica secondaria. Tutti i database nella replica sono disponibili per l'accesso in lettura.|  
|**Consenti tutte le connessioni**|Tutte le connessioni sono consentite a questi database per l'accesso in sola lettura quando questa replica agisce come una replica secondaria.|  
  
 **Stato connessione**  
 Indica se una replica secondaria è attualmente connessa alla replica primaria. I valori possibili sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Disconnesso**|Per una replica di disponibilità remota, indica che è disconnessa dalla replica di disponibilità locale. La risposta della replica locale allo stato Disconnesso dipende dal relativo ruolo:<br /><br /> Sulla replica primaria, se una replica secondaria è disconnessa, i database secondari sono contrassegnati come **Non sincronizzato** sulla replica primaria e la replica primaria attende che la replica secondaria venga riconnessa.<br /><br /> Sulla replica secondaria, dopo avere rilevato che è disconnessa, tenta di riconnettersi alla replica primaria.|  
|**Connesso**|Una replica di disponibilità remota attualmente connessa alla replica locale.|  
|**NULL**|Se la replica locale è una replica secondaria, questo valore è NULL per altre repliche secondarie.|  
  
 **Stato di sincronizzazione**  
 Indica se una replica secondaria è attualmente sincronizzata con la replica primaria. I valori possibili sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Non sincronizzato**|Il database non è sincronizzato o non è stato ancora aggiunto al gruppo di disponibilità.|  
|**Sincronizzato**|Il database è sincronizzato con il database primario sulla replica primaria corrente o sull'ultima replica primaria.<br /><br /> Nota: In modalità a prestazioni, il database si trova mai nello stato Synchronized.|  
|**NULL**|Stato sconosciuto. Si ottiene questo valore quando l'istanza del server locale non è in grado di comunicare con il cluster di failover WSFC, ovvero il nodo locale non fa parte del quorum WSFC.|  
  
> [!NOTE]  
>  Per informazioni sui contatori delle prestazioni per le repliche di disponibilità, vedere [SQL Server, replica di disponibilità](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbDetails"></a> Dettagli database di disponibilità  
 Nella schermata dei dettagli **Database di disponibilità** vengono visualizzare le seguenti proprietà dei database di disponibilità di un determinato gruppo di disponibilità:  
  
 **Name**  
 Nome del database di disponibilità.  
  
 **Stato di sincronizzazione**  
 Indica se il database di disponibilità è attualmente sincronizzato con la replica primaria.  
  
 Gli stati di sincronizzazione possibili sono:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Sincronizzazione in corso|Il database secondario ha ricevuto i record del log delle transazioni per il database primario che non sono ancora scritti su disco (finali).<br /><br /> Nota: Nella modalità con commit asincrono, lo stato di sincronizzazione è sempre **Synchronizing**.|  
  
 **Sospeso**  
 Indica se il database di disponibilità è attualmente online. I valori possibili sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Sospeso**|Questo stato indica che il database è stato sospeso in locale e che deve essere ripreso manualmente.<br /><br /> Sulla replica primaria, il valore non è attendibile per un database secondario. Per determinare in modo affidabile se un database secondario è sospeso, eseguire una query sulla replica secondaria che ospita il database.|  
|**Non unito in join**|Indica che il database secondario non è stato aggiunto al gruppo di disponibilità o stato rimosso dal gruppo.|  
|**Online**|Indica che il database non è sospeso sulla replica di disponibilità locale e che il database è connesso.|  
|**Non connesso**|Indica che la replica secondaria non è attualmente in grado di connettersi alla replica primaria.|  
  
> [!NOTE]  
>  Per informazioni sui contatori delle prestazioni per i database di disponibilità, vedere [SQL Server, replica di database](../../../relational-databases/performance-monitor/sql-server-database-replica.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Usare il Dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Visualizzare le proprietà dei gruppi di disponibilità &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)   
 [Visualizzazione delle proprietà della replica di disponibilità &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
  

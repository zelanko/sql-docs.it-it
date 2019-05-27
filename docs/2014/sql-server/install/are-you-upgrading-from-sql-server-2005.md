---
title: Aggiornamento da SQL Server 2005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d50a66a-1845-4116-8b3a-7b5a2eeb78e6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5795d91c02227db555401b3474e19ae39f9dd759
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096714"
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>Aggiornamento da SQL Server 2005
  La fine del supporto esteso per SQL Server 2005 è uno dei motivi per cui si consiglia di aggiornare subito il sistema a una nuova versione di SQL Server e al database SQL di Azure. L'aggiornamento consente di garantire sicurezza e conformità, di raggiungere eccellenti livelli di prestazioni e di ottimizzare l'infrastruttura della piattaforma di dati.  
  
 Per altre informazioni, indicazioni e strumenti per pianificare e automatizzare l'aggiornamento o la migrazione, vedere [SQL Server 2005 end of support](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)(Fine del supporto per SQL Server 2005).  
  
## <a name="why-upgrade"></a>Vantaggi dell'aggiornamento  
  
> [!IMPORTANT]  
>  Il supporto esteso per SQL Server 2005 termina il 12 aprile 2016. Se si continua a usare SQL Server 2005 dopo il 12 aprile 2016, non si riceveranno più aggiornamenti della sicurezza.  
  
 Per ottenere il foglio dati in formato PDF relativo all'aggiornamento da SQL Server 2005, [fare clic qui](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf) (non sull'immagine di anteprima riportata di seguito).  
  
 ![Foglio dati sull'aggiornamento da SQL Server 2005](../../../2014/sql-server/install/media/sqlserver2005eos.png "foglio dati sull'aggiornamento da SQL Server 2005")  
  
## <a name="choose-your-upgrade-option"></a>Opzioni di aggiornamento disponibili  
 Se si esegue l'aggiornamento a database relazionali da SQL Server 2005, ecco le opzioni per l'archiviazione relazionale nella piattaforma Microsoft.  
  
 Per un'analisi più completa di queste opzioni, [fare clic qui](http://sql05upgrade.azurewebsites.net/).  
  
|Opzione di archiviazione relazionale|Vantaggi|Altri fattori da considerare|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server locale**<br /><br /> Prendere in considerazione questa opzione per le applicazioni di database di qualsiasi tipo, dai sistemi transazionali ai data warehouse.<br /><br /> Per altre informazioni, vedi [SQL Server 2014](https://www.microsoft.com/EN-US/server-cloud/products/sql-server/).|Si ha un maggiore controllo sulle funzionalità e la scalabilità perché vengono gestiti sia l'hardware che il software.<br /><br /> Se esegue l'aggiornamento da SQL Server 2005, questa è l'ambiente più simile.|L'investimento iniziale è elevato ed è necessaria una gestione continua perché è necessario acquistare, mantenere e gestire il proprio hardware e software.|  
|**SQL Server ospitato in macchine virtuali di Azure**<br /><br /> Prendere in considerazione questa opzione se si hanno le esigenze seguenti.<br />-Vantaggi della migrazione a un ambiente ospitato.<br />-Controllo sull'ambiente operativo.<br />-Set di funzionalità familiare di SQL Server.<br /><br /> Per altre informazioni, vedi [SQL Server in macchine virtuali di Azure Panoramica](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Per informazioni sulla migrazione, vedere [Eseguire la migrazione di un database di SQL Server a SQL Server in una macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|È possibile eseguire rapidamente la distribuzione da una libreria di immagini della macchina virtuale.<br /><br /> Viene fornito il set di funzionalità completo di SQL Server.<br /><br /> Si risparmiano i costi per l'hardware e il software del server. Si paga per ora in base all'utilizzo.|È necessario configurare e gestire sia SQL Server che il software del sistema operativo.|  
|**Servizio di database ospitato nel database SQL di Azure**<br /><br /> Prendere in considerazione questa opzione se si preferisce una soluzione a basso costo che necessita di poca manutenzione.<br /><br /> Questa opzione è particolarmente adatta per le app che non richiedono una capacità costante o che devono fornire un accesso esterno.<br /><br /> Per altre informazioni, vedi [Database SQL](https://azure.microsoft.com/services/sql-database/).<br /><br /> Per informazioni sulla migrazione, vedi [migrazione di un database di SQL Server al Database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|La distribuzione è rapida e la scalabilità verticale semplice.<br /><br /> Si paga per ora in base all'utilizzo.<br /><br /> Il costo del servizio include anche la disponibilità elevata e i backup automatici, oltre all'archiviazione.|Il database SQL di Azure non offre alcune delle funzionalità di SQL Server non applicabili a un ambiente cloud ospitato. Per altre informazioni, vedere [Differenze di Transact-SQL del database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> Anche le dimensioni massime del database SQL di Azure sono di 500 GB, invece dei 524 PB di SQL Server.|  
  
 Per alcuni dati e applicazioni si può valutare anche una soluzione non relazionale o NoSQL.  
  
|Soluzione non relazionale|Vantaggi|  
|------------------------------|--------------|  
|**Azure DocumentDB**<br /><br /> Prendere in considerazione questa opzione per applicazioni moderne, scalabili, mobili e Web che usano i dati JSON e richiedono una combinazione affidabile di funzionalità di query e di elaborazione dei dati transazionali.<br /><br /> Per altre informazioni, vedere [DocumentDB](https://azure.microsoft.com/en-us/services/documentdb/).|I documenti vengono indicizzati ed è possibile eseguire query usando la sintassi SQL con cui si ha già familiarità.<br /><br /> Il database è senza schema.<br /><br /> È possibile aggiungere proprietà ai documenti senza dover ricompilare gli indici.<br /><br /> Il supporto per JSON e JavaScript viene fornito direttamente all'interno del motore di database.<br /><br /> Il supporto nativo viene fornito per i dati geospaziali e l'integrazione con altri servizi di Azure, inclusi Ricerca di Azure, HDInsight e Data Factory.<br /><br /> Si ottiene un'archiviazione a bassa latenza e ad alte prestazioni con livelli di velocità effettiva riservati.|  
|**Archiviazione tabelle di Azure**<br /><br /> Prendere in considerazione questa opzione per archiviare petabyte di dati semistrutturati in una soluzione conveniente.<br /><br /> Per altre informazioni, vedere [Archivio tabelle](https://azure.microsoft.com/services/storage/tables/).|È possibile sviluppare le app e lo schema della tabella senza disconnettere i dati.<br /><br /> È possibile usare la scalabilità verticale senza partizionamento orizzontale del set di dati.<br /><br /> Si ottiene un'archiviazione con ridondanza geografica che replica i dati in più regioni.|  
  
 Per scaricare il report sulla migrazione da SQL Server 2005 di Directions on Microsoft, contenente altre informazioni sulle opzioni di aggiornamento, [fare clic qui](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) (non sull'immagine di anteprima riportata di seguito).  
  
 ![Report sulla migrazione da SQL Server 2005](../../../2014/sql-server/install/media/sqlserver2005migratingdoc.png "Report sulla migrazione da SQL Server 2005")  
  
## <a name="plan-your-upgrade"></a>Pianificare l'aggiornamento  
  
-   Per informazioni su come pianificare l'aggiornamento, vedere la serie seguente di post di blog del team di SQL Server.  
  
    -   [Pianificazione di un aggiornamento efficiente da SQL Server 2005: Passaggio 1 di 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Pianificazione di un aggiornamento efficiente da SQL Server 2005: Passaggio 2 di 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Pianificazione di un aggiornamento efficiente da SQL Server 2005: Passaggio 3 di 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Esaminare i requisiti e considerazioni sotto [pianificazione di un'installazione di SQL Server](../../../2014/sql-server/install/planning-a-sql-server-installation.md), tra cui le [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Vedere come eseguire l'aggiornamento.  
  
    -   Esaminare i metodi di aggiornamento disponibili e ottenere informazioni sulla pianificazione e sull'esecuzione dei test nell'argomento [Aggiornare il motore di database](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >  Non è possibile eseguire l'aggiornamento di un server SQL Server 2005 a un server SQL Server 2014 sul posto. È necessario installare SQL Server 2014, quindi eseguire la migrazione dei database SQL Server 2005 alla nuova installazione.  
  
    -   Per ottenere una guida tecnica all'aggiornamento più dettagliata in formato PDF, [fare clic qui](https://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf).  
  
-   Per altre informazioni, indicazioni e strumenti per pianificare e automatizzare l'aggiornamento o la migrazione, vedere [SQL Server 2005 end of support](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)(Fine del supporto per SQL Server 2005).  
  
## <a name="get-sql-server-2014"></a>Ottenere SQL Server 2014  
 Per scaricare una copia di valutazione di SQL Server 2014 [fare clic qui](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2014).  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server 2014](https://www.microsoft.com/en-us/server-cloud/products/sql-server/default.aspx)   
 [SQL Server 2005 end of support](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
 [Eseguire l'aggiornamento da SQL Server 2005 a SQL Server 2016](https://msdn.microsoft.com/library/mt168847.aspx)  
  
  

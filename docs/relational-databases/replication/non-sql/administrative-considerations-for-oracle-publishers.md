---
title: Considerazioni amministrative per i server di pubblicazione Oracle
description: Considerazioni per l'amministrazione dei server di pubblicazione Oracle che pubblicano modifiche per i sottoscrittori di SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8f8a436035c18f7bd6e5a1867ebe92433e4e5951
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "75321899"
---
# <a name="administrative-considerations-for-oracle-publishers"></a>Considerazioni amministrative per i server di pubblicazione Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dopo la configurazione di un server di pubblicazione Oracle e l'implementazione dei meccanismi di rilevamento delle modifiche della replica, gli amministratori del sistema di database Oracle possono utilizzare utilità di database Oracle standard ed eseguire attività tipiche di amministrazione dei sistemi. È tuttavia opportuno considerare gli effetti sui dati pubblicati di determinate attività amministrative.  
  
 Ad eccezione dell'eliminazione o della modifica di una colonna pubblicata per la replica oppure dell'eliminazione o della modifica di oggetti di replica, queste considerazioni non sono applicabili alle pubblicazioni snapshot.  
  
## <a name="importing-and-loading-data"></a>Importazione e caricamento di dati  
 I trigger vengono utilizzati nel rilevamento delle modifiche per le pubblicazioni transazionali in Oracle. Le modifiche apportate alle tabelle pubblicate possono essere replicate nei Sottoscrittori soltanto in caso di attivazione di trigger di replica al momento di un aggiornamento, un inserimento o un'eliminazione. Le utilità Oracle SQL*Loader e Oracle Import dispongono di opzioni che influiscono sull'attivazione di trigger in caso di inserimento di righe nelle tabelle replicate con queste utilità.  
  
### <a name="oracle-import"></a>Oracle Import  
 Con Oracle Import, è possibile impostare l'opzione **ignore** su "y" o "n". L'impostazione predefinita è "n". Se **ignore** è impostata su "n", la tabella viene eliminata e ricreata durante l'importazione. In questo modo, vengono rimossi i trigger di replica e viene disabilitata la replica. Se **ignore** è impostata su "y", durante l'importazione viene tentato il caricamento delle righe nella tabella esistente, attivando i trigger di replica. In caso di importazione in una tabella replicata con lo strumento Oracle Import, assicurarsi pertanto che l'opzione **ignore** sia impostata su "y".  
  
### <a name="sqlloader"></a>SQL*Loader  
 Con SQL\*Loader è possibile impostare l'opzione **direct** su 'true' o 'false'. L'impostazione predefinita è "false". Se **direct** è impostata su "false", le righe vengono inserite mediante istruzioni INSERT convenzionali, che attivano trigger di replica. Se **direct** è impostata su "true", il caricamento viene ottimizzato e i trigger non vengono attivati. In caso di caricamento in una tabella replicata con lo strumento SQL*Loader, assicurarsi pertanto che l'opzione **direct** sia impostata su "false".  
  
## <a name="making-changes-to-published-objects"></a>Modifiche a oggetti pubblicati  
 Le azioni seguenti non richiedono speciali considerazioni:  
  
-   Ricompilazione di indici su tabelle pubblicate.  
  
-   Aggiunta di trigger dell'utente a una tabella pubblicata.  
  
 L'azione seguente richiede l'arresto di tutte le attività sulle tabelle pubblicate:  
  
-   Spostamento di una tabella pubblicata.  
  
 Le azioni seguenti richiedono l'eliminazione della pubblicazione, l'esecuzione dell'operazione e infine la ricreazione della pubblicazione:  
  
-   Troncamento di una tabella pubblicata.  
  
-   Ridenominazione di una tabella pubblicata.  
  
-   Aggiunta di una colonna a una tabella pubblicata.  
  
-   Eliminazione o modifica di una colonna pubblicata per la replica.  
  
-   Esecuzione di operazioni non registrate.  
  
## <a name="dropping-or-modifying-replication-objects"></a>Eliminazione o modifica di oggetti di replica  
 In caso di eliminazione o modifica di qualsiasi trigger, sequenza, stored procedure o tabella di rilevamento a livello di server di pubblicazione, è necessario eliminare e riconfigurare il server di pubblicazione. Per un elenco parziale di questi oggetti, vedere [Oggetti creati nel server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md).  
  
 Per informazioni sull'eliminazione e sulla riconfigurazione del server di pubblicazione, vedere la sezione relativa alle modifiche che richiedono la riconfigurazione del server di pubblicazione nell'argomento [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Considerazioni e limitazioni relative alla progettazione dei server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Panoramica della pubblicazione Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  

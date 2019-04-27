---
title: Configurare le istanze del motore di database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 578b870128486285a7c31bf9a860b85d170f8771
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786604"
---
# <a name="configure-database-engine-instances-sql-server"></a>Configurare le istanze del motore di database (SQL Server)
  È necessario configurare ogni istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] per soddisfare i requisiti di prestazione e disponibilità definiti per i database ospitati dall'istanza. [!INCLUDE[ssDE](../../includes/ssde-md.md)] include opzioni di configurazione che controllano i comportamenti quale utilizzo della risorsa e la disponibilità di funzionalità come il controllo o il trigger recursion.  
  
## <a name="instance-configuration"></a>Configurazione dell'istanza  
 Quando un database viene distribuito in produzione spesso esiste un contratto sul livello di servizio (Service Level Agreement, SLA) che definisce aree come i livelli di prestazioni richiesti dal database e il livello di disponibilità richiesto del database. I termini del contratto sul livello di servizio in genere fornisce i requisiti di configurazione per l'istanza.  
  
 Un'istanza viene configurata generalmente immediatamente dopo l'installazione. La configurazione iniziale è solitamente determinata dai requisiti del contratto sul livello di servizio dei tipi di database studiato per essere distribuito all'istanza. Dopo la distribuzione dei database, gli amministratori del database controllano le prestazioni dell'istanza e regolano le impostazioni di configurazione in base alle necessità se la metrica delle prestazioni mostra che l'istanza non sta soddisfacendo i requisiti del contratto del livello di servizio.  
  
## <a name="configuration-tasks"></a>Attività di configurazione  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Si descrivono le varie opzioni di configurazione dell'istanza e come visualizzare o modificare queste opzioni.|[Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)|  
|Si descrive come visualizzare e configurare i percorsi predefiniti dei nuovi file di dati e di log nell'istanza.|[Visualizzare o modificare i percorsi predefiniti per i file di dati e di log &#40;SQL Server Management Studio&#41;](view-or-change-the-default-locations-for-data-and-log-files.md)|  
|Si descrive come configurare SQL Server per l'utilizzo di Soft-NUMA|[Configurare SQL Server per l'utilizzo di Soft-NUMA &#40;SQL Server&#41;](soft-numa-sql-server.md)|  
|Si descrive come eseguire il mapping di una porta TCP/IP all'affinità del nodo NUMA (non-uniform memory access).|[Eseguire il mapping delle porte TCP/IP ai nodi NUMA &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Si descrive come abilitare i criteri di Blocco di pagine in memoria di Windows. Con questi criteri è possibile determinare gli account autorizzati a utilizzare un processo per mantenere i dati nella memoria fisica, impedendo al sistema di eseguire il paging dei dati nella memoria virtuale su disco.|[Abilitare l'opzione Blocco di pagine in memoria &#40;Windows&#41;](enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Istanze del motore di database &#40;SQL Server&#41;](database-engine-instances-sql-server.md)  
  
  

---
title: Gestione di un dominio composito
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 47821eff-800b-4053-8d36-e42bbc267f54
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 0f6c31e8e1cb40c5fbb00eaaf42c8734a8392f74
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898079"
---
# <a name="managing-a-composite-domain"></a>Gestione di un dominio composito

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  In questo argomento viene descritto l'utilizzo dei domini composti in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Talvolta un singolo dominio non è sufficiente per rappresentare i dati in un campo ed è possibile rappresentare i dati solo raggruppando i singoli domini. A tale scopo, è possibile creare un dominio composito. Un dominio composito è costituito da due o più singoli domini di cui viene eseguito il mapping a un campo dati costituito da più termini correlati che non vengono analizzati, ma inclusi in un singolo valore composito. Ogni termine nel valore sarà rappresentato da un singolo dominio diverso. Dopo avere incluso i singoli domini in domini compositi e quindi eseguito il mapping del dominio composito al campo dati, è possibile compilare le informazioni nella Knowledge Base sui dati del campo compilando le informazioni nei singoli domini. Un dominio composito, analogamente a un singolo dominio, è una rappresentazione semantica dei dati in un singolo campo dati.  
  
 I singoli domini in un dominio composito devono contenere un'area delle informazioni in comune. Un esempio è un campo indirizzo che contiene i dati per strada, città, provincia, comune e codice postale. I diversi termini in questo campo potrebbero contenere tipi di dati diversi. Per gestire questa condizione, eseguire il mapping di tali termini ai diversi singoli domini. Un altro esempio è un campo nome che contiene i dati per nome, secondo nome e cognome. Per utilizzare un dominio composito, è necessario potere analizzare i dati nel campo nei diversi singoli domini, creando un dominio composito per il campo e un singolo dominio per parte del campo.  
  
 I domini compositi hanno funzionalità diverse rispetto ai singoli domini. Non è possibile modificare i valori nel dominio composito. È necessario eseguire tale operazione in un singolo dominio. Con i domini compositi è possibile utilizzare le regole tra domini per testare i valori nei singoli domini del dominio composito. È inoltre possibile visualizzare le combinazioni di valori presenti nei domini compositi.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 L'utilizzo di un dominio composito consente di effettuare le operazioni seguenti:  
  
|||  
|-|-|  
|Creare una rappresentazione semantica per un campo dati costituito da più termini correlati non analizzati.|[Creazione di un dominio composito](../data-quality-services/create-a-composite-domain.md)|  
|Quando si esegue il mapping di dati complessi a un dominio composito, è possibile analizzare i dati in base alle informazioni oltre che in base a un delimitatore. Verranno innanzitutto utilizzate le informazioni sui singoli domini per determinare come le parti della stringa complessa appartengano ai singoli domini.|[Creazione di un dominio composito](../data-quality-services/create-a-composite-domain.md)|  
|Associare un servizio dati di riferimento, ad esempio un servizio di gestione dei dati di indirizzo, a un dominio composito.|[Collegare un dominio o un dominio composito ai dati di riferimento](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Creare una regola tra domini quando il valore di un dominio in un dominio composito influisce sul valore di un altro dominio.|[Creare una regola tra domini](../data-quality-services/create-a-cross-domain-rule.md)|  
|Identificare le combinazioni di valori in modo da indicarne la frequenza.|[Utilizzare le relazioni di valori in un dominio composito](../data-quality-services/use-value-relations-in-a-composite-domain.md)|  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Compilazione di una Knowledge Base eseguendo l'individuazione delle informazioni e gestendo queste ultime in modo interattivo|[Compilazione di una Knowledge Base](../data-quality-services/building-a-knowledge-base.md)|  
|Importazione o esportazione di informazioni da una Knowledge Base.|[Importazione ed esportazione delle informazioni](../data-quality-services/importing-and-exporting-knowledge.md)|  
|Creazione di un singolo dominio e aggiunta di informazioni al dominio.|[Gestione di un dominio](../data-quality-services/managing-a-domain.md)|  
  
  

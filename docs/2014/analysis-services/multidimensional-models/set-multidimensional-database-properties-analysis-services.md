---
title: Impostare le proprietà di Database multidimensionale (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], databases
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa3e1544f625183df3240359aa22b117144244d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072996"
---
# <a name="set-multidimensional-database-properties-analysis-services"></a>Impostare le proprietà dei database multidimensionali (Analysis Services)
  Sono disponibili numerose proprietà di database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che possono essere configurate in Progettazione database di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
 In questa finestra di progettazione è possibile eseguire i tipi di attività seguenti:  
  
-   In caso di connessione al database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità online, è possibile modificare il nome del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In modalità progetto è possibile modificare il nome del database per la successiva distribuzione del progetto. Per altre informazioni, vedere [Rinominare un database multidimensionale &#40;Analysis Services&#41;](rename-a-multidimensional-database-analysis-services.md) e [Configurare proprietà di progetti di Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md).  
  
-   È possibile specificare una descrizione del database presentabile agli utenti. È inoltre possibile visualizzare il nome del database, ma non modificarlo. Per modificare il nome del database, è necessario modificare le proprietà del progetto.  
  
-   È possibile specificare traduzioni per il nome del database e la descrizione in una o più lingue. Per altre informazioni, vedere [traduzioni di cubi](../multidimensional-models-olap-logical-cube-objects/cube-translations.md), [traduzioni delle dimensioni](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md), e [traduzioni &#40;Analysis Services&#41;](../translations-analysis-services.md).  
  
-   È possibile visualizzare e modificare i mapping dei tipi di conto predefiniti. I mapping dei tipi di conto vengono usati quando una o più misure usano la funzione di aggregazione *ByAccount* . Per ogni tipo di conto è possibile specificare un alias e modificare la funzione di aggregazione predefinita associata al tipo di conto. Per altre informazioni sulla modifica dell'aggregazione predefinita, vedere [Definire una funzione semiadditiva](define-semiadditive-behavior.md).  
  
## <a name="database-properties"></a>Proprietà dei database  
 In aggiunta alle attività sopra descritte, è possibile configurare alcune proprietà di un database nella finestra Proprietà.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|Prefisso aggregazioni|Prefisso comune utilizzabile per i nomi di aggregazioni in tutte le partizioni di un database. Per altre informazioni, vedere [Elemento AggregationPrefix &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/aggregationprefix-element-assl).|  
|Regole di confronto|Quando il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene distribuito in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , il database eredita la proprietà Regole di confronto del server a meno che non venga specificato un valore diverso in questa finestra.|  
|DataSourceImpersonationInfo|Specifica la modalità di rappresentazione predefinita per tutti gli oggetti origine dei dati nel database. Tale modalità viene usata dal servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante l'elaborazione degli oggetti, la sincronizzazione dei server e l'esecuzione delle istruzioni di data mining OpenQuery e SystemOpenSchema.|  
|Dimensioni stimate|Fornisce una dimensione stimata dei file di database su disco. Se i dati vengono archiviati in più percorsi, questa stima sarà limitata solo ai file di dati archiviati nella cartella del database.<br /><br /> `EstimatedSize` può essere utilizzata anche come base per stimare la memoria. In genere i requisiti di memoria sono maggiori delle dimensioni dei dati su disco, a causa di strutture di dati aggiuntive create quando il database tabulare viene caricato in memoria.<br /><br /> Per stimare ulteriormente i requisiti di memoria, è inoltre possibile utilizzare Gestione attività per analizzare la memoria del processo di Analysis Services prima e dopo avere l'elaborazione del database e osservare la memoria utilizzata come metodo per capire i requisiti di memoria del database.|  
|Linguaggio|Quando il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene distribuito in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , il database eredita la proprietà Lingua del server a meno che non venga specificato un valore diverso in questa finestra.|  
|MasterDataSourceID|Utilizzata con le partizioni remote. Per altre informazioni, vedere [Partizioni remote](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Proprietà database &#40;SSAS - Multidimensionale&#41;](../database-properties-dialog-box-ssas-multidimensional.md)   
 [Configurare proprietà di progetti di Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)  
  
  

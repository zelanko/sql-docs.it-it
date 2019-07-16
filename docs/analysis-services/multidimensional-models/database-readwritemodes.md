---
title: Proprietà readwritemode del database | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e80433c224f08b9074a8d1ef93ef96bdc157853
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178845"
---
# <a name="database-readwritemodes"></a>Proprietà ReadWriteMode del database
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Spesso, un amministratore di database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vuole impostare un database di lettura/scrittura in sola lettura o viceversa. Queste situazioni sono il più delle volte determinate da esigenze aziendali, ad esempio la condivisione della stessa cartella di database tra più server per ottenere la scalabilità orizzontale di una soluzione, e per migliorare le prestazioni. In questi casi, la proprietà di database **ReadWriteMode** consente all'amministratore di database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di cambiare facilmente la modalità operativa del database.  
  
## <a name="readwritemode-database-property"></a>Proprietà di database ReadWriteMode  
 La proprietà di database **ReadWriteMode** specifica se il database è in modalità lettura/scrittura o in modalità sola lettura. Questi sono i due soli valori possibili della proprietà. Quando il database è in modalità sola lettura, non è possibile applicare modifiche o aggiornamenti. Quando invece il database è in modalità lettura/scrittura, le modifiche e gli aggiornamenti possono verificarsi. La proprietà di database **ReadWriteMode** è definita come proprietà di sola lettura e può essere impostata solo tramite un comando **Attach** .  
  
 Quando un database è in modalità sola lettura, si applicano determinate restrizioni che influiscono sul set ordinario di operazioni consentite sul database. Per informazioni sulle operazioni con restrizioni, vedere la tabella seguente.  
  
|Modalità ReadOnly|Operazioni con restrizioni|  
|-------------------|---------------------------|  
|Comandi XML/A<br /><br /> <br /><br /> Nota: Quando si esegue uno di questi comandi, viene generato un errore.|**Creare**<br /><br /> **Alter**<br /><br /> **Elimina**<br /><br /> **Process**<br /><br /> **MergePartitions**<br /><br /> **DesignAggregations**<br /><br /> **CommitTransaction**<br /><br /> **Restore**<br /><br /> **Sincronizza**<br /><br /> **Insert**<br /><br /> **Update**<br /><br /> **Drop**<br /><br /> <br /><br /> Nota: Il writeback delle celle è consentito nei database impostati in sola lettura. Tuttavia, le modifiche non possono essere eseguito il commit.|  
|Istruzioni MDX<br /><br /> <br /><br /> Nota: Viene generato un errore quando si esegue una di queste istruzioni.|**COMMIT TRAN**<br /><br /> **CREATE SESSION CUBE**<br /><br /> **ALTER CUBE**<br /><br /> **ALTER DIMENSION**<br /><br /> **CREATE DIMENSION MEMBER**<br /><br /> **DROP DIMENSION MEMBER**<br /><br /> **ALTER DIMENSION**<br /><br /> <br /><br /> Nota: Gli utenti di Excel non è possibile utilizzare la caratteristica di raggruppamento nelle tabelle Pivot, perché tale caratteristica è implementata internamente tramite **CREATE SESSION CUBE** comandi.|  
|Istruzioni DMX<br /><br /> <br /><br /> Nota: Viene generato un errore quando si esegue una di queste istruzioni.|**CREATE [SESSION] MINING STRUCTURE**<br /><br /> **ALTER MINING STRUCTURE**<br /><br /> **DROP MINING STRUCTURE**<br /><br /> **CREATE [SESSION] MINING MODEL**<br /><br /> **DROP MINING MODEL**<br /><br /> **IMPORT**<br /><br /> **SELECT INTO**<br /><br /> **INSERT**<br /><br /> **UPDATE**<br /><br /> **DELETE**|  
|Operazioni in background|Le operazioni in background che comportano la modifica del database sono disabilitate, ad esempio l'elaborazione lenta e la memorizzazione nella cache attiva.|  
  
## <a name="readwritemode-usage"></a>Utilizzo di ReadWriteMode  
 La proprietà di database **ReadWriteMode** deve essere usata come parte di un comando di database **Attach** . Il comando **Attach** consente di impostare la proprietà di database su **ReadWrite** o **ReadOnly**. Il valore della proprietà di database **ReadWriteMode** non può essere aggiornato direttamente perché la proprietà è definita di sola lettura. I database vengono creati con la proprietà **ReadWriteMode** impostata su **ReadWrite**. Non è possibile creare un database in modalità sola lettura.  
  
 Per alternare la proprietà di database **ReadWriteMode** tra **ReadWrite** e **ReadOnly**, è necessario immettere una sequenza di comandi **Detach/Attach** .  
  
 Tutte le operazioni di database, ad eccezione di **Attach**, mantengono la proprietà di database **ReadWriteMode** nello stato corrente. Ad esempio, operazioni come **Alter**, **Backup**, **Restore**e **Synchronize** mantengono il valore di **ReadWriteMode** .  
  
> [!NOTE]  
>  È possibile creare cubi locali da un database di sola lettura.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Collegamento e scollegamento di database di Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Spostare un database di Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  

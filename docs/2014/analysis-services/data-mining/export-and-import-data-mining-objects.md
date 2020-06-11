---
title: Esportare e importare oggetti di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- exporting mining models
- exporting mining structures
- mining structures [Analysis Services], creating
- mining structures [DMX], exporting
- mining models [Analysis Services], migration
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
author: minewiskan
ms.author: owend
ms.openlocfilehash: 01e8651dd7e9d59012b0ba065bccb9ea62a1ee54
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522537"
---
# <a name="export-and-import-data-mining-objects"></a>Esportare e importare gli oggetti di data mining
  Oltre alle funzionalità fornite in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per il backup, il ripristino e la migrazione di soluzioni, il componente Data mining di SQL Server offre la possibilità di trasferire rapidamente strutture e modelli di data mining tra server diversi tramite DMX (Data Mining Extensions).  
  
 Se la soluzione di data mining utilizza dati relazionali anziché un database multidimensionale, il trasferimento dei modelli mediante `EXPORT` e `IMPORT` risulta molto più veloce e semplice rispetto all'utilizzo della funzione di ripristino del database o alla distribuzione di un'intera soluzione.  
  
 In questa sezione viene fornita una panoramica di come trasferire strutture e modelli di data mining mediante istruzioni DMX. Per informazioni dettagliate sulla sintassi con relativi esempi, vedere [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx) e [IMPORT &#40;DMX&#41;](/sql/dmx/import-dmx).  
  
> [!NOTE]  
>  Per esportare o importare oggetti da un database di Microsoft SQL Server Analysis Services, è necessario essere un amministratore del server o del database.  
  
## <a name="exporting-data-mining-structures"></a>Esportazione di strutture di data mining  
 Quando si esporta una struttura di data mining, l'istruzione EXPORT esporta automaticamente tutti i modelli associati. Se si desidera controllare gli oggetti esportati, è necessario specificare ogni oggetto per nome.  
  
 Se durante l'esportazione la struttura di data mining è stata elaborata e i risultati sono stati memorizzati nella cache, che rappresenta il comportamento predefinito, la definizione conterrà un riepilogo dei dati su cui si basa la struttura. Per rimuovere questo riepilogo, è necessario cancellare la cache associata alla struttura di data mining eseguendo l'operazione `Process Clear Structure`. Per altre informazioni, vedere [Elaborare una struttura di data mining](process-a-mining-structure.md).  
  
### <a name="exporting-data-mining-models"></a>Esportazione di modelli di data mining  
 È possibile utilizzare la parola chiave `WITH DEPENDENCIES` per esportare l'origine dati e la definizione della vista origine dati insieme al modello di data mining e alla relativa struttura.  
  
 Quando si esporta un modello di data mining senza esportarne le dipendenze, l'istruzione EXPORT esporta la definizione del modello di data mining e la relativa struttura di data mining, ma non la definizione delle origini dati. Di conseguenza, dopo aver importato il modello sarà possibile esplorarlo immediatamente ma, se si desidera rielaborarlo nel server di destinazione o eseguire query sui dati sottostanti, sarà necessario creare un'origine dati corrispondente nel server di destinazione.  
  
## <a name="importing-data-mining-structures-and-models"></a>Importazione di strutture e modelli di data mining  
 Quando si importa un oggetto di data mining, esso viene importato nel server e nel database ai cui si è connessi quando si esegue l'istruzione IMPORT. Se il file di importazione include un database che non esiste nel server, il database verrà creato.  
  
 È inoltre possibile importare una struttura o un modello di data mining mediante il comando `Restore`. I modelli o le strutture verranno ripristinate nel database che presenta lo stesso nome del database dal quale sono stati esportati. Per altre informazioni, vedere [Opzioni di ripristino](../multidimensional-models/restore-options.md).  
  
## <a name="remarks"></a>Commenti  
 Non è possibile importare un modello o una struttura in un server se in tale server è già presente un modello o una struttura con lo stesso nome. Inoltre, non è possibile esportare un oggetto di data mining, quindi modificarne il nome nel file di esportazione. Pertanto, se si prevedono conflitti di denominazione, è necessario eliminare l'oggetto di data mining nel server di destinazione o rinominare l'oggetto di data mining prima di esportare la definizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli oggetti e delle soluzioni di data mining](management-of-data-mining-solutions-and-objects.md)  
  
  

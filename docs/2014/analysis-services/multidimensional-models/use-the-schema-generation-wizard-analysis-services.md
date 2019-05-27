---
title: Utilizzare la generazione guidata Schema (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e434493813f0237533ca2e50ff089974f3556f34
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072650"
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>Utilizzare la Generazione guidata schema (Analysis Services)
  Durante la fase di generazione con Generazione guidata schema è necessario disporre di una quantità ridotta di informazioni. La maggior parte delle informazioni richieste dalla Generazione guidata schema per la generazione di schemi relazionali vengono estratte dai cubi e dalle dimensioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] già creati nel progetto. Inoltre, è possibile personalizzare come viene generato lo schema del database dell'area di interesse, nonché come vengono denominati gli oggetti nello schema.  
  
## <a name="start-the-wizard"></a>Avviare la procedura guidata  
 È possibile aprire la Generazione guidata schema da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in diversi modi:  
  
-   Fare clic con il pulsante destro del mouse sull'oggetto progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi scegliere **Genera schema relazionale** dal menu di scelta rapida.  
  
-   Fare clic sull'oggetto progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi scegliere **Genera schema relazionale** dal menu **Database** .  
  
-   Avviare la procedura guidata da Creazione guidata dimensione facendo clic sulla casella di controllo **Genera schema adesso** nell'ultima pagina della procedura.  
  
## <a name="step-1-specify-targets"></a>Passaggio 1: Specificare le destinazioni  
 È necessario specificare la vista origine dati in cui si desidera venga generato lo schema del database dell'area di interesse mediante la Generazione guidata schema. Anche se è possibile selezionare una vista origine dati esistente, viene in genere creata una nuova in base a un'origine dati. È possibile creare l'origine dati in base a una connessione esistente o nuova oppure in base a un altro oggetto. Lo schema del database dell'area di interesse viene generato dalla Generazione guidata schema sia nel database a cui fa riferimento l'origine dei dati sia nella vista origine dati. La Generazione guidata schema non crea il database dell'area di interesse, bensì lo schema relazionale in grado di supportare i cubi e le dimensioni contenuti in un database esistente specificato.  
  
 Quando Generazione guidata schema genera gli oggetti sottostanti, le dimensioni e i cubi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono associati alle tabelle e alle colonne generate usando associazioni di tipo vista origine dati.  
  
> [!NOTE]  
>  Per disassociare dimensioni e cubi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da oggetti generati in precedenza, eliminare la vista origine dati a cui sono associati i cubi e le dimensioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi definire una nuova vista origine dati per i cubi e le dimensioni mediante la Generazione guidata schema.  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>Passaggio 3: Specificare le opzioni dello Schema per il Database dell'Area di interesse  
 In Generazione guidata schema sono disponibili varie opzioni per la definizione dello schema da generare per il database dell'area di interesse. È possibile impostare queste opzioni nella pagina **Opzioni schema database area di interesse** della procedura guidata.  
  
### <a name="specifying-the-schema-owner"></a>Impostazione del proprietario dello schema  
 È possibile specificare il proprietario dello schema impostando il valore di **Nome schema** su una stringa valida. Per impostazione predefinita il proprietario dello schema è il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ma è possibile impostare qualsiasi altro proprietario a seconda delle preferenze.  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>Impostazione di chiavi primarie, indici e vincoli  
 Per impostazione predefinita, Generazione guidata schema crea un vincolo di chiave primaria in ogni tabella delle dimensioni del database dell'area di interesse. La chiave primaria corrisponde all'attributo designato come attributo chiave nella dimensione corrispondente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questo vincolo consente di migliorare le prestazioni di elaborazione nella maggior parte degli ambienti con costi ridotti. Le chiavi primarie logiche vengono create sempre nella vista origine dati, anche se si sceglie di non creare la chiave primaria nel database dell'area di interesse. Per definire i vincoli di chiave primaria nelle tabelle delle dimensioni, selezionare **Crea chiavi primarie nelle tabelle delle dimensioni**.  
  
 Per impostazione predefinita verranno creati anche gli indici nelle colonne chiavi esterne di ogni tabella dei fatti. Questi indici consentono di migliorare le prestazioni di elaborazione nella maggior parte degli ambienti. In genere, le prestazioni migliorano poiché le query di elaborazione generate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per recuperare nuovi dati dal database dell'area di interesse includono un numero significativo di istruzioni per il join tra la tabella dei fatti e le tabelle delle dimensioni. Per definire gli indici nelle colonne chiave esterna di ogni tabella dei fatti, selezionare **Crea indici**.  
  
 Per impostazione predefinita, tra la tabella dei fatti e ogni tabella delle dimensioni viene applicata l'integrità referenziale. Se si sceglie di non applicare l'integrità referenziale, Generazione guidata schema creerà comunque queste relazioni nel database e nella vista origine dati. Per applicare l'integrità referenziale, selezionare **Applica integrità referenziale**.  
  
### <a name="preserving-data-for-incremental-generation"></a>Mantenimento dei dati per la generazione incrementale  
 Per impostazione predefinita, Generazione guidata schema tenta di mantenere i dati durante la rigenerazione dello schema del database. Nel caso in cui durante l'esecuzione di Generazione guidata schema sia necessario eliminare una riga in seguito a una modifica dello schema, verrà visualizzato un avviso prima dell'eliminazione effettiva delle righe. Ad esempio, può rivelarsi necessario eliminare determinate righe per risolvere problemi di integrità referenziale in seguito all'eliminazione di una dimensione oppure in seguito alla modifica del tipo di dati dovuta alla modifica di un attributo della dimensione. Per mantenere i dati durante la rigenerazione dello schema del database, selezionare **Mantieni dati in caso di rigenerazione**.  
  
## <a name="step-4-specify-naming-conventions"></a>Passaggio 4: Impostazione convenzioni di denominazione  
 È possibile definire convenzioni di denominazione da usare in Generazione guidata schema per la generazione di determinati oggetti nel database dell'area di interesse tramite la pagina **Impostazione convenzioni di denominazione** della procedura guidata. Per altre informazioni sulle opzioni disponibili nella pagina **Impostazione convenzioni di denominazione** , vedere [Impostazione convenzioni di denominazione &#40;Generazione guidata schema&#41; &#40;Analysis Services - Dati multidimensionali&#41;](../specify-naming-conventions-schema-generation-analysis-services-multidimensional-data.md).  
  
  

---
title: Editor trasformazione Ricerca fuzzy (scheda tabella di riferimento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eb86e4a6382095bb8bb0edc744fe6d16650581fd
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425208"
---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>Editor trasformazione Ricerca fuzzy (scheda Tabella di riferimento)
  Usare la scheda **Tabella di riferimento** della finestra di dialogo **Editor trasformazione Ricerca fuzzy** per specificare la tabella di origine e l'indice da usare per la ricerca. Tale origine deve essere una tabella di un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  La trasformazione Ricerca fuzzy crea una copia di lavoro della tabella di riferimento. Gli indici descritti di seguito vengono creati su tale tabella di lavoro usando una tabella speciale invece di un normale indice [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La trasformazione non modifica le tabelle di origine esistenti, a meno che non sia stata selezionata l'opzione **Manutenzione indice archiviato**. In questo caso viene creato un trigger sulla tabella di riferimento che aggiorna la tabella di lavoro e la tabella dell'indice di ricerca in base alle modifiche apportate alla tabella di riferimento.  
  
> [!NOTE]  
>  Le `Exhaustive` proprietà e `MaxMemoryUsage` della trasformazione Ricerca fuzzy non sono disponibili nell' **Editor trasformazione Ricerca fuzzy**, ma possono essere impostate tramite il **Editor avanzato**. Inoltre, è possibile specificare un valore maggiore di 100 per `MaxOutputMatchesPerInput` solo nell' **Editor avanzato**. Per altre informazioni su queste proprietà, vedere la sezione relativa alla trasformazione Ricerca fuzzy in [Proprietà personalizzate delle trasformazioni](data-flow/transformations/transformation-custom-properties.md).  
  
 Per ulteriori informazioni sulla trasformazione Ricerca fuzzy, vedere [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione OLE DB esistente nell'elenco o fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuovo**  
 Consente di creare una nuova connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Genera nuovo indice**  
 Consente di specificare che la trasformazione deve creare un nuovo indice da utilizzare per la ricerca.  
  
 **Nome tabella di riferimento**  
 Consente di selezionare la tabella esistente da utilizzare come tabella di riferimento, ovvero di ricerca.  
  
 **Archivia nuovo indice**  
 Selezionare questa opzione per salvare il nuovo indice di ricerca.  
  
 **Nome nuovo indice**  
 Consente di digitare un nome descrittivo per il nuovo indice di ricerca da salvare.  
  
 **Manutenzione indice archiviato**  
 Consente di specificare se la manutenzione dell'indice deve essere eseguita anche da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se si è scelto di salvare il nuovo indice di ricerca.  
  
> [!NOTE]  
>  Se si seleziona **Manutenzione indice archiviato** nella scheda **Tabella di riferimento** di **Editor trasformazione Ricerca fuzzy**, la trasformazione utilizza stored procedure gestite per gestire l'indice. Queste stored procedure gestite usano la funzionalità di integrazione con Common Language Runtime (CLR) presente in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per impostazione predefinita, l'integrazione con CLR non è abilitata in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per utilizzare la funzionalità **Manutenzione indice archiviato** è necessario abilitare l'integrazione con CLR. Per altre informazioni, vedere [Enabling CLR Integration](../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Considerato che l'opzione **Manutenzione indice archiviato** richiede l'integrazione con CLR, questa funzionalità può essere usata solo se si seleziona una tabella di riferimento in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in cui è abilitata l'integrazione con CLR.  
  
 **Usa indice esistente**  
 Consente di specificare che la trasformazione deve utilizzare un indice esistente per la ricerca.  
  
 **Nome di un indice esistente**  
 Consente di selezionare nell'elenco un indice di ricerca creato precedentemente.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor trasformazione Ricerca fuzzy &#40;scheda colonne&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor trasformazione Ricerca fuzzy &#40;scheda Avanzate&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  

---
title: Recuperare e comprendere i dati delle modifiche | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76635a5c1f1140bb66adf1d9ac40885c3dc43269
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771247"
---
# <a name="retrieve-and-understand-the-change-data"></a>Recupero e comprensione dei dati delle modifiche
  La prima attività nel flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che esegue un caricamento incrementale dei dati delle modifiche consiste nell'eseguire la query per il recupero dei dati delle modifiche. Questa query deve essere eseguita all'interno di un componente di origine in un'attività Flusso di dati. È quindi possibile utilizzare trasformazioni a valle e destinazioni per applicare i dati delle modifiche alla destinazione.  
  
> [!NOTE]  
>  La creazione di una query contenente una funzione valutata a livello di tabella costituisce il terzo passaggio del processo di creazione di un pacchetto per l'esecuzione di un caricamento incrementale dei dati delle modifiche. Per altre informazioni su questa query, vedere, [Creazione della funzione per il recupero dei dati delle modifiche](create-the-function-to-retrieve-the-change-data.md). Per una descrizione del processo complessivo di creazione di un pacchetto in cui viene eseguito un caricamento incrementale dei dati delle modifiche, vedere [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="adding-the-data-flow-task"></a>Aggiunta dell'attività Flusso di dati  
 Nel flusso di dati del pacchetto è necessario recuperare i dati delle modifiche, separare le righe in base al tipo di modifica apportata e quindi applicare le modifiche alla destinazione.  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>Per aggiungere un'attività Flusso di dati al pacchetto  
  
1.  Nella scheda [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Flusso di controllo **in** aggiungere un'attività Flusso di dati.  
  
2.  Connettere l'attività precedente tramite cui è stata preparata la stringa di query all'attività Flusso di dati.  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>Configurazione del componente di origine per l'esecuzione della query per le modifiche  
 Il componente di origine utilizza la stringa di query preparata e archiviata in una variabile per chiamare la funzione valutata a livello di tabella che recupera i dati modificati.  
  
> [!NOTE]  
>  Per altre informazioni sulla stringa di query preparata e archiviata in una variabile, vedere [Preparazione dell'esecuzione di una query per i dati delle modifiche](prepare-to-query-for-the-change-data.md). Per altre informazioni sulla funzione valutata a livello di tabella che recupera i dati delle modifiche, vedere [Creazione della funzione per il recupero dei dati delle modifiche](create-the-function-to-retrieve-the-change-data.md).  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>Per configurare un'origine OLE DB per recuperare i dati delle modifiche  
  
1.  Nella scheda [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Flusso di dati **in** aggiungere un'origine OLE DB.  
  
2.  Nella pagina **Gestione connessione**in **Editor origine OLE DB** selezionare le opzioni seguenti:  
  
    1.  Configurare una connessione valida al database di origine.  
  
    2.  Per **Modalità di accesso ai dati**selezionare **Comando SQL da variabile**.  
  
    3.  Per **Nome variabile**selezionare **User::SqlDataQuery**.  
  
3.  Nella pagina **Colonne**in **Editor origine OLE DB** verificare che su tutte le colonne desiderate sia eseguito il mapping a colonne di output.  
  
## <a name="next-step"></a>passaggio successivo  
 Dopo avere configurato un'origine OLE DB per recuperare i dati delle modifiche, il passaggio successivo consiste nell'iniziare a progettare il flusso di dati nel pacchetto.  
  
 **Argomento successivo:** [Elaborare inserimenti, aggiornamenti ed eliminazioni](process-inserts-updates-and-deletes.md)  
  
  

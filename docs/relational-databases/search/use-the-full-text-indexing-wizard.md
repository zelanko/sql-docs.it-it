---
title: Usare l'Indicizzazione guidata full-text | Microsoft Docs
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql13.swb.fulltextindexingwizard.welcome.f1
- sql13.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql13.swb.fulltextindexingwizard.progress.f1
- sql13.swb.fulltextindexingwizard.selectchangetracking.f1
- sql13.swb.fulltextindexingwizard.selectacatalog.f1
- sql13.swb.fulltextindexingwizard.selectatableorview.f1
- sql13.swb.fulltextindexingwizard.selectanindex.f1
- sql13.swb.fulltextindexingwizard.summary.f1
- sql13.swb.fulltextindexingwizard.selecttablecolumns.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2531d7f8034440b48a032ee1e9e74ae7fdb9df73
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85628803"
---
# <a name="use-the-full-text-indexing-wizard"></a>Utilizzare l'Indicizzazione guidata full-text
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  L'Indicizzazione guidata full-text in SQL Server Management Studio illustra la procedura di creazione di un indice full-text.  
  
## <a name="create-a--full-text-index"></a>Creare un indice full-text 

1. In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella nella quale si desidera creare un indice full-text, scegliere **Indice full-text**, quindi fare clic su **Definisci indice full-text**. Questa azione avvia la procedura guidata in una finestra separata.
   Fare clic su Next (Avanti) 
  
2. **Indice univoco.**  Selezionare un indice dall'elenco a discesa. L'indice deve essere univoco, a colonna singola, che non ammette valori Null. Selezionare l'indice di chiave univoca più piccolo possibile per la chiave univoca full-text. Per prestazioni ottimali, utilizzare un indice cluster.  
  
3.  **Colonne disponibili.** Selezionare la casella accanto a tutti i nomi delle colonne da includere.  casella di controllo accanto al nome della colonna. Le colonne non idonee sono visualizzate in grigio e le caselle di controllo sono disabilitate.  
  
4. **Lingua per il word breaker.** Consente di selezionare una lingua nell'elenco a discesa. La selezione verrà usata per identificare i word breaker corretti per l'indice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa i word breaker per individuare i delimitatori delle parole nei dati con indicizzazione full-text.  
  
5.  **Colonna tipo.** Consente di selezionare il nome della colonna che contiene il tipo di documento della colonna sottoposta all'indicizzazione full-text.  

> **NOTA:** l'opzione  **Colonna tipo** è abilitata solo se la colonna specificata nella colonna **Colonne disponibili** è di tipo **varbinary(max)** o **image**.  
  
6. **Semantica statistica.** Consente di selezionare se abilitare l'indicizzazione semantica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
>**NOTE** 
>
>Se il linguaggio selezionato non è associato a un modello di linguaggio semantico, la casella di controllo **Semantica statistica** non è abilitata. Se si seleziona **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella casella combinata a discesa saranno limitate a quelle per cui è disponibile un modello di lingua semantico.  
>
> L'opzione Ricerca semantica **non è disponibile per il database SQL di Azure.** L'opzione Semantica statistica non viene visualizzata quando si esegue questa procedura guidata in un database SQL di Azure.
  
7. Selezionare le opzioni di rilevamento delle modifiche.  
  
     **Automatico**  
     Selezionare questo pulsante di opzione per aggiornare automaticamente l'indice full-text a mano a mano che le modifiche vengono apportate ai dati sottostanti.  
  
     **Manualmente**  
     Selezionare questo pulsante di opzione se non si desidera che l'indice full-text venga aggiornato automaticamente a mano a mano che le modifiche vengono apportate ai dati sottostanti. Le modifiche apportate ai dati sottostanti vengono mantenute. Tuttavia, per applicare le modifiche all'indice full-text è necessario avviare o pianificare il processo in modo manuale.  
  
     **Non rilevare modifiche**  
     Selezionare questo pulsante di opzione se non si desidera che l'indice full-text venga aggiornato con le modifiche apportate ai dati sottostanti.  
  
8.  Avvia popolamento completo quando viene creato l'indice (disponibile solo se non si tiene traccia delle modifiche).
  
     Selezionare questo pulsante di opzione per avviare il popolamento completo dopo il completamento della procedura guidata. Ciò comporterà la creazione della struttura dell'indice full-text nel catalogo e il suo popolamento con dati con indicizzazione full-text.  
     
     Fare clic su Next (Avanti)
  
## <a name="catalog-index-filegroup-and-stoplist"></a>Catalogo, filegroup indice ed elenco di parole non significative   
  
9.  **Seleziona catalogo full-text**  

     **Selezione catalogo:** consente di selezionare un catalogo full-text dall'elenco. Il catalogo predefinito del database corrisponderà all'elemento selezionato per impostazione predefinita nell'elenco. Se non è disponibile alcun catalogo, l'elenco sarà disabilitato e la casella di controllo **Crea un nuovo catalogo** sarà selezionata e disabilitata.  
  
  o
  
 10. **Crea un nuovo catalogo**
 - Selezionare un catalogo full-text.  
  
    a. **Nome**  
     Immettere un nome per il nuovo catalogo full-text.  
  
     b. **Imposta come catalogo predefinito**  
     Selezionare questa opzione per impostare il catalogo come predefinito per il database.  
  
     c. **Distinzione caratteri accentati/non accentati**  
     Consente di specificare se nel catalogo viene fatta distinzione tra caratteri accentati e non accentati. Se il database supporta la distinzione tra caratteri accentati e non accentati, l'opzione **Attiva** sarà selezionata per impostazione predefinita.  
  
     d. **Selezione filegroup indice**  
     Consente di specificare il filegroup in cui creare l'indice full-text.  
  
     e. Selezionare un valore:  
      |valore|Descrizione|  
      |-----------|-----------------|
      |**<default>**| Se la tabella o la vista non è partizionata, selezionare questa opzione per utilizzare lo stesso filegroup della tabella o della vista sottostante. Se la tabella o la vista è partizionata, viene usato il filegroup primario|
      |**PRIMARY**|Selezionare questa opzione per utilizzare il filegroup primario per il nuovo indice full-text.|
      *user-specified default filegroup*|Se è presente un elenco di parole non significative predefinito, definito dall'utente, selezionarne il nome nell'elenco per usare questo filegroup per il nuovo indice full-text.|   
  
     
 11. **Selezione elenco di parole non significative full-text**  
     Consente di specificare un elenco di parole non significative da utilizzare per l'indice full-text o di disabilitare l'utilizzo dell'elenco di parole non significative.  
  
     Le parole non significative vengono gestite nei database utilizzando oggetti denominati elenchi di parole non significative. Un *elenco di parole non significative* è un elenco che, quando associato a un indice full-text, viene applicato alle query full-text su tale indice. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
     Selezionare uno dei valori seguenti:  
  
   |valore|Descrizione|  
    |-----------|-----------------|  
    |**<system>**|Selezionare questa opzione per utilizzare l'elenco di parole non significative di sistema nel nuovo indice full-text. Si tratta dell'impostazione predefinita.|  
    |**<off>**|Selezionare questa opzione per disabilitare gli elenchi di parole non significative per il nuovo indice full-text.|  
    |*user-defined-stoplist-name*|Nell'elenco viene visualizzato il nome di ogni elenco di parole non significative definito dall'utente, se presente, creato nel database. Selezionare qualsiasi elenco di parole non significative definito dall'utente da utilizzare per il nuovo indice full-text.|  
  
  Fare clic su Next (Avanti)
  
11. Facoltativamente e solo in SQL Server, definire la pianificazione di popolamento. Le operazioni di indicizzazione avranno inizio immediatamente, a meno che non siano state pianificate per un'esecuzione futura. Le pianificazioni verranno create immediatamente, anche se l'esecuzione avverrà solo all'ora pianificata.  
  
     **Nuova pianificazione tabella**  
     Consente di definire una pianificazione di popolamento per una tabella.  
  
     **Nuova pianificazione catalogo**  
     Consente di definire una pianificazione di popolamento per un catalogo full-text.  
  
     **Modifica**  
     Consente di modificare una pianificazione.  
  
     **Elimina**  
     Consente di eliminare una pianificazione.  
  
5.  Visualizzare o controllare lo stato dell'Indicizzazione guidata full-text.  
  
     **Stop**  
     Consente di interrompere l'operazione corrente e impedire l'esecuzione di operazioni full-text successive da parte della procedura guidata nel corso della sessione.  
  
     **Report**  
     Al termine dell'esecuzione di tutte le operazioni, fare clic su questo pulsante per accedere a un report delle operazioni eseguite. È possibile visualizzare il report, stamparlo su file, copiarlo negli Appunti o inviarlo tramite posta elettronica.  
  
  

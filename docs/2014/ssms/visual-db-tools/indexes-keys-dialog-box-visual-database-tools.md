---
title: Gli indici e le chiavi di finestra di dialogo (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65539
- vdt.ppg.indexeskeys
ms.assetid: 9e4060ba-80c3-468f-bccb-e12e99f672c2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0244530672e9db4a43f3dbe80f0c67cc86f8a67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63015418"
---
# <a name="indexes-and-keys-dialog-box-visual-database-tools"></a>Finestra di dialogo Indici e chiavi (Visual Database Tools)
  Questa finestra di dialogo consente di creare o modificare indici, chiavi primarie e chiavi univoche. Per accedere a questa finestra di dialogo, aprire la definizione della tabella con l'indice o la chiave, fare clic con il pulsante destro del mouse sulla griglia della definizione della tabella e quindi scegliere **Indici/chiavi**.  
  
> [!NOTE]  
>  Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="options"></a>Opzioni  
 **Indice o chiave primari/univoci selezionati**  
 Visualizza un elenco delle chiavi primarie o univoche e degli indici. Selezionare una chiave o un indice per visualizzarne le proprietà nella griglia a destra. Se l'elenco è vuoto, per la tabella non sono stati definiti indici.  
  
 **Aggiungi**  
 Crea una chiave primaria o univoca oppure un indice.  
  
 **Elimina**  
 Elimina la chiave o l'indice selezionato nell'elenco **Selected Primary/Unique Key or Index** (Indice o chiave primaria/univoca selezionata).  
  
 **Categoria Generale**  
 Se viene espansa, visualizza le proprietà **Colonne**, **Univoco**e **Tipo**.  
  
 **Colonne**  
 Elenca i criteri di ordinamento selezionati per le colonne nella chiave o nell'indice e consente di accedere a una finestra di dialogo in cui è possibile definire i criteri di ordinamento. Per visualizzare la finestra di dialogo, fare clic su **Colonne** e quindi sui puntini di sospensione (...) a destra del campo della proprietà.  
  
 **Univoco**  
 Indica se i dati immessi nell'indice o nella chiave devono essere univoci. Questa proprietà non è disponibile per gli indici XML.  
  
 **Tipo**  
 Specifica se l'elemento selezionato nell'elenco **Selected Primary/Unique Key or Index** (Indice o chiave primaria/univoca selezionata) è una chiave univoca, una chiave primaria o un indice. Per le chiavi primarie, questo campo è di sola lettura.  
  
 **Categoria Identità**  
 Se viene espansa, visualizza i campi delle proprietà **Nome** e **Descrizione**.  
  
 **Name**  
 Visualizza il nome della chiave o dell'indice. Quando si crea un nuovo indice, gli viene assegnato un nome predefinito sulla base della tabella presente nella finestra attiva di Progettazione tabelle. Il nome può essere modificato in qualunque momento.  
  
 **Descrizione**  
 Consente di immettere una descrizione della chiave o dell'indice. Per inserire una descrizione più dettagliata, fare clic su **Descrizione** e sui puntini di sospensione (**...**) a destra del campo della proprietà. Viene così visualizzata un'area più grande in cui scrivere il testo.  
  
 **Categoria Progettazione tabelle**  
 Se viene espansa, visualizza le informazioni relative a **Crea come CLUSTERED**.  
  
 **Crea come CLUSTERED**  
 Trasforma la chiave o l'indice in chiave o indice cluster. In una tabella è consentito un solo indice cluster. I dati nella tabella vengono archiviati secondo l'ordine dell'indice cluster. Per altre informazioni, vedere [Creare indici cluster](../../relational-databases/indexes/indexes.md) e [Creare indici non cluster](../../relational-databases/indexes/create-nonclustered-indexes.md).  
  
 **Specifica spazio dei dati**  
 Se viene espansa, visualizza le informazioni relative a **(Tipo spazio dei dati)**, **Nome gruppo di file o schema di partizione**ed **Elenco colonne di partizione**.  
  
 **(Tipo spazio dei dati)**  
 Indica se l'indice o la chiave appartiene a un gruppo di file o a uno schema di partizione.  
  
 **Nome gruppo di file o schema di partizione**  
 Visualizza il nome del gruppo di file o dello schema di partizione in cui l'indice o la chiave è archiviata.  
  
 **Elenco colonne di partizione**  
 Visualizza un elenco separato da virgole con le colonne che partecipano alla funzione delle colonne di partizione. Questa opzione non è disponibile se nel campo **(Tipo spazio dei dati)** è selezionato Gruppo di file.  
  
 **Specifica riempimento**  
 Se viene espansa, visualizza le informazioni relative a **Riempimento** e **Riempi indice**.  
  
 **Riempimento**  
 Specifica quale percentuale delle pagine a livello foglia dell'indice può essere riempita dal sistema. Quando la pagina è piena, dovrà essere divisa se verranno aggiunti nuovi dati, con un conseguente rallentamento delle prestazioni.  
  
-   Un valore pari a 100 indica che le pagine saranno piene. Tale impostazione richiede la quantità più ridotta di spazio di archiviazione. È consigliabile utilizzare questa impostazione solo se non verranno apportate modifiche ai dati, ad esempio per una tabella di sola lettura.  
  
-   Se si specifica un valore inferiore, nelle pagine di dati sarà presente più spazio vuoto. Questa soluzione consente di ridurre la necessità di dividere le pagine di dati a causa dell'aumento delle dimensioni degli indici, ma richiede più spazio di archiviazione.  
  
 **Riempi indice**  
 Indica se per le pagine intermedie dell'indice viene usata la stessa percentuale di spazio vuoto (riempimento) specificata in **Riempimento** in caso di aumento delle dimensioni.  
  
 **Ignora chiavi duplicate**  
 Specifica l'effetto prodotto dall'inserimento di una riga con valore di chiave uguale a un valore di chiave esistente durante un'operazione di inserimento bulk. Se si sceglie:  
  
-   **Sì** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un avviso, ignora la riga in ingresso errata e tenta di inserire le righe rimanenti.  
  
-   **No** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un messaggio di errore ed esegue il rollback dell'intera operazione di inserimento bulk.  
  
 **Colonne incluse**  
 Visualizza un elenco separato da virgole con i nomi di tutte le colonne che costituiscono la chiave di indice. Le colonne di sottochiave possono essere specificate solo per gli indici non cluster. La proprietà è nascosta per gli indici XML.  
  
 **Disabilitato**  
 Indica se l'indice è disabilitato. Questa proprietà è di sola lettura. Viene impostata su **Sì** solo se l'indice è stato disabilitato all'esterno di Visual Database Tools.  
  
 **Chiave di ricerca completa**  
 Specifica se l'indice è una chiave full-text. Per ulteriori informazioni sulle chiavi full-text, vedere la documentazione online di SQL Server. La proprietà è nascosta per gli indici XML.  
  
 **Blocchi pagine consentiti**  
 Specifica se per l'indice è consentito il blocco a livello delle pagine. L'attivazione o la disattivazione di tale blocco incide sulle prestazioni del database. L'impostazione consigliata è **Sì**.  
  
 **Ricalcola statistiche**  
 Specifica se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] sottostante ricalcola le nuove statistiche quando viene creato l'indice. Il ricalcolo delle statistiche rallenta la compilazione degli indici, ma in genere può migliorare in modo significativo le prestazioni delle query.  
  
 **Blocchi righe consentiti**  
 Specifica se per l'indice è consentito il blocco a livello delle righe. L'attivazione o la disattivazione di tale blocco incide sulle prestazioni del database. L'impostazione consigliata è **Sì**.  
  
## <a name="see-also"></a>Vedere anche  
 [I vincoli UNIQUE e Check](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Vincoli di chiavi primarie ed esterne](../../relational-databases/tables/primary-and-foreign-key-constraints.md)  
  
  

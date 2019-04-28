---
title: Gestione connessione file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4466ebd24647520c7cbba2bf0baa93a0f60a72bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833816"
---
# <a name="flat-file-connection-manager"></a>Flat File Connection Manager
  Una gestione connessione file flat consente a un pacchetto di accedere ai dati contenuti in un file flat. L'origine e la destinazione del file flat possono ad esempio utilizzare gestioni connessioni file flat per estrarre e caricare dati.  
  
 La gestione connessione file flat è in grado di accedere a un solo file. Per fare riferimento a più file, al posto di una gestione connessione file flat utilizzare una gestione connessione per più file flat. Per ulteriori informazioni, vedere [Multiple Flat Files Connection Manager](multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Lunghezza di colonna  
 Per impostazione predefinita la gestione connessione file flat imposta la lunghezza delle colonne di tipo stringa su 50 caratteri. Nella finestra di dialogo **Editor gestione connessione file flat** è possibile valutare dati di esempio e modificare automaticamente la lunghezza di tali colonne in modo da evitare il troncamento dei dati o il superamento della larghezza massima delle colonne. La lunghezza di una colonna di tipo stringa rimane inoltre invariata per tutto il flusso di dati, a meno che non venga modificata successivamente in un'origine file flat o in una trasformazione. Se su tali colonne di tipo stringa viene eseguito il mapping a colonne di destinazione di larghezza inferiore, verrà visualizzato un avviso nell'interfaccia utente e in fase di esecuzione potrebbero verificarsi errori dovuti al troncamento dei dati. Per evitare errori o troncamenti, è possibile ridimensionare le colonne in modo che siano compatibili con le colonne di destinazione nella gestione connessione file flat, nell'origine file flat o in una trasformazione. Per modificare la lunghezza delle colonne di output, è necessario impostare il `Length` proprietà della colonna di output nel **proprietà Input e Output** scheda il **Editor avanzato** nella finestra di dialogo.  
  
 Se, dopo avere aggiunto e configurato l'origine file flat che utilizza la gestione connessione, si modifica la lunghezza delle colonne nella gestione connessione file flat, non sarà necessario ridimensionare manualmente le colonne di output nell'origine file flat. Nella finestra di dialogo **Origine file flat** è disponibile un'opzione che consente di sincronizzare i metadati delle colonne per l'origine file flat.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Configurazione della gestione connessione file flat  
 Quando si aggiunge una gestione connessione file flat a un pacchetto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione file flat, imposta le proprietà della connessione file flat e aggiunge la gestione connessione file flat alla raccolta `Connections` del pacchetto.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `FLATFILE`.  
  
 Per impostazione predefinita, tramite la gestione connessione file flat viene sempre verificata la presenza di un delimitatore di riga in dati senza virgolette e viene iniziata una nuova riga quando viene individuato un relativo delimitatore. In questo modo, con la gestione connessione è possibile analizzare correttamente i file con righe prive di campi colonna.  
  
 In alcuni casi, la disabilitazione di questa funzionalità potrebbe migliorare le prestazioni del pacchetto. È possibile disabilitare questa funzionalità impostando la proprietà della gestione connessione File Flat **AlwaysCheckForRowDelimiters**, a `False`.  
  
 Per configurare la gestione connessione file flat, procedere nel modo seguente:  
  
-   Specificare il file, le impostazioni locali e la tabella codici da utilizzare. Le impostazioni locali vengono utilizzate per interpretare i dati con formato dipendente dalla lingua, come le date, mentre la tabella codici viene utilizzata per convertire i dati stringa in formato Unicode.  
  
-   Specificare il formato dei file. È possibile utilizzare un formato delimitato, a larghezza fissa o non allineato a destra.  
  
-   Specificare i delimitatori della riga di intestazione, delle righe di dati e delle colonne. I delimitatori delle colonne possono essere impostati a livello di file e sovrascritti a livello di colonna.  
  
-   Indicare se la prima riga del file contiene i nomi delle colonne.  
  
-   Specificare un qualificatore di testo. Ogni colonna può essere configurata in modo da riconoscere un qualificatore di testo.  
  
     Ora è supportato l'utilizzo di un qualificatore di testo per incorporare quest'ultimo in una stringa qualificata. L'istanza doppia di un qualificatore di testo viene interpretata come una singola istanza letterale di questa stringa. Ad esempio, se il qualificatore di testo è una virgoletta singola e i dati di input sono 'abc', 'def', 'g'hi', i dati di output saranno abc, def, g'hi.  
  
-   Impostare proprietà quali il nome, il tipo di dati e la larghezza massima delle singole colonne.  
  
 È possibile impostare la proprietà ConnectionString per la gestione connessione file flat specificando un'espressione nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per evitare errori di convalida, effettuare le operazioni seguenti.  
  
-   Quando si usa un'espressione per specificare il file, aggiungere il percorso del file nella casella **Nome file** nell' **Editor gestione connessione file flat**.  
  
-   Impostare la proprietà **DelayValidation** della gestione connessione file flat su **True**.  
  
 È possibile utilizzare un'espressione per creare un nome di file in fase di esecuzione utilizzando la gestione connessione file flat con la destinazione file flat.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor gestione connessione file flat &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  

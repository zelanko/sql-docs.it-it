---
title: Origine OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsource.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a89632ad5502cee9599d1eea6e1cd0a0bebe7d1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384931"
---
# <a name="ole-db-source"></a>Origine OLE DB
  L'origine OLE DB consente di estrarre dati da un'ampia gamma di database relazionali conformi con OLE DB, tramite una tabella o vista di database oppure un comando SQL. L'origine OLE DB consente ad esempio di estrarre dati dalle tabelle nei database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Sono disponibili quattro diverse modalità di accesso ai dati per l'estrazione dei dati:  
  
-   Vista o tabella.  
  
-   Vista o tabella specificata in una variabile.  
  
-   Risultato di un'istruzione SQL. La query può essere con parametri.  
  
-   Risultato di un'istruzione SQL archiviata in una variabile.  
  
> [!NOTE]  
>  Quando si utilizza un'istruzione SQL per richiamare una stored procedure che restituisce risultati da una tabella temporanea, utilizzare l'opzione WITH RESULT SETS per definire metadati per il set di risultati.  
  
 Se si utilizza una query con parametri, sarà possibile eseguire il mapping delle variabili ai parametri per specificare i valori dei singoli parametri nelle istruzioni SQL.  
  
 Per connettersi a un'origine dei dati questa origine utilizza una gestione connessione OLE DB, che specifica il provider OLE DB da utilizzare. Per altre informazioni, vedere [Gestione connessione OLE DB](../connection-manager/ole-db-connection-manager.md).  
  
 In un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene inoltre fornito l'oggetto di origine dati da cui è possibile creare una gestione connessione OLE DB, rendendo disponibili origini dati e relative viste all'origine OLE DB.  
  
 A seconda del provider OLE DB, l'origine OLE DB può presentare le limitazioni seguenti:  
  
-   Il provider OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Oracle non supporta i tipi di dati Oracle BLOB, CLOB, NCLOB, BFILE e UROWID e l'origine OLE DB non è in grado di estrarre dati da tabelle che contengono colonne con tali tipi di dati.  
  
-   I provider IBM OLE DB per DB2 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per DB2 non supportano l'utilizzo di comandi SQL che chiamano stored procedure. Quando viene utilizzato un comando di questo tipo l'origine OLE DB non è in grado di creare i metadati delle colonne e, di conseguenza, i dati delle colonne non sono disponibili per i componenti del flusso di dati che seguono l'origine OLE DB nel flusso di dati. Questo impedisce di completare l'esecuzione del flusso di dati.  
  
 L'origine OLE DB include un output regolare e un output degli errori.  
  
## <a name="using-parameterized-sql-statements"></a>Utilizzo di istruzioni SQL con parametri  
 Per l'estrazione dei dati l'origine OLE DB può utilizzare un'istruzione SQL, che può essere costituita da un'istruzione SELECT o EXEC.  
  
 L'origine OLE DB utilizza una gestione connessione OLE DB per connettersi all'origine dei dati da cui estrae i dati. A seconda del provider utilizzato dalla gestione connessione OLE DB e del sistema di gestione di database relazionali (RDBMS) a cui si connette la gestione connessione, verranno applicate regole diverse per la denominazione e l'elencazione dei parametri. Se i nomi dei parametri vengono restituiti dal sistema RDBMS, sarà possibile utilizzare nomi di parametro per eseguire il mapping dei parametri di un elenco di parametri a quelli inclusi in un'istruzione SQL. In caso contrario, sui parametri viene eseguito il mapping a quelli dell'istruzione SQL in base alla posizione ordinale nell'elenco dei parametri. I tipi di nomi di parametro supportati variano a seconda del provider. Alcuni provider richiedono ad esempio che vengano utilizzati i nomi delle variabili o delle colonne, mentre altri richiedono l'utilizzo di nomi simbolici, quali 0 o Param0. Per informazioni sui nomi di parametro da utilizzare nelle istruzioni SQL, vedere la documentazione specifica del provider.  
  
 Quando si utilizza una gestione connessione OLE DB, non è possibile utilizzare sottoquery con parametri, perché l'origine OLE DB non può derivare le informazioni sui parametri tramite il provider OLE DB. Tuttavia, è possibile usare un'espressione per concatenare i valori dei parametri nella stringa di query e impostare la proprietà SqlCommand dell'origine. In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , è possibile configurare un'origine OLE DB usando la finestra di dialogo **Editor origine OLE DB** ed eseguire il mapping dei parametri alle variabili nella finestra di dialogo **Imposta parametri query** .  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>Indicazione dei parametri tramite la posizione ordinale  
 Se non viene restituito alcun nome di parametro, gli indicatori di parametro a cui viene eseguito il mapping dei parametri in fase di esecuzione sono determinati dall'ordine in cui compaiono i parametri nell'elenco **Parametri** della finestra di dialogo **Imposta parametri query** . Viene eseguito il mapping del primo parametro dell'elenco al primo ? nell'istruzione SQL, il secondo al secondo? e così via.  
  
 L'istruzione SQL seguente seleziona righe dalla tabella **Product[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] del database** . Sul primo parametro nell'elenco **Mapping** viene eseguito il mapping al primo parametro nella colonna**Color**, mentre sul secondo parametro viene eseguito il mapping alla colonna **Size**.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 I nomi di parametro sono ininfluenti. Se ad esempio un determinato parametro ha lo stesso nome della colonna a cui si riferisce, ma non compare nella posizione ordinale corretta nell'elenco **Parameters** , per il mapping dei parametri eseguito in fase di esecuzione verrà comunque usata la posizione ordinale del parametro e non il suo nome.  
  
 Per il comando EXEC, come nomi di parametro è in genere necessario utilizzare i nomi delle variabili che specificano i valori dei parametri nella procedura.  
  
### <a name="specifying-parameters-by-using-names"></a>Indicazione dei parametri tramite i nomi  
 Se il sistema RDBMS restituisce i nomi effettivi dei parametri, sui parametri utilizzati dalle istruzioni SELECT ed EXEC verrà eseguito il mapping in base al nome. I nomi dei parametri devono essere quelli previsti dalla stored procedure eseguita dall'istruzione SELECT o EXEC.  
  
 L'istruzione SQL seguente esegue la stored procedure **uspGetWhereUsedProductID** disponibile nel database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] .  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 La stored procedure prevede che i valori dei parametri vengano specificati dalle variabili `@StartProductID` e `@CheckDate`. L'ordine in cui i parametri sono visualizzati nell'elenco **Mapping** è irrilevante. L'unico requisito consiste nel fatto che i nomi dei parametri devono coincidere con quelli delle variabili nella stored procedure, incluso il simbolo \@.  
  
### <a name="mapping-parameters-to-variables"></a>Mapping di parametri a variabili  
 Il mapping dei parametri alle variabili che ne specificano i valori avviene in fase di esecuzione. Sebbene in genere vengano usate variabili definite dall'utente, è possibile usare anche le variabili di sistema disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se si utilizzano variabili definite dall'utente, verificare che il tipo di dati impostato sia compatibile con quello della colonna a cui fa riferimento il parametro di cui viene eseguito il mapping. Per altre informazioni, vedere [Integration Services &#40;SSIS&#41; Variables](../integration-services-ssis-variables.md).  
  
## <a name="troubleshooting-the-ole-db-source"></a>Risoluzione dei problemi relativi all'origine OLE DB  
 È possibile registrare le chiamate eseguite dall'origine OLE DB a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al caricamento di dati da origini esterne da parte dell'origine OLE DB. Per registrare le chiamate eseguite dall'origine OLE DB a provider di dati esterni, attivare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-source"></a>Configurazione dell'origine OLE DB  
 È possibile impostare le proprietà a livello di programmazione o tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor origine OLE DB**, fare clic su uno degli argomenti seguenti:  
  
-   [Editor origine OLE DB &#40;pagina Gestione connessione&#41;](../ole-db-source-editor-connection-manager-page.md)  
  
-   [Editor origine OLE DB &#40;pagina Colonne&#41;](../ole-db-source-editor-columns-page.md)  
  
-   [Editor origine OLE DB &#40;pagina Output degli errori&#41;](../ole-db-source-editor-error-output-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate OLE DB](ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Estrazione dei dati tramite l'origine OLE DB](ole-db-source.md)  
  
-   [Mapping dei parametri di query a variabili in un componente flusso di dati](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo di Wiki sui [connettori SSIS con Oracle](https://go.microsoft.com/fwlink/?LinkId=220670)sul sito Web social.technet.microsoft.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione OLE DB](ole-db-destination.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md)   
 [Flusso di dati](data-flow.md)  
  
  

---
title: Inserimento di dati in parametri con valori di tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
ms.assetid: 9c1a3234-4675-40d3-b473-8df06208f880
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eb8e32b0008cba846679e7704a3a9ab9cef6e93d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103445"
---
# <a name="inserting-data-into-table-valued-parameters"></a>Inserimento di dati in parametri con valori di tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provider Native Client OLE DB supporta due modelli per il consumer può specificare i dati per righe di parametri con valori di tabella: un modello push e un modello pull. Per un esempio in cui viene illustrato il modello pull, vedere la pagina relativa agli [esempi di programmazione dati di SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
> [!NOTE]  
>  Una colonna di parametri con valori di tabella deve includere valori non predefiniti in tutte le righe o valori predefiniti in tutte le righe. Non è possibile che vi siano valori predefiniti in alcune righe e non in altre. Nelle associazioni di parametri con valori di tabella, pertanto, gli unici valori di stato consentiti per i dati di colonna dei set di righe di parametri con valori di tabella sono DBSTATUS_S_ISNULL e DBSTATUS_S_OK. DBSTATUS_S_DEFAULT comporteranno un errore e il valore di stato associato verrà impostato su DBSTATUS_E_BADSTATUS.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>Modello push (carica in memoria tutti i dati dei parametri con valori di tabella)  
 L'uso del modello push è simile all'uso di set di parametri, ovvero del parametro DBPARAMS in ICommand::Execute. Il modello push viene usato solo se gli oggetti set di righe di parametri con valori di tabella vengono usati senza un'implementazione personalizzata delle interfacce IRowset. Il modello push è consigliabile quando il numero di righe nel set di righe di parametri con valori di tabella è ridotto e non si prevede un utilizzo elevato della memoria nell'applicazione. Questo modello è più semplice del modello pull, in quanto non richiede altre funzionalità dall'applicazione consumer rispetto a quelle comuni normalmente utilizzate nelle applicazioni OLE DB tipiche.  
  
 In genere il consumer fornisce al provider tutti i dati dei parametri con valori di tabella prima di eseguire un comando. Per fornire i dati, il consumer popola un oggetto set di righe di parametri con valori di tabella per ogni parametro con valori di tabella. L'oggetto set di righe di parametri con valori di tabella espone operazioni Insert, Set e Delete per il set di righe che verranno utilizzate dal consumer per modificare i dati dei parametri con valori di tabella. Il provider recupererà i dati da questo oggetto set di righe di parametri con valori di tabella in fase di esecuzione.  
  
 Quando al consumer viene fornito un oggetto set di righe di parametri con valori di tabella, il consumer può elaborarlo come oggetto set di righe. Il consumer può ottenere le informazioni sul tipo di ogni colonna (tipo, lunghezza massima, precisione e scala) tramite il metodo di interfaccia IColumnsInfo:: GetColumnInfo o IColumnsRowset::. Il consumer crea quindi una funzione di accesso per specificare le associazioni per i dati. Il passaggio successivo consiste nell'inserire righe di dati nel set di righe di parametri con valori di tabella. Questa operazione può essere eseguita usando IRowsetChange:: InsertRow. IRowsetChange:: SetData o IRowsetChange:: è anche utilizzabile per l'oggetto set di righe di parametri con valori di tabella se è necessario modificare i dati. Gli oggetti set di righe di parametri con valori di tabella sono soggetti a conteggio dei riferimenti, analogamente agli oggetti di flusso.  
  
 Se viene usato IColumnsRowset::, esisterà le successive chiamate a IRowset:: GetNextRows IRowset:: GetData e:: ReleaseRows metodi sull'oggetto set di righe della colonna risultante.  
  
 Dopo il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Provider OLE DB Native inizia l'esecuzione del comando, i valori dei parametri con valori di tabella verranno recuperati da questo oggetto di set di righe di parametri con valori di tabella e inviati al server.  
  
 Il modello push richiede attività minime da parte del consumer, ma utilizza una maggiore quantità di memoria rispetto al modello pull, in quanto tutti i dati dei parametri con valori di tabella devono essere presenti in memoria in fase di esecuzione.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>Modello pull (recupero di dati dei parametri con valori di tabella su richiesta dal consumer)  
 Il modello pull è utile per due scenari:  
  
-   Per eseguire il flusso di righe.  
  
-   Se si utilizza un set di righe di un altro provider come valore di parametro con valori di tabella.  
  
 Nel modello pull il consumer fornisce dati su richiesta al provider. Utilizzare questo approccio se nell'applicazione vengono eseguiti molti inserimenti di dati, e i dati del set di righe di parametri con valori di tabella in memoria comporterebbero un eccessivo accesso alla memoria. Se si utilizzano più provider OLE DB, il modello pull del consumer consente al consumer di fornire qualsiasi oggetto set di righe come valore di parametro con valori di tabella.  
  
 Per utilizzare il modello pull, i consumer devono specificare l'implementazione personalizzata di un oggetto set di righe. Quando si usa il modello pull con set di righe di parametri con valori di tabella (CLSID_ROWSET_TVP), il consumer viene richiesto di aggregare l'oggetto set di righe di parametri con valori di tabella esposte dal provider tramite il ITableDefinitionWithConstraints:: Metodo CreateTableWithConstraints o IOpenRowset:: OPENROWSET. Il comportamento previsto per l'oggetto consumer consiste esclusivamente nel sostituire l'implementazione dell'interfaccia IRowset. È necessario sostituire le funzioni seguenti:  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 Il provider OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client leggerà una o più righe per volta dall'oggetto set di righe del consumer per supportare l'esecuzione del flusso in parametri con valori di tabella. L'utente, ad esempio, potrebbe disporre dei dati dei set di righe di parametri con valori di tabella su disco (non in memoria) e implementare la funzionalità di lettura dei dati dal disco se richiesto dal provider OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Il consumer comunicherà il formato dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Provider OLE DB Native usando IAccessor:: CreateAccessor per l'oggetto set di righe di parametri con valori di tabella. Durante la lettura dei dati dal buffer del consumer, il provider verifica che tutte le colonne accessibili in scrittura e non predefinite siano disponibili tramite almeno un handle della funzione di accesso e utilizza gli handle corrispondenti per leggere i dati delle colonne. Per evitare ambiguità, deve essere presente una corrispondenza uno-a-uno tra una colonna del set di righe di parametri con valori di tabella e un'associazione. Associazioni duplicate alla stessa colonna comporteranno un errore. Inoltre, ogni funzione di accesso deve disporre di *iOrdinal* membro DBBindings in sequenza. Verranno eseguite tante chiamate a IRowset::GetData quanto è il numero di funzioni di accesso per riga e l'ordine delle chiamate sarà basato sull'ordine del valore *iOrdinal*, dai valori inferiori a quelli superiori.  
  
 Il comportamento previsto del provider consiste nell'implementare la maggior parte delle interfacce esposte dall'oggetto set di righe di parametri con valori di tabella. Il consumer implementerà un oggetto set di righe con interfacce minime (IRowset). A causa dell'aggregazione nascosta, le interfacce obbligatorie rimanenti dell'oggetto set di righe verranno implementate dall'oggetto set di righe di parametri con valori di tabella.  
  
 Per qualsiasi altro oggetto set di righe, ad esempio gli oggetti set di righe ottenuti per qualunque provider OLE DB, il set di righe fornito dal consumer deve implementare tutte le interfacce dell'oggetto set di righe obbligatorie in base a quanto indicato dalla specifica OLE DB.  
  
 In fase di esecuzione, il provider OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client richiamerà l'oggetto set di righe per recuperare righe e leggere i dati delle colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

---
title: Requisiti dei tipi definiti dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fc3da1474546f0719af20c52f44248baa8ce5da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028265"
---
# <a name="creating-user-defined-types---requirements"></a>Creazione di tipi definiti dall'utente - Requisiti
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si crea un tipo definito dall'utente (UDT) da installare in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario prendere alcune importanti decisioni di progettazione. Benché nella maggior parte dei casi sia consigliabile creare il tipo definito dall'utente come struttura, la creazione come classe rappresenta un'altra opzione valida. Perché il tipo venga registrato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la definizione del tipo definito dall'utente deve essere conforme alle specifiche relative alla creazione di tali tipi.  
  
## <a name="requirements-for-implementing-udts"></a>Requisiti per l'implementazione di tipi definiti dall'utente  
 Ai fini dell'esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo definito dall'utente deve implementare i requisiti seguenti nella relativa definizione:  
  
 Il tipo definito dall'utente deve specificare **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**. L'uso di **System. SerializableAttribute** è facoltativo, ma consigliato.  
  
-   Il tipo definito dall'utente deve implementare l'interfaccia **System. Data. SqlTypes. INullable** nella classe o nella struttura creando un metodo **null** pubblico [!INCLUDE[msCoName](../../includes/msconame-md.md)] **statico** (**Shared** in Visual Basic). 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta il valore null per impostazione predefinita. Questa condizione è necessaria affinché il codice in esecuzione nel tipo definito dall'utente sia in grado di riconoscere un valore Null.  
  
-   Il tipo definito dall'utente deve contenere un metodo di **analisi** **statico** pubblico (o **condiviso**) che supporta l'analisi da e un metodo **ToString** pubblico per la conversione in una rappresentazione di stringa dell'oggetto.  
  
-   Un tipo definito dall'utente con un formato di serializzazione definito dall'utente deve implementare l'interfaccia **System. Data. IBinarySerialize** e fornire un metodo **Read** e **Write** .  
  
-   Il tipo definito dall'utente deve implementare **System. XML. Serialization. IXmlSerializable**oppure tutti i campi e le proprietà pubblici devono essere di tipi XML serializzabili o decorati con l'attributo **XmlIgnore** se è necessario eseguire l'override della serializzazione standard.  
  
-   È necessario che sia presente solo una serializzazione di un oggetto del tipo definito dall'utente. La convalida ha esito negativo se le routine di serializzazione e deserializzazione riconoscono più di una rappresentazione di un oggetto specifico.  
  
-   **SqlUserDefinedTypeAttribute. IsByteOrdered** deve essere **true** per confrontare i dati in base all'ordine dei byte. Se l'interfaccia IComparable non è implementata e **SqlUserDefinedTypeAttribute. IsByteOrdered** è **false**, i confronti dell'ordine dei byte avranno esito negativo.  
  
-   Un tipo definito dall'utente specificato in una classe deve disporre di un costruttore pubblico che non accetta argomenti. È eventualmente possibile creare costruttori di classe di overload aggiuntivi.  
  
-   Il tipo definito dall'utente deve esporre elementi dati come campi pubblici o routine di proprietà.  
  
-   I nomi pubblici non possono contenere più di 128 caratteri e devono essere conformi alle regole di denominazione per gli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificatori come definito negli [identificatori del database](../../relational-databases/databases/database-identifiers.md).  
  
-   **sql_variant** colonne non possono contenere istanze di un tipo definito dall'utente.  
  
-   I membri ereditati non sono accessibili da [!INCLUDE[tsql](../../includes/tsql-md.md)] perché il sistema dei tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non riconosce la gerarchia di ereditarietà tra tipi definiti dall'utente. È tuttavia possibile utilizzare l'ereditarietà quando si strutturano le classi ed è possibile chiamare tali metodi nell'implementazione di codice gestito del tipo.  
  
-   Non è possibile eseguire l'overload dei membri, ad eccezione del costruttore della classe. Se si crea un metodo di overload, non viene generato alcun errore quando si registra l'assembly o si crea il tipo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il rilevamento del metodo di overload si verifica in fase di esecuzione e non durante la creazione del tipo. Nella classe possono essere presenti metodi di overload, a condizione che non vengano mai richiamati. Quando si richiama il metodo di overload, viene generato un errore.  
  
-   Tutti i membri **statici** (o **condivisi**) devono essere dichiarati come costanti o come di sola lettura. I membri statici non possono essere modificati.  
  
-   Se il campo **SqlUserDefinedTypeAttribute. MaxByteSize** è impostato su-1, il tipo definito dall'utente serializzato può avere dimensioni pari al limite di dimensioni LOB (Large Object) (attualmente 2 GB). Le dimensioni del tipo definito dall'utente non possono superare il valore specificato nel campo **MaxByteSized** .  
  
> [!NOTE]  
>  Sebbene non venga utilizzato dal server per l'esecuzione di confronti, è possibile implementare facoltativamente l'interfaccia **System. IComparable** , che espone un singolo metodo, **CompareTo**. Tale metodo viene utilizzato sul lato client in situazioni in cui è preferibile confrontare o ordinare in modo accurato i valori del tipo definito dall'utente.  
  
## <a name="native-serialization"></a>Serializzazione nativa  
 La scelta degli attributi di serializzazione corretti per il tipo definito dall'utente dipende dal tipo definito dall'utente che si desidera creare. Il formato di serializzazione **nativo** utilizza una struttura molto semplice che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente a di archiviare una rappresentazione nativa efficiente del tipo definito dall'utente su disco. Il formato **nativo** è consigliato se il tipo definito dall'utente è semplice e contiene solo campi dei tipi seguenti:  
  
 **bool**, **byte**, **SByte**, **short**, **ushort**, **int**, **uint**, **Long**, **ULONG**, **float**, **Double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 I tipi di valore composti da campi dei tipi precedenti sono candidati validi per il formato **nativo** , ad esempio gli **struct** in Visual C#, o le **strutture** come sono note in Visual Basic. Un tipo definito dall'utente con il formato di serializzazione **nativo** , ad esempio, può contenere un campo di un altro tipo definito dall'utente, anch ' esso specificato con il formato **nativo** . Se la definizione del tipo definito dall'utente è più complessa e contiene tipi di dati non presenti nell'elenco precedente, è necessario specificare invece il formato di serializzazione **UserDefined** .  
  
 Il formato **nativo** prevede i requisiti seguenti:  
  
-   Il tipo non deve specificare un valore per **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. MaxByteSize**.  
  
-   Tutti i campi devono essere serializzabili.  
  
-   **System. Runtime. InteropServices. StructLayoutAttribute** deve essere specificato come **StructLayout. LayoutKindSequential** se il tipo definito dall'utente è definito in una classe e non in una struttura. Questo attributo controlla il layout fisico dei campi dati e viene utilizzato per forzare la disposizione dei membri in base all'ordine in cui vengono visualizzati. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza questo attributo per determinare l'ordine dei campi per i tipi definiti dall'utente con più valori.  
  
 Per un esempio di un tipo definito dall'utente definito con la serializzazione **nativa** , vedere il tipo definito dall'utente Point in [codifica dei tipi definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serializzazione UserDefined  
 L'impostazione del formato **UserDefined** per l'attributo **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** fornisce allo sviluppatore il controllo completo sul formato binario. Quando si specifica la proprietà **Format** attribute come **UserDefined**, è necessario eseguire le operazioni seguenti nel codice:  
  
-   Specificare la proprietà facoltativa dell'attributo **IsByteOrdered** . Il valore predefinito è **false**.  
  
-   Specificare la proprietà **MaxByteSize** di **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**.  
  
-   Scrivere il codice per implementare i metodi di **lettura** e **scrittura** per il tipo definito dall'utente implementando l'interfaccia **System. Data. SQL. IBinarySerialize** .  
  
 Per un esempio di un tipo definito dall'utente definito con la serializzazione **UserDefined** , vedere il tipo definito dall'utente Currency in [codifica dei tipi definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Ai fini dell'indicizzazione, i campi con tipo definito dall'utente devono utilizzare la serializzazione nativa o essere resi persistenti.  
  
## <a name="serialization-attributes"></a>Attributi di serializzazione  
 Gli attributi consentono di determinare la modalità di utilizzo della serializzazione per costruire la rappresentazione di archiviazione dei tipi definiti dall'utente e per trasmettere tali tipi al client in base al valore. Quando si crea il tipo definito dall'utente, è necessario specificare **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** . L'attributo **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** indica che la classe è un tipo definito dall'utente e specifica lo spazio di archiviazione per il tipo definito dall'utente. Facoltativamente, è possibile specificare l'attributo **Serializable** , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sebbene non lo richieda.  
  
 **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** dispone delle proprietà seguenti.  
  
 **Formato**  
 Specifica il formato di serializzazione, che può essere **native** o **UserDefined**, a seconda dei tipi di dati del tipo definito dall'utente.  
  
 **IsByteOrdered**  
 Valore **booleano** che determina il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo in cui esegue i confronti binari nel tipo definito dall'utente.  
  
 **Impossibile IsFixedLength**  
 Indica se tutte le istanze del tipo definito dall'utente sono della stessa lunghezza.  
  
 **MaxByteSize**  
 Dimensioni massime, in byte, dell'istanza. È necessario specificare **MaxByteSize** con il formato di serializzazione **UserDefined** . Per un tipo definito dall'utente con serializzazione definita dall'utente, **MaxByteSize** fa riferimento alla dimensione totale del tipo definito dall'utente nel formato serializzato in base a quanto definito dall'utente. Il valore di **MaxByteSize** deve essere compreso tra 1 e 8000 oppure impostato su-1 per indicare che il tipo definito dall'utente è maggiore di 8000 byte (le dimensioni totali non possono superare le dimensioni massime LOB). Si consideri un tipo definito dall'utente con una proprietà di una stringa di 10 caratteri (**System. Char**). Quando il tipo definito dall'utente viene serializzato utilizzando un oggetto BinaryWriter, le dimensioni totali della stringa serializzata sono pari a 22 byte per ciascun carattere Unicode UTF-16, moltiplicati per il numero massimo di caratteri, più 2 byte di controllo per l'overhead generato dalla serializzazione di un flusso binario. Pertanto, quando si determina il valore di **MaxByteSize**, è necessario prendere in considerazione la dimensione totale del tipo definito dall'utente serializzato, ovvero la dimensione dei dati serializzati in formato binario e l'overhead causato dalla serializzazione.  
  
 **ValidationMethodName**  
 Nome del metodo utilizzato per convalidare le istanze del tipo definito dall'utente.  
  
### <a name="setting-isbyteordered"></a>Impostazione di IsByteOrdered  
 Quando la proprietà **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. IsByteOrdered** è impostata su **true**, si garantisce che i dati binari serializzati possano essere utilizzati per l'ordinamento semantico delle informazioni. In questo modo, ogni istanza di un oggetto del tipo definito dall'utente ordinato per byte può disporre di una sola rappresentazione serializzata. Se in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguita un'operazione di confronto sui byte serializzati, i risultati di tale operazione dovranno essere identici a quelli di un caso in cui la stessa operazione di confronto venga eseguita nel codice gestito. Quando **IsByteOrdered** è impostato su **true**, sono supportate anche le funzionalità seguenti:  
  
-   Capacità di creare indici nelle colonne di questo tipo.  
  
-   Capacità di creare chiavi primarie ed esterne, nonché vincoli CHECK e UNIQUE sulle colonne di questo tipo.  
  
-   Capacità di utilizzare le clausole [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY e PARTITION BY. In questi casi, per determinare l'ordine viene utilizzata la rappresentazione binaria del tipo.  
  
-   Capacità di utilizzare operatori di confronto in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Capacità di garantire la persistenza delle colonne calcolate di questo tipo.  
  
 Si noti che entrambi i formati di serializzazione **nativi** e **UserDefined** supportano gli operatori di confronto seguenti quando **IsByteOrdered** è impostato su **true**:  
  
-   Uguale a (=)  
  
-   Diverso da (!=)  
  
-   Maggiore di (>)  
  
-   Minore di (\<)  
  
-   Maggiore o uguale a (>=)  
  
-   Minore o uguale a (<=)  
  
### <a name="implementing-nullability"></a>Implementazione del supporto dei valori Null  
 Oltre a specificare correttamente gli attributi per gli assembly, la classe deve inoltre supportare i valori Null. I tipi definiti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dall'utente caricati in sono compatibili con i valori null, ma per consentire al tipo definito dall'utente di riconoscere un valore null, la classe deve implementare l'interfaccia **INullable** . Per ulteriori informazioni e un esempio di come implementare il supporto di valori null in un tipo definito dall'utente, vedere [codifica di tipi definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversioni di stringhe  
 Per supportare la conversione di stringhe da e verso il tipo definito dall'utente, è necessario fornire un metodo **Parse** e un metodo **ToString** nella classe. Il metodo **Parse** consente la conversione di una stringa in un tipo definito dall'utente. Deve essere dichiarato come **static** (o **Shared** in Visual Basic) e accetta un parametro di tipo **System. Data. SqlTypes. SqlString**. Per ulteriori informazioni e un esempio di come implementare i metodi **Parse** e **ToString** , vedere [codifica di tipi definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serializzazione XML  
 I tipi definiti dall'utente devono supportare la conversione da e verso il tipo di dati **XML** conformi al contratto per la serializzazione XML. Lo spazio dei nomi **System. XML. Serialization** contiene le classi utilizzate per serializzare oggetti in flussi o documenti in formato XML. È possibile scegliere di implementare la serializzazione **XML** utilizzando l'interfaccia **IXmlSerializable** , che fornisce la formattazione personalizzata per la serializzazione e la deserializzazione XML.  
  
 Oltre a eseguire conversioni esplicite da UDT a **XML**, la serializzazione XML consente di:  
  
-   Utilizzare **XQuery** su valori di istanze UDT dopo la conversione nel tipo di dati **XML** .  
  
-   Utilizzare i tipi definiti dall'utente (UDT) in metodi Web e query con parametri con i servizi Web XML nativi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzare i tipi definiti dall'utente per ricevere un caricamento bulk di dati XML.  
  
-   Serializzare set di dati che contengono tabelle con colonne del tipo definito dall'utente.  
  
 I tipi definiti dall'utente non vengono serializzati nelle query FOR XML. Per eseguire una query FOR XML che visualizza la serializzazione XML dei tipi definiti dall'utente, convertire in modo esplicito ogni colonna UDT nel tipo di dati **XML** nell'istruzione SELECT. È anche possibile convertire in modo esplicito le colonne in **varbinary**, **varchar**o **nvarchar**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un tipo definito dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  

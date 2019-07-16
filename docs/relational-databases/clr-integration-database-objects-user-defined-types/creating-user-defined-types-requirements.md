---
title: Requisiti del tipo definito dall'utente | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028265"
---
# <a name="creating-user-defined-types---requirements"></a>Creazione di tipi definiti dall'utente - Requisiti
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È necessario apportare alcune decisioni di progettazione importante durante la creazione di un tipo definito dall'utente (UDT) per l'installazione nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Benché nella maggior parte dei casi sia consigliabile creare il tipo definito dall'utente come struttura, la creazione come classe rappresenta un'altra opzione valida. Perché il tipo venga registrato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la definizione del tipo definito dall'utente deve essere conforme alle specifiche relative alla creazione di tali tipi.  
  
## <a name="requirements-for-implementing-udts"></a>Requisiti per l'implementazione di tipi definiti dall'utente  
 Ai fini dell'esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo definito dall'utente deve implementare i requisiti seguenti nella relativa definizione:  
  
 Il tipo definito dall'utente deve specificare il **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**. L'utilizzo dei **System. SerializableAttribute** è facoltativo ma consigliato.  
  
-   Il tipo definito dall'utente deve implementare il **System.Data.SqlTypes.INullable** interfaccia nella classe o struttura creando un pubblico **statici** (**condiviso** in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) **Null** (metodo). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta il valore null per impostazione predefinita. Questa condizione è necessaria affinché il codice in esecuzione nel tipo definito dall'utente sia in grado di riconoscere un valore Null.  
  
-   Il tipo definito dall'utente deve contenere un pubblico **statici** (o **condiviso**) **analizzare** metodo che supporti l'analisi e una pubblica **ToString** metodo per conversione in una rappresentazione di stringa dell'oggetto.  
  
-   Un tipo definito dall'utente con un formato di serializzazione definita dall'utente deve implementare il **System.Data.IBinarySerialize** l'interfaccia e fornire una **lettura** e un **scrivere** (metodo).  
  
-   Il tipo definito dall'utente deve implementare **System.Xml.Serialization.IXmlSerializable**, o tutti i campi pubblici e proprietà devono essere di tipi di serializzazione XML o decorati con i **XmlIgnore** attributo se è necessario eseguire l'override della serializzazione standard.  
  
-   È necessario che sia presente solo una serializzazione di un oggetto del tipo definito dall'utente. La convalida ha esito negativo se le routine di serializzazione e deserializzazione riconoscono più di una rappresentazione di un oggetto specifico.  
  
-   **SqlUserDefinedTypeAttribute** deve essere **true** per confrontare i dati nell'ordine dei byte. Se non viene implementata l'interfaccia IComparable e **SqlUserDefinedTypeAttribute** viene **false**, i confronti di ordine byte avrà esito negativo.  
  
-   Un tipo definito dall'utente specificato in una classe deve disporre di un costruttore pubblico che non accetta argomenti. È eventualmente possibile creare costruttori di classe di overload aggiuntivi.  
  
-   Il tipo definito dall'utente deve esporre elementi dati come campi pubblici o routine di proprietà.  
  
-   Nomi pubblici non può contenere più di 128 caratteri e deve essere conforme per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regole di denominazione per gli identificatori come definito in [identificatori del Database](../../relational-databases/databases/database-identifiers.md).  
  
-   **sql_variant** colonne non possono contenere istanze di un tipo definito dall'utente.  
  
-   I membri ereditati non sono accessibili da [!INCLUDE[tsql](../../includes/tsql-md.md)] perché il sistema dei tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non riconosce la gerarchia di ereditarietà tra tipi definiti dall'utente. È tuttavia possibile utilizzare l'ereditarietà quando si strutturano le classi ed è possibile chiamare tali metodi nell'implementazione di codice gestito del tipo.  
  
-   Non è possibile eseguire l'overload dei membri, ad eccezione del costruttore della classe. Se si crea un metodo di overload, non viene generato alcun errore quando si registra l'assembly o si crea il tipo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il rilevamento del metodo di overload si verifica in fase di esecuzione e non durante la creazione del tipo. Nella classe possono essere presenti metodi di overload, a condizione che non vengano mai richiamati. Quando si richiama il metodo di overload, viene generato un errore.  
  
-   Eventuali **statici** (o **condiviso**) i membri devono essere dichiarati come costanti o di sola lettura. I membri statici non possono essere modificati.  
  
-   Se il **SqlUserDefinedTypeAttribute.MaxByteSize** campo è impostato su -1, il tipo definito dall'utente serializzato possono raggiungere il limite di dimensioni LOB (large object) (attualmente 2 GB). La dimensione del tipo in questione non può superare il valore specificato nella **MaxByteSized** campo.  
  
> [!NOTE]  
>  Anche se non viene utilizzato dal server per l'esecuzione di confronti, è possibile implementare facoltativamente il **System. IComparable** interfaccia che espone un solo metodo, **CompareTo**. Tale metodo viene utilizzato sul lato client in situazioni in cui è preferibile confrontare o ordinare in modo accurato i valori del tipo definito dall'utente.  
  
## <a name="native-serialization"></a>Serializzazione nativa  
 La scelta degli attributi di serializzazione corretti per il tipo definito dall'utente dipende dal tipo definito dall'utente che si desidera creare. Il **nativi** formato di serializzazione utilizza una struttura molto semplice che consente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare una rappresentazione nativa efficace dell'UDT su disco. Il **nativa** formato è consigliato se il tipo definito dall'utente è semplice e contiene solo campi dei tipi seguenti:  
  
 **bool**, **byte**, **sbyte**, **breve**, **ushort**, **int**,  **uint**, **lungo**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**,  **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Tipi di valore sono composte da dei campi dei tipi precedenti sono buoni candidati per **nativi** formato, ad esempio **struct** in Visual c# (o **strutture** in cui sono noti Visual Basic). Ad esempio, un tipo definito dall'utente specificato con il **nativa** formato di serializzazione può contenere un campo di un altro tipo definito dall'utente che è stato specificato anche con il **Native** formato. Se la definizione UDT è più complessa e contiene tipi di dati non presenti nell'elenco precedente, è necessario specificare il **UserDefined** invece formato di serializzazione.  
  
 Il **nativa** formato presenta i requisiti seguenti:  
  
-   Il tipo non deve specificare un valore per **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**.  
  
-   Tutti i campi devono essere serializzabili.  
  
-   Il **StructLayoutAttribute** deve essere specificata come **StructLayout. LayoutKindSequential** se il tipo definito dall'utente viene definito in una classe e non in una struttura. Questo attributo controlla il layout fisico dei campi dati e viene utilizzato per forzare la disposizione dei membri in base all'ordine in cui vengono visualizzati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza questo attributo per determinare l'ordine dei campi per i tipi definiti dall'utente con più valori.  
  
 Per un esempio di un tipo definito dall'utente definito con **nativi** serializzazione, vedere il punto di tipo definito dall'utente nella [codifica di tipi](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serializzazione UserDefined  
 Il **UserDefined** formattare impostazione per il **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** offre attributo completo allo sviluppatore il controllo sul formato binario. Quando si specifica la **formato** come proprietà dell'attributo **UserDefined**, è necessario eseguire le operazioni seguenti nel codice:  
  
-   Specificare l'opzione facoltativa **IsByteOrdered** proprietà dell'attributo. Il valore predefinito è **false**.  
  
-   Specificare il **MaxByteSize** proprietà delle **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
-   Scrivere codice per implementare **Read** e **scrivere** metodi per il tipo definito dall'utente implementando il **System.Data.Sql.IBinarySerialize** interfaccia.  
  
 Per un esempio di un tipo definito dall'utente definito con **UserDefined** serializzazione, vedere il tipo definito dall'utente Currency in [codifica di tipi](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Ai fini dell'indicizzazione, i campi con tipo definito dall'utente devono utilizzare la serializzazione nativa o essere resi persistenti.  
  
## <a name="serialization-attributes"></a>Attributi di serializzazione  
 Gli attributi consentono di determinare la modalità di utilizzo della serializzazione per costruire la rappresentazione di archiviazione dei tipi definiti dall'utente e per trasmettere tali tipi al client in base al valore. È necessario specificare il **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** quando si crea il tipo definito dall'utente. Il **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** attributo indica che la classe è un tipo definito dall'utente e consente di specificare lo spazio di archiviazione per il tipo definito dall'utente. È possibile specificare facoltativamente il **Serializable** dell'attributo, anche se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è richiesto.  
  
 Il **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** presenta le proprietà seguenti.  
  
 **Formato**  
 Specifica il formato di serializzazione, che può essere **nativi** oppure **UserDefined**, in base ai tipi di dati dell'UDT.  
  
 **IsByteOrdered**  
 Oggetto **booleana** valore che determina come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue confronti binari il tipo definito dall'utente.  
  
 **IsFixedLength**  
 Indica se tutte le istanze del tipo definito dall'utente sono della stessa lunghezza.  
  
 **MaxByteSize**  
 Dimensioni massime, in byte, dell'istanza. È necessario specificare **MaxByteSize** con il **UserDefined** formato di serializzazione. Per un tipo definito dall'utente con serializzazione definita dall'utente specificata, **MaxByteSize** si riferisce alle dimensioni totali dell'UDT nella sua forma serializzata come definito dall'utente. Il valore di **MaxByteSize** deve essere compreso nell'intervallo tra 1 e 8000 o impostato su -1 per indicare che il tipo definito dall'utente è maggiore di 8000 byte (le dimensioni totali non possono superare le dimensioni LOB massime). Si consideri un tipo definito dall'utente con una proprietà di una stringa di 10 caratteri (**System. Char**). Quando il tipo definito dall'utente viene serializzato utilizzando un oggetto BinaryWriter, le dimensioni totali della stringa serializzata sono 22 byte: 2 byte per carattere UTF-16 Unicode, moltiplicato per il numero massimo di caratteri più 2, il controllo byte di overhead generato dalla serializzazione di un flusso binario. Pertanto, quando si determina il valore di **MaxByteSize**, le dimensioni totali del tipo serializzato in questione devono essere considerata: le dimensioni dei dati serializzati in formato binario più l'overhead generato dalla serializzazione.  
  
 **Metodo ValidationMethodName**  
 Nome del metodo utilizzato per convalidare le istanze del tipo definito dall'utente.  
  
### <a name="setting-isbyteordered"></a>Impostazione di IsByteOrdered  
 Quando la **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** è impostata su **true**, in realtà si garantendo che i dati binari serializzati possono essere utilizzati per Semantic Model ordinamento delle informazioni. In questo modo, ogni istanza di un oggetto del tipo definito dall'utente ordinato per byte può disporre di una sola rappresentazione serializzata. Se in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguita un'operazione di confronto sui byte serializzati, i risultati di tale operazione dovranno essere identici a quelli di un caso in cui la stessa operazione di confronto venga eseguita nel codice gestito. Le funzionalità seguenti sono anche supportate quando **IsByteOrdered** è impostata su **true**:  
  
-   Capacità di creare indici nelle colonne di questo tipo.  
  
-   Capacità di creare chiavi primarie ed esterne, nonché vincoli CHECK e UNIQUE sulle colonne di questo tipo.  
  
-   Capacità di utilizzare le clausole [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY e PARTITION BY. In questi casi, per determinare l'ordine viene utilizzata la rappresentazione binaria del tipo.  
  
-   Capacità di utilizzare operatori di confronto in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Capacità di garantire la persistenza delle colonne calcolate di questo tipo.  
  
 Si noti che sia la **nativi** e **UserDefined** formati di serializzazione supportano gli operatori di confronto seguenti quando **IsByteOrdered** è impostata su **true** :  
  
-   Uguale a (=)  
  
-   Diverso da (!=)  
  
-   Maggiore di (>)  
  
-   Minore di (\<)  
  
-   Maggiore o uguale a (> =)  
  
-   Minore o uguale a (< =)  
  
### <a name="implementing-nullability"></a>Implementazione del supporto dei valori Null  
 Oltre a specificare correttamente gli attributi per gli assembly, la classe deve inoltre supportare i valori Null. Tipi definiti dall'utente caricati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano i valori null, ma in ordine per il tipo definito dall'utente possa riconoscere un valore null, la classe deve implementare il **INullable** interfaccia. Per altre informazioni e un esempio di come implementare l'ammissione di valori null in un tipo definito dall'utente, vedere [codifica di tipi](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversioni di stringhe  
 Per supportare la conversione di stringhe da e verso il tipo definito dall'utente, è necessario specificare una **analizzare** metodo e un **ToString** metodo nella classe. Il **analizzare** metodo consente a una stringa da convertire in un tipo definito dall'utente. Deve essere dichiarata come **statici** (o **condiviso** in Visual Basic) e accettare un parametro di tipo **System.Data.SqlTypes.SqlString**. Per altre informazioni e un esempio di come implementare il **analizzare** e **ToString** metodi, vedere [codifica di tipi](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serializzazione XML  
 Tipi definiti dall'utente deve supportare la conversione da e verso i **xml** tipo di dati conformi al contratto per la serializzazione XML. Il **Serialization** dello spazio dei nomi contiene classi utilizzate per serializzare oggetti in flussi o documenti in formato XML. È possibile scegliere di implementare **xml** serializzazione utilizzando il **IXmlSerializable** interfaccia, che fornisce formattazione personalizzata per la serializzazione XML e la deserializzazione.  
  
 Oltre a eseguire conversioni esplicite dal tipo definito dall'utente per **xml**, la serializzazione XML consente di:  
  
-   Uso **Xquery** sui valori delle istanze di tipo definito dall'utente dopo la conversione nel **xml** tipo di dati.  
  
-   Utilizzare i tipi definiti dall'utente (UDT) in metodi Web e query con parametri con i servizi Web XML nativi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzare i tipi definiti dall'utente per ricevere un caricamento bulk di dati XML.  
  
-   Serializzare set di dati che contengono tabelle con colonne del tipo definito dall'utente.  
  
 I tipi definiti dall'utente non vengono serializzati nelle query FOR XML. Per eseguire una query FOR XML che visualizza la serializzazione XML dei tipi definiti dall'utente, convertire in modo esplicito ogni colonna di tipo definito dall'utente per il **xml** tipo di dati nell'istruzione SELECT. È possibile convertire in modo esplicito le colonne da **varbinary**, **varchar**, o **nvarchar**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un tipo definito dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  

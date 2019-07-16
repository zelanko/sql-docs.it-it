---
title: Riferimento errore ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da9d7d2374f8e3410598bfdfbd97e59eb505b255
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926248"
---
# <a name="ado-errors"></a>Errori ADO
Il **ErrorValueEnum** costante vengono descritti i valori di errore ADO. Per un elenco completo di queste costanti enumerate, compresi i valori, vedere [appendice b: Errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md). In questa sezione verrà esaminare alcuni degli errori più interessanti e illustrano alcune situazioni specifiche in grado di generare, o soluzioni per risolvere il problema. Entrambi i **ErrorValueEnum** costante e il numero di decimale positivo brevi sono elencati.

|Number|ErrorValueEnum (costante)|Descrizione/le possibili cause|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|Provider non è stato possibile eseguire l'operazione richiesta.|
|**3001**|**adErrInvalidArgument**|Gli argomenti sono di tipo errato, sono comprese nell'intervallo accettabile o sono in conflitto tra loro. Questo errore è spesso causato da un errore di ortografia in un'istruzione SQL SELECT. Ad esempio, un nome di campo con errori di ortografia o un nome di tabella può generare questo errore. Questo errore può verificarsi anche quando un campo o una tabella denominata in un'istruzione SELECT non esiste nell'archivio dati.|
|**3002**|**adErrOpeningFile**|Non è stato possibile aprire i file. È stato specificato un nome di file con errori di ortografia, o un file è stato spostato, rinominato o eliminato. In una rete, l'unità potrebbe essere temporaneamente non disponibile o il traffico di rete consentano una connessione.|
|**3003**|**adErrReadFile**|File non è stato possibile leggere. Il nome del file è stato specificato correttamente, il file potrebbe essere stato spostato o eliminato o il file potrebbe essere danneggiato.|
|**3004**|**adErrWriteFile**|Impossibile scrivere nel file. È un file potrebbe essere stato chiuso e ha cercato di scrivere in esso oppure il file potrebbe essere danneggiato. Se il file si trova in un'unità di rete, condizioni temporanee della rete potrebbero impedire la scrittura in un'unità di rete.|
|**3021**|**adErrNoCurrentRecord**|Entrambi **BOF** oppure **EOF** è True, o il record corrente è stato eliminato. L'operazione richiesta richiede un record corrente.<br /><br /> Si è verificato un tentativo di aggiornare i record usando **trovare** oppure **Seek** per spostare il puntatore di record per il record desiderato. Se il record non viene trovato, **EOF** sarà True. Questo errore può verificarsi anche dopo un tentativo fallito **AddNew** oppure **eliminare** perché non sono presenti record corrente quando questi metodi hanno esito negativo.|
|**3219**|**adErrIllegalOperation**|Operazione non è consentita in questo contesto.|
|**3220**|**adErrCantChangeProvider**|Il provider specificato è diverso da quello già in uso.|
|**3246**|**adErrInTransaction**|**Connessione** oggetto non può essere chiusa in modo esplicito in una transazione. Oggetto **Recordset** oppure **connessione** oggetto attualmente fa parte di una transazione non può essere chiusa. Chiameranno **RollbackTrans** oppure **CommitTrans** prima della chiusura dell'oggetto.|
|**3251**|**adErrFeatureNotAvailable**|L'oggetto o il provider non è in grado di eseguire l'operazione richiesta. Alcune operazioni dipendono da una versione specifica del provider.|
|**3265**|**adErrItemNotFound**|Impossibile trovare l'elemento nella raccolta corrispondente per il nome richiesto o per ordinale. È stato specificato un nome di campo o una tabella non corretto.|
|**3367**|**adErrObjectInCollection**|Oggetto è già nella raccolta. Impossibile accodare. Un oggetto non può essere aggiunto due volte nella stessa raccolta.|
|**3420**|**adErrObjectNotSet**|Oggetto non è più valido.|
|**3421**|**adErrDataConversion**|Applicazione usa un valore di tipo errato per l'operazione corrente. Si potrebbe essere stata specificata una stringa a un'operazione che prevede un flusso, ad esempio.|
|**3704**|**adErrObjectClosed**|Operazione non è consentita quando l'oggetto è chiuso. Il **Connection** oppure **Recordset** è stata chiusa. Alcune altre routine, ad esempio, potrebbe essersi chiusa un oggetto globale. È possibile impedire questo errore controllando le **stato** proprietà prima di eseguire un'operazione.|
|**3705**|**adErrObjectOpen**|Operazione non è consentita quando l'oggetto è aperto. Impossibile aprire un oggetto che è aperto. Impossibile aggiungere campi a un oggetto aperto **Recordset**.|
|**3706**|**adErrProviderNotFound**|Impossibile trovare il provider. Si potrebbe non essere installato correttamente.<br /><br /> Il nome del provider potrebbe essere specificato in modo non corretto, il provider specificato potrebbe non essere installato nel computer in cui il codice è in esecuzione o l'installazione potrebbe essere danneggiato.|
|**3707**|**adErrBoundToCommand**|Il **ActiveConnection** proprietà di un **Recordset** object, che contiene una **comando** oggetto come origine, non può essere modificato. L'applicazione ha tentato di assegnare un nuovo **Connection** dell'oggetto a un **Recordset** che ha un **comando** oggetto come origine.|
|**3708**|**adErrInvalidParamInfo**|**Parametro** oggetto stato definito correttamente. È state fornite informazioni incoerenti o incomplete.|
|**3709**|**adErrInvalidConnection**|La connessione non può essere usata per eseguire questa operazione. È chiuso o non valido in questo contesto.|
|**3710**|**adErrNotReentrant**|Impossibile eseguire l'operazione durante l'elaborazione dell'evento. Impossibile eseguire un'operazione all'interno di un gestore eventi che genera l'evento attiva nuovamente. Ad esempio, i metodi di navigazione non devono essere chiamati dall'interno una **WillMove** gestore dell'evento.|
|**3711**|**adErrStillExecuting**|Impossibile eseguire l'operazione durante l'esecuzione in modo asincrono.|
|**3712**|**adErrOperationCancelled**|Operazione è stata annullata dall'utente. L'applicazione ha chiamato la **CancelUpdate** oppure **CancelBatch** (metodo) e l'operazione corrente è stata annullata.|
|**3713**|**adErrStillConnecting**|Operazione non può essere eseguita durante la connessione in modo asincrono.|
|**3714**|**adErrInvalidTransaction**|Il coordinamento della transazione non è valido o non è stata avviata.|
|**3715**|**adErrNotExecuting**|Impossibile eseguire l'operazione se non in esecuzione.|
|**3716**|**adErrUnsafeOperation**|Le impostazioni di sicurezza in questo computer non consentono l'accesso a un'origine dati in un altro dominio.|
|**3717**|**adWrnSecurityDialog**|Solo per uso interno. Non usare. (Voce è stata inclusa per ragioni di completezza. Questo errore non deve essere visualizzati nel codice.)|
|**3718**|**adWrnSecurityDialogHeader**|Solo per uso interno. Non usare. (Voce è stata inclusa per ragioni di completezza. Questo errore non deve essere visualizzati nel codice.)|
|**3719**|**adErrIntegrityViolation**|Il valore dei dati è in conflitto con i vincoli di integrità del campo. Un nuovo valore per un **campo** causerebbe una chiave duplicata. Un valore corrispondente a un lato di una relazione tra due record potrebbe non essere aggiornabile.|
|**3720**|**adErrPermissionDenied**|Autorizzazione insufficiente impedisce la scrittura nel campo. L'utente specificato nella stringa di connessione non dispone delle autorizzazioni appropriate per scrivere in un **campo**.|
|**3721**|**adErrDataOverflow**|Valore dei dati è troppo grande per essere rappresentato dal tipo di campo dati. È stato assegnato un valore numerico che è troppo grande per il campo desiderato. Ad esempio, un valore long integer è stato assegnato a un campo del valore short integer.|
|**3722**|**adErrSchemaViolation**|Il valore dei dati è in conflitto con il tipo di dati o i vincoli del campo. L'archivio dati presenta vincoli di convalida che differiscono dal **campo** valore.|
|**3723**|**adErrSignMismatch**|Conversione non riuscita perché il valore dei dati è con segno mentre il tipo di dati di campo utilizzato dal provider è senza segno.|
|**3724**|**adErrCantConvertvalue**|Impossibile convertire il valore di dati per cause diverse da overflow o non corrispondenza di segno. Ad esempio, la conversione causi il troncamento dei dati.|
|**3725**|**adErrCantCreate**|Valore di dati non può essere impostata o recuperata perché il tipo di dati del campo è sconosciuto, o il provider di risorse insufficienti per eseguire l'operazione.|
|**3726**|**adErrColumnNotOnThisRow**|Record non contiene questo campo. È stato specificato un nome di campo errato o non in un campo la **campi** raccolta del record corrente è stato fatto riferimento.|
|**3727**|**adErrURLDoesNotExist**|L'URL di origine o l'elemento padre dell'URL di destinazione non esiste. È un errore di digitazione nell'URL di origine o destinazione. È possibile avere `https://mysite/photo/myphoto.jpg` quando è effettivamente necessario `https://mysite/photos/myphoto.jpg` invece. L'errore di digitazione nell'URL padre (in questo caso *foto* invece di *foto*) che ha causato l'errore.|
|**3728**|**adErrTreePermissionDenied**|Le autorizzazioni sono insufficienti per accedere ad albero o un sottoalbero. L'utente specificato nella stringa di connessione non dispone delle autorizzazioni appropriate.|
|**3729**|**adErrInvalidURL**|L'URL contiene caratteri non validi. Assicurarsi che l'URL sia stato digitato correttamente. L'URL segue lo schema di registrazione al provider corrente (ad esempio, Internet Publishing Provider è registrato per il protocollo http).|
|**3730**|**adErrResourceLocked**|Oggetto rappresentato dall'URL specificato è bloccato da uno o più processi. Attendere fino al termine del processo e ripetere l'operazione. L'oggetto a cui che si sta provando ad accedere è stato bloccato da un altro utente o da un altro processo all'interno dell'applicazione. Questo è più probabile che si verificano in un ambiente multiutente.|
|**3731**|**adErrResourceExists**|Impossibile eseguire l'operazione di copia. Oggetto con il nome dall'URL di destinazione già esistente. Specificare **adCopyOverwrite** sostituire l'oggetto. Se non si specifica **adCopyOverwrite** quando si copiano i file in una directory, la copia ha esito negativo quando si tenta di copiare un elemento che esiste già nel percorso di destinazione.|
|**3732**|**adErrCannotComplete**|Il server non è possibile completare l'operazione. È possibile che il server è occupato con altre operazioni o potrebbe essere insufficiente delle risorse.|
|**3733**|**adErrVolumeNotFound**|Impossibile individuare il dispositivo di archiviazione indicato dall'URL. Assicurarsi che l'URL sia stato digitato correttamente. L'URL del dispositivo di archiviazione potrebbe non essere corretto, ma questo errore può verificarsi per altri motivi. Il dispositivo potrebbe essere offline o un volume elevato di traffico di rete potrebbe impedire la connessione venga eseguito.|
|**3734**|**adErrOutOfSpace**|Impossibile eseguire l'operazione. Il provider non è possibile ottenere spazio di archiviazione sufficiente. Potrebbe non esserci sufficiente RAM o spazio su disco rigido per i file temporanei nel server.|
|**3735**|**adErrResourceOutOfScope**|URL di origine o di destinazione è all'esterno dell'ambito del record corrente.|
|**3736**|**adErrUnavailable**|Impossibile completare l'operazione e lo stato non è disponibile. Il campo può essere non disponibile o non è stata tentata l'operazione. Un altro utente potrebbe avere modificarla o eliminarla il campo che si sta provando ad accedere.|
|**3737**|**adErrURLNamedRowDoesNotExist**|Il record specificato da questo URL non esiste. Durante il tentativo di aprire un file usando un **Record** dell'oggetto, il nome del file o il percorso del file di stato digitato correttamente.|
|**3738**|**adErrDelResOutOfScope**|L'URL dell'oggetto da eliminare è all'esterno dell'ambito del record corrente.|
|**3747**|**adErrCatalogNotSet**|Operazione richiede un valore valido **ParentCatalog**.|
|**3748**|**adErrCantChangeConnection**|Connessione è stata negata. La nuova connessione richiesto ha caratteristiche diverse rispetto a quello già in uso.|
|**3749**|**adErrFieldsUpdateFailed**|Impossibile aggiornare i campi. Per altre informazioni, esaminare i **stato** proprietà degli oggetti singoli campi. Questo errore può verificarsi in due situazioni: quando si modifica un **campo** valore dell'oggetto in fase di modifica o aggiunta di un record nel database; e quando si modificano le proprietà delle **campo** oggetto stesso.<br /><br /> Il **Record** oppure **Recordset** aggiornamento non è riuscito a causa di un problema con uno dei campi nel record corrente. Enumerare i **i campi** insieme e verificare le **stato** proprietà di ogni campo per determinare la causa del problema.|
|**3750**|**adErrDenyNotSupported**|Provider non supporta restrizioni di condivisione. Si è verificato un tentativo di limitare la condivisione di file e il provider non supporta il concetto.|
|**3751**|**adErrDenyTypeNotSupported**|Provider non supporta il tipo richiesto di restrizioni di condivisione. Si è verificato un tentativo di stabilire un particolare tipo di condivisione file restrizione che non è supportato dal provider. Vedere la documentazione del provider per determinare quali restrizioni di condivisione file sono supportati.|

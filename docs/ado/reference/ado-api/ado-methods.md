---
title: Metodi ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 67b428a06679bdb0cade14314195d576a1ccc596
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696860"
---
# <a name="ado-methods"></a>Metodi ADO

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Crea un nuovo record per un aggiornabile **Recordset** oggetto.|  
|[Accoda](../../../ado/reference/ado-api/append-method-ado.md)|Aggiunge un oggetto a una raccolta. Se la raccolta è **i campi**, un nuovo **campo** oggetto può essere creato prima di essere aggiunta alla raccolta.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Accoda i dati a un testo di grandi dimensioni o dati binari **campo**, o a un **parametro** oggetto.|  
|[BeginTrans, CommitTrans e RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Gestisce l'elaborazione all'interno delle transazioni di un **connessione** oggetto come indicato di seguito:<br /><br /> **BeginTrans** -inizia una nuova transazione.<br /><br /> **CommitTrans** : Salva eventuali modifiche apportate e termina la transazione corrente. Anche possibile avviare una nuova transazione.<br /><br /> **RollbackTrans** : Annulla le modifiche e termina la transazione corrente. Anche possibile avviare una nuova transazione.|  
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|Annulla l'esecuzione di un'in sospeso, chiamata asincrona al metodo.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Annulla un aggiornamento batch in sospeso.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Annulla tutte le modifiche apportate alla riga corrente o nuova di un' **Recordset** oggetto, o il **campi** raccolta di un **Record** oggetto, prima di chiamare il  **Aggiornamento** (metodo).|  
|[Clear](../../../ado/reference/ado-api/clear-method-ado.md)|Rimuove tutti i **errore** oggetti dalle **errori** raccolta.|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Crea un duplicato **Recordset** oggetto da un oggetto esistente **Recordset** oggetto. Facoltativamente, specifica che il clone sia di sola lettura.|  
|[Chiudi](../../../ado/reference/ado-api/close-method-ado.md)|Chiude un oggetto aperto e tutti gli oggetti dipendenti.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Confronta due segnalibri e restituisce un'indicazione dei relativi valori.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Copia un file o directory e il relativo contenuto, in un'altra posizione.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Copia il numero specificato di caratteri o byte (a seconda **tipo**) nella **Stream** a un altro **Stream** oggetto.|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Crea un nuovo **parametro** oggetto contenente le proprietà specificate.|  
|[Delete (raccolta di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Elimina un oggetto dal **parametri** raccolta.|  
|[Delete (raccolta Fields ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Elimina un oggetto dal **campi** raccolta.|  
|[Delete (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Elimina il record corrente o un gruppo di record.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Elimina un file o directory e tutte le relative sottodirectory.|  
|[Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Esegue la query, l'istruzione SQL o stored procedure specificata nel **CommandText** proprietà.|  
|[Execute (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Esegue la query specificata, SQL istruzione, stored procedure o il testo del provider.|  
|[Find](../../../ado/reference/ado-api/find-method-ado.md)|Cerca un **Recordset** per la riga che soddisfa i criteri specificati.|  
|[Flush](../../../ado/reference/ado-api/flush-method-ado.md)|Forza il contenuto del **Stream** rimanenti nel buffer di ADO per l'oggetto sottostante a cui il **Stream** è associato.|  
|[Metodo get_OLEDBCommand](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Restituisce il comando OLE DB sottostanti, prima di tutto la propagazione di tutte le informazioni sui parametri impostata per il comando ADO per comando OLE DB.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Restituisce un **Recordset** contenente le righe rappresentano i file e sottodirectory nella directory rappresentata da questo **Record**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Restituisce tutte le o in parte, il contenuto di un testo di grandi dimensioni o dati binari **campo** oggetto.|  
|[Metodo GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera l'oggetto origine dati OLE DB sottostante dal provider di forma.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Recupera i record più di una **Recordset** oggetto in una matrice.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Restituisce il **Recordset** sotto forma di stringa.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Carica il contenuto di un file esistente in un **Stream**.|  
|[Sposta](../../../ado/reference/ado-api/move-method-ado.md)|Sposta la posizione del record corrente in un **Recordset** oggetto.|  
|[Metodi MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sposta il primo, ultimo, successivo o precedente record in un oggetto specificato **Recordset** specificato e ne fanno il record corrente.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Sposta un file o una directory e il relativo contenuto, in un'altra posizione.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Cancella l'oggetto corrente **Recordset** dell'oggetto e restituisce il successivo **Recordset** anticipando attraverso una serie di comandi.|  
|[Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Apre una connessione a un'origine dati.|  
|[Open (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)|Apre un oggetto esistente **Record** dell'oggetto o creare un nuovo file o directory.|  
|[Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Apre un cursore.|  
|[Aprire (Stream ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Consente di aprire una **Stream** oggetto per gestire i flussi di dati binari o testo.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Ottiene le informazioni sullo schema di database dal provider.|  
|[Metodo put_OLEDBCommand](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Questo metodo non esegue alcuna operazione, viene sempre restituito S_OK.|  
|[Lettura](../../../ado/reference/ado-api/read-method.md)|Legge un numero specificato di byte da un **Stream** oggetto.|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Legge un numero specificato di caratteri da un testo **Stream** oggetto.|  
|[Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md)|Aggiorna gli oggetti in una raccolta in modo da riflettere gli oggetti disponibili e specifiche del provider.|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Aggiorna i dati in un **Recordset** oggetto eseguendo nuovamente la query in cui si basa l'oggetto.|  
|[Resync](../../../ado/reference/ado-api/resync-method.md)|Aggiorna i dati nell'attuale **Recordset** oggetto, o **campi** raccolta di un **Record** oggetto, dal database sottostante.|  
|[Salvare](../../../ado/reference/ado-api/save-method.md)|Salva il **Recordset** in un file o **Stream** oggetto.|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Salva il contenuto binario di un **Stream** in un file.|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|Cerca l'indice di un **Recordset** per individuare rapidamente la riga che corrisponde ai valori specificati e cambia la posizione della riga corrente di tale riga.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|Imposta la posizione che rappresenta la fine del flusso.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Ignora un'intera riga durante la lettura di un flusso di testo.|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|Ottiene le informazioni statistiche su un flusso aperto.|  
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Determina se un oggetto specificato **Recordset** oggetto supporta un determinato tipo di funzionalità.|  
|[Update](../../../ado/reference/ado-api/update-method.md)|Salva le modifiche apportate alla riga corrente di un **Recordset** oggetto, o il **campi** raccolta di un **Record** oggetto.|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Scrive tutti gli aggiornamenti in blocco in sospeso sul disco.|  
|[Write](../../../ado/reference/ado-api/write-method.md)|Scrive dati binari in una **Stream** oggetto.|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|Scrive una stringa di testo specificato in un **Stream** oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte di ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: Errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfacce e oggetti ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)

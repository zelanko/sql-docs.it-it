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
author: rothja
ms.author: jroth
ms.openlocfilehash: 65145ce8f77c352fb24a2a206d99828298b6a60c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747252"
---
# <a name="ado-methods"></a>Metodi ADO

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Crea un nuovo record per un oggetto **Recordset** aggiornabile.|  
|[Aggiungere](../../../ado/reference/ado-api/append-method-ado.md)|Accoda un oggetto a una raccolta. Se la raccolta è **Fields**, è possibile creare un nuovo oggetto **campo** prima che venga aggiunto alla raccolta.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Accoda i dati a un **campo**di dati di testo o binario di grandi dimensioni o a un oggetto **Parameter** .|  
|[BeginTrans, CommitTrans e RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Gestisce l'elaborazione delle transazioni all'interno di un oggetto **connessione** come indicato di seguito:<br /><br /> **BeginTrans** : inizia una nuova transazione.<br /><br /> **CommitTrans** -Salva le modifiche e termina la transazione corrente. Potrebbe inoltre avviare una nuova transazione.<br /><br /> **RollbackTrans** : Annulla tutte le modifiche e termina la transazione corrente. Potrebbe inoltre avviare una nuova transazione.|  
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|Annulla l'esecuzione di una chiamata al metodo asincrona in sospeso.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Annulla un aggiornamento batch in sospeso.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Annulla tutte le modifiche apportate alla riga corrente o nuova di un oggetto **Recordset** oppure alla raccolta **Fields** di un oggetto **record** , prima di chiamare il metodo **Update** .|  
|[Cancella](../../../ado/reference/ado-api/clear-method-ado.md)|Rimuove tutti gli oggetti **Error** dalla raccolta **Errors** .|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md) (Clona)|Crea un oggetto **Recordset** duplicato da un oggetto **Recordset** esistente. Facoltativamente, specifica che il clone deve essere di sola lettura.|  
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|Chiude un oggetto aperto e tutti gli oggetti dipendenti.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Confronta due segnalibri e restituisce un'indicazione dei valori relativi.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Copia un file o una directory e il relativo contenuto in un'altra posizione.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Copia il numero specificato di caratteri o byte (a seconda del **tipo**) nel **flusso** in un altro oggetto **flusso** .|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Crea un nuovo oggetto **Parameter** con le proprietà specificate.|  
|[Delete (raccolta di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Elimina un oggetto dalla raccolta di **parametri** .|  
|[Delete (raccolta di campi ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Elimina un oggetto dalla raccolta di **campi** .|  
|[Delete (recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Elimina il record corrente o un gruppo di record.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Elimina un file o una directory e tutte le relative sottodirectory.|  
|[Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Esegue la query, l'istruzione SQL o stored procedure specificata nella proprietà **CommandText** .|  
|[Execute (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Esegue la query, l'istruzione SQL, il stored procedure o il testo specifico del provider specificato.|  
|[Trova](../../../ado/reference/ado-api/find-method-ado.md)|Esegue la ricerca di un **Recordset** per la riga che soddisfa i criteri specificati.|  
|[Filo](../../../ado/reference/ado-api/flush-method-ado.md)|Impone il contenuto del **flusso** rimanente nel buffer ADO all'oggetto sottostante a cui è associato il **flusso** .|  
|[Metodo get_OLEDBCommand](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Restituisce il comando OLEDB sottostante, propagando prima di tutto le informazioni sui parametri impostate nel comando ADO al comando OLEDB.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Restituisce un **Recordset** le cui righe rappresentano i file e le sottodirectory della directory rappresentata da questo **record**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Restituisce tutto o una parte di, il contenuto di un oggetto **campo** di dati di testo o binario di grandi dimensioni.|  
|[Metodo GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera l'oggetto origine dati OLEDB sottostante dal provider di forme.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Recupera più record di un oggetto **Recordset** in una matrice.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Restituisce il **Recordset** sotto forma di stringa.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Carica il contenuto di un file esistente in un **flusso**.|  
|[Spostamento](../../../ado/reference/ado-api/move-method-ado.md)|Sposta la posizione del record corrente in un oggetto **Recordset** .|  
|[MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Passa al record primo, ultimo, successivo o precedente in un oggetto **Recordset** specificato e fa in modo che registri il record corrente.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Sposta un file o una directory e il relativo contenuto in un'altra posizione.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Cancella l'oggetto **Recordset** corrente e restituisce il **Recordset** successivo avanzando attraverso una serie di comandi.|  
|[Apri (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Apre una connessione a un'origine dati.|  
|[Apri (record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|Apre un oggetto **record** esistente o crea un nuovo file o directory.|  
|[Open (recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Apre un cursore.|  
|[Apri (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Apre un oggetto **Stream** per modificare i flussi di dati binari o di testo.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Ottiene le informazioni sullo schema del database dal provider.|  
|[Metodo put_OLEDBCommand](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Questo metodo non esegue alcuna operazione. restituisce sempre S_OK.|  
|[Lettura](../../../ado/reference/ado-api/read-method.md)|Legge un numero specificato di byte da un oggetto **flusso** .|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Legge un numero specificato di caratteri da un oggetto **flusso** di testo.|  
|[Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md)|Aggiorna gli oggetti di una raccolta in modo da riflettere gli oggetti disponibili e specifici del provider.|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Aggiorna i dati in un oggetto **Recordset** eseguendo nuovamente la query su cui è basato l'oggetto.|  
|[Risincronizza](../../../ado/reference/ado-api/resync-method.md)|Aggiorna i dati nell'oggetto **Recordset** corrente o nella raccolta di **campi** di un oggetto **record** dal database sottostante.|  
|[Salva](../../../ado/reference/ado-api/save-method.md)|Salva il **Recordset** in un oggetto file o **flusso** .|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Salva il contenuto binario di un **flusso** in un file.|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|Esegue una ricerca nell'indice di un **Recordset** per individuare rapidamente la riga che corrisponde ai valori specificati e imposta la posizione della riga corrente su quella riga.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|Imposta la posizione che rappresenta la fine del flusso.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Ignora un'intera riga durante la lettura di un flusso di testo.|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|Ottiene informazioni statistiche su un flusso aperto.|  
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Determina se un oggetto **Recordset** specificato supporta un particolare tipo di funzionalità.|  
|[Aggiornamento](../../../ado/reference/ado-api/update-method.md)|Salva le modifiche apportate alla riga corrente di un oggetto **Recordset** o alla raccolta di **campi** di un oggetto **record** .|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Scrive tutti gli aggiornamenti batch in sospeso sul disco.|  
|[Scrittura](../../../ado/reference/ado-api/write-method.md)|Scrive dati binari in un oggetto **flusso** .|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|Scrive una stringa di testo specificata in un oggetto **flusso** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Oggetti e interfacce ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)

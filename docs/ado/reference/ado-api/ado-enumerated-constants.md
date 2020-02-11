---
title: Costanti enumerate ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a2b02498905b73f321d7585b5c91adfbfd1b4b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921024"
---
# <a name="ado-enumerated-constants"></a>Costanti enumerate ADO
Per semplificare il debug, le enumerazioni ADO elencano un valore per ogni costante. Tuttavia, questo valore è puramente consultivo e può variare da una versione di ADO a un'altra. Il codice deve dipendere solo dal nome, non dal valore effettivo, di ogni costante enumerata.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Per un oggetto **Recordset** RDS, specifica la priorità di esecuzione del thread asincrono che recupera i dati.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Specifica quando il provider **MSDataShape** ricalcola le colonne aggregate e calcolate in un **Recordset**gerarchico.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Specifica i campi che è possibile utilizzare per rilevare i conflitti durante un aggiornamento ottimistico di una riga dell'origine dati con un oggetto **Recordset** .|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Specifica se il metodo **UpdateBatch** è seguito da un'operazione implicita di **Risincronizzazione** del metodo e, in tal caso, dall'ambito di tale operazione.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Specifica quali record sono interessati da un'operazione.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Specifica un segnalibro che indica dove deve iniziare l'operazione.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Specifica la modalità di interpretazione di un argomento di comando.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Specifica la posizione relativa di due record rappresentati dai relativi segnalibri.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Specifica le autorizzazioni disponibili per la modifica dei dati in una **connessione**, l'apertura di un **record**o la specifica di valori per la proprietà **mode** degli oggetti **record** e **flusso** .|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Specifica se il metodo **Open** di un oggetto **Connection** deve essere restituito dopo (in modalità sincrona) o prima (in modo asincrono) che la connessione viene stabilita.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Specifica se deve essere visualizzata una finestra di dialogo per richiedere parametri mancanti durante l'apertura di una connessione a un'origine dati ODBC.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Specifica il comportamento del metodo **CopyRecord** .|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Specifica la posizione del motore del cursore.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Specifica la funzionalità che il metodo **supporta** deve testare.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Specifica il tipo di cursore utilizzato in un oggetto **Recordset** .|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Specifica il tipo di dati di un **campo**, un **parametro**o una **proprietà**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Specifica lo stato di modifica di un record.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Specifica il tipo di errore in fase di esecuzione ADO.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Specifica il motivo per cui è stato generato un evento.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Specifica lo stato corrente dell'esecuzione di un evento.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Specifica la modalità di esecuzione di un comando da un provider.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Specifica i campi speciali a cui viene fatto riferimento nella raccolta **Fields** di un oggetto **record** .|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Specifica uno o più attributi di un oggetto **campo** .|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Specifica lo stato di un oggetto **campo** .|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Specifica il gruppo di record da filtrare da un **Recordset**.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Specifica il numero di record da recuperare da un **Recordset**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Specifica il livello di isolamento della transazione per un oggetto **Connection** .|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Specifica il carattere utilizzato come separatore di riga negli oggetti del **flusso** di testo.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Specifica il tipo di blocco inserito nei record durante la modifica.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Specifica i record che devono essere restituiti al server.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Specifica il comportamento del metodo **MoveRecord** dell'oggetto **record** .|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Specifica se un oggetto è aperto o chiuso, connettendosi a un'origine dati, eseguendo un comando o recuperando i dati.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Specifica gli attributi di un oggetto **Parameter** .|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Specifica se il **parametro** rappresenta un parametro di input, un parametro di output o entrambi o se il parametro è il valore restituito da un stored procedure.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Specifica il formato in cui salvare un **Recordset**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Specifica la posizione corrente del puntatore del record all'interno di un **Recordset**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Specifica gli attributi di un oggetto **Proprietà** .|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Specifica per il metodo di **apertura** dell'oggetto **record** se deve essere aperto un **record** esistente o se deve essere creato un nuovo **record** .|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Specifica le opzioni per l'apertura di un **record**. Questi valori possono essere combinati usando un operatore OR.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Specifica lo stato di un record per quanto riguarda gli aggiornamenti in batch e altre operazioni bulk.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Specifica il tipo di oggetto **record** .|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Specifica se i valori sottostanti vengono sovrascritti da una chiamata alla **Risincronizzazione**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Specifica se un file deve essere creato o sovrascritto durante il salvataggio da un oggetto **flusso** . I valori possono essere combinati con un operatore AND.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Specifica il tipo di **Recordset** dello schema recuperato dal metodo **OpenSchema** . Specifica la direzione di una ricerca di record in un **Recordset**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Specifica la direzione di una ricerca di record in un **Recordset**. Specifica il tipo di **ricerca** da eseguire.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Specifica il tipo di **ricerca** da eseguire. Specifica le opzioni per l'apertura di un oggetto **flusso** . I valori possono essere combinati con un operatore AND.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Specifica le opzioni per l'apertura di un oggetto **flusso** . I valori possono essere combinati con un operatore AND. Specifica se l'intero flusso o la riga successiva devono essere letti da un oggetto **flusso** .|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Specifica se l'intero flusso o la riga successiva devono essere letti da un oggetto **flusso** . Specifica il tipo di dati archiviati in un oggetto **flusso** .|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Specifica il tipo di dati archiviati in un oggetto **flusso** . Specifica se un separatore di riga viene aggiunto alla stringa scritta in un oggetto **flusso** .|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Specifica se un separatore di riga viene aggiunto alla stringa scritta in un oggetto **flusso** . Specifica il formato durante il recupero di un **Recordset** come stringa.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Specifica il formato durante il recupero di un **Recordset** come stringa. Specifica gli attributi di transazione di un oggetto **Connection** .|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Specifica gli attributi di transazione di un oggetto **Connection** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Appendice B: errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Oggetti e interfacce ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)

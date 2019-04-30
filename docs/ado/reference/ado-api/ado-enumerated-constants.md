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
manager: craigg
ms.openlocfilehash: a13adf7aa1a769f6e63f9686938cb801cd6383fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249059"
---
# <a name="ado-enumerated-constants"></a>Costanti enumerate ADO
Per semplificare il debug, le enumerazioni ADO elenca un valore per ciascuna costante. Tuttavia, questo valore è puramente consulenza e può variare da una versione di ADO a un altro. Il codice deve dipendere esclusivamente il nome, non il valore effettivo di ogni costante enumerata.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Per un RDS **Recordset** oggetto, specifica la priorità di esecuzione del thread asincrona che recupera i dati.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Specifica quando il **MSDataShape** provider nuovamente Calcola aggregazione e le colonne calcolate in un modello gerarchico **Recordset**.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Specifica quali campi possono essere usati per rilevare i conflitti durante un aggiornamento ottimistica di una riga dell'origine dati con un **Recordset** oggetto.|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Specifica se il **UpdateBatch** metodo è seguito da implicita **Risincronizza** operazione del metodo e in questo caso, l'ambito di tale operazione.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Consente di specificare quali record sono interessati da un'operazione.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Specifica un segnalibro che indica dove iniziare l'operazione.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Specifica come deve essere interpretato un argomento di comando.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Specifica la posizione relativa di due record rappresentati dai relativi segnalibri.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Specifica le autorizzazioni disponibili per la modifica dei dati in un **Connection**, aprire un **Record**, o specificando i valori per il **modalità** proprietà del  **Record** e **Stream** oggetti.|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Specifica se il **aperto** metodo di un **connessione** oggetto deve essere restituito dopo (in modo sincrono) o prima (in modo asincrono) viene stabilita la connessione.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Specifica se deve essere visualizzata una finestra di dialogo per la richiesta di parametri mancanti quando si apre una connessione a un'origine dati ODBC.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Specifica il comportamento dei **CopyRecord** (metodo).|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Specifica la posizione del motore del cursore.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Specifica il tipo di funzionalità di **supporta** metodo deve verificare la presenza.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Specifica il tipo di cursore utilizzato una **Recordset** oggetto.|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Specifica il tipo di dati di un **campo**, **parametro**, o **proprietà**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Specifica lo stato di modifica di un record.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Specifica il tipo di errore di run-time di ADO.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Specifica il motivo che ha causato un evento si verifichi.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Specifica lo stato corrente dell'esecuzione di un evento.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Specifica il modo in cui un provider di eseguire un comando.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Specifica i campi speciali a cui fa riferimento il **i campi** raccolta di un **Record** oggetto.|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Specifica uno o più attributi di un **campo** oggetto.|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Specifica lo stato di un **campo** oggetto.|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Specifica il gruppo di record da filtrare da una **Recordset**.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Specifica il numero di record da recuperare da un **Recordset**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Specifica il livello di isolamento delle transazioni per un **connessione** oggetto.|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Specifica il carattere utilizzato come separatore di riga nel testo **Stream** oggetti.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Specifica il tipo di blocco inserito nei record durante la modifica.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Consente di specificare quali record devono essere restituiti al server.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Specifica il comportamento dei **Record** oggetto **MoveRecord** (metodo).|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Specifica se un oggetto è aperto o chiuso, ci si connette a un'origine dati, l'esecuzione di un comando o il recupero dei dati.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Specifica gli attributi di un **parametro** oggetto.|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Specifica se il **parametro** rappresenta un parametro di input, un parametro di output o entrambi, o se il parametro è il valore restituito da una stored procedure.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Specifica il formato in cui salvare una **Recordset**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Specifica la posizione corrente del puntatore del record all'interno di un **Recordset**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Specifica gli attributi di un **proprietà** oggetto.|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Specifica per il **Record** oggetto **Open** metodo se un oggetto esistente **Record** deve essere aperto, o un nuovo **Record** deve essere creata.|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Specifica le opzioni per aprire una **Record**. Questi valori possono essere combinati utilizzando l'operatore OR.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Specifica lo stato di un record per quanto riguarda gli aggiornamenti in batch e altre operazioni bulk.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Specifica il tipo della **Record** oggetto.|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Specifica se i valori sottostanti vengono sovrascritti da una chiamata a **Risincronizza**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Specifica se un file deve essere creato o sovrascritto durante il salvataggio di un **Stream** oggetto. I valori possono essere combinati con l'operatore AND.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Specifica il tipo di schema **Recordset** che il **OpenSchema** recuperata dal metodo. Specifica la direzione di una ricerca di record all'interno di un **Recordset**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Specifica la direzione di una ricerca di record all'interno di un **Recordset**. Specifica il tipo della **Seek** da eseguire.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Specifica il tipo della **Seek** da eseguire. Specifica le opzioni per aprire una **Stream** oggetto. I valori possono essere combinati con l'operatore AND.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Specifica le opzioni per aprire una **Stream** oggetto. I valori possono essere combinati con l'operatore AND. Specifica se l'intero flusso o nella riga successiva deve essere letti da un **Stream** oggetto.|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Specifica se l'intero flusso o nella riga successiva deve essere letti da un **Stream** oggetto. Specifica il tipo di dati archiviati in un **Stream** oggetto.|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Specifica il tipo di dati archiviati in un **Stream** oggetto. Specifica se un separatore di riga viene aggiunto alla stringa di cui è scritto in un **Stream** oggetto.|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Specifica se un separatore di riga viene aggiunto alla stringa di cui è scritto in un **Stream** oggetto. Specifica il formato durante il recupero di un **Recordset** sotto forma di stringa.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Specifica il formato durante il recupero di un **Recordset** sotto forma di stringa. Specifica gli attributi di transazione di un **connessione** oggetto.|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Specifica gli attributi di transazione di un **connessione** oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte di ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Appendice b: Errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfacce e oggetti ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)

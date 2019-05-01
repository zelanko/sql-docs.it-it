---
title: Indice proprietà dinamica ADO | Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60347cbffcc169c47149e27cf1064cd9c68494f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249561"
---
# <a name="ado-dynamic-property-index"></a>Indice delle proprietà dinamiche ADO
Provider di dati, i provider di servizi e componenti del servizio possono aggiungere proprietà dinamiche per le **delle proprietà** raccolte di oggetti [connessione](../../../ado/reference/ado-api/connection-object-ado.md) e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti. Un determinato provider può inoltre inserire le proprietà aggiuntive quando questi oggetti sono aperti. Alcune di queste proprietà sono elencate le [proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md) sezione. Più sono elencati sotto il provider specifici nel [appendice a: I provider](../../../ado/guide/appendixes/appendix-a-providers.md) sezione.  
  
 Le tabelle seguenti sono cross-indexes dei nomi ADO e OLE DB per ogni proprietà dinamica di provider OLE DB standard. I provider possono aggiungere ulteriori proprietà oltre a quelle elencate di seguito. Per informazioni specifiche sulle proprietà dinamiche specifiche del provider, vedere la documentazione del provider.  
  
 Riferimento dei programmatori OLE DB è relativo a un nome di proprietà di ADO con il termine "Description". Per altre informazioni su queste proprietà standard, cercare o sfogliare l'indice nel [documentazione di OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)per la proprietà OLE DB in base al nome.  
  
## <a name="connection-dynamic-properties"></a>Proprietà dinamiche di connessione  
  
|Nome della proprietà ADO|Nome della proprietà OLE DB|  
|-----------------------|--------------------------|  
|Sessioni attive|DBPROP_ACTIVESESSIONS|  
|Interruzione asincrona|DBPROP_ASYNCTXNABORT|  
|Commit asincrono|DBPROP_ASYNCTNXCOMMIT|  
|Livelli di isolamento autocommit|DBPROP_SESS_AUTOCOMMITISOLEVELS|  
|Posizione catalogo|DBPROP_CATALOGLOCATION|  
|Termine catalogo|DBPROP_CATALOGTERM|  
|Definizione di colonna|DBPROP_COLUMNDEFINITION|  
|Timeout di connessione|DBPROP_INIT_TIMEOUT|  
|Catalogo corrente|DBPROP_CURRENTCATALOG|  
|origine dati|DBPROP_INIT_DATASOURCE|  
|Nome origine dati|DBPROP_DATASOURCENAME|  
|Oggetto di origine dati modello di Threading|DBPROP_DSOTHREADMODEL|  
|Nome DBMS|DBPROP_DBMSNAME|  
|Versione DBMS|DBPROP_DBMSVER|  
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|  
|Supporto GROUP BY|DBPROP_GROUPBY|  
|Supporto tabelle eterogenee|DBPROP_HETEROGENEOUSTABLES|  
|Distinzione maiuscole/minuscole identificatore|DBPROP_IDENTIFIERCASE|  
|Catalogo iniziale|DBPROP_INIT_CATALOG|  
|Livelli di isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|  
|Mantenimento isolamento|DBPROP_SUPPORTEDTXNISORETAIN|  
|Locale Identifier|DBPROP_INIT_LCID|  
|Location|DBPROP_INIT_LOCATION|  
|Dimensione massima dell'indice|DBPROP_MAXINDEXSIZE|  
|Dimensioni massime delle righe|DBPROP_MAXROWSIZE|  
|Dimensioni massime riga con BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|  
|Numero massimo di tabelle in SELECT|DBPROP_MAXTABLESINSELECT|  
|Modalità|DBPROP_INIT_MODE|  
|Più set di parametri|DBPROP_MULTIPLEPARAMSETS|  
|Risultati multipli|DBPROP_MULTIPLERESULTS|  
|Più oggetti di archiviazione|DBPROP_MULTIPLESTORAGEOBJECTS|  
|Aggiornamento tabelle multiple|DBPROP_MULTITABLEUPDATE|  
|Ordine delle regole di confronto NULL|DBPROP_NULLCOLLATION|  
|Comportamento concatenazione NULL|DBPROP_CONCATNULLBEHAVIOR|  
|Servizi OLE DB|DBPROP_INIT_OLEDBSERVICES|  
|Versione OLE DB|DBPROP_PROVIDEROLEDBVER|  
|Supporto oggetti OLE|DBPROP_OLEOBJECTS|  
|Supporto per Rowset aperto|DBPROP_OPENROWSETSUPPORT|  
|Colonne ORDER BY nell'elenco di selezione|DBPROP_ORDERBYCOLUMNSINSELECT|  
|Disponibilità parametro di output|DBPROP_OUTPUTPARAMETERAVAILABILITY|  
|Passa per le funzioni di accesso di riferimento|DBPROP_BYREFACCESSORS|  
|Password|DBPROP_AUTH_PASSWORD|  
|Persist Security Info|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|  
|Tipo ID persistente|DBPROP_PERSISTENTIDTYPE|  
|Comportamento preparazione interruzione|DBPROP_PREPAREABORTBEHAVIOR|  
|Comportamento preparazione Commit|DBPROP_PREPARECOMMITBEHAVIOR|  
|Termine routine|DBPROP_PROCEDURETERM|  
|Messaggio di richiesta|DBPROP_INIT_PROMPT|  
|Nome descrittivo del provider|DBPROP_PROVIDERFRIENDLYNAME|  
|Provider Name|DBPROP_PROVIDERFILENAME|  
|Versione del provider|DBPROP_PROVIDERVER|  
|Origine dati di sola lettura|DBPROP_DATASOURCEREADONLY|  
|Conversioni di set di righe di comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|  
|Termine schema|DBPROP_SCHEMATERM|  
|Utilizzo dello schema|DBPROP_SCHEMAUSAGE|  
|Supporto di SQL|DBPROP_SQLSUPPORT|  
|Archiviazione strutturata|DBPROP_STRUCTUREDSTORAGE|  
|Supporto delle sottoquery|DBPROP_SUBQUERIES|  
|Termine tabella|DBPROP_TABLETERM|  
|Transazione DDL|DBPROP_SUPPORTEDTXNDDL|  
|ID utente|DBPROP_AUTH_USERID|  
|Nome utente|DBPROP_USERNAME|  
|Handle di finestra|DBPROP_INIT_HWND|  
  
## <a name="recordset-dynamic-properties"></a>Proprietà dinamiche del recordset  
 Si noti che il **proprietà dinamiche** delle **Recordset** oggetto passare dall'ambito (diventano non disponibile) quando il **Recordset** viene chiuso.  
  
|Nome della proprietà ADO|Nome della proprietà OLE DB|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|Ordine di accesso|DBPROP_ACCESSORDER|  
|Set di righe solo Accodamento|DBPROP_APPENDONLY|  
|Elaborazione asincrona gruppo di righe|DBPROP_ROWSET_ASYNCH|  
|Ricalcolo automatico|DBPROP_ADC_AUTORECALC|  
|Dimensione di recupero in background|DBPROP_ASYNCHFETCHSIZE|  
|Background Thread Priority|DBPROP_ASYNCHTHREADPRIORITY|  
|Dimensioni batch|DBPROP_ADC_BATCHSIZE|  
|Blocca gli oggetti di archiviazione|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|Tipo di segnalibro|DBPROP_BOOKMARKTYPE|  
|Supporta|DBPROP_IROWSETLOCATE|  
|Segnalibri ordinati|DBPROP_ORDEREDBOOKMARKS|  
|Memorizzare nella cache le righe figlio|DBPROP_ADC_CACHECHILDROWS|  
|Memorizzare nella cache le colonne posticipate|DBPROP_CACHEDEFERRED|  
|Modificare le righe inserite|DBPROP_CHANGEINSERTEDROWS|  
|Privilegi colonna|DBPROP_COLUMNRESTRICT|  
|Notifica impostazione colonna|DBPROP_NOTIFYCOLUMNSET|  
|Colonna scrivibile|DBPROP_MAYWRITECOLUMN|  
|Timeout comando|DBPROP_COMMANDTIMEOUT|  
|Versione del motore del cursore|DBPROP_ADC_CEVER|  
|Rinviare colonna|DBPROP_DEFERRED|  
|Aggiornamenti degli oggetti di archiviazione di ritardo|DBPROP_DELAYSTORAGEOBJECTS|  
|Recupera all'indietro|DBPROP_CANFETCHBACKWARDS|  
|Operazioni di filtro|DBPROP_FILTERCOMPAREOPS|  
|Operazioni di ricerca|DBPROP_FINDCOMPAREOPS|  
|Colonne nascoste (conteggio)|DBPROP_HIDDENCOLUMNS|  
|Contenere righe|DBPROP_CANHOLDROWS|  
|Righe immobili|DBPROP_IMMOBILEROWS|  
|Dimensione di recupero iniziale|DBPROP_ASYNCHPREFETCHSIZE|  
|Segnalibri letterali|DBPROP_LITERALBOOKMARKS|  
|Identità di riga letterale|DBPROP_LITERALIDENTITY|  
|Gestire lo stato di modifica|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|Numero massimo righe aperte|DBPROP_MAXOPENROWS|  
|Numero massimo righe in sospeso|DBPROP_MAXPENDINGROWS|  
|Numero massimo di righe|DBPROP_MAXROWS|  
|Utilizzo memoria|DBPROP_MEMORYUSAGE|  
|Granularità notifiche|DBPROP_NOTIFICATIONGRANULARITY|  
|Fasi di notifica|DBPROP_NOTIFICATIONPHASES|  
|Oggetti transazione|DBPROP_TRANSACTEDOBJECT|  
|Modifiche di altri utenti visibili|DBPROP_OTHERUPDATEDELETE|  
|Inserimenti di altri utenti visibili|DBPROP_OTHERINSERT|  
|Proprie modifiche visibili|DBPROP_OWNUPDATEDELETE|  
|Inserimenti locali visibili|DBPROP_OWNINSERT|  
|Mantieni in caso di interruzione|DBPROP_ABORTPRESERVE|  
|Mantieni in caso di Commit|DBPROP_COMMITPRESERVE|  
|Private1||  
|Riavvio rapido|DBPROP_QUICKRESTART|  
|Eventi rientranti|DBPROP_REENTRANTEVENTS|  
|Rimuovere le righe eliminate|DBPROP_REMOVEDELETED|  
|Riporta modifiche Multiple|DBPROP_REPORTMULTIPLECHANGES|  
|Proprietà dinamica Reshape Name|DBPROP_ADC_RESHAPENAME|  
|La risincronizzazione di comando|DBPROP_ADC_CUSTOMRESYNCH|  
|Restituisci inserimenti in sospeso|DBPROP_RETURNPENDINGINSERTS|  
|Notifica eliminazione riga|DBPROP_NOTIFYROWDELETE|  
|Notifica prima modifica riga|DBPROP_NOTIFYROWFIRSTCHANGE|  
|Notifica inserimento riga|DBPROP_NOTIFYROWINSERT|  
|Privilegi riga|DBPROP_ROWRESTRICT|  
|Notifica risincronizzazione riga|DBPROP_NOTIFYROWRESYNCH|  
|Modello di Threading riga|DBPROP_ROWTHREADMODEL|  
|Notifica annullamento Modifica riga|DBPROP_NOTIFYROWUNDOCHANGE|  
|Notifica annullamento eliminazione riga|DBPROP_NOTIFYROWUNDODELETE|  
|Notifica annullamento inserimento riga|DBPROP_NOTIFYROWUNDOINSERT|  
|Notifica aggiornamento riga|DBPROP_NOTIFYROWUPDATE|  
|Notifica modifica posizione recupero gruppo di righe|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|  
|Notifica rilascio gruppo di righe|DBPROP_NOTIFYROWSETRELEASE|  
|Scorri indietro|DBPROP_CANSCROLLBACKWARDS|  
|Cursore del server|DBPROP_SERVERCURSOR|  
|Ignora segnalibri eliminati|DBPROP_BOOKMARKSKIPPED|  
|Identità riga forte|DBPROP_STRONGIDENTITY|  
|Catalogo univoco|DBPROP_ADC_UNIQUECATALOG|  
|Righe univoche|DBPROP_UNIQUEROWS|  
|Schema univoco|DBPROP_ADC_UNIQUESCHEMA|  
|tabella univoca|DBPROP_ADC_UNIQUETABLE|  
|Aggiornabile|DBPROP_UPDATABILITY|  
|Criteri di aggiornamento|DBPROP_ADC_UPDATECRITERIA|  
|Update Resync|DBPROP_ADC_UPDATERESYNC|  
|Usare i segnalibri|DBPROP_BOOKMARKS|

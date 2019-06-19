---
title: Interfaccia IMDEmbeddedData | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 203eae4b3660aaf5d1f2ed3a92ba844e88a518ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467782"
---
# <a name="imdembeddeddata-interface"></a>Interfaccia IMDEmbeddedData
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'interfaccia IMDEmbeddedData è un'interfaccia pubblica utilizzata per la gestione incorporata [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] database o un database modello tabulare. L'interfaccia eredita dal **IPersistStream** interfaccia. e consente di effettuare le operazioni seguenti:  
  
-   Ottenere un identificatore per il flusso incorporato nel documento contenitore.  
  
-   Impostare l'URL del documento contenitore.  
  
-   Impostare un flag per specificare se l'applicazione in cui viene eseguito l'incorporamento è in ambiente host.  
  
-   Impostare il percorso dei file temporanei utilizzati dall'applicazione in cui viene eseguito l'incorporamento.  
  
-   Annullare l'operazione incorporata corrente.  
  
-   Ottenere le dimensioni stimate (in byte) del flusso per il salvataggio dell'oggetto incorporato. Ereditato da **IPersistStream**.  
  
-   Verificare se il database incorporato è stato modificato rispetto all'ultimo salvataggio. Ereditato da **IPersistStream**.  
  
-   Caricare il database incorporato nel motore locale o in-process. Ereditato da **IPersistStream**.  
  
-   Salvare il database locale o in-process nel flusso incorporato del documento contenitore. Ereditato da **IPersistStream**.  
  
## <a name="reference"></a>Riferimenti  
 Documenti di riferimento seguenti il **IMDEmbeddedData** interfaccia presentato nei **msmd** file di intestazione.  
  
### <a name="source-file-pxoembeddeddataidl"></a>File di origine: PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Ottiene l'identificatore utilizzato dall'applicazione host per il flusso incorporato nel documento contenitore.  
  
#### <a name="parameters"></a>Parametri  
 *out_pbstrStreamId*  
 Specifica la posizione dell'identificatore di flusso.  
  
#### <a name="return-value"></a>Valore restituito  
 **S_OK**  
 L'identificatore di flusso è stato restituito correttamente.  
  
 **S_FALSE**  
 Non esiste alcun identificatore di flusso.  
  
 **E_FAIL**  
 Si è verificato un errore durante l'accesso all'identificatore di flusso.  
  
#### <a name="remarks"></a>Note  
 Per verificare se la connessione corrente contiene un database incorporato, l'utente deve controllare il valore della proprietà DBPROP_MSMD_EMBEDDED_DATA dalle proprietà di connessione di OLE DB.  
  
 I valori possibili per DBPROP_MSMD_EMBEDDED_DATA sono:  
  
|Nome|Value|Definizione|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|Nessun database incorporato disponibile|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|L'applicazione corrente contiene il database incorporato|  
|DBPROPVAL_EMBED_LINKED|0x02|Il database incorporato è ospitato in un'applicazione remota, ad esempio SharePoint Server|  
  
#### <a name="source"></a>`Source`  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Viene impostato l'URL per il file in cui è contenuto il flusso incorporato.  
  
#### <a name="parameters"></a>Parametri  
 *in_bstrURL*  
 Specifica l'URL per il documento contenitore.  
  
#### <a name="return-value"></a>Valore restituito  
 **S_OK**  
 L'URL del contenitore è stato impostato correttamente.  
  
 **E_FAIL**  
 Si è verificato un errore durante l'impostazione dell'URL del contenitore.  
  
#### <a name="source"></a>`Source`  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Impostare un flag per specificare se l'applicazione in cui viene eseguito l'incorporamento è in ambiente host.  
  
#### <a name="parameters"></a>Parametri  
 *in_ftHosted*  
 TRUE se il chiamante è in un ambiente host in un'applicazione di servizio (come IIS).  
  
#### <a name="return-value"></a>Valore restituito  
 **S_OK**  
 Il flag è stato impostato correttamente.  
  
 **E_FAIL**  
 Si è verificato un errore durante l'impostazione del flag.  
  
#### <a name="source"></a>`Source`  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Impostare il percorso dei file temporanei utilizzati dall'applicazione in cui viene eseguito l'incorporamento.  
  
#### <a name="parameters"></a>Parametri  
 *in_bstrPath*  
 Il percorso dei file temporanei utilizzato dall'applicazione host.  
  
#### <a name="return-value"></a>Valore restituito  
 **S_OK**  
 La directory dei file temporanei è stata impostata correttamente.  
  
 **E_FAIL**  
 Si è verificato un errore durante l'impostazione del percorso.  
  
#### <a name="source"></a>`Source`  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Descrizione  
 Annulla l'operazione del database incorporato corrente.  
  
#### <a name="parameters"></a>Parametri  
 Nessuna.  
  
#### <a name="return-value"></a>Valore restituito  
 **S_OK**  
 L'operazione è stata annullata correttamente.  
  
 **DB_E_CANTCANCEL**  
 Non è in corso alcuna operazione annullabile.  
  
 **E_FAIL**  
 Si verificato un errore durante l'annullamento dell'operazione incorporata.  
  
#### <a name="source"></a>`Source`  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Ottiene la dimensione stimata (in byte) del flusso per il salvataggio dell'oggetto incorporato. Ereditato da **IPersistStream**.  
  
#### <a name="parameters"></a>Parametri  
 *in_bstrPath*  
 La dimensione stimata (in byte) dell'immagine del database incorporato.  
  
#### <a name="return-value"></a>Valore restituito  
 **S_OK**  
 La dimensione è stata ottenuta correttamente.  
  
 **E_FAIL**  
 Errore durante il calcolo della dimensione.  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Descrizione  
 Verifica se il database incorporato è stato modificato rispetto all'ultimo salvataggio. Ereditato da **IPersistStream**.  
  
#### <a name="parameters"></a>Parametri  
 none  
  
#### <a name="return-values"></a>Valori restituiti  
 **S_OK**  
 Il database è stato modificato rispetto all'ultimo salvataggio.  
  
 **S_FALSE**  
 Il database non è stato modificato rispetto all'ultimo salvataggio.  
  
 **E_FAIL**  
 Si è verificato un errore durante il recupero dello stato del database.  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Carica il database incorporato sul motore locale o in-process. Ereditato da **IPersistStream**.  
  
#### <a name="parameters"></a>Parametri  
 *in_pStm*  
 Un puntatore a un'interfaccia del flusso da cui caricare il database incorporato.  
  
#### <a name="return-values"></a>Valori restituiti  
 **S_OK**  
 Il database è stato caricato correttamente.  
  
 **E_OUTOFMEMORY**  
 Memoria insufficiente per il caricamento del database.  
  
 **E_FAIL**  
 Si è verificato un errore durante il caricamento del database, diverso da **E_OUTOFMEMORY**.  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Descrizione  
 Salva il database locale o in-process nel flusso incorporato del documento contenitore. Ereditato da **IPersistStream**.  
  
#### <a name="parameters"></a>Parametri  
 *in_pStm*  
 Un puntatore a un'interfaccia del flusso in cui salvare il database incorporato.  
  
 *in_fClearDirty*  
 Un flag che indica se il flag modificato deve essere eliminato dopo questa operazione.  
  
#### <a name="return-values"></a>Valori restituiti  
 **S_OK**  
 Il database è stato salvato correttamente.  
  
 **STG_E_CANTSAVE**  
 Si è verificato un errore durante il salvataggio del database, diverso da **STG_E_MEDIUMFULL**.  
  
 **STG_E_MEDIUMFULL**  
 Non è possibile salvare il database perché lo spazio sul dispositivo di memorizzazione è esaurito.  
  
  

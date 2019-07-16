---
title: I record e campi specificati dal Provider | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54d55926d2bec89b0764b751bf165586e8d3c6c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924511"
---
# <a name="records-and-provider-supplied-fields"></a>Record e campi specificati dal provider
Quando un [Record](../../../ado/reference/ado-api/record-object-ado.md) apertura dell'oggetto, l'origine può essere la riga corrente di un elemento aperto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), un URL assoluto o un URL relativo in combinazione con un elemento aperto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto .  
  
 Se il **Record** viene aperto da un **Recordset**, il **Record** oggetto [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta conterrà tutti i campi dal  **Recordset**, oltre a tutti i campi aggiunti dal provider sottostante.  
  
 Il provider può inserire campi aggiuntivi che fungono da supplementari caratteristiche dei **Record**. Di conseguenza, una **Record** può includere campi univoci non nel **Recordset** come intero o qualsiasi **Record** derivato da un'altra riga del **Recordset**.  
  
 Ad esempio, tutte le righe di una **Recordset** derivato da un messaggio con origine dati potrebbe disporre di colonne, ad esempio, a e il soggetto. Oggetto **Record** deriva da quello **Recordset** avranno gli stessi campi. Tuttavia, il **Record** debba anche gli altri campi univoci al messaggio specifico, rappresentato da tale **Record**, ad esempio allegato e Cc (copia).  
  
 Anche se il **Record** oggetto e la riga corrente delle **Recordset** hanno gli stessi campi sono diversi perché **Record** e **Recordset**gli oggetti hanno proprietà e metodi diversi.  
  
 Un campo comune per il **Record** e **Recordset** può essere modificato in uno qualsiasi degli oggetti. Tuttavia, non è possibile eliminare il campo sul **Record** dell'oggetto, anche se il provider sottostante può supportare l'impostazione del campo su null.  
  
 Dopo il **Record** è aperto, è possibile aggiungere a livello di programmazione i campi. È anche possibile eliminare i campi che sono stati aggiunti, ma non è possibile eliminare i campi dalla versione originale **Recordset**.  
  
 È anche possibile aprire il **Record** oggetto direttamente da un URL. In questo caso, i campi aggiunti per il **Record** dipendono dal provider sottostante. Attualmente, la maggior parte dei provider di aggiungere un set di campi che descrivono l'entità rappresentata dal **Record**. Se l'entità è costituita da un flusso di byte, ad esempio un semplice file, un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto in genere può essere aperta dalle **Record**.  
  
## <a name="special-fields-for-document-source-providers"></a>Provider di origine di campi specifici per documento  
 Una classe speciale di provider, detti *provider di origine del documento*, gestisce le cartelle e documenti. Quando un **Record** oggetto rappresenta un documento o un **Recordset** oggetto rappresenta una cartella dei documenti, il provider di origine del documento consente di popolare gli oggetti con un set univoco di campi che descrivono caratteristiche del documento invece dell'effettivo del documento stesso. In genere, un campo contiene un riferimento per la **Stream** che rappresenta il documento.  
  
 Questi campi rappresentano una risorsa **record** oppure **recordset** e sono elencate per il provider specifici che li supportano in [appendice a: I provider](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Indice di due costanti il **campi** raccolta di una risorsa **Record** oppure **Recordset** per recuperare due campi di usati comune. Il **campo** oggetto [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà restituisce il contenuto desiderato.  
  
-   Il campo cui si accede con il **adDefaultStream** costante contiene un flusso predefinito associato il **Record** oppure **Recordset** oggetto. Il provider assegna un flusso predefinito a un oggetto.  
  
-   Il campo cui si accede con il **adRecordURL** costante contiene l'URL assoluto che identifica il documento.  
  
 Un provider di origine del documento non supporta il [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta di **Record** e **campo** oggetti. Il contenuto di **proprietà** la raccolta è null per tali oggetti.  
  
 Un provider di origine del documento potrebbe aggiungere una proprietà specifica del provider, ad esempio **tipo di origine dati** per identificare se un provider di origine del documento. Per altre informazioni su come determinare il tipo di provider, vedere la documentazione del provider.  
  
## <a name="resource-recordset-columns"></a>Risorsa colonne dei Recordset  
 Oggetto *recordset risorse* costituito dalle colonne seguenti.  
  
|Nome colonna|type|Descrizione|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|Di sola lettura. Indica l'URL della risorsa.|  
|RESOURCE_PARENTNAME|AdVarWChar|Di sola lettura. Indica l'URL assoluto del record padre.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|Di sola lettura. Indica l'URL assoluto della risorsa, che rappresenta la concatenazione di PARENTNAME e PARSENAME.|  
|CUI RESOURCE_ISHIDDEN|adBoolean|True se la risorsa è nascosto. Verrà restituita alcuna riga, a meno che il comando che crea in modo esplicito il set di righe consente di selezionare le righe in cui RESOURCE_ISHIDDEN è True.|  
|RESOURCE_ISREADONLY|adBoolean|True se la risorsa è di sola lettura. Tentativi per aprire questa risorsa con DBBINDFLAG_WRITE e che non riescono con DBBINDFLAG_WRITE. Questa proprietà può essere modificata anche quando la risorsa è stata aperta solo per la lettura.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|Indica l'utilizzo probabile del documento, ad esempio, un avvocato del breve. Questo valore può corrispondere al modello di Office che è stato usato per creare il documento.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|Indica il tipo MIME del documento, che indica il formato, ad esempio "`text/html`".|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|Indica la lingua in cui è archiviato il contenuto.|  
|RESOURCE_CREATIONTIME|adFileTime|Di sola lettura. Indica una struttura FILETIME che contiene l'ora di che creazione della risorsa. Il tempo è espresso nel formato Coordinated Universal Time (UTC).|  
|RESOURCE_LASTACCESSTIME|AdFileTime|Di sola lettura. Indica una struttura FILETIME che contiene l'ora di ultimo accesso alla risorsa. Il tempo è in formato UTC. I membri FILETIME sono zero se il provider non supporta questo membro temporale.|  
|RESOURCE_LASTWRITETIME|AdFileTime|Di sola lettura. Indica una struttura FILETIME che contiene l'ora dell'ultima scrittura alla risorsa. Il tempo è in formato UTC. I membri FILETIME sono zero se il provider non supporta questo membro temporale.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Di sola lettura. Indica le dimensioni della risorsa predefinita, in byte del flusso.|  
|RESOURCE_ISCOLLECTION|adBoolean|Di sola lettura. True se la risorsa è una raccolta, ad esempio una directory. False se la risorsa è un semplice file.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|True se la risorsa è un documento strutturato. False se la risorsa non è un documento strutturato. Potrebbe trattarsi di una raccolta o un file semplice.|  
|DEFAULT_DOCUMENT|AdVarWChar|Di sola lettura. Indica che questa risorsa contiene un URL per il documento predefinito semplice di una cartella o un documento strutturato. Utilizzato quando viene richiesto il flusso predefinito da una risorsa. Questa proprietà è vuota per un semplice file.|  
|CHAPTERED_CHILDREN|adChapter|Di sola lettura. facoltativo. Indica il capitolo del set di righe che contiene gli elementi figlio della risorsa. (Il *Provider OLE DB per Internet Publishing* non usare questa colonna.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|Di sola lettura. Indica il nome visualizzato della risorsa.|  
|RESOURCE_ISROOT|adBoolean|Di sola lettura. True se la risorsa è la radice di una raccolta o documento strutturato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Appendice A: provider](../../../ado/guide/appendixes/appendix-a-providers.md)

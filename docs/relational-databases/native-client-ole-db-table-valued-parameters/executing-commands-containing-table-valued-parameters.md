---
title: Esecuzione di comandi contenenti parametri con valori di tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93f88971a466d997aa7a32b80b029e10a80af3d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103455"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Esecuzione di comandi contenenti parametri con valori di tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  L'esecuzione di un comando contenente parametri con valori di tabella avviene in due fasi.  
  
1.  Specifica dei tipi del parametro.  
  
2.  Associazione dei dati del parametro.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="table-valued-parameter-specification"></a>Specifica del parametro con valori di tabella  
 Il tipo del parametro con valori di tabella può essere specificato dal consumer. Le informazioni relative al tipo includono il nome del tipo e il nome dello schema, se il tipo di tabella definito dall'utente per il parametro con valori di tabella non è presente nello schema predefinito corrente per la connessione. In base al supporto server, il consumer può specificare anche informazioni facoltative sui metadati, ad esempio l'ordine delle colonne, e specificare che tutte le righe di determinate colonne includano i valori predefiniti.  
  
 Per specificare un parametro con valori di tabella, il consumer chiama ISSCommandWithParameter::SetParameterInfo e, facoltativamente, chiama isscommandwithparameters:: Setparameterproperties. Per un parametro con valori di tabella, il campo *pwszDataSourceType* nella struttura DBPARAMBINDINFO presenta un valore pari a DBTYPE_TABLE. Il campo *ulParamSize* è impostato su ~0 per indicare che la lunghezza non è nota. Proprietà specifica per i parametri con valori di tabella, ad esempio nome dello schema, nome del tipo, ordine delle colonne e colonne predefinite, possono essere impostate tramite isscommandwithparameters:: Setparameterproperties.  
  
## <a name="table-valued-parameter-binding"></a>Associazione del parametro con valori di tabella  
 Un parametro con valori di tabella può essere qualsiasi oggetto set di righe. Il provider legge da questo oggetto mentre invia parametri con valori di tabella al server durante l'esecuzione.  
  
 Per associare il parametro con valori di tabella, il consumer chiama IAccessor:: CreateAccessor. Il campo *wType* della struttura DBBINDING per il parametro con valori di tabella è impostato su DBTYPE_TABLE. Il membro *pObject* della struttura DBBINDING è non NULL e il membro *iid* di *pObject* è impostato su IID_IRowset o su qualsiasi altra interfaccia dell'oggetto set di righe del parametro con valori di tabella. I campi restanti nella struttura DBBINDING devono essere impostati con la stessa modalità con cui sono impostati per i BLOB di flusso.  
  
 Alle associazioni relative al parametro con valori di tabella e all'oggetto set di righe associato a un parametro con valori di tabella vengono applicate le restrizioni seguenti:  
  
-   Gli unici valori di stato consentiti per i dati di colonna dei set di righe di parametri con valori di tabella sono DBSTATUS_S_ISNULL e DBSTATUS_S_OK. DBSTATUS_S_DEFAULT genera un errore e il valore di stato associato viene impostato su DBSTATUS_E_BADSTATUS.  
  
-   Un parametro con valori di tabella può essere contrassegnato dallo stato DBSTATUS_S_DEFAULT. Gli unici valori validi sono DBSTATUS_S_DEFAULT e DBSTATUS_S_OK. Quando lo stato è impostato su DBSTATUS_S_DEFAULT, il valore del parametro con valori di tabella corrisponde a una tabella vuota.  
  
-   Le colonne di sola lettura nei parametri con valori di tabella (colonne Identity o calcolate) devono essere contrassegnate come predefinite tramite la proprietà SSPROP_PARAM_TABLE_DEFAULT_COLUMNS. Anche le colonne che presentano un valore predefinito devono essere contrassegnate come predefinite tramite la proprietà SSPROP_PARAM_TABLE_DEFAULT_COLUMNS per far sì che il valore predefinito venga usato per i valori dei dati della colonna per un determinato parametro con valori di tabella. Il provider ignorerà i valori dei dati associati per le colonne contrassegnate come predefinite.  
  
-   I dati saranno inviati al server per le colonne con DBPROP_COL_AUTOINCREMENT o SSPROP_COL_COMPUTED, a meno che non sia impostata anche la proprietà SSPROP_PARAM_TABLE_DEFAULT.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

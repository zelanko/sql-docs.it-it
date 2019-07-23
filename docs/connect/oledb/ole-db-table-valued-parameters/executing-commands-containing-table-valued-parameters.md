---
title: Esecuzione di comandi contenenti parametri con valori di tabella | Microsoft Docs
description: Esecuzione di comandi contenenti parametri con valori di tabella
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 320a66b84c6a5b904e98941251801c7ee5927087
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994146"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Esecuzione di comandi contenenti parametri con valori di tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  L'esecuzione di un comando con parametri con valori di tabella avviene in due fasi:  
  
1.  Specifica dei tipi del parametro.  
  
2.  Associazione dei dati del parametro.  
  
## <a name="table-valued-parameter-specification"></a>Specifica del parametro con valori di tabella  
 Il tipo del parametro con valori di tabella può essere specificato dal consumer. Le informazioni relative al tipo includono il nome del tipo e il nome dello schema, se il tipo di tabella definito dall'utente per il parametro con valori di tabella non è presente nello schema predefinito corrente per la connessione. In base al supporto server, il consumer può specificare anche informazioni facoltative sui metadati, ad esempio l'ordine delle colonne, e indicare che tutte le righe di determinate colonne includano i valori predefiniti.  
  
 Per specificare un parametro con valori di tabella, il consumer chiama ISSCommandWithParameter:: separameterinfo e, facoltativamente, chiama ISSCommandWithParameters:: SetParameterProperties. Per un parametro con valori di tabella, il campo *pwszDataSourceType* nella struttura DBPARAMBINDINFO presenta un valore pari a DBTYPE_TABLE. Il campo *ulParamSize* è impostato su ~0 per indicare che la lunghezza non è nota. Le proprietà specifiche per i parametri con valori di tabella, ad esempio il nome dello schema, il nome del tipo, l'ordine delle colonne e le colonne predefinite, possono essere impostate tramite ISSCommandWithParameters:: SetParameterProperties.  
  
## <a name="table-valued-parameter-binding"></a>Associazione del parametro con valori di tabella  
 Un parametro con valori di tabella può essere qualsiasi oggetto set di righe. Il provider legge da questo oggetto mentre invia parametri con valori di tabella al server durante l'esecuzione.  
  
 Per associare il parametro con valori di tabella, il consumer chiama IAccessor:: CreateAccessor. Il campo *wType* della struttura DBBINDING per il parametro con valori di tabella è impostato su DBTYPE_TABLE. Il membro *pObject* della struttura DBBINDING è non NULL e il membro *iid* di *pObject* è impostato su IID_IRowset o su qualsiasi altra interfaccia dell'oggetto set di righe del parametro con valori di tabella. I campi restanti nella struttura DBBINDING devono essere impostati con la stessa modalità con cui sono impostati per i BLOB di flusso.  
  
 Alle associazioni relative al parametro con valori di tabella e all'oggetto set di righe associato a un parametro con valori di tabella vengono applicate le restrizioni seguenti:  
  
-   Gli unici valori di stato consentiti per i dati di colonna dei set di righe di parametri con valori di tabella sono DBSTATUS_S_ISNULL e DBSTATUS_S_OK. DBSTATUS_S_DEFAULT genera un errore e il valore di stato associato viene impostato su DBSTATUS_E_BADSTATUS.  
  
-   Un parametro con valori di tabella può essere contrassegnato dallo stato DBSTATUS_S_DEFAULT. Gli unici valori validi sono DBSTATUS_S_DEFAULT e DBSTATUS_S_OK. Quando lo stato è impostato su DBSTATUS_S_DEFAULT, il valore del parametro con valori di tabella corrisponde a una tabella vuota.  
  
-   Le colonne di sola lettura nei parametri con valori di tabella (colonne Identity o calcolate) devono essere contrassegnate come predefinite tramite la proprietà SSPROP_PARAM_TABLE_DEFAULT_COLUMNS. Anche le colonne che presentano un valore predefinito devono essere contrassegnate come predefinite tramite la proprietà SSPROP_PARAM_TABLE_DEFAULT_COLUMNS per far sì che il valore predefinito venga usato per i valori dei dati della colonna per un determinato parametro con valori di tabella. Il provider ignorerà i valori dei dati associati per le colonne contrassegnate come predefinite.  
  
-   I dati saranno inviati al server per le colonne con DBPROP_COL_AUTOINCREMENT o SSPROP_COL_COMPUTED, a meno che non sia impostata anche la proprietà SSPROP_PARAM_TABLE_DEFAULT.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

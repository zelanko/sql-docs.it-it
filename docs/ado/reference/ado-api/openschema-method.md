---
title: Esempio di metodo OpenSchema | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2b4df18cf783e23792b51fb2c437b82c6a8ec52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239999"
---
# <a name="openschema-method"></a>Metodo OpenSchema
Ottiene le informazioni sullo schema di database dal provider.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto che contiene le informazioni sullo schema. Il **Recordset** verrà aperto un cursore statico di sola lettura. Il *QueryType* determina le colonne visualizzate nel **Recordset**.  
  
#### <a name="parameters"></a>Parametri  
 *QueryType*  
 Eventuali [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valore che rappresenta il tipo di query di schema per l'esecuzione.  
  
 *Criteri*  
 Facoltativo. Una matrice dei vincoli di query per ognuno *QueryType* opzione, come elencato nella [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md).  
  
 *SchemaID*  
 Il GUID per una query dello schema di provider non è definito dalla specifica OLE DB. Questo parametro è obbligatorio se *QueryType* è impostata su **adSchemaProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Note  
 Il **OpenSchema** metodo restituisce autodescrittivo informazioni sull'origine dati, ad esempio quali sono le tabelle nell'origine dati, le colonne nelle tabelle e i tipi di dati supportati.  
  
 Il *QueryType* argomento è un GUID che indica le colonne (schemi) restituiti. La specifica OLE DB include un elenco completo degli schemi.  
  
 Il *criteri* argomento limita i risultati di una query di schema. *I criteri* specifica una matrice di valori che devono verificarsi in un subset di colonne, denominate colonne di vincolo, nella finestra di corrispondente **Recordset**.  
  
 La costante **adSchemaProviderSpecific** viene usato per il *QueryType* argomento se il provider definisce la propria query di schema conforme allo standard oltre a quelle elencate in precedenza. Quando questa costante viene utilizzata, il *SchemaID* argomento è necessario passare il GUID della query dello schema per l'esecuzione. Se *QueryType* è impostata su **adSchemaProviderSpecific** ma *SchemaID* non viene specificato, verrà generato un errore.  
  
 I provider non sono necessari per supportare tutte le query di schema standard OLE DB. In particolare, solo **adSchemaTables**, **adSchemaColumns**, e **adSchemaProviderTypes** necessari per la specifica OLE DB. Tuttavia, il provider non è necessario per supportare le *criteri* vincoli indicati in precedenza per le query di schema.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** il **OpenSchema** metodo non è disponibile sul lato client [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
> [!NOTE]
>  In Visual Basic, le colonne che dispongono di un intero senza segno a quattro byte (UI4 DBTYPE) nel **Recordset** restituiti dal **OpenSchema** metodo sul **connessione** oggetto non è possibile da confrontare con le altre variabili. Per altre informazioni sui tipi di dati OLE DB, vedere [tipi di dati in OLE DB (OLE DB)](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a) e [appendice a: Tipi di dati](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6) nel riferimento per programmatori OLE DB Microsoft.  
  
> [!NOTE]
>  **Visual C# /C++ gli utenti** quando non si utilizzano cursori sul lato client, il recupero "ORDINAL_POSITION" di uno schema di colonna in ADO restituisce una variante di tipo VT_R8 in MDAC 2.7, MDAC 2.8 e Windows Data Access Components (Windows DAC) 6.0, mentre il tipo utilizzato in MDAC 2.6 è VT_I4. I programmi scritti per MDAC 2.6 che rappresentano solo per una variabile variant restituito di tipo che VT_I4 otterrebbe pari a zero per ogni numero ordinale se vengono eseguiti con MDAC 2.7, MDAC 2.8 e 6.0 di Windows dell'applicazione livello dati senza alcuna modifica. Questa modifica è stata apportata perché il tipo di dati OLE DB restituisce DBTYPE_UI4 e il tipo VT_I4 firmato non c'è spazio sufficiente per contenere tutti i valori possibili senza troncamenti eventualmente in corso e causando una perdita di dati.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo OpenSchema (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [Esempio di metodo OpenSchema (VC + +)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Metodo Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Appendice a: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)

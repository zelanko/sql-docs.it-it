---
description: Provider Microsoft OLE DB per Microsoft Active Directory Service
title: Provider Microsoft OLE DB per Microsoft Active Directory Service | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: rothja
ms.author: jroth
ms.openlocfilehash: f5a2513d8440adedaa0faecae2b544c9ea99bef0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454123"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Provider Microsoft OLE DB per Microsoft Active Directory Service
Il provider ADSI (Active Directory Service Interfaces) consente a ADO di connettersi a servizi di directory eterogenei tramite ADSI. Ciò consente alle applicazioni ADO di accedere in sola lettura ai servizi directory di Microsoft Windows NT 4,0 e Microsoft Windows 2000, oltre a qualsiasi servizio di directory compatibile con LDAP e a servizi directory di Novell. ADSI si basa su un modello di provider, in modo che se è presente un nuovo provider che concede l'accesso a un'altra directory, l'applicazione ADO sarà in grado di accedervi facilmente. Il provider ADSI è a thread libero e il formato Unicode è abilitato.  
  
## <a name="connection-string-parameters"></a>Parametri della stringa di connessione  
 Per connettersi a questo provider, impostare l'argomento del **provider** della proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) su quanto segue:  
  
```vb
ADSDSOObject  
```  
  
 La lettura della proprietà del [provider](../../../ado/reference/ado-api/provider-property-ado.md) restituirà anche questa stringa.  
  
## <a name="typical-connection-string"></a>Stringa di connessione tipica  
 Una stringa di connessione tipica per questo provider è la seguente:  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 La stringa è costituita dalle parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|**Provider**|Specifica il provider di OLE DB per Active Directory servizio.|  
|**ID utente**|Specifica il nome utente. Se questa parola chiave viene omessa, viene utilizzato l'account di accesso corrente.|  
|**Password**|Specifica la password dell'utente. Se questa parola chiave viene omessa. Viene quindi usato l'account di accesso corrente.|  
  
> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = Yes** o **Integrated Security = SSPI** anziché le informazioni relative a ID utente e password nella stringa di connessione.  
  
## <a name="command-text"></a>Testo comando  
 Una stringa di testo del comando in quattro parti è riconosciuta dal provider nella sintassi seguente:  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*Radice*|Indica l'oggetto **ADsPath** da cui iniziare la ricerca (ovvero la radice della ricerca).|  
|*Filter*|Indica il filtro di ricerca nel formato RFC 1960.|  
|*Attributes (Attributi)*|Indica un elenco delimitato da virgole di attributi da restituire.|  
|*Ambito*|Facoltativo. **Stringa** che specifica l'ambito della ricerca. Può essere uno dei valori seguenti:<br /><br /> -Base: Cerca solo l'oggetto di base (radice della ricerca).<br />-Unlivello-Cerca solo un livello.<br />-Subtree-Cerca nell'intero sottoalbero.|  
  
 Ad esempio:  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 Il provider supporta inoltre SQL SELECT per il testo del comando. Ad esempio:  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il provider non accetta stored procedure chiamate o nomi di tabella semplici (ad esempio, la proprietà [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) sarà sempre **adCmdText**). Per una descrizione più completa degli elementi di testo del comando, vedere la documentazione relativa alle interfacce del servizio Active Directory.  
  
## <a name="recordset-behavior"></a>Comportamento del recordset  
 Nelle tabelle seguenti sono elencate le funzionalità disponibili in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aperto utilizzando questo provider. È disponibile solo il tipo di cursore statico (**adOpenStatic**).  
  
 Per ulteriori informazioni sul comportamento del **Recordset** per la configurazione del provider, eseguire il metodo [Supports](../../../ado/reference/ado-api/supports-method.md) ed enumerare la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) del **Recordset** per determinare se sono presenti proprietà dinamiche specifiche del provider.  
  
 **Disponibilità delle proprietà del recordset ADO standard:**  
  
|Proprietà|Disponibilità|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lettura/scrittura|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lettura/scrittura|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Sola lettura|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|  
|[Creare un segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md)|lettura/scrittura|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lettura/scrittura|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|sempre **adUseServer come**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|sempre **adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|sempre **adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lettura/scrittura|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lettura/scrittura|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|non disponibile|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lettura/scrittura|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|Sola lettura|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lettura/scrittura|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Sola lettura|  
|[Origine](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lettura/scrittura|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|Sola lettura|  
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Sola lettura|  
  
 **Disponibilità dei metodi Recordset ADO standard:**  
  
|Metodo|Disponibile?|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|No|  
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|No|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Sì|  
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|Sì|  
|[Elimina](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sì|  
|[Spostamento](../../../ado/reference/ado-api/move-method-ado.md)|Sì|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sì|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sì|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sì|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sì|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sì|  
|[Apri](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sì|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sì|  
|[Risincronizza](../../../ado/reference/ado-api/resync-method.md)|Sì|  
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Sì|  
|[Aggiornamento](../../../ado/reference/ado-api/update-method.md)|No|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|  
  
 Per ulteriori informazioni su ADSI e sulle specifiche del provider, fare riferimento alla documentazione relativa alle interfacce del servizio Active Directory oppure visitare la pagina Web ADSI.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Proprietà ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Proprietà provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Oggetto recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)

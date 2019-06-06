---
title: Provider Microsoft OLE DB per il servizio Microsoft Active Directory | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: acd7c73926e996100511569df3a5693068894b10
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702728"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Provider Microsoft OLE DB per il servizio Microsoft Active Directory
Il Provider di Active Directory Service Interfaces (ADSI) consente di ADO per connettersi ai servizi eterogenei directory tramite ADSI. In questo modo le applicazioni ADO accesso in lettura per i servizi directory di Microsoft Windows NT 4.0 e Microsoft Windows 2000, oltre a qualsiasi servizio di directory compatibile con LDAP e Novell Directory Services. ADSI è basato su un modello di provider, in modo che se è presente un nuovo provider concedere l'accesso a un'altra directory, l'applicazione ADO sarà in grado di accedervi facilmente. Il provider ADSI è a thread libero e abilitata per Unicode.  
  
## <a name="connection-string-parameters"></a>Parametri della stringa di connessione  
 Per connettersi a questo provider, impostare il **Provider** argomento delle [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà al seguente:  
  
```vb
ADSDSOObject  
```  
  
 Leggere il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà restituirà anche questa stringa.  
  
## <a name="typical-connection-string"></a>Stringa di connessione tipica  
 Una stringa di connessione tipica per questo provider è il seguente:  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 La stringa è costituito da parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|**Provider**|Specifica il Provider OLE DB per il servizio Active Directory.|  
|**ID utente**|Specifica il nome utente. Se questa parola chiave viene omesso, viene usato l'account di accesso corrente.|  
|**Password**|Specifica la password dell'utente. Se si omette questa parola chiave. Viene quindi usato l'account di accesso corrente.|  
  
> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = yes** oppure **Integrated Security = SSPI** anziché un ID utente e password informazioni nella stringa di connessione.  
  
## <a name="command-text"></a>Testo comando  
 Una stringa di testo di comando in quattro parti è riconosciuta dal provider nella sintassi seguente:  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*Root*|Indica la **ADsPath** oggetto da cui iniziare la ricerca (vale a dire, la radice della ricerca).|  
|*Filter*|Indica il filtro di ricerca nel formato RFC 1960.|  
|*Attributi*|Indica un elenco delimitato da virgole di attributi da restituire.|  
|*Ambito*|Facoltativo. Oggetto **stringa** che specifica l'ambito della ricerca. I possibili valori sono i seguenti:<br /><br /> -Base - eseguire la ricerca solo l'oggetto di base (radice della ricerca).<br />-UnLivello - ricerca di un solo livello.<br />-Sottoalbero, eseguire una ricerca nell'intero sottoalbero.|  
  
 Ad esempio:  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 Il provider supporta anche SQL SELECT per il testo del comando. Ad esempio:  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Note  
 Il provider non accetta chiamate di stored procedure o i nomi di tabella semplice (ad esempio, il [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) proprietà sarà sempre **adCmdText**). Vedere la documentazione di Active Directory Service Interfaces per una descrizione più completa degli elementi di testo di comando.  
  
## <a name="recordset-behavior"></a>Comportamento dell'oggetto Recordset  
 Le tabelle seguenti elencano le funzionalità disponibili in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto aperto utilizzando questo provider. Solo il tipo di cursore statico (**adOpenStatic**) è disponibile.  
  
 Per altre informazioni sulle **Recordset** comportamento per la configurazione del provider, eseguire il [supporta](../../../ado/reference/ado-api/supports-method.md) metodo ed enumerare il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta del  **Recordset** per determinare se sono presenti proprietà dinamiche specifiche del provider.  
  
 **Disponibilità di proprietà Recordset ADO standard:**  
  
|Proprietà|Disponibilità|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lettura/scrittura|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lettura/scrittura|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Sola lettura|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|  
|[Segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md)|lettura/scrittura|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lettura/scrittura|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Sola lettura|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lettura/scrittura|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lettura/scrittura|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|non disponibile|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lettura/scrittura|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|Sola lettura|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lettura/scrittura|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Sola lettura|  
|[Origine](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lettura/scrittura|  
|[Stato](../../../ado/reference/ado-api/state-property-ado.md)|Sola lettura|  
|[Stato](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Sola lettura|  
  
 **Disponibilità di metodi di Recordset ADO standard:**  
  
|Metodo|Disponibile?|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|no|  
|[Annulla](../../../ado/reference/ado-api/cancel-method-ado.md)|No|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Yes|  
|[Chiudi](../../../ado/reference/ado-api/close-method-ado.md)|Yes|  
|[Elimina](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Yes|  
|[Sposta](../../../ado/reference/ado-api/move-method-ado.md)|Yes|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Yes|  
|[Aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Yes|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Yes|  
|[Resync](../../../ado/reference/ado-api/resync-method.md)|Yes|  
|[Supporti](../../../ado/reference/ado-api/supports-method.md)|Yes|  
|[Update](../../../ado/reference/ado-api/update-method.md)|No|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|  
  
 Per altre informazioni su ADSI e le specifiche del provider, consultare la documentazione di Active Directory Service Interfaces o visitare la pagina Web ADSI.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Proprietà ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Proprietà del provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)

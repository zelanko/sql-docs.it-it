---
title: Metodo Open (connessione ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931936"
---
# <a name="open-method-ado-connection"></a>Metodo Open (Connection - ADO)
Apre una connessione a un'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 facoltativo. Oggetto **stringa** valore contenente le informazioni di connessione. Vedere le [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà per informazioni dettagliate sulle impostazioni valide.  
  
 *UserID*  
 facoltativo. Oggetto **stringa** valore che contiene un nome utente da usare quando si stabilisce la connessione.  
  
 *Password*  
 facoltativo. Oggetto **stringa** valore contenente una password da usare quando si stabilisce la connessione.  
  
 *Opzioni*  
 facoltativo. Oggetto [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) valore che determina se questo metodo deve restituire dopo (in modo sincrono) o prima (in modo asincrono) viene stabilita la connessione.  
  
## <a name="remarks"></a>Note  
 Usando il **aperto** metodo su un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto stabilisce la connessione fisica a un'origine dati. Dopo che questo metodo viene completato correttamente, viene stabilita la connessione ed è possibile eseguire comandi su di esso ed elaborare i risultati.  
  
 Usare l'opzione facoltativa *ConnectionString* argomento per specificare una stringa di connessione contenente una serie di *argomento* *= valore* istruzioni separate da punti e virgola o un oggetto risorsa file o directory identificata da un URL. Il **ConnectionString** proprietà eredita automaticamente il valore usato per il *ConnectionString* argomento. Pertanto, è possibile impostare il **ConnectionString** proprietà delle **connessione** dell'oggetto prima di aprirlo oppure usare il *ConnectionString* argomento per impostare o eseguire l'override i parametri di connessione corrente durante la **aperto** chiamata al metodo.  
  
 Se si passa l'utente e password informazioni entrambi nel *ConnectionString* argomento e in facoltativo *UserID* e *Password* argomenti, il *UserID*  e *Password* argomenti sostituiranno i valori specificati nella *ConnectionString*.  
  
 Quando aver concluso le operazioni su un oggetto aperto **connessione**, utilizzare il [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) metodo da liberare eventuali risorse di sistema associate. Chiusura di un oggetto senza rimuoverlo dalla memoria. è possibile modificare le impostazioni delle proprietà e usare la **aprire** metodo aprirlo più tardi. Per eliminare completamente un oggetto dalla memoria, impostare la variabile oggetto *Nothing*.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **connessione** oggetto, il **Open** metodo non stabilisce una connessione al server fino a un [Recordset ](../../../ado/reference/ado-api/recordset-object-ado.md) viene aperto nel **connessione** oggetto.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Esempio di metodi Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Esempio di metodi Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Metodo Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Metodo Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)

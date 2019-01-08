---
title: La scrittura di un gestore personalizzato | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daddb9057775e1f098754dd2a331c1dc77194d10
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53214010"
---
# <a name="writing-your-own-customized-handler"></a>Scrittura di un gestore personalizzato
È possibile scrivere un gestore personalizzato se sei un amministratore di server IIS che richiede l'impostazione predefinita il supporto di servizi desktop remoto, ma un maggior controllo sulle richieste degli utenti e diritti di accesso.  
  
 MSDFMAP. Gestore implementa il **IDataFactoryHandler** interfaccia.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interfaccia IDataFactoryHandler  
 Questa interfaccia dispone di due metodi **GetRecordset** e **Riconnetti**. Entrambi i metodi richiedono che il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) impostata su **adUseClient**.  
  
 Entrambi i metodi accettano gli argomenti visualizzati dopo la prima virgola nel "**gestore =**" parola chiave. Ad esempio, `"Handler=progid,arg1,arg2;"` passerà una stringa dell'argomento `"arg1,arg2"`, e `"Handler=progid"` passa un argomento null.  
  
## <a name="getrecordset-method"></a>Metodo GetRecordset  
 Questo metodo esegue query sull'origine dati e crea un nuovo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) utilizzando gli argomenti specificati. Il **Recordset** deve essere aperta con **adLockBatchOptimistic** e non deve essere aperto in modo asincrono.  
  
### <a name="arguments"></a>Argomenti  
 ***Conn*** la stringa di connessione.  
  
 ***args*** gli argomenti per il gestore.  
  
 ***query*** il testo del comando per eseguire una query.  
  
 ***ppRS*** il puntatore in cui la **Recordset** devono essere restituiti.  
  
## <a name="reconnect-method"></a>Ristabilire la connessione (metodo)  
 Questo metodo aggiorna l'origine dati. Crea una nuova [Connection](../../../ado/reference/ado-api/connection-object-ado.md) oggetto e consente di collegare il determinato **Recordset**.  
  
### <a name="arguments"></a>Argomenti  
 ***Conn*** la stringa di connessione.  
  
 ***args*** gli argomenti per il gestore.  
  
 ***le richieste pull*** un' **Recordset** oggetto.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 Si tratta della definizione di interfaccia per **IDataFactoryHandler** che viene visualizzato nella **msdfhdl** file.  
  
```cpp
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione sulla connessione del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sezione Log File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sezione SQL del File di personalizzazione](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sezione UserList del File personalizzazione](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Impostazioni Client richieste](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Informazioni sul file di personalizzazione](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)



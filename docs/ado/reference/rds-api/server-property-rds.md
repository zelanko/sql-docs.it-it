---
title: Proprietà server (Servizi Desktop remoto) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d196a60986734c5717be9711af1fa28accee414
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963479"
---
# <a name="server-property-rds"></a>Proprietà Server (Servizi Desktop remoto)
Indica il protocollo di nome e la comunicazione Internet Information Services (IIS).  
  
 È possibile impostare il **Server** in fase di progettazione nei tag dell'oggetto di proprietà di[Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto, o in fase di esecuzione nel codice di script.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 **HTTP**  
  
 Sintassi in fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 Sintassi in fase di esecuzione  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 Sintassi in fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Sintassi in fase di esecuzione  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Sintassi in fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 Sintassi in fase di esecuzione  
  
```  
  
DataControl.Server="computername"  
```  
  
 **In-process**  
  
 Sintassi in fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Sintassi in fase di esecuzione  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parametri  
 *awebsrvr*o *computername*  
 Oggetto **stringa** valore che contiene un Internet o intranet percorso o nome del computer, se il server è in un computer remoto; oppure, una stringa vuota se il server nel computer locale.  
  
 *port*  
 facoltativo. Una porta che viene usata per connettersi a un server che esegue IIS. Il numero di porta è impostato in Internet Explorer (nelle **visualizzazione** menu, fare clic su **opzioni**e quindi selezionare il **connessione** scheda) o in IIS.  
  
 *DataControl*  
 Una variabile oggetto che rappresenta un **Servizi Desktop remoto. DataControl** oggetto.  
  
## <a name="remarks"></a>Note  
 Il server è la posizione in cui il **Servizi Desktop remoto. DataControl** elaborazione richiesta (vale a dire, una query o aggiornamento). Per impostazione predefinita, tutte le richieste vengono elaborate le [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto [MSDFMAP. Gestore](../../../ado/guide/remote-data-service/datafactory-customization.md) componente, e [MSDFMAP. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) file nel server specificato. Tenere presente che quando si modificano i server per risolvere le impostazioni nel vecchio e nuovo **MSDFMAP. INI** file. Incompatibilità possono causare richieste con esito positivo su un server a non riuscire in un altro. Se la proprietà del Server è impostata su una stringa vuota "", questi oggetti verranno utilizzati nel computer locale.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà server (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Proprietà Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Proprietà SQL](../../../ado/reference/rds-api/sql-property.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



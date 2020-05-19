---
title: Proprietà Server (RDS) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5cd4f578a8146a8fa7d45dcfd8e2b58f795def13
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750858"
---
# <a name="server-property-rds"></a>Proprietà Server (Servizi Desktop remoto)
Indica il nome del Internet Information Services (IIS) e il protocollo di comunicazione.  
  
 È possibile impostare la proprietà **Server** in fase di progettazione nei tag Object di[RDS. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) o in fase di esecuzione nel codice di scripting.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 **HTTP**  
  
 Sintassi della fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 Sintassi della fase di esecuzione  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 Sintassi della fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Sintassi della fase di esecuzione  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Sintassi della fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 Sintassi della fase di esecuzione  
  
```  
  
DataControl.Server="computername"  
```  
  
 **In-process**  
  
 Sintassi della fase di progettazione  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Sintassi della fase di esecuzione  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parametri  
 *awebsrvr*o *nomecomputer*  
 Valore **stringa** che contiene un percorso Internet o Intranet oppure un nome computer se il server si trova in un computer remoto; oppure una stringa vuota se il server si trova nel computer locale.  
  
 *porta*  
 Facoltativa. Porta utilizzata per la connessione a un server che esegue IIS. Il numero di porta è impostato in Internet Explorer. scegliere **Opzioni**dal menu **Visualizza** , quindi selezionare la scheda **connessione** oppure in IIS.  
  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto **. Oggetto DataControl** .  
  
## <a name="remarks"></a>Commenti  
 Il server è il percorso in cui **RDS. **Viene elaborata la richiesta DataControl, ovvero una query o un aggiornamento. Per impostazione predefinita, tutte le richieste vengono elaborate dall'oggetto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) , [MSDFMAP. ](../../../ado/guide/remote-data-service/datafactory-customization.md)Componente del gestore e [MSDFMAP. File INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) nel server specificato. Tenere presente che quando si modificano i server per riconciliare le impostazioni nel vecchio e nel nuovo **MSDFMAP. File INI** . Le incompatibilità possono causare errori delle richieste che hanno esito positivo su un server in un altro. Se la proprietà server è impostata sulla stringa vuota "", questi oggetti verranno utilizzati nel computer locale.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà server (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Proprietà Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Proprietà SQL](../../../ado/reference/rds-api/sql-property.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



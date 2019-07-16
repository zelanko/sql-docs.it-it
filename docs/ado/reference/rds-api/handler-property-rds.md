---
title: Proprietà Handler (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a7423879b8263d87575d913c4863143faf3573e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963993"
---
# <a name="handler-property-rds"></a>Proprietà Handler (Servizi Desktop remoto)
Indica il nome di un programma di personalizzazione lato server (gestore) che estende le funzionalità dei [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)ed eventuali parametri utilizzati per il *gestore*.  
  
 **Si applica a:** [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *String*  
 Oggetto **stringa** valore contenente il nome del gestore e parametri, tutti separati da virgole (ad esempio `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Note  
 Questa proprietà supporta [personalizzazione](../../../ado/guide/remote-data-service/datafactory-customization.md), una funzionalità che richiede l'impostazione di [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient**.  
  
 Il nome del gestore e i relativi parametri, se presenti, sono separati da virgole (","). Verrà generato un comportamento imprevedibile se un punto e virgola (";"), viene visualizzato in un punto qualsiasi all'interno *stringa*. È possibile scrivere un gestore personalizzato, purché supportino la **IDataFactoryHandler** interfaccia.  
  
 Il nome del gestore predefinito è **MSDFMAP. Gestore**, e il relativo parametro predefinito è un file di personalizzazione denominato **MSDFMAP. INI**. Usare questa proprietà per richiamare i file di personalizzazione alternativo creati dall'amministratore del server.  
  
 L'alternativa all'impostazione di **gestore** proprietà consiste nello specificare parametri in e un gestore il [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà; vale a dire, "**gestore =** _NomeGestore, parameter1, parameter2,...._ ".  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Handler (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [Personalizzazione di DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



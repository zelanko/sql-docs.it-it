---
title: Metodo CreateObject (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d220a9abc0e2dc72d7ab65306b514a9925b4fc43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281062"
---
# <a name="createobject-method-rds"></a>Metodo CreateObject (Servizi Desktop remoto)
Crea il proxy per l'oggetto business di destinazione e restituisce un puntatore a esso. I proxy pacchetti esegue il marshalling dei dati e per lo stub del lato server per le comunicazioni con l'oggetto business alla invierà le richieste e i dati tramite Internet. Per gli oggetti di componente in-process, non vengono utilizzati proxy, viene fornito solo un puntatore all'oggetto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
 Servizio dati remoto supporta i protocolli seguenti: HTTP, HTTPS (HTTP over Secure Socket Layer), DCOM e in-process.  
  
|Protocol|Sintassi|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|In-Process|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Parametri  
 *Oggetto*  
 Una variabile oggetto che restituisce un oggetto che rappresenta il tipo specificato nel *ProgID*.  
  
 *DataSpace*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetto utilizzato per creare un'istanza del nuovo oggetto.  
  
 *ProgID*  
 Oggetto **stringa** valore che contiene l'identificatore a livello di codice che specifica un oggetto business sul lato server che implementa le regole di business dell'applicazione.  
  
 *awebsrvr* o *computername*  
 Oggetto **stringa** valore che rappresenta un URL che identifica il server Web Internet Information Services (IIS) in cui viene creata un'istanza dell'oggetto business server.  
  
## <a name="remarks"></a>Note  
 Il *protocollo HTTP* è il protocollo Web standard; *HTTPS* è un protocollo Web sicuro. Usare la *protocollo DCOM* quando si esegue una rete locale senza HTTP. Il *in-process* protocollo è una libreria di collegamento dinamico (DLL) locale, non usa una rete.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataSpace (Servizi Desktop remoto)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto DataFactory, metodo di Query ed esempio metodo CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [Oggetto DataSpace e metodo CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Metodo CreateRecordset (Servizi Desktop remoto)](../../../ado/reference/rds-api/createrecordset-method-rds.md)



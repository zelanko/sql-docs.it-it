---
title: Proprietà Connect (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba8b5aa1f59fbb161da878f5930f83d2f6ff0bdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964562"
---
# <a name="connect-property-rds"></a>Proprietà Connect (Servizi Desktop remoto)
Indica il nome del database da cui vengono eseguite le operazioni di query e aggiornamento.  
  
 È possibile impostare il **Connect** proprietà in fase di progettazione nel [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) tag di oggetti dell'oggetto, o in fase di esecuzione di script di codice (ad esempio, VBScript).  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Una stringa di connessione valida. Per informazioni più generali sulle stringhe di connessione, vedere la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà o la documentazione del provider.  
  
> [!NOTE]
>  Se si specifica MS Remote come il provider per il **Servizi Desktop remoto. DataControl** creerebbe un scenario a quattro livelli. Scenari di maggiori di tre livelli non sono stati testati e non sono necessari.  
  
 *DataControl*  
 Una variabile oggetto che rappresenta un **Servizi Desktop remoto. DataControl** oggetto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [La connessione di esempio di proprietà (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Metodo query (Servizi Desktop remoto)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Metodo Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



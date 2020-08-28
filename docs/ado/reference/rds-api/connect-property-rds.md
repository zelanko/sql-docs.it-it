---
description: Proprietà Connect (Servizi Desktop remoto)
title: Proprietà Connect (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: rothja
ms.author: jroth
ms.openlocfilehash: e956a86333479320fe18114705148bad77ea0440
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982672"
---
# <a name="connect-property-rds"></a>Proprietà Connect (Servizi Desktop remoto)
Indica il nome del database da cui vengono eseguite le operazioni di aggiornamento e query.  
  
 È possibile impostare la proprietà di **connessione** in fase di progettazione in Servizi Desktop remoto [. ](./datacontrol-object-rds.md) Tag Object dell'oggetto DataControl oppure in fase di esecuzione nel codice di scripting, ad esempio VBScript.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa di connessione valida. Per informazioni più generali sulle stringhe di connessione, vedere la proprietà [ConnectionString](../ado-api/connectionstring-property-ado.md) o la documentazione del provider.  
  
> [!NOTE]
>  Specificando MS Remote come provider per **RDS. DataControl** creerebbe uno scenario a quattro livelli. Gli scenari di dimensioni superiori a tre livelli non sono stati testati e non dovrebbero essere necessari.  
  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto **. Oggetto DataControl** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Connect (VBScript)](./connect-property-example-vbscript.md)   
 [Metodo query (RDS)](./query-method-rds.md)   
 [Metodo Refresh (RDS)](./refresh-method-rds.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](./submitchanges-method-rds.md)
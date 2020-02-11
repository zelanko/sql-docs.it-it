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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964562"
---
# <a name="connect-property-rds"></a>Proprietà Connect (Servizi Desktop remoto)
Indica il nome del database da cui vengono eseguite le operazioni di aggiornamento e query.  
  
 È possibile impostare la proprietà di **connessione** in fase di progettazione in Servizi Desktop remoto [. ](../../../ado/reference/rds-api/datacontrol-object-rds.md)Tag Object dell'oggetto DataControl oppure in fase di esecuzione nel codice di scripting, ad esempio VBScript.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa di connessione valida. Per informazioni più generali sulle stringhe di connessione, vedere la proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) o la documentazione del provider.  
  
> [!NOTE]
>  Specificando MS Remote come provider per **RDS. DataControl** creerebbe uno scenario a quattro livelli. Gli scenari di dimensioni superiori a tre livelli non sono stati testati e non dovrebbero essere necessari.  
  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto **. Oggetto DataControl** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Connect (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Metodo query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Metodo Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Metodo SubmitChanges (Servizi Desktop remoto)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



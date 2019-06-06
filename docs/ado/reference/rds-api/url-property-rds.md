---
title: Proprietà URL (Servizi Desktop remoto) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d5c1975e72a90defc15e4fcb41f0cfe44a714dc8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697194"
---
# <a name="url-property-rds"></a>Proprietà URL (Servizi Desktop remoto)
Indica una stringa che contiene un URL relativo o assoluto.  
  
 È possibile impostare il **URL** proprietà in fase di progettazione nel [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto di tag, o in fase di esecuzione nel codice di script.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parametri  
 *Server*  
 Oggetto **stringa** valore che contiene un URL valido.  
  
 *DataControl*  
 Una variabile oggetto che rappresenta un **DataControl** oggetto.  
  
## <a name="remarks"></a>Note  
 In genere, l'URL identifica un file Active Server Page (ASP) che può generare e restituire un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Di conseguenza, l'utente può ottenere un **Recordset** senza dover richiamare il server-side [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) dell'oggetto oppure programmare un oggetto business personalizzato.  
  
 Se il **URL** proprietà è stata impostata, [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) invierà le modifiche nel percorso specificato dall'URL.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà URL (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)



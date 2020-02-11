---
title: Proprietà URL (RDS) | Microsoft Docs
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
ms.openlocfilehash: c88b8029ee5d96986cf9b366bd8faee53ca1393b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963222"
---
# <a name="url-property-rds"></a>Proprietà URL (Servizi Desktop remoto)
Indica una stringa che contiene un URL relativo o assoluto.  
  
 È possibile impostare la proprietà **URL** in fase di progettazione nel tag Object dell'oggetto [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oppure in fase di esecuzione nel codice di scripting.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parametri  
 *Server*  
 Valore **stringa** che contiene un URL valido.  
  
 *DataControl*  
 Variabile oggetto che rappresenta un oggetto **DataControl** .  
  
## <a name="remarks"></a>Osservazioni  
 In genere, l'URL identifica un file di pagina Active Server (. asp) che può produrre e restituire un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Pertanto, l'utente può ottenere un **Recordset** senza dover richiamare l'oggetto [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) sul lato server oppure programmare un oggetto business personalizzato.  
  
 Se è stata impostata la proprietà **URL** , [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) invierà le modifiche al percorso specificato dall'URL.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio della proprietà URL (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)



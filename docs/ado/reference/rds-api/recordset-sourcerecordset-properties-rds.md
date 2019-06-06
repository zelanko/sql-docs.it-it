---
title: Proprietà Recordset e SourceRecordset (Servizi Desktop remoto) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3ec8dbdce6a813663f7909adb2a9ec1edacee9b1
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718759"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Proprietà Recordset e SourceRecordset (Servizi Desktop remoto)
Indica la **Recordset** oggetto restituito da un oggetto business personalizzato.  
  
 **Si applica a:** [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *Recordset*  
 Una variabile oggetto che rappresenta un **Recordset** oggetto.  
  
## <a name="remarks"></a>Note  
 È possibile impostare il **SourceRecordset** proprietà di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) restituito da un oggetto business personalizzato.  
  
 Queste proprietà consentono a un'applicazione per gestire il processo di associazione tramite un processo personalizzato. Ricevono un set di righe inserito in una **Recordset** in modo che sia possibile interagire direttamente con il **Recordset**, eseguire azioni quali l'impostazione delle proprietà o l'iterazione attraverso la **Recordset** .  
  
 È possibile impostare il **SourceRecordset** proprietà o lettura il **Recordset** proprietà in fase di esecuzione nel codice di script.  
  
 **SourceRecordset** è una proprietà di sola scrittura, in contrasto con le **Recordset** proprietà, ovvero una proprietà di sola lettura.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Recordset e SourceRecordset (esempio di proprietà (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [Esempio di metodo CreateRecordset (Servizi Desktop remoto)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Metodo Query (Servizi Desktop remoto)](../../../ado/reference/rds-api/query-method-rds.md)



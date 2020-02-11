---
title: Metodo ConvertToString (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71e50c4f611342c8e06687c47ab1c45fb60974ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964570"
---
# <a name="converttostring-method-rds"></a>Metodo ConvertToString (Servizi Desktop remoto)
Converte un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in una stringa MIME che rappresenta i dati del recordset.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataFactory*  
 Variabile oggetto che rappresenta un oggetto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *recordset*  
 Variabile oggetto che rappresenta un oggetto **Recordset** .  
  
## <a name="remarks"></a>Osservazioni  
 Con i file ASP, usare **ConvertToString** per incorporare il **Recordset** in una pagina HTML generata sul server per il trasporto in un computer client.  
  
 **ConvertToString** carica innanzitutto il **Recordset** nelle tabelle dei servizi del cursore e quindi genera un flusso in formato MIME.  
  
 Nel client, Remote Data Service può convertire di nuovo la stringa MIME in un **Recordset**completamente funzionante. Funziona bene per gestire meno di 400 righe di dati con una larghezza non superiore a 1024 byte per riga. Non è consigliabile usarlo per il flusso di dati BLOB e set di risultati di grandi dimensioni tramite HTTP. Sulla stringa non viene eseguita alcuna compressione di rete, quindi i set di dati di dimensioni molto grandi impiegheranno molto tempo per il trasporto su HTTP rispetto al formato Tablegram ottimizzato per la rete definito e distribuito da Remote Data Service come formato del protocollo di trasporto nativo.  
  
> [!NOTE]
>  Se si usano Active Server pagine per incorporare la stringa MIME risultante in una pagina HTML del client, tenere presente che le versioni di VBScript precedenti alla versione 2,0 limitano le dimensioni della stringa a 32K. Se questo limite viene superato, viene restituito un errore. Quando si usa l'incorporamento MIME tramite i file ASP, l'ambito della query è relativamente piccolo. Per risolvere il problema, scaricare la versione più recente di VBScript dal sito Web Microsoft Windows Script Technologies.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo ConvertToString (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [Esempio del metodo ConvertToString (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)



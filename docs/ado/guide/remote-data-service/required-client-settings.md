---
description: Impostazioni obbligatorie dei client
title: Impostazioni client obbligatorie | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: rothja
ms.author: jroth
ms.openlocfilehash: a68ad96d6573ba6f3f61eb993d63d181939590a7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977762"
---
# <a name="required-client-settings"></a>Impostazioni obbligatorie dei client
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Specificare le impostazioni seguenti per usare un gestore di **DataFactory** personalizzato.  
  
-   Specificare "provider = MS Remote" nella proprietà dell' [oggetto Connection (ADO)](../../reference/ado-api/connection-object-ado.md) Object [provider Property (ADO)](../../reference/ado-api/provider-property-ado.md) o nella **stringa di connessione dell'oggetto Connection "** **provider**=".  
  
-   Impostare la proprietà [CursorLocation (ADO)](../../reference/ado-api/cursorlocation-property-ado.md) su **adUseClient**.  
  
-   Specificare il nome del gestore da utilizzare nella proprietà del **gestore** dell'oggetto [datacontrollo (RDS)](../../reference/rds-api/datacontrol-object-rds.md) o nella stringa di connessione dell'oggetto [Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md) "**handler**=". Non è possibile impostare il gestore nella stringa di connessione dell'oggetto **connessione** .  
  
 RDS fornisce un gestore predefinito sul server denominato **MSDFMAP. Gestore**. Il file di personalizzazione predefinito è denominato MSDFMAP.INI.  
  
 **Esempio**  
  
 Si supponga che le sezioni seguenti in **MSDFMAP.INI** e il nome dell'origine dati, AdvWorks, siano state definite in precedenza:  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 I frammenti di codice seguenti sono scritti in Visual Basic:  
  
## <a name="rdsdatacontrol-version"></a>RDS. Versione di DataControl  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>Versione recordset  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 Specificare la proprietà o la parola chiave [handler (RDS)](../../reference/rds-api/handler-property-rds.md) ; Proprietà o parola chiave del [provider (ADO)](../../reference/ado-api/provider-property-ado.md) ; e gli identificatori *CustomerByID* e *CustomerDatabase* . Aprire quindi l'oggetto **Recordset**  
  
 RS. Aprire "CustomerById (4)", "Handler = MSDFMAP. Gestore; "& _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sezione connessione file di personalizzazione](./customization-file-connect-section.md)   
 [Sezione SQL del file di personalizzazione](./customization-file-sql-section.md)   
 [Sezione utenti del file di personalizzazione](./customization-file-userlist-section.md)   
 [Personalizzazione di datafactory](./datafactory-customization.md)   
 [Impostazioni client obbligatorie]()   
 [Informazioni sul file di personalizzazione](./understanding-the-customization-file.md)   
 [Scrittura di un gestore personalizzato](./writing-your-own-customized-handler.md)
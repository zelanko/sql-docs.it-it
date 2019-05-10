---
title: sp_OAGetErrorInfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2f4ab09693234d72890524628f4def5afcf447ef
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2019
ms.locfileid: "65450075"
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ottiene informazioni sull'errore di automazione OLE.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>Argomenti  
 *objecttoken*  
 È il token di oggetto di un oggetto OLE creato in precedenza tramite **sp_OACreate** oppure valore NULL. Se *vengono restituite le* è specificato, vengono restituite informazioni sull'errore per l'oggetto. Se viene specificato NULL, vengono restituite le informazioni sull'errore relative all'intero batch.  
  
 _source_ **OUTPUT**  
 Origine delle informazioni sull'errore. Se specificato, deve essere una variabile locale **char**, **nchar**, **varchar**, oppure **nvarchar** variabile. Se necessario, il valore restituito viene troncato in base alla dimensione della variabile locale.  
  
 _Descrizione_ **OUTPUT**  
 Descrizione dell'errore. Se specificato, deve essere una variabile locale **char**, **nchar**, **varchar**, oppure **nvarchar** variabile. Se necessario, il valore restituito viene troncato in base alla dimensione della variabile locale.  
  
 _HelpFile_ **OUTPUT**  
 File della Guida relativo all'oggetto OLE. Se specificato, deve essere una variabile locale **char**, **nchar**, **varchar**, oppure **nvarchar** variabile. Se necessario, il valore restituito viene troncato in base alla dimensione della variabile locale.  
  
 _HelpID_ **OUTPUT**  
 ID di contesto del file della Guida. Se specificato, deve essere una variabile locale **int** variabile.  
  
> [!NOTE]  
>  I parametri di questa stored procedure vengono specificati in base alla posizione, non in base al nome.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o un numero diverso da zero (esito negativo) corrispondente al valore intero del codice HRESULT restituito dall'oggetto di automazione OLE.  
  
 Per altre informazioni sui codici restituiti HRESULT, vedere [OLE Automation codici restituiti e informazioni sull'errore](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Set di risultati  
 Se non viene specificato alcun parametro di output, le informazioni sull'errore vengono restituite al client come set di risultati.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|------------------|---------------|-----------------|  
|**Errore**|**binary(4)**|Rappresentazione binaria del numero di errore.|  
|**Origine**|**nvarchar(nn)**|Origine dell'errore.|  
|**Descrizione**|**nvarchar(nn)**|Descrizione dell'errore.|  
|**HelpFile**|**nvarchar(nn)**|File della Guida relativo all'origine.|  
|**HelpID**|**int**|ID di contesto della Guida nel file di origine della Guida.|  
  
## <a name="remarks"></a>Note  
 Stored procedure di ogni chiamata a un'automazione OLE (tranne **sp_OAGetErrorInfo**) Reimposta le informazioni sull'errore, pertanto, **sp_OAGetErrorInfo** recupera informazioni sugli errori solo per i più recenti OLE Automazione di chiamata della stored procedure. Si noti che, poiché **sp_OAGetErrorInfo** non ripristina le informazioni sull'errore, può essere chiamato più volte per ottenere le informazioni sull'errore stesso.  
  
 Nella tabella seguente vengono elencati gli errori di automazione OLE e le cause più comuni.  
  
|Errore e codice HRESULT|Causa più comune|  
|-----------------------|------------------|  
|**Tipo di variabile non valido (0x80020008)**|Tipo di dati di un [!INCLUDE[tsql](../../includes/tsql-md.md)] valore passato come parametro di metodo non corrisponde il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] tipo di dati del parametro del metodo o un valore NULL è stato passato come parametro di metodo.|  
|**Nome sconosciuto (0x8002006)**|Il nome di proprietà o metodo specificato non è stato trovato per l'oggetto specificato.|  
|**Stringa della classe non valida (0x800401f3)**|Il valore ProgID o CLSID specificato non è registrato come oggetto OLE in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Server di automazione OLE personalizzati devono essere registrati prima può essere implementati con **sp_OACreate**. Questa operazione può essere eseguita tramite l'utilità Regsvr32.exe per server in-process (DLL), o la **/REGSERVER** switch della riga di comando per i server locali (.exe).|  
|**L'esecuzione del server fallita (0x80080005)**|L'oggetto OLE specificato è registrato come server OLE locale (file exe), ma non è stato possibile trovare o avviare il file.|  
|**Il modulo specificato non è stato trovato (0x8007007e)**|L'oggetto OLE specificato è registrato come server OLE in-process (file dll), ma non è stato possibile trovare o caricare il file.|  
|**Tipo non corrispondente (0x80020005)**|Il tipo di dati di una variabile locale [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzata per l'archiviazione del valore restituito di una proprietà o un metodo non corrisponde al tipo di dati di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] del valore restituito della proprietà o del metodo oppure è stato richiesto il valore restituito di una proprietà o un metodo ma non viene restituito alcun valore.|  
|**Tipo di dati o il valore del parametro 'context' di sp_OACreate non è valido. (0x8004275B)**|Il valore del parametro di contesto deve essere uno dei seguenti: 1, 4 o 5.|  
  
 Per altre informazioni sull'elaborazione dei codici restituiti HRESULT, vedere [OLE Automation codici restituiti e informazioni sull'errore](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** ruolo predefinito del server o execute direttamente su questa Stored Procedure. `Ole Automation Procedures` configurazione deve essere **abilitato** usare eventuali procedure di sistema correlate a automazione OLE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono visualizzate le informazioni sull'errore di automazione OLE.  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Automazione OLE Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script di automazione OLE di esempio](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  

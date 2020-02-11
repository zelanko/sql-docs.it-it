---
title: sp_OASetProperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OASetProperty
- sp_OASetProperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OASetProperty
ms.assetid: 0fe7d554-6b67-4d55-9d3e-4096802c47f8
author: stevestein
ms.author: sstein
ms.openlocfilehash: ecbfba038b1954565839a3d931ef96431b77f50b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008946"
---
# <a name="sp_oasetproperty-transact-sql"></a>sp_OASetProperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta una proprietà di un oggetto OLE su un nuovo valore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_OASetProperty objecttoken , propertyname , newvalue [ , index... ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *objecttoken*  
 Token dell'oggetto di un oggetto OLE creato in precedenza da **sp_OACreate**.  
  
 *propertyName*  
 Nome della proprietà dell'oggetto OLE da impostare su un nuovo valore.  
  
 *NewValue*  
 Nuovo valore della proprietà con il tipo di dati appropriato.  
  
 *index*  
 Parametro di indice. Se specificato, *index* deve essere un valore del tipo di dati appropriato.  
  
 Ad alcune proprietà sono associati parametri. Tali proprietà sono denominate proprietà indicizzate e i parametri corrispondenti sono denominati parametri di indice. A una proprietà possono essere associati più parametri di indice.  
  
> [!NOTE]  
>  I parametri di questa stored procedure vengono specificati in base alla posizione, non in base al nome.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo) o un numero diverso da zero (esito negativo) corrispondente al valore intero del codice HRESULT restituito dall'oggetto di automazione OLE.  
  
 Per ulteriori informazioni sui codici restituiti HRESULT, vedere [codici restituiti e informazioni sugli errori di automazione OLE](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o l'autorizzazione Execute direttamente in questa stored procedure. `Ole Automation Procedures`la configurazione deve essere **abilitata** per l'utilizzo di qualsiasi procedura di sistema correlata all'automazione OLE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente la `HostName` proprietà (dell'oggetto **SqlServer** creato in precedenza) viene impostata su un nuovo valore.  
  
```  
EXEC @hr = sp_OASetProperty @object, 'HostName', 'Gizmo';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di automazione OLE &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script di automazione OLE di esempio](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  

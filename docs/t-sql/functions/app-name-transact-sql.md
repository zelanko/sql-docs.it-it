---
title: APP_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21b49eb9638b4651ff52c6515f6e5f62177fc504
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843438"
---
# <a name="app_name-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Questa funzione restituisce il nome dell'applicazione per la sessione corrente, se impostato dall'applicazione.
  
> [!IMPORTANT]  
>  Il client specifica il nome dell'applicazione e `APP_NAME` non lo verifica in alcun modo. Non usare `APP_NAME` come parte di un controllo di sicurezza.  
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
Usare `APP_NAME` per distinguere le diverse applicazioni, in modo da eseguire azioni diverse per ognuna. Ad esempio, `APP_NAME` consente di distinguere diverse applicazioni e di applicare quindi un formato data diverso per ognuna. È anche possibile restituire un messaggio informativo in determinate applicazioni.
  
Per impostare un nome applicazione in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], fare clic su **Opzioni** nella finestra di dialogo **Connetti al motore di database**. Nella scheda **Parametri aggiuntivi per la connessione** fornire un attributo **app** nel formato `;app='application_name'`
  
## <a name="example"></a>Esempio  
Questo esempio controlla se l'applicazione client che ha avviato questo processo è una sessione di `SQL Server Management Studio` e specifica quindi un valore di data in formato US o ANSI.
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche
[Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
[Funzioni](../../t-sql/functions/functions.md)
  
  

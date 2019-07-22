---
title: HOST_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HOST_NAME_TSQL
- HOST_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- HOST_NAME function
- workstation names [SQL Server]
ms.assetid: 4b8b0705-c083-4b07-b954-c83ee73b2ebb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c39d56ec338be798f9e9dd5589d3a63a65b95d6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024408"
---
# <a name="hostname-transact-sql"></a>HOST_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce il nome della workstation.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HOST_NAME ()  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 Se il parametro per una funzione di sistema è facoltativo, vengono utilizzati il database, il computer host, l'utente del server o l'utente del database correnti. Le funzioni predefinite devono essere sempre seguite da parentesi.  
  
 È possibile utilizzare funzioni di sistema nell'elenco di selezione, nella clausola WHERE e in tutti i casi in cui è consentita un'espressione.  
  
> [!IMPORTANT]  
>  L'applicazione client fornisce il nome della workstation e può indicare dati non accurati. Non considerare HOST_NAME una caratteristica di sicurezza.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata una tabella che utilizza `HOST_NAME()` in una definizione `DEFAULT` per registrare il nome di workstation dei computer in cui vengono inserite righe in una tabella di registrazione degli ordini.  
  
```  
CREATE TABLE Orders  
   (OrderID     int        PRIMARY KEY,  
    CustomerID  nchar(5)   REFERENCES Customers(CustomerID),  
    Workstation nchar(30)  NOT NULL DEFAULT HOST_NAME(),  
    OrderDate   datetime   NOT NULL,  
    ShipDate    datetime   NULL,  
    ShipperID   int        NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

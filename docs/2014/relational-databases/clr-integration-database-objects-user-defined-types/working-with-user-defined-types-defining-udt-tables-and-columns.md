---
title: Definizione di tabelle e colonne UDT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [CLR integration], columns
- UDTs [CLR integration], columns
- columns [CLR integration]
- user-defined types [CLR integration], tables
- tables [CLR integration]
- UDTs [CLR integration], tables
- UDTs [CLR integration], indexes
- user-defined types [CLR integration], indexes
- indexes [CLR integration]
ms.assetid: aea495f4-ce26-4952-b019-38f012625f3f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1b87e497c6610a2d75daa9432246e4f4b4690bab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874453"
---
# <a name="defining-udt-tables-and-columns"></a>Definizione di tabelle e colonne con tipi definiti dall'utente
  Una volta che l'assembly contenente la definizione del tipo definito dall'utente (UDT) è stato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrato in un database, può essere utilizzato in una definizione di colonna.  
  
## <a name="creating-tables-with-udts"></a>Creazione di tabelle con tipo definito dall'utente  
 Per la creazione di una colonna con tipo definito dall'utente in una tabella non è necessaria una sintassi speciale. È possibile utilizzare il nome del tipo definito dall'utente in una definizione di colonna come se fosse uno dei tipi di dati intrinseci di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'istruzione CREATE TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente crea una tabella denominata **Points**, con una colonna denominata **ID,** definita come colonna `int` Identity e la chiave primaria per la tabella. La seconda colonna è denominata **PointValue**, con tipo di dati **Point**. Il nome dello schema utilizzato in questo esempio è **dbo**. Si noti che per specificare un nome di schema è necessario disporre delle autorizzazioni appropriate. Se si omette il nome dello schema, viene utilizzato lo schema predefinito per l'utente del database.  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>Creazione di indici in colonne con tipo definito dall'utente  
 Per indicizzare una colonna con tipo definito dall'utente, sono disponibili due opzioni:  
  
-   Indicizzare il valore completo. In questo caso, se il tipo definito dall'utente ha ordinamento binario, è possibile creare un indice sull'intera colonna con tipo definito dall'utente utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX.  
  
-   Indicizzare espressioni dei tipi definiti dall'utente. È possibile creare indici in colonne calcolate persistenti su espressioni dei tipi definiti dall'utente. L'espressione del tipo definito dall'utente può essere un campo, un metodo o una proprietà di un tipo definito dall'utente. L'espressione deve essere deterministica e non deve eseguire accesso ai dati.  
  
 Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente](clr-user-defined-types.md) e [CREATE INDEX &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-index-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo dei tipi definiti dall'utente in SQL Server](working-with-user-defined-types-in-sql-server.md)  
  
  

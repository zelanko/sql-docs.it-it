---
title: Creare sinonimi | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- sql13.swb.synonym.general.f1
helpviewer_keywords:
- creating synonyms
- synonyms [SQL Server], creating
ms.assetid: fedfa7a5-d0b6-4e2b-90f4-a08122958e33
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b6ccdce58ca96a26a607996943e6d48d9bac1d8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "72909734"
---
# <a name="create-synonyms"></a>Creare sinonimi
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento viene descritto come creare un sinonimo in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare un sinonimo utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per poter creare un sinonimo in un determinato schema, un utente deve disporre dell'autorizzazione CREATE SYNONYM, oltre a disporre della proprietà dello schema o dell'autorizzazione ALTER SCHEMA. L'autorizzazione CREATE SYNONYM è un'autorizzazione che può essere concessa.  
  
####  <a name="Permissions"></a> Autorizzazioni  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-create-a-synonym"></a>Per creare un sinonimo  
  
1.  In **Esplora oggetti**espandere il database in cui si desidera creare la nuova vista.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Sinonimi**, quindi selezionare **Nuovo sinonimo...** .  
  
3.  Nella finestra di dialogo **Aggiungi sinonimo** immettere le informazioni riportate di seguito.  

     **Nome sinonimo**  
     Digitare il nuovo nome che verrà utilizzato per questo oggetto.  
  
     **Schema sinonimo**  
     Digitare lo schema del nuovo nome che verrà utilizzato per questo oggetto.  
  
     **Nome server**  
     Digitare l'istanza del server a cui connettersi.  
  
     **Nome database**  
     Digitare o selezionare il database contenente l'oggetto.  
  
     **Schema**  
     Digitare o selezionare lo schema proprietario dell'oggetto.  
  
     **Tipo oggetto**  
     Selezionare il tipo di oggetto.  
  
     **Nome oggetto**  
     Digitare il nome dell'oggetto al quale fa riferimento il sinonimo.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-create-a-synonym"></a>Per creare un sinonimo  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare gli esempi seguenti nella finestra Query, quindi fare clic su **Esegui**.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 Nell'esempio seguente viene creato un sinonimo per una tabella esistente nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Il sinonimo viene quindi utilizzato negli esempi successivi.  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyAddressType  
FOR AdventureWorks2012.Person.AddressType;  
GO  
```  
  
 Nell'esempio seguente viene inserita una riga nella tabella di base cui fa riferimento il sinonimo `MyAddressType` .  
  
```  
USE tempdb;  
GO  
INSERT INTO MyAddressType (Name)  
VALUES ('Test');  
GO  
```  
  
 Nell'esempio seguente viene illustrato il modo in cui è possibile fare riferimento a un sinonimo in un'istruzione nel linguaggio SQL dinamico.  
  
```  
USE tempdb;  
GO  
EXECUTE ('SELECT Name FROM MyAddressType');  
GO  
```  
  
  

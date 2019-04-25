---
title: Identificatori del database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- regular identifiers [SQL Server]
- identifiers [SQL Server]
- names [SQL Server], identifiers
- identifiers [SQL Server], about identifiers
- SQL Server identifiers
- Transact-SQL identifiers
- database objects [SQL Server], names
ms.assetid: 171291bb-f57f-4ad1-8cea-0b092d5d150c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a492aee19d6b09cb7d227b34648f1ea35d1d95d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62762080"
---
# <a name="database-identifiers"></a>Identificatori del database
  Il nome di un oggetto di database rappresenta l'identificatore dell'oggetto stesso. È possibile associare un identificatore a qualunque elemento di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio server, database e oggetti di database quali tabelle, viste, colonne, indici, trigger, procedure, vincoli, regole e così via. Gli identificatori sono richiesti con la maggior parte degli oggetti. Per alcuni oggetti, quali i vincoli, sono facoltativi.  
  
 L'identificatore viene creato in fase di definizione dell'oggetto e viene successivamente utilizzato per fare riferimento all'oggetto. Ad esempio, l'istruzione seguente crea una tabella a cui viene associato l'identificatore `TableX`e due colonne a cui vengono associati gli identificatori `KeyCol` e `Description`:  
  
```  
CREATE TABLE TableX  
(KeyCol INT PRIMARY KEY, Description nvarchar(80))  
```  
  
 La tabella include inoltre un vincolo senza nome. Il vincolo `PRIMARY KEY` è privo di identificatore.  
  
 Le regole di confronto di un identificatore dipendono dal livello nel quale viene definito. Agli identificatori degli oggetti a livello di istanza, quali gli account di accesso e i nomi di database, vengono assegnate le regole di confronto predefinite dell'istanza. Agli identificatori degli oggetti di un database, quali tabelle, viste e nomi di colonna, vengono assegnate le regole di confronto predefinite del database. Ad esempio, due tabelle i cui nomi si differenziano soltanto per l'utilizzo del maiuscolo e del minuscolo possono essere create in un database con regole di confronto in cui l'uso di maiuscole e minuscole è rilevante, ma non in un database con regole di confronto in cui l'uso di maiuscole e minuscole non è rilevante.  
  
> [!NOTE]  
>  È necessario che i nomi di variabili o i parametri di funzioni e stored procedure siano conformi alle regole relative agli identificatori [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="classes-of-identifiers"></a>Classi di identificatori  
 Esistono due classi di identificatori:  
  
 Identificatori regolari  
 Sono conformi alle regole relative al formato degli identificatori. Gli identificatori regolari non vengono delimitati quando vengono utilizzati in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
```  
SELECT *  
FROM TableX  
WHERE KeyCol = 124  
```  
  
 Identificatori delimitati  
 Sono racchiusi tra virgolette doppie (") o tra parentesi quadre ([ ]). Gli identificatori conformi alle regole relative al formato degli identificatori possono non essere delimitati. Ad esempio:   
  
```  
SELECT *  
FROM [TableX]         --Delimiter is optional.  
WHERE [KeyCol] = 124  --Delimiter is optional.  
```  
  
 All'interno di un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] è necessario che gli identificatori non conformi alle regole relative agli identificatori siano delimitati. Ad esempio:   
  
```  
SELECT *  
FROM [My Table]      --Identifier contains a space and uses a reserved keyword.  
WHERE [order] = 10   --Identifier is a reserved keyword.  
```  
  
 Sia gli identificatori regolari che quelli delimitati devono includere da 1 a 128 caratteri. Gli identificatori delle tabelle temporanee locali possono includere al massimo 116 caratteri.  
  
## <a name="rules-for-regular-identifiers"></a>Regole relative agli identificatori regolari  
 È necessario che i nomi di variabili, funzioni e stored procedure siano conformi alle seguenti regole relative agli identificatori [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
1.  Il primo carattere deve essere uno dei seguenti:  
  
    -   Una lettera definita dallo standard Unicode 3,2, ovvero i caratteri dell'alfabeto latino a-z e A-Z e i caratteri di altre lingue.  
  
    -   Il carattere di sottolineatura (_), il simbolo di chiocciola (@) o il simbolo di cancelletto (#).  
  
         Alcuni caratteri utilizzati all'inizio di un identificatore assumono un significato particolare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un identificatore regolare che inizia con il carattere @ indica sempre una variabile locale o un parametro e non può essere utilizzato per il nome di un tipo di oggetto diverso. il carattere # indica una tabella o una procedura temporanea, mentre due simboli di cancelletto (##) indicano un oggetto temporaneo globale. Nonostante sia possibile usare uno o due simboli di cancelletto all'inizio dei nomi di altri tipi di oggetti, è consigliabile non adottare questa tecnica.  
  
         I nomi di alcune funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] iniziano con due simboli di chiocciola (@@). Per evitare confusione in merito a tali funzioni, è consigliabile non usare nomi che iniziano con @@.  
  
2.  I caratteri successivi possono includere gli elementi seguenti:  
  
    -   Lettere definite nello standard Unicode 3,2.  
  
    -   Numeri decimali inclusi nell'alfabeto Latino di base o in altri alfabeti nazionali.  
  
    -   Il simbolo di chiocciola, il simbolo di dollaro ($), il simbolo di cancelletto o il carattere di sottolineatura.  
  
3.  L'identificatore non deve essere una parola riservata [!INCLUDE[tsql](../../includes/tsql-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riserva sia le versioni maiuscole sia quelle minuscole delle parole riservate. Quando vengono utilizzati in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , gli identificatori non conformi a queste regole devono essere racchiusi tra virgolette doppie o parentesi quadre. Le parole riservate dipendono dal livello di compatibilità del database. Questo livello può essere impostato usando l'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) .  
  
4.  Non sono consentiti spazi incorporati o caratteri speciali.  
  
5.  Non sono consentiti caratteri supplementari.  
  
 Quando vengono utilizzati in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , gli identificatori non conformi a queste regole devono essere racchiusi tra virgolette doppie o parentesi quadre.  
  
> [!NOTE]  
>  Alcune regole relative al formato degli identificatori regolari dipendono dal livello di compatibilità del database. È possibile impostare tale livello con [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [Parole chiave riservate &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
  

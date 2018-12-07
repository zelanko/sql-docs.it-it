---
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2829710d348c56a5b3fcc09d06436929bcbfe16
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418322"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce un valore **datetimeoffset** convertito da un'espressione **datetime2**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 [Espressione](../../t-sql/language-elements/expressions-transact-sql.md) che viene risolta in un valore [datetime2](../../t-sql/data-types/datetime2-transact-sql.md).  
  
> [!NOTE]  
>  L'espressione non può essere di tipo **text**, **ntext** o **image** perché questi tipi non possono essere convertiti in modo implicito in **varchar** o **nvarchar**.  
  
 *time_zone*  
 Espressione che rappresenta la differenza di fuso orario in minuti (se è un numero intero), ad esempio -120, o in ore e minuti (se è una stringa), ad esempio '+13.00'. L'intervallo è compreso tra +14 e -14 (in ore). L'espressione viene interpretata come ora locale in base al valore time_zone specificato.  
  
> [!NOTE]  
>  Se l'espressione è una stringa di caratteri, il formato deve essere {+|-}TZH:THM.  
  
## <a name="return-type"></a>Tipo restituito  
 **datetimeoffset**. La precisione frazionaria è la stessa di quella dell'argomento *datetime*.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. Modifica della differenza di fuso orario della data e ora correnti  
 Nell'esempio seguente viene impostata la differenza di fuso orario della data e ora correnti sul valore `-07:00`.  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. Modifica della differenza di fuso orario in minuti  
 Nell'esempio seguente la differenza di fuso orario viene impostata sul valore `-120` minuti.  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. Aggiunta di una differenza di fuso orario di 13 ore  
 Nell'esempio seguente viene aggiunta una differenza di fuso orario di 13 ore a una data e a un'ora.  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Funzioni e tipi di dati di data e ora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


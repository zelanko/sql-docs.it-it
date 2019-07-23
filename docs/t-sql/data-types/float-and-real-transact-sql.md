---
title: float e real (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9811fdb3f7199e3a4cf10053f0f8c2f850a57845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086747"
---
# <a name="float-and-real-transact-sql"></a>float e real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipi di dati numerici approssimati da utilizzare con dati numerici a virgola mobile. I dati a virgola mobile sono approssimati. Pertanto, non tutti i valori nell'intervallo del tipo di dati possono essere rappresentati in modo esatto. Il sinonimo ISO per **real** è **float(24)** .
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
**float** [ **(** _n_ **)** ] dove *n* è il numero di bit usato per archiviare la mantissa del numero **float** in notazione scientifica e pertanto determina la precisione e le dimensioni di archiviazione. Se *n* è specificato, deve essere un valore tra **1** e **53**. Il valore predefinito di *n* è **53**.
  
|Valore *n*|Precisione|Dimensioni dello spazio di archiviazione|  
|---|---|---|
|**1-24**|7 cifre|4 byte|  
|**25-53**|15 cifre|8 byte|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta *n* come uno dei due valori possibili. Se **1**<=n<=**24**, *n* viene interpretato come **24**. Se **25**<=n<=**53**, *n* viene interpretato come **53**.  
  
Il tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**[ **(n)** ] è conforme allo standard ISO per tutti i valori di *n* da **1** a **53**. Il sinonimo di **double precision** è **float(53)** .
  
## <a name="remarks"></a>Remarks  
  
|Tipo di dati|Intervallo|Archiviazione|  
|---|---|---|
|**float**|Da - 1,79E+308 a -2,23E-308, 0 e da 2,23E-308 a 1,79E+308|Dipende dal valore di *n*|  
|**real**|Da - 3,40E + 38 a -1,18E - 38, 0 e da 1,18E - 38 a 3,40E + 38|4 byte|  
  
##  <a name="converting-float-and-real-data"></a>Conversione dei dati di tipo float e real  
I valori di tipo **float** vengono troncati in fase di conversione in un tipo di dati Integer.
  
Durante la conversione dal tipo di dati **float** o **real** a dati carattere, l'uso della funzione stringa STR è in genere più pratico rispetto all'uso di CAST( ). STR infatti garantisce un maggiore controllo sul formato. Per altre informazioni, vedere[STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md) e [Funzioni &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md).
  
La conversione dei valori **float** che usano come notazione scientifica **decimal** o **numeric** è limitata ai soli valori con precisione a 17 cifre. Qualsiasi valore < 5E-18 viene arrotondato per difetto a 0.
  
## <a name="see-also"></a>Vedere anche
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Conversione del tipo di dati &#40;motore di database&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

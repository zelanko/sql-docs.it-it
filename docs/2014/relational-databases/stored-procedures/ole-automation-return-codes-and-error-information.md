---
title: Codici restituiti e informazioni sugli errori di automazione OLE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- return codes [SQL Server]
- OLE Automation [SQL Server], return codes
- OLE Automation [SQL Server], errors
ms.assetid: 9696fb05-e9e8-4836-b359-d4de0be0eeb2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34744bedb701155d2695f6efc5aab3c493e6cf48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63011267"
---
# <a name="ole-automation-return-codes-and-error-information"></a>Codici restituiti e informazioni sugli errori di automazione OLE
  Le stored procedure del sistema di automazione OLE restituiscono un codice `int` che corrisponde al valore HRESULT restituito dall'operazione di automazione OLE sottostante. Se HRESULT è 0, l'operazione è riuscita. Un `int` valore HRESULT diverso da zero è un codice di errore OLE nel formato esadecimale 0x800*nnnnn*, ma quando viene restituito come valore in un stored procedure codice restituito, HRESULT presenta il formato 214*nnnnnnn*.  
  
 Ad esempio, passando un nome di oggetto non valido (SQLDMO. Xyzzy) per sp_OACreate fa in modo che la routine `int` restituisca un valore HRESULT 2147221005, ovvero 0x800401F3 in formato esadecimale.  
  
 È possibile utilizzare `CONVERT(binary(4), @hresult)` per convertire un valore HRESULT di tipo `int` in un valore `binary`. Se tuttavia si utilizza `CONVERT(char(10), CONVERT(binary(4), @hresult))` viene generata una stringa illeggibile, in quanto ogni byte di HRESULT viene convertito in un singolo carattere ASCII. È possibile usare il HexToChar di esempio seguente stored procedure per convertire `int` un valore HRESULT `char` in un valore che contiene una stringa esadecimale leggibile.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT name FROM sys.objects  
          WHERE name = N'dbo.sp_HexToChar')  
    DROP PROCEDURE HexToChar;  
GO  
CREATE PROCEDURE dbo.sp_HexToChar  
    @BinValue varbinary(255),  
    @HexCharValue nvarchar(255) OUTPUT  
AS  
    DECLARE @CharValue nvarchar(255);  
    DECLARE @Position int;  
    DECLARE @Length int;  
    DECLARE @HexString nchar(16);  
    SELECT @CharValue = N'0x';  
    SELECT @Position = 1;  
    SELECT @Length = DATALENGTH(@BinValue);  
    SELECT @HexString = N'0123456789ABCDEF';  
    WHILE (@Position <= @Length)  
    BEGIN  
        DECLARE @TempInt int;  
        DECLARE @FirstInt int;  
        DECLARE @SecondInt int;  
        SELECT @TempInt = CONVERT(int, SUBSTRING(@BinValue,@Position,1));  
        SELECT @FirstInt = FLOOR(@TempInt/16);  
        SELECT @SecondInt = @TempInt - (@FirstInt*16);  
        SELECT @CharValue = @CharValue +  
            SUBSTRING(@HexString, @FirstInt+1, 1) +  
            SUBSTRING(@HexString, @SecondInt+1, 1);  
        SELECT @Position = @Position + 1;  
    END  
    SELECT @HexCharValue = @CharValue;  
GO  
DECLARE @BinVariable varbinary(35);  
DECLARE @CharValue nvarchar(35);  
  
SET @BinVariable = 123456;  
  
EXECUTE dbo.sp_HexToChar  
    @binvalue = @BinVariable,  
    @HexCharValue = @CharValue OUTPUT;  
  
SELECT @BinVariable AS BinaryValue,  
    @CharValue AS CharacterRep;  
GO  
```  
  
 La stored procedure **sp_displayoaerrorinfo** dell'esempio seguente consente di visualizzare le informazioni sugli errori di automazione OLE quando una delle procedure di automazione OLE restituisce un codice di restituzione HRESULT diverso da zero. Questo esempio stored procedure USA `HexToChar`.  
  
```  
CREATE PROCEDURE dbo.sp_DisplayOAErrorInfo  
    @Object int,  
    @HResult int  
AS  
    DECLARE @Output nvarchar(255);  
    DECLARE @HRHex nchar(10);  
    DECLARE @HR int;  
    DECLARE @Source nvarchar(255);  
    DECLARE @Description nvarchar(255);  
    PRINT N'OLE Automation Error Information';  
    EXEC HexToChar @HResult, @HRHex OUT;  
    SELECT @Output = N'  HRESULT: ' + @HRHex;  
    PRINT @Output;  
    EXEC @HR = sp_OAGetErrorInfo  
        @Object,  
        @Source OUT,  
        @Description OUT;  
    IF @HR = 0  
    BEGIN  
        SELECT @Output = N'  Source: ' + @Source;  
        PRINT @Output;  
        SELECT @Output = N'  Description: '  
               + @Description;  
        PRINT @Output;  
    END  
    ELSE  
    BEGIN  
       PRINT N' sp_OAGetErrorInfo failed.';  
       RETURN;  
    END  
GO  
```  
  
## <a name="related-content"></a>Contenuto correlato  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
  

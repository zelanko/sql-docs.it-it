---
title: PWDENCRYPT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PWDENCRYPT
- PWDENCRYPT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PWDENCRYPT function [Transact-SQL]
ms.assetid: 333e9a43-1099-4b9b-b941-4b0b016f47f3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c058f81e016cf3678289fdb48e77c71cb87d0cf7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67914289"
---
# <a name="pwdencrypt-transact-sql"></a>PWDENCRYPT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce l'hash della password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il valore di input che utilizza la versione corrente dell'algoritmo di hashing delle password.  
  
 PWDENCRYPT è una funzione precedente e potrebbe non essere supportata in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usare invece [HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md). HASHBYTES rende disponibili ulteriori algoritmi di hashing.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PWDENCRYPT ( 'password' )  
```  
  
## <a name="arguments"></a>Argomenti  
 *password*  
 Password da crittografare. *password* è di tipo **sysname**.  
  
## <a name="return-types"></a>Tipi restituiti  
 **varbinary(128)**  
  
## <a name="permissions"></a>Autorizzazioni  
 PWDENCRYPT è disponibile per il ruolo public.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di sicurezza &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)  
  
  

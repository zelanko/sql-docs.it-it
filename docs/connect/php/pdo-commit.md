---
title: PDO::commit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41a87a6444ce61af5b2b8a00aa61306dd90d0d8c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993290"
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Invia al database i comandi rilasciati dopo la chiamata a [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) e restituisce la connessione in modalità di commit automatico.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>Valore restituito  
true se la chiamata al metodo ha avuto esito positivo; in caso contrario, false.  
  
## <a name="remarks"></a>Osservazioni  
PDO::commit non è influenzato e non influisce sul valore di PDO::ATTR_AUTOCOMMIT.  
  
Per un esempio d'uso di PDO::commit, vedere [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) .  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  

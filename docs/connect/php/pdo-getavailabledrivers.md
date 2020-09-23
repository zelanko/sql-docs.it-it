---
title: PDO::getAvailableDrivers
description: Informazioni di riferimento sulle API per la funzione PDO::getAvailableDrivers nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e43ef53820d24128d16ee0f0c7a5d6f1077ff6d2
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646621"
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Restituisce una matrice dei driver PDO nell'installazione di PHP.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>Valore restituito  
Una matrice con l'elenco dei driver PDO.  
  
## <a name="remarks"></a>Osservazioni  
Il nome del driver PDO usato in PDO::__construct per creare un'istanza PDO.  
  
PDO::getAvailableDrivers non deve essere implementata dai driver PHP. Per altre informazioni su questo metodo, vedere la documentazione di PHP.  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  

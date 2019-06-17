---
title: PDO::__construct | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2822c0f80aa342881e820b2edce2f99388efdc68
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772785"
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Crea una connessione a un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>Parametri  
*$dsn*: stringa che contiene il nome del prefisso (sempre `sqlsrv`), due punti e la parola chiave Server. Ad esempio, `"sqlsrv:server=(local)"`. È possibile specificare facoltativamente altre parole chiave di connessione. Vedere [Connection Options](../../connect/php/connection-options.md) per una descrizione della parola chiave Server e di altre parole chiave di connessione. L'intera stringa *$dsn* è delimitata, quindi ogni parola chiave di connessione non deve essere delimitata singolarmente.  
  
*$username*: parametro facoltativo. Stringa che contiene il nome dell'utente. Per connettersi usando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare l'ID di accesso. Per connettersi usando l'autenticazione di Windows, specificare `""`.  
  
*$password*: parametro facoltativo. Stringa che contiene la password dell'utente. Per connettersi usando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare la password. Per connettersi usando l'autenticazione di Windows, specificare `""`.  
  
*$driver_options*: facoltativo. È possibile specificare gli attributi di Gestione driver del PDO e gli attributi dei driver specifici di [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]: PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ATTR_DIRECT_QUERY. Un attributo non valido non genera un'eccezione. Gli attributi non validi generano eccezioni quando viene specificato [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
## <a name="return-value"></a>Valore restituito  
Restituisce un oggetto PDO. In caso di errore, viene restituito un oggetto PDOException.  
  
## <a name="exceptions"></a>Eccezioni  
PDOException  
  
## <a name="remarks"></a>Remarks  
È possibile chiudere un oggetto di connessione impostando l'istanza su Null.  
  
Dopo la connessione, PDO:: ErrorCode Visualizza 01000 anziché 00000.  
  
Se per qualsiasi motivo PDO::__construct non viene eseguito correttamente, viene generata un'eccezione, anche se PDO::ATTR_ERRMODE è impostato su PDO::ERRMODE_SILENT.  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
In questo esempio viene illustrato come connettersi a un server usando l'autenticazione di Windows e specificando un database.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>Esempio  
In questo esempio viene illustrato come connettersi a un server, specificando il database in un secondo momento.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
